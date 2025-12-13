# C# features that support LINQ

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: LINQ có phải chỉ là một thư viện không?**
> **A:** Không hẳn. LINQ dựa trên một tập hợp các tính năng ngôn ngữ được thêm vào C# (từ bản 3.0) để làm cho cú pháp truy vấn trở nên tự nhiên và dễ đọc. Nếu không có các tính năng này, code LINQ sẽ cực kỳ dài dòng và khó viết.



---

**Q2: Query Expressions (Biểu thức truy vấn) là gì?**
> **A:** Là cú pháp khai báo tương tự như SQL (`from`, `where`, `select`).
> - Nó giúp bạn viết truy vấn một cách trực quan. Trình biên dịch sẽ tự động chuyển đổi nó thành các lời gọi phương thức.

---

**Q3: Tại sao Implicitly typed variables (var) lại bắt buộc trong một số trường hợp LINQ?**
> **A:** Mặc dù `var` thường dùng cho gọn, nhưng trong LINQ, nó là **bắt buộc** khi bạn sử dụng phép chiếu (**projection**) để tạo ra các **Anonymous Types** (kiểu vô danh).
> - Vì kiểu dữ liệu mới được tạo ra ngay lúc biên dịch và không có tên, bạn không thể khai báo tường minh (như `Customer c = ...`) mà buộc phải dùng `var`.

---

**Q4: Object and Collection Initializers (Bộ khởi tạo đối tượng và tập hợp) giúp ích gì?**
> **A:** Chúng cho phép bạn khởi tạo đối tượng và gán giá trị cho các thuộc tính ngay trong một câu lệnh duy nhất mà không cần gọi constructor hay các dòng gán riêng lẻ.
> - Trong LINQ, tính năng này cực kỳ quan trọng mệnh đề `select` khi bạn muốn tạo ra các đối tượng kết quả mới ngay lập tức.
> *Ví dụ:* `select new Customer { Name = "A", Age = 20 }`

---

**Q5: Anonymous Types (Kiểu vô danh) là gì?**
> **A:** Là các kiểu dữ liệu được trình biên dịch tự tạo ra (như một class tạm thời) chứa các thuộc tính chỉ đọc (**read-only properties**).
> - Dùng khi bạn chỉ muốn lấy một vài thuộc tính từ nguồn dữ liệu (ví dụ: chỉ lấy `Name` và `Phone` từ bảng `Customer`) mà không muốn định nghĩa một class DTO riêng biệt.

---

**Q6: Extension Methods (Phương thức mở rộng) đóng vai trò gì trong LINQ?**
> **A:** Các toán tử truy vấn chuẩn của LINQ (như `Where`, `Select`, `OrderBy`) thực chất là các **Static Methods** nhưng được gọi như thể chúng là **Instance Methods** của tập hợp (`IEnumerable<T>`). Đây chính là tính năng Extension Methods.

---

**Q7: Lambda Expressions (Biểu thức Lambda) là gì?**
> **A:** Là một hàm vô danh inline (viết ngay tại chỗ) dùng để tạo ra các loại delegate hoặc cây biểu thức.
> - Trong LINQ, chúng được dùng làm đối số cho các phương thức chuẩn để định nghĩa điều kiện lọc hoặc logic tính toán.
> *Ví dụ:* `c => c.City == "London"` (Đọc là: "c goes to c.City equals London").