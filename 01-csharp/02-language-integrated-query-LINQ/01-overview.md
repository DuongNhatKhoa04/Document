# Language Integrated Query (LINQ)

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: LINQ là gì?**
> **A:** **LINQ** (Language-Integrated Query) là tên gọi của một tập hợp các công nghệ cho phép tích hợp khả năng truy vấn trực tiếp vào ngôn ngữ C#.
> - Trước đây, truy vấn dữ liệu thường dùng chuỗi văn bản (như SQL string) không có kiểm tra kiểu.
> - Với LINQ, truy vấn là một cấu trúc ngôn ngữ hạng nhất (**first-class language construct**), hỗ trợ kiểm tra kiểu lúc biên dịch và IntelliSense.

---

**Q2: Query expression (Biểu thức truy vấn) trong LINQ là gì?**
> **A:** Là phần "tích hợp ngôn ngữ" dễ thấy nhất của LINQ. Nó sử dụng cú pháp truy vấn khai báo (**declarative query syntax**) tương tự như SQL để lọc, sắp xếp, và nhóm dữ liệu.
> - *Cấu trúc cơ bản:* `from ... where ... select`.

---

**Q3: Ba giai đoạn của một hoạt động truy vấn (Query operation) là gì?**
> **A:**
> 1.  **Obtain the data source:** Xác định nguồn dữ liệu (như mảng, list, database).
> 2.  **Define the query:** Định nghĩa câu truy vấn (nhưng chưa thực thi).
> 3.  **Execute the query:** Thực thi truy vấn (thường dùng vòng lặp `foreach`).

---

**Q4: Query variable (Biến truy vấn) lưu trữ cái gì?**
> **A:** Biến truy vấn chỉ lưu trữ **các lệnh truy vấn** (query commands/logic), chứ **KHÔNG** lưu trữ dữ liệu kết quả thực tế.

---

**Q5: Deferred execution (Thực thi trì hoãn) trong LINQ là gì?**
> **A:** Là cơ chế mà truy vấn **không được thực thi** ngay tại thời điểm nó được định nghĩa. Truy vấn chỉ thực sự chạy khi bạn lặp qua biến truy vấn (ví dụ: trong vòng lặp `foreach`). Điều này giúp tiết kiệm tài nguyên và luôn lấy được dữ liệu mới nhất.

---

**Q6: Immediate execution (Thực thi ngay lập tức) xảy ra khi nào?**
> **A:** Xảy ra khi bạn gọi các phương thức yêu cầu trả về một kết quả đơn lẻ (như `Count`, `Max`, `Average`, `First`) hoặc ép kiểu về tập hợp (như `ToList()`, `ToArray()`). Lúc này, truy vấn buộc phải chạy ngay lập tức để tính toán kết quả.

---

**Q7: Sự khác biệt giữa Query syntax và Method syntax?**
> **A:**
> - **Query syntax:** Giống SQL, dễ đọc, khai báo rõ ràng (`from num in numbers where num > 5 select num`).
> - **Method syntax:** Sử dụng các phương thức mở rộng (**extension methods**) và biểu thức lambda (`numbers.Where(num => num > 5)`).
> - **Lưu ý:** Không có sự khác biệt về hiệu năng hay ngữ nghĩa giữa hai cách này. Trình biên dịch sẽ chuyển đổi Query syntax thành Method syntax.

---

**Q8: Data source (Nguồn dữ liệu) cần thỏa mãn điều kiện gì để dùng được LINQ?**
> **A:**
> - Với dữ liệu trong bộ nhớ (**In-memory data**): Phải thực thi giao diện `IEnumerable<T>` (ví dụ: Array, List).
> - Với dữ liệu từ xa (**Remote data** - như SQL): Phải thực thi giao diện `IQueryable<T>`.

---

**Q9: Expression Trees (Cây biểu thức) liên quan gì đến LINQ?**
> **A:** Khi truy vấn nguồn dữ liệu từ xa (`IQueryable`), trình biên dịch không biên dịch truy vấn thành mã thực thi ngay (delegates), mà biên dịch thành **Expression Trees**. Cấu trúc dữ liệu này sau đó được các **LINQ Providers** (như Entity Framework) dịch sang ngôn ngữ truy vấn phù hợp (như SQL) để chạy trên server.