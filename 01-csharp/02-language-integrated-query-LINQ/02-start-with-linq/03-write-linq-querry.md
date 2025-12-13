# Write C# LINQ queries to query data

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Có bao nhiêu cách để viết truy vấn LINQ trong C#?**
> **A:** Có 3 cách chính:
> 1.  **Query Syntax (Cú pháp truy vấn):** Sử dụng các từ khóa khai báo giống SQL (`from`, `where`, `select`).
> 2.  **Method Syntax (Cú pháp phương thức):** Sử dụng các phương thức mở rộng (`Enumerable.Where`, `Enumerable.Max`) kết hợp với biểu thức Lambda.
> 3.  **Mixed Syntax (Cú pháp hỗn hợp):** Kết hợp cả hai cách trên khi cần thiết.

---

**Q2: Query Syntax hoạt động như thế nào?**
> **A:** Nó là "Syntactic Sugar" (cú pháp đường mật) giúp code dễ đọc hơn.
> - **Lúc biên dịch (Compile time):** Trình biên dịch C# sẽ chuyển đổi toàn bộ Query Syntax thành Method Syntax tương ứng.
> - Do đó, **không có sự khác biệt về hiệu năng** giữa hai cách viết này.



---

**Q3: Khi nào bắt buộc phải dùng Method Syntax?**
> **A:** Một số toán tử truy vấn **không có** từ khóa tương ứng trong Query Syntax, nên bạn bắt buộc phải gọi phương thức. Các toán tử này thường là các hàm tổng hợp hoặc phân trang như:
> - `Count()`, `Max()`, `Min()`, `Average()`, `Sum()`.
> - `Take()`, `Skip()`, `First()`, `Any()`.

---

**Q4: Biểu thức Lambda (Lambda Expressions) trong Method Syntax là gì?**
> **A:** Là các hàm vô danh ngắn gọn dùng để định nghĩa điều kiện lọc hoặc phép chiếu.
> *Ví dụ:* `num => num < 5`
> - Đọc là: "input `num` goes to `num` less than 5".
> - `num`: Tham số đầu vào.
> - `=>`: Toán tử lambda.
> - `num < 5`: Biểu thức thực thi.

---

**Q5: Mixed Syntax (Cú pháp hỗn hợp) thường được dùng như thế nào?**
> **A:** Thường dùng khi bạn muốn viết logic lọc/nhóm phức tạp bằng Query Syntax cho dễ đọc, sau đó bao đóng lại bằng ngoặc đơn để gọi hàm tổng hợp (Method Syntax).
> *Ví dụ:*
> ```csharp
> int numCount = (from num in numbers
>                 where num < 10
>                 select num).Count();
> ```

---

**Q6: Microsoft khuyến nghị nên dùng cách nào?**
> **A:** Microsoft khuyên dùng **Query Syntax** bất cứ khi nào có thể vì nó dễ đọc, rõ ràng và giống ngôn ngữ tự nhiên hơn. Chỉ dùng Method Syntax khi bắt buộc (các toán tử không hỗ trợ) hoặc khi câu lệnh rất đơn giản.