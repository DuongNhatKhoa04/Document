# Interfaces - define behavior for multiple types

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Interface (Giao diện) trong C# là gì?**
> **A:** Một **interface** chứa các định nghĩa (**definitions**) cho một nhóm các chức năng liên quan mà một **non-abstract class** (lớp không trừu tượng) hoặc **struct** bắt buộc phải triển khai (**implement**).
> - Nó đóng vai trò như một bản hợp đồng: bất kỳ class nào thực thi interface đều cam kết cung cấp các chức năng mà interface đó định nghĩa.

---

**Q2: Tại sao Interface lại quan trọng trong C# (liên quan đến Multiple Inheritance)?**
> **A:**
> - C# **không** hỗ trợ đa kế thừa lớp (multiple inheritance of classes) - tức là một class chỉ được kế thừa từ một class cha duy nhất.
> - Tuy nhiên, một class hoặc struct có thể triển khai **nhiều interfaces**. Do đó, **interface** cho phép bạn nạp thêm hành vi (**include behavior**) từ nhiều nguồn khác nhau vào một class.

---

**Q3: Quy ước đặt tên cho Interface là gì?**
> **A:** Theo quy ước, tên của **interface** phải là một định danh C# hợp lệ và bắt đầu bằng chữ cái **I** viết hoa.
> *Ví dụ:* `IEquatable<T>`, `IEnumerable`, `IDisposable`.

---

**Q4: Interface có thể chứa những thành phần nào?**
> **A:** **Interface** có thể chứa:
> - Các phương thức thể hiện (**instance methods**), thuộc tính (**properties**), sự kiện (**events**), và bộ chỉ mục (**indexers**).
> - Các thành viên tĩnh (**static members**) như static constructors, fields, constants, hoặc operators.
> - **Lưu ý quan trọng:** Interface **không thể** chứa instance fields (trường dữ liệu thể hiện), instance constructors, hoặc finalizers.

---

**Q5: Default implementation (Triển khai mặc định) trong Interface là gì (từ C# 8.0)?**
> **A:** Từ C# 8.0, **interface** có thể định nghĩa phần triển khai mặc định cho một số hoặc tất cả các thành viên của nó.
> - Điều này có nghĩa là class thực thi interface **không bắt buộc** phải triển khai lại các thành viên đã có default implementation.
> - Tính năng này giúp bạn thêm thành viên mới vào interface mà không làm hỏng code của các class đã thực thi interface đó trước đây.

---

**Q6: Sự khác biệt về Accessibility (Quyền truy cập) của các thành viên trong Interface?**
> **A:**
> - Mặc định, các thành viên interface là **public**.
> - Bạn có thể chỉ định rõ ràng các access modifiers như `private`, `protected`, `internal`...
> - **Lưu ý:** Nếu một thành viên là `private`, nó bắt buộc phải có **default implementation** bên trong interface đó.

---

**Q7: Cách triển khai (Implement) một Interface trong Class như thế nào?**
> **A:**
> - Class phải cung cấp phần triển khai (**implementation**) cho tất cả các thành viên được khai báo trong interface (trừ khi thành viên đó đã có default implementation).
> - Các thành viên trong class dùng để triển khai interface phải là **public**, **non-static** và có cùng tên cũng như chữ ký (**signature**) với interface.

---

**Q8: Explicit interface implementation (Triển khai giao diện tường minh) là gì và khi nào cần dùng?**
> **A:** Là cách triển khai mà thành viên interface không được truy cập trực tiếp qua biến của class, mà phải ép kiểu về interface.
> - **Dùng khi:**
>   1. Class thực thi hai interface có thành viên cùng tên và chữ ký.
>   2. Bạn muốn che giấu thành viên đó, không cho phép truy cập công khai từ class, mà chỉ truy cập được khi coi đối tượng đó là interface.
>   3. Khi interface sử dụng các kiểu dữ liệu nội bộ (**internal types**) mà class không thể công khai (publicly expose).

---

**Q9: Interface có thể kế thừa từ Interface khác không?**
> **A:** Có. Một **interface** có thể kế thừa từ một hoặc nhiều **interfaces** khác. Class thực thi interface con sẽ phải triển khai tất cả các thành viên của cả interface cha và con.