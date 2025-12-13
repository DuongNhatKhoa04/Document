# Query based on run-time state

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Tại sao cần xây dựng truy vấn dựa trên trạng thái thời gian chạy (Run-time state)?**
> **A:** Hầu hết các truy vấn LINQ có hình dạng cố định khi viết code (compile time). Tuy nhiên, trong thực tế, hình dạng của truy vấn thường phụ thuộc vào đầu vào của người dùng lúc chạy chương trình (ví dụ: người dùng tick vào checkbox "Sắp xếp theo giá" hoặc nhập từ khóa tìm kiếm).
> - Để giải quyết vấn đề này, ta cần dùng `IQueryable<T>` để sửa đổi hình dạng của truy vấn (thêm bớt các mệnh đề `where`, `orderby`) ngay tại thời gian chạy.

---

**Q2: Cách đơn giản nhất để thêm tiêu chí lọc động là gì? (Call more LINQ methods)**
> **A:** Vì `IQueryable` thực thi theo cơ chế trì hoãn (**Deferred Execution**), bạn có thể chia nhỏ câu truy vấn và nối thêm các phương thức LINQ vào biến truy vấn gốc dựa trên các điều kiện `if`.
>
> **Ví dụ:** Xây dựng bộ lọc tìm kiếm động.
> ```csharp
> IQueryable<Student> query = db.Students; // Bắt đầu với truy vấn gốc
>
> // 1. Nếu người dùng nhập tên -> Nối thêm mệnh đề Where
> if (!string.IsNullOrEmpty(searchTerm))
> {
>     query = query.Where(s => s.Name.Contains(searchTerm));
> }
>
> // 2. Nếu người dùng chọn lọc theo lớp -> Nối thêm tiếp
> if (selectedClassId.HasValue)
> {
>     query = query.Where(s => s.ClassId == selectedClassId.Value);
> }
>
> // 3. Nếu người dùng muốn sắp xếp
> if (sortByScore)
> {
>     query = query.OrderBy(s => s.Score);
> }
>
> // Cuối cùng mới thực thi
> var results = query.ToList(); 
> ```

---

**Q3: Expression Trees (Cây biểu thức) là gì và khi nào cần dùng nó để xây dựng truy vấn?**
> **A:**
> - **Expression Trees** là cấu trúc dữ liệu đại diện cho mã lệnh (code) dưới dạng cây, thay vì mã thực thi. Các LINQ provider (như Entity Framework) dịch cây này thành SQL.
> - Bạn cần tự xây dựng Expression Trees thủ công khi **không biết trước tên thuộc tính** cần lọc tại thời điểm biên dịch (ví dụ: người dùng chọn "Lọc theo cột A" từ dropdown menu, và cột A chỉ là một chuỗi string "Age").

---

**Q4: Làm thế nào để xây dựng một Expression Tree thủ công cho mệnh đề Where? (Code nâng cao)**
> **A:** Bạn phải dùng các phương thức factory từ lớp `System.Linq.Expressions.Expression`.
> Quy trình:
> 1.  Tạo **ParameterExpression** (đại diện cho biến `x` trong `x => ...`).
> 2.  Tạo **Body Expression** (đại diện cho logic so sánh, ví dụ `x.Age > 18`).
> 3.  Gói chúng lại thành **LambdaExpression**.
>
> **Ví dụ:** Tạo động biểu thức `x => x.Name.Contains("Term")`.
> ```csharp
> // using System.Linq.Expressions;
>
> // 1. Tạo tham số 'x' (kiểu Student)
> ParameterExpression prm = Expression.Parameter(typeof(Student), "x");
>
> // 2. Tạo thân hàm: x.Name.Contains("Term")
> // Lấy property "Name"
> Expression property = Expression.Property(prm, "Name");
> // Lấy giá trị hằng số "Term"
> ConstantExpression value = Expression.Constant("Term");
> // Lấy method "Contains" của string
> MethodInfo containsMethod = typeof(string).GetMethod("Contains", new[] { typeof(string) });
> // Tạo lời gọi hàm: Name.Contains("Term")
> Expression body = Expression.Call(property, containsMethod, value);
>
> // 3. Tạo Lambda: x => x.Name.Contains("Term")
> Expression<Func<Student, bool>> lambda = Expression.Lambda<Func<Student, bool>>(body, prm);
>
> // 4. Sử dụng vào LINQ
> var results = db.Students.Where(lambda).ToList();
> ```

---

**Q5: Có thư viện nào hỗ trợ Dynamic LINQ dễ dàng hơn không?**
> **A:** Có, tài liệu Microsoft nhắc đến **Dynamic LINQ library** (`System.Linq.Dynamic.Core`).
> - Nó cho phép bạn viết truy vấn bằng chuỗi văn bản (String) thay vì phải dựng Expression Trees phức tạp.
> - Ví dụ: `query.Where("Score > 80 AND Name.Contains(@0)", "An")`.