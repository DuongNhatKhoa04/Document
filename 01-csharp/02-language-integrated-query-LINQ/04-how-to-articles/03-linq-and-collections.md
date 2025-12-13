# LINQ and collections

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: LINQ tương tác với các Collections (List, Array) như thế nào?**
> **A:** Trong .NET, mọi Collection phổ biến (`List<T>`, `Array`, `Dictionary<TKey, TValue>`) đều thực thi giao diện `IEnumerable<T>`.
> - Do đó, bạn có thể dùng LINQ để truy vấn, lọc, sắp xếp bất kỳ danh sách nào trong code của bạn mà không cần cài đặt thêm thư viện gì.
> - Đây được gọi là **LINQ to Objects**.

---

**Q2: Ví dụ thực tế: Truy vấn và sắp xếp một List đối tượng?**
> **A:** Giả sử bạn có danh sách Sinh viên, bạn muốn tìm sinh viên có điểm > 8 và sắp xếp theo tên.
>
> ```csharp
> class Student { public string Name; public int Score; }
>
> List<Student> students = new List<Student>
> {
>     new Student { Name = "An", Score = 7 },
>     new Student { Name = "Binh", Score = 9 },
>     new Student { Name = "Cuong", Score = 8 }
> };
>
> // Dùng LINQ để lọc và sắp xếp
> var topStudents = from s in students
>                   where s.Score >= 8
>                   orderby s.Score descending // Điểm cao nhất lên đầu
>                   select s;
>
> foreach (var s in topStudents)
> {
>     Console.WriteLine($"{s.Name}: {s.Score}");
> }
> // Output:
> // Binh: 9
> // Cuong: 8
> ```

---

**Q3: Làm thế nào để Join (kết hợp) hai Collection khác nhau?**
> **A:** Rất thường gặp khi bạn có 2 danh sách riêng biệt (ví dụ: lấy từ 2 bảng database khác nhau hoặc 2 file API khác nhau) và muốn ghép chúng lại trong bộ nhớ.
>
> **Ví dụ:** Ghép danh sách Sinh viên với danh sách Lớp học.
> ```csharp
> class ClassRoom { public int Id; public string Name; }
> class Student { public string Name; public int ClassId; }
>
> var classes = new List<ClassRoom> 
> { 
>     new ClassRoom { Id = 1, Name = "12A" }, 
>     new ClassRoom { Id = 2, Name = "12B" } 
> };
>
> var students = new List<Student> 
> { 
>     new Student { Name = "Hùng", ClassId = 1 }, 
>     new Student { Name = "Dũng", ClassId = 2 } 
> };
>
> // Join 2 List lại với nhau
> var query = from s in students
>             join c in classes on s.ClassId equals c.Id
>             select new { StudentName = s.Name, ClassName = c.Name };
>
> foreach (var item in query)
> {
>     Console.WriteLine($"{item.StudentName} học lớp {item.ClassName}");
> }
> ```

---

**Q4: Làm việc với Collection cũ (Non-generic như ArrayList) thế nào?**
> **A:** Các collection cũ (trước .NET 2.0) như `ArrayList` chứa các đối tượng kiểu `object`, không phải `T`. LINQ không thể chạy trực tiếp trên đó.
> - **Giải pháp:** Dùng `Cast<T>()` hoặc `OfType<T>()` để chuyển nó về `IEnumerable<T>` trước.
>
> ```csharp
> ArrayList list = new ArrayList();
> list.Add("Hello");
> list.Add(123);
> list.Add("World");
>
> // Dùng OfType để lọc lấy chuỗi và biến thành IEnumerable<string>
> var stringQuery = from s in list.OfType<string>()
>                   select s;
> ```

---

**Q5: LINQ có thay đổi dữ liệu gốc trong Collection không?**
> **A:** **Không**. LINQ được thiết kế để không gây tác dụng phụ (**Side-effect free**).
> - Khi bạn `Select` hoặc `Where`, LINQ tạo ra một chuỗi kết quả mới. Danh sách gốc (`students`, `classes`...) vẫn giữ nguyên giá trị và thứ tự ban đầu.
> - Nếu muốn thay đổi danh sách gốc, bạn phải gán lại kết quả: `students = query.ToList();`