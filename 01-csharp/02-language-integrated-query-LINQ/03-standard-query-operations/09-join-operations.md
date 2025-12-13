# Join Operations (C#)

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Join Operations trong LINQ dùng để làm gì?**
> **A:** Dùng để kết hợp các phần tử từ hai nguồn dữ liệu độc lập (ví dụ: Danh sách Nhân viên và Danh sách Phòng ban) dựa trên sự bằng nhau của một khóa chung.
> - LINQ hỗ trợ 3 kiểu join chính: **Inner Join**, **Group Join**, và **Left Outer Join**.

---

**Q2: Cú pháp của mệnh đề 'join' cần lưu ý gì?**
> **A:** Trong Query Syntax, bạn phải dùng từ khóa `equals` thay vì toán tử `==` để so sánh khóa.
> - Cấu trúc: `join [biến_phải] in [nguồn_phải] on [khóa_trái] equals [khóa_phải]`.

---

**Q3: Inner Join (Kết nối trong) là gì? (Kèm ví dụ)**
> **A:** Trả về các cặp phần tử **chỉ khi** khóa của chúng khớp nhau ở cả hai nguồn. Nếu một phần tử không tìm thấy cặp ở nguồn kia, nó sẽ bị loại bỏ.
>
> **Ví dụ:** Ghép Nhân viên vào Phòng ban.
> ```csharp
> class Person { public string Name; public int DepId; }
> class Dept { public int Id; public string DeptName; }
>
> var people = new List<Person> { 
>     new Person { Name = "Magnus", DepId = 1 }, 
>     new Person { Name = "Terry", DepId = 2 } // DepId 2 không tồn tại trong Dept -> Sẽ bị loại
> };
> var depts = new List<Dept> { new Dept { Id = 1, DeptName = "IT" } };
>
> var query = from p in people
>             join d in depts on p.DepId equals d.Id
>             select new { p.Name, d.DeptName };
>
> // Output: { Name = "Magnus", DeptName = "IT" }
> ```

---

**Q4: Group Join (Kết nối nhóm) là gì? (Kèm ví dụ)**
> **A:** Đây là tính năng đặc biệt của LINQ. Nó kết hợp mỗi phần tử của nguồn bên trái với **một tập hợp** các phần tử khớp từ nguồn bên phải.
> - Kết quả trả về có dạng phân cấp (Hierarchical): `1 Parent -> List<Children>`.
> - Từ khóa quan trọng: `into`.
>
> **Ví dụ:** Lấy danh sách Phòng ban và tất cả nhân viên thuộc phòng ban đó.
> ```csharp
> var query = from d in depts
>             join p in people on d.Id equals p.DepId into employeeGroup
>             select new 
>             { 
>                 Department = d.DeptName, 
>                 Employees = employeeGroup // Đây là một danh sách con
>             };
>
> foreach (var item in query)
> {
>     Console.WriteLine($"Phòng: {item.Department}");
>     foreach (var emp in item.Employees)
>     {
>         Console.WriteLine($" - {emp.Name}");
>     }
> }
> ```

---

**Q5: Left Outer Join (Kết nối ngoài trái) thực hiện thế nào trong LINQ?**
> **A:** LINQ không có từ khóa `left join` trực tiếp như SQL. Để làm được điều này, bạn phải kết hợp **Group Join** với phương thức **DefaultIfEmpty()**.
> - Mục đích: Lấy tất cả phần tử bên trái, ngay cả khi không có phần tử nào khớp bên phải (lúc này bên phải sẽ trả về null/default).
>
> **Ví dụ:** Lấy tất cả Nhân viên và tên Phòng ban của họ (nếu nhân viên chưa có phòng ban, vẫn hiện tên nhân viên đó).
> ```csharp
> var query = from p in people
>             join d in depts on p.DepId equals d.Id into empDepts
>             from item in empDepts.DefaultIfEmpty() // Nếu danh sách rỗng, trả về 1 phần tử null
>             select new 
>             { 
>                 PersonName = p.Name, 
>                 DeptName = item?.DeptName ?? "No Department" // Kiểm tra null
>             };
> ```

---

**Q6: Khi nào nên dùng Join thay vì SelectMany?**
> **A:**
> - Dùng **Join** khi hai nguồn dữ liệu không có quan hệ trực tiếp trong cấu trúc đối tượng (ví dụ: 2 bảng riêng biệt trong database, 2 list rời rạc).
> - Dùng **SelectMany** khi dữ liệu đã có sẵn quan hệ lồng nhau (ví dụ: Class `Department` đã có sẵn property `List<Employee>`).