# Tuples and anonymous types

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Sự khác biệt cơ bản nhất giữa Tuples và Anonymous types là gì?**
> **A:**
> - **Anonymous types:** Là **Reference type** (kiểu tham chiếu - class), được cấp phát trên Heap. Các thuộc tính là **read-only** (chỉ đọc).
> - **Tuples:** Là **Value type** (kiểu tham trị - struct), được cấp phát trên Stack (hiệu năng tốt hơn). Các trường là **mutable** (có thể thay đổi).

---

**Q2: Khi nào nên sử dụng Tuples?**
> **A:**
> - Khi bạn cần hiệu năng tốt hơn (**better performance**).
> - Khi bạn muốn trả về nhiều giá trị từ một phương thức (**return multiple values**).
> - Khi bạn cần phân rã (**deconstruct**) các giá trị vào các biến riêng biệt.
> - Khi bạn KHÔNG cần hỗ trợ Expression trees.

---

**Q3: Khi nào nên sử dụng Anonymous types?**
> **A:**
> - Khi bạn làm việc với **Expression trees** (ví dụ: trong LINQ providers như Entity Framework).
> - Khi bạn cần đối tượng là một **Reference type**.
> - Thường dùng nhất trong mệnh đề `select` của câu truy vấn LINQ để trả về một tập con dữ liệu.

---

**Q4: Cú pháp khởi tạo (Syntax) của hai loại này khác nhau thế nào?**
> **A:**
> - **Tuple:** Dùng dấu ngoặc đơn `()`.
>   *Ví dụ:* `var product = (Name: "Widget", Price: 19.99);`
> - **Anonymous type:** Dùng từ khóa `new` và dấu ngoặc nhọn `{}`.
>   *Ví dụ:* `var product = new { Name = "Widget", Price = 19.99 };`

---

**Q5: Tuple Deconstruction (Phân rã Tuple) là gì?**
> **A:** Là tính năng cho phép bạn tách các phần tử của Tuple ra thành các biến độc lập ngay lập tức.
> *Ví dụ:* `var (name, age) = GetPersonInfo();`
> *(Anonymous types không hỗ trợ cú pháp này).*

---

**Q6: Anonymous types có thể dùng làm kiểu trả về của phương thức (Method return type) không?**
> **A:** **Không**. Vì Anonymous types không có tên (do trình biên dịch tự sinh), bạn không thể khai báo nó trong chữ ký phương thức.
> -> **Giải pháp:** Sử dụng **Tuples** hoặc tạo một `class`/`struct` có tên rõ ràng.

---

**Q7: Projection initializers (Khởi tạo phép chiếu) trong Anonymous types là gì?**
> **A:** Là cú pháp tắt cho phép bạn khởi tạo Anonymous type bằng cách dùng luôn tên biến có sẵn làm tên thuộc tính.
> *Ví dụ:*
> ```csharp
> var firstName = "Kyle";
> var lastName = "Mit";
> var person = new { firstName, lastName }; // Tự động có property firstName và lastName
> ```

---

**Q8: Tính năng "Non-destructive mutation" (biến đổi không phá hủy) với từ khóa 'with' hoạt động thế nào với Anonymous types?**
> **A:** Tương tự như Record, bạn có thể dùng từ khóa **with** để tạo ra một bản sao mới của Anonymous type với một vài giá trị thay đổi.
> *Ví dụ:* `var onSale = apple with { Price = 0.79 };`

---

**Q9: Trình biên dịch xử lý Anonymous types như thế nào?**
> **A:** Trình biên dịch sẽ tạo ra một class có tên ngẫu nhiên (bạn không thể truy cập tên này).
> - Nếu hai Anonymous types trong cùng một assembly có cùng thứ tự, tên và kiểu của các thuộc tính, trình biên dịch sẽ coi chúng là **cùng một kiểu** (instances of the same type).

---

**Q10: Phương thức ToString() của Anonymous types hiển thị gì?**
> **A:** Nó ghi đè phương thức `ToString()` để in ra chuỗi chứa tên và giá trị của tất cả các thuộc tính, bao quanh bởi dấu ngoặc nhọn.
> *Ví dụ output:* `{ Title = Hello, Age = 24 }`