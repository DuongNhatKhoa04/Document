# Introduction to record types in C#

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Record trong C# là gì và mục đích chính của nó?**
> **A:** **Record** là một loại `class` hoặc `struct` cung cấp cú pháp và hành vi đặc biệt để làm việc với các mô hình dữ liệu (**data models**).
> - Từ khóa `record` hướng dẫn trình biên dịch tự động tạo ra (synthesize) các thành viên hữu ích cho việc lưu trữ dữ liệu, đặc biệt là hỗ trợ **Value equality** (so sánh bằng giá trị) và **ToString()**.

---

**Q2: Khi nào nên sử dụng Record thay vì Class thông thường?**
> **A:** Bạn nên cân nhắc sử dụng **Record** khi:
> 1.  Bạn muốn định nghĩa một mô hình dữ liệu phụ thuộc vào **Value equality** (so sánh dựa trên giá trị các thuộc tính).
> 2.  Bạn muốn định nghĩa một kiểu dữ liệu mà các đối tượng của nó là **immutable** (bất biến - không thay đổi sau khi tạo).

---

**Q3: Value equality (So sánh bằng giá trị) trong Record hoạt động như thế nào?**
> **A:**
> - Hai biến **record** được coi là bằng nhau nếu kiểu của chúng khớp nhau và **tất cả** các giá trị thuộc tính/trường bên trong đều bằng nhau.
> - *(Khác với Class: Mặc định so sánh bằng tham chiếu - Reference equality, tức là chỉ bằng nhau khi cùng trỏ đến một vùng nhớ).*

---

**Q4: Immutability (Tính bất biến) là gì và tại sao nó hữu ích?**
> **A:**
> - **Immutable type** là kiểu dữ liệu ngăn chặn việc thay đổi giá trị của bất kỳ thuộc tính/trường nào sau khi đối tượng đã được khởi tạo.
> - **Lợi ích:** Giúp đảm bảo an toàn khi chạy đa luồng (**thread-safe**) và giữ nguyên mã băm (**hash code**) khi sử dụng trong các cấu trúc dữ liệu như hash table.

---

**Q5: Sự khác biệt về cú pháp khai báo giữa Record và Class/Struct?**
> **A:** Bạn chỉ cần thay từ khóa `class` bằng `record`, hoặc dùng `record struct` thay vì `struct`.
> - **Record class:** Là reference type (giống class).
> - **Record struct:** Là value type (giống struct).

---

**Q6: Positional parameters (Tham số vị trí) trong Record là gì?**
> **A:** Là cách khai báo ngắn gọn bằng cách đặt danh sách tham số ngay sau tên record (Primary constructor). Trình biên dịch sẽ tự động tạo ra các thuộc tính tương ứng.
> *Ví dụ:* `public record Person(string FirstName, string LastName);`

---

**Q7: With expression dùng để làm gì trong Record?**
> **A:** **With expression** cho phép bạn tạo ra một bản sao (**copy**) của một đối tượng immutable, nhưng thay đổi giá trị của một số thuộc tính cụ thể.
> *Ví dụ:* `Person person2 = person1 with { FirstName = "John" };`
> - `person2` là một object mới, copy dữ liệu từ `person1` nhưng có `FirstName` là "John".

---

**Q8: Record có hỗ trợ kế thừa (Inheritance) không?**
> **A:**
> - **Record** có thể kế thừa từ một **Record** khác.
> - **Record** KHÔNG thể kế thừa từ một **Class**, và ngược lại **Class** cũng KHÔNG thể kế thừa từ **Record**.

---

**Q9: Phương thức ToString() của Record có gì đặc biệt?**
> **A:** Trình biên dịch tự động tạo phương thức **ToString()** in ra tên của kiểu và danh sách các tên & giá trị của tất cả các thuộc tính công khai (**public properties**).
> *Ví dụ output:* `Person { FirstName = Nancy, LastName = Davolio }`

---

**Q10: Sự khác biệt về Property được tạo ra giữa Record Class và Record Struct khi dùng Positional parameters?**
> **A:**
> - **Record class:** Trình biên dịch tạo ra **init-only property** (bất biến).
> - **Record struct:** Trình biên dịch tạo ra **read-write property** (có thể thay đổi), trừ khi bạn khai báo là `readonly record struct`.