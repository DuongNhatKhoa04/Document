# Generic classes and methods

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Generics giới thiệu khái niệm gì vào .NET?**
> **A:** **Generics** giới thiệu khái niệm tham số kiểu (**type parameters**). Nó cho phép bạn thiết kế các lớp (classes) và phương thức (methods) mà việc chỉ định kiểu dữ liệu cụ thể (**specification of types**) được trì hoãn lại cho đến khi class hoặc method đó được sử dụng trong code.

---

**Q2: Lợi ích chính khi sử dụng tham số kiểu generic (Generic type parameter T) là gì?**
> **A:** Bạn có thể viết một class duy nhất mà các đoạn code khác (**client code**) có thể sử dụng mà không gặp phải chi phí hoặc rủi ro về:
> - Ép kiểu tại thời điểm chạy (**runtime casts**).
> - Các hoạt động đóng hộp (**boxing operations**).

---

**Q3: Ba ưu điểm lớn nhất của Generics so với các đối tác không dùng generic (nongeneric counterparts) là gì?**
> **A:**
> 1.  Khả năng tái sử dụng (**Reusability**).
> 2.  An toàn kiểu (**Type safety**).
> 3.  Hiệu quả/Hiệu năng (**Efficiency**).

---

**Q4: Quá trình thay thế Generic type parameter diễn ra khi nào?**
> **A:** Các tham số kiểu generic được thay thế bằng các đối số kiểu thực tế (**type arguments**) trong quá trình biên dịch (**compilation**).
> *Ví dụ:* Trong `GenericList<int>`, trình biên dịch thay thế `T` bằng `int`.

---

**Q5: Ứng dụng phổ biến nhất của Generics là gì?**
> **A:** Generics được sử dụng thường xuyên nhất để tạo ra các lớp tập hợp (**collection classes**).
> - Namespace chứa các lớp này là: `System.Collections.Generic`.
> - **Lời khuyên:** Nên dùng các collection generic (như `List<T>`) thay vì các collection cũ như `ArrayList` (thuộc `System.Collections`) để đảm bảo hiệu năng và an toàn kiểu.

---

**Q6: Bạn có thể tạo ra những thành phần generic tùy chỉnh nào?**
> **A:** Bạn có thể tạo ra các thành phần generic tùy chỉnh (**custom generic types**) bao gồm:
> - Interfaces
> - Classes
> - Methods
> - Events
> - Delegates

---

**Q7: Làm thế nào để giới hạn các kiểu dữ liệu có thể được sử dụng trong Generic?**
> **A:** Bạn có thể sử dụng các ràng buộc (**constraints**) để giới hạn quyền truy cập vào các phương thức trên các kiểu dữ liệu cụ thể.
> *(Thường dùng từ khóa `where` - ví dụ: `where T : class` hoặc `where T : struct`).*

---

**Q8: Làm thế nào để lấy thông tin về kiểu dữ liệu được sử dụng trong Generic tại thời điểm chạy (Run time)?**
> **A:** Bạn có thể sử dụng cơ chế **Reflection** để lấy thông tin về kiểu dữ liệu thực tế đang được sử dụng.