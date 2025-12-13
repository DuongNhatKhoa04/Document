# Inheritance - derive types to create more specialized behavior

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Inheritance (Kế thừa) trong C# là gì?**
> **A:** **Inheritance** cho phép bạn tạo ra các class mới tái sử dụng, mở rộng và sửa đổi hành vi được định nghĩa trong các class khác.
> - **Base class** (Lớp cơ sở): Class mà các thành viên của nó được kế thừa.
> - **Derived class** (Lớp dẫn xuất): Class kế thừa các thành viên đó.


---

**Q2: C# hỗ trợ loại kế thừa nào?**
> **A:**
> - C# chỉ hỗ trợ **Single inheritance** (Đơn kế thừa) cho class: Một derived class chỉ có thể có **một** base class trực tiếp.
> - Tuy nhiên, inheritance có tính chất bắc cầu (**transitive**): Nếu C kế thừa B, và B kế thừa A, thì C kế thừa các thành viên của cả B và A.
> - **Lưu ý:** Structs **không** hỗ trợ kế thừa (nhưng có thể triển khai interface).

---

**Q3: Những thành viên nào được kế thừa?**
> **A:** Derived class ngầm định kế thừa tất cả các thành viên của base class, **trừ** các constructors và finalizers.
> - Derived class có thể thêm các thành viên mới của riêng nó để mở rộng chức năng.

---

**Q4: Quan hệ "IS-A" (Là một) là gì?**
> **A:** Về mặt khái niệm, derived class là một sự chuyên biệt hóa (**specialization**) của base class.
> *Ví dụ:* Nếu có base class `Animal` và derived class `Mammal`. Ta nói: `Mammal` **is an** `Animal`.

---

**Q5: Implicit Inheritance (Kế thừa ngầm định) từ System.Object là gì?**
> **A:** Tất cả các class trong .NET, nếu không chỉ định rõ base class, đều ngầm định kế thừa từ `System.Object`. Do đó, mọi class đều có các phương thức cơ bản như `ToString()`, `Equals()`, `GetHashCode()`.

---

**Q6: Virtual và Override đóng vai trò gì trong kế thừa?**
> **A:**
> - **virtual:** Từ khóa dùng trong base class để cho phép phương thức đó được ghi đè.
> - **override:** Từ khóa dùng trong derived class để cung cấp triển khai mới cho phương thức virtual của base class.

---

**Q7: Abstract class (Lớp trừu tượng) là gì?**
> **A:** Là class được khai báo với từ khóa **abstract**.
> - Không thể khởi tạo (**instantiated**) trực tiếp bằng toán tử `new`.
> - Có thể chứa các **abstract methods** (phương thức không có thân hàm - body).
> - Derived class bắt buộc phải cung cấp triển khai cho tất cả các abstract methods (trừ khi derived class đó cũng là abstract).

---

**Q8: Làm thế nào để ngăn chặn kế thừa (Preventing derivation)?**
> **A:** Sử dụng từ khóa **sealed**.
> - **Sealed class:** Không cho phép class nào khác kế thừa từ nó.
> - **Sealed member:** Ngăn chặn các class con tiếp theo ghi đè (**override**) thành viên đó.

---

**Q9: Từ khóa base dùng để làm gì?**
> **A:** Từ khóa **base** được dùng trong derived class để truy cập các thành viên của base class hoặc gọi constructor của base class.
> *Ví dụ:* `base.ToString()` hoặc `public Derived() : base() { }`