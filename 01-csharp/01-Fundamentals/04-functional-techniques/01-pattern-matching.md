# Pattern matching overview

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Pattern matching là gì?**
> **A:** **Pattern matching** là một kỹ thuật cho phép bạn kiểm tra một biểu thức (**expression**) để xem nó có các đặc điểm (**characteristics**) nhất định hay không (ví dụ: kiểm tra kiểu dữ liệu, giá trị, hoặc cấu trúc). C# cung cấp cú pháp ngắn gọn để thực hiện việc kiểm tra và thực thi hành động ngay khi biểu thức khớp mẫu.

---

**Q2: Hai cấu trúc (Expressions) chính hỗ trợ pattern matching trong C# là gì?**
> **A:**
> 1.  **is expression:** Dùng để kiểm tra biểu thức và có thể khai báo biến mới (`if (input is int count)`).
> 2.  **switch expression:** Cho phép thực thi hành động dựa trên mẫu khớp đầu tiên. Cú pháp ngắn gọn hơn `switch` statement truyền thống.

---

**Q3: Kịch bản phổ biến nhất khi dùng Pattern matching là gì?**
> **A:** Kiểm tra **Null checks**.
> - Bạn có thể dùng `is not null` để đảm bảo giá trị không bị null trước khi xử lý.
> *Ví dụ:* `if (message is not null) { ... }`

---

**Q4: Type tests (Kiểm tra kiểu) và Declaration pattern hoạt động như thế nào?**
> **A:** Nó cho phép bạn kiểm tra kiểu của biến và gán nó vào một biến mới ngay trong cùng một biểu thức nếu khớp.
> *Ví dụ:* `if (sequence is IList<T> list) { ... }`
> - Nếu `sequence` là `IList<T>`, biến `list` sẽ được khởi tạo và chỉ có thể truy cập trong khối lệnh `if`.

---

**Q5: Constant pattern (Mẫu hằng số) dùng để làm gì?**
> **A:** Dùng để so sánh giá trị với các hằng số rời rạc (**discrete values**) như số (`1`, `2`), chuỗi (`"Start"`), ký tự, hoặc giá trị `enum`.
> *Ví dụ:* `command switch { "Start" => StartSystem(), "Stop" => StopSystem(), ... }`

---

**Q6: Relational patterns (Mẫu quan hệ) cho phép so sánh gì?**
> **A:** Cho phép so sánh giá trị số với các hằng số bằng các toán tử quan hệ (`<`, `>`, `<=`, `>=`).
> *Ví dụ:* `temp switch { < 32 => "solid", > 212 => "gas", ... }`

---

**Q7: Logical patterns (Mẫu logic) gồm những từ khóa nào?**
> **A:** Gồm `and`, `or`, và `not`. Dùng để kết hợp các pattern khác lại với nhau.
> *Ví dụ:* `(> 32) and (< 212)` (vừa lớn hơn 32 VÀ nhỏ hơn 212).

---

**Q8: Discard pattern (_) là gì?**
> **A:** Dấu gạch dưới `_` đại diện cho một mẫu "khớp với mọi thứ" (**matches all values**) nhưng không lưu trữ giá trị đó. Thường dùng làm trường hợp mặc định (**default case**) trong `switch expression` để xử lý các giá trị còn lại.

---

**Q9: Property pattern dùng để làm gì?**
> **A:** Dùng để kiểm tra giá trị của các thuộc tính (**properties**) bên trong đối tượng.
> *Ví dụ:* `{ Items: > 10, Cost: > 1000 }` (Kiểm tra nếu Items > 10 và Cost > 1000).

---

**Q10: Positional pattern (Mẫu vị trí) hoạt động như thế nào?**
> **A:** Hoạt động dựa trên tính năng **Deconstruct** của đối tượng hoặc Tuple. Nó khớp các giá trị dựa trên vị trí của chúng.
> *Ví dụ:* `(> 10, > 1000)` (Phần tử thứ nhất > 10, phần tử thứ hai > 1000).

---

**Q11: List pattern (Mẫu danh sách) là gì?**
> **A:** Cho phép kiểm tra các phần tử trong danh sách hoặc mảng (**sequence**).
> - Bạn có thể khớp chính xác giá trị, hoặc dùng `_` để bỏ qua phần tử, hoặc dùng `..` (slice pattern) để khớp một khoảng nhiều phần tử.
> *Ví dụ:* `[_, "DEPOSIT", _, var amount]` (Bỏ qua phần tử 1 và 3, phần tử 2 phải là "DEPOSIT", phần tử 4 gán vào biến amount).