# Polymorphism

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Polymorphism (Đa hình) là gì và nó có mấy dạng?**
> **A:** Polymorphism có nghĩa là "nhiều hình dạng" (**many-shaped**). Nó là trụ cột thứ ba của lập trình hướng đối tượng. Trong C#, nó có 2 khía cạnh:
> 1.  **At run time:** Thông qua kế thừa và phương thức ảo (Inheritance & Virtual methods). Đối tượng của class con được đối xử như đối tượng của class cha.
> 2.  **At compile time:** Thông qua nạp chồng phương thức (**Method overloading**) và nạp chồng toán tử (**Operator overloading**).


---

**Q2: Cơ chế Run-time Polymorphism hoạt động như thế nào với Virtual methods?**
> **A:**
> - Khi một derived class ghi đè (**override**) một phương thức **virtual** của base class, phương thức được gọi sẽ dựa trên **Run-time type** (kiểu thực tế của đối tượng lúc chạy) chứ không phải **Compile-time type** (kiểu của biến khai báo).
> - *Ví dụ:* Nếu bạn có một list `List<Shape>` chứa các hình `Circle`, `Triangle`, khi gọi `shape.Draw()`, phiên bản `Draw` của đúng hình đó sẽ được chạy.

---

**Q3: Để cho phép Polymorphism, Base class và Derived class cần dùng từ khóa gì?**
> **A:**
> - **Base class:** Phải khai báo phương thức với từ khóa **virtual**.
> - **Derived class:** Phải khai báo phương thức với từ khóa **override** để cung cấp triển khai mới.

---

**Q4: Những thành viên nào có thể là Virtual?**
> **A:** Chỉ có **Methods**, **Properties**, **Events**, và **Indexers** mới có thể là virtual. Các **Fields** (trường dữ liệu) không thể là virtual.

---

**Q5: Sự khác biệt giữa 'override' và 'new' (Member hiding)?**
> **A:**
> - **override:** Mở rộng chuỗi kế thừa ảo. Phương thức mới sẽ được gọi ngay cả khi đối tượng được truy cập thông qua biến kiểu Base class. (Dựa trên **Run-time type**).
> - **new:** Ẩn thành viên của base class. Phương thức mới chỉ được gọi khi truy cập qua biến kiểu Derived class. Nếu truy cập qua biến kiểu Base class, phương thức cũ của Base class sẽ được gọi. (Dựa trên **Compile-time type**).

---

**Q6: Làm thế nào để ngăn chặn một class con tiếp tục override một phương thức?**
> **A:** Sử dụng từ khóa **sealed** trước từ khóa **override**.
> *Ví dụ:* `public sealed override void DoWork() { }`
> - Từ class này trở đi, phương thức `DoWork` không còn là virtual đối với các class con của nó nữa.

---

**Q7: Làm thế nào để truy cập lại phương thức của Base class từ bên trong Derived class?**
> **A:** Sử dụng từ khóa **base**.
> *Ví dụ:* `base.Draw();` thường được dùng để gọi logic gốc của lớp cha trước hoặc sau khi thực hiện logic riêng của lớp con.

---

**Q8: Tại sao mọi Type trong C# đều có tính đa hình?**
> **A:** Vì tất cả các type (kể cả type do người dùng định nghĩa) đều kế thừa từ `System.Object`. Do đó, mọi đối tượng đều có thể được đối xử như là một `Object`.