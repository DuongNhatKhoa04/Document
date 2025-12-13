# Exception Handling (C# Programming Guide)

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Cấu trúc của một khối try-catch-finally hoàn chỉnh hoạt động như thế nào?**
> **A:**
> - **try block:** Chứa đoạn code có khả năng gây ra ngoại lệ. Code trong này được thực thi cho đến khi gặp lỗi hoặc chạy xong.
> - **catch block:** Có thể có nhiều khối catch để xử lý các loại ngoại lệ khác nhau. Nếu ngoại lệ xảy ra trong `try`, CLR sẽ tìm khối `catch` phù hợp đầu tiên để thực thi.
> - **finally block:** Code trong này **luôn luôn** được thực thi (dù có lỗi hay không, hoặc thậm chí có lệnh `return` trong khối `try/catch`). Nó dùng để giải phóng tài nguyên.



---

**Q2: Stack trace (Dấu vết ngăn xếp) là gì và tại sao nó quan trọng?**
> **A:** **Stack trace** là danh sách các phương thức đã được gọi dẫn đến điểm xảy ra lỗi.
> - Nó cung cấp thông tin cực kỳ chi tiết: tên phương thức, tên file source code, và **số dòng** (line number) nơi lỗi xảy ra.
> - CLR tự động tạo stack trace từ điểm ném ra ngoại lệ (`throw point`) ngược lên đến nơi bắt ngoại lệ (`catch`).

---

**Q3: Điều gì xảy ra với Stack trace khi bạn dùng 'throw' so với 'throw ex'?**
> **A:**
> - `throw;` (Khuyên dùng trong catch): Giữ nguyên **stack trace** gốc ban đầu của lỗi, giúp bạn biết chính xác lỗi bắt nguồn từ đâu.
> - `throw ex;` (Không khuyên dùng): Sẽ reset lại **stack trace**. Lỗi sẽ trông như thể nó bắt đầu từ dòng `throw ex`, làm mất dấu vết của lỗi gốc thực sự.

---

**Q4: Thứ tự sắp xếp các khối catch (Ordering of catch blocks) quan trọng như thế nào?**
> **A:** Rất quan trọng. Bạn phải đặt các khối catch xử lý ngoại lệ cụ thể (**specific exceptions**) lên trước, và ngoại lệ tổng quát (**generic exceptions**) xuống dưới cùng.
> - Nếu đặt `catch (Exception e)` lên đầu, các khối catch phía sau (ví dụ `catch (IOException e)`) sẽ không bao giờ được chạy (**unreachable code**).

---

**Q5: Exception filters (Bộ lọc ngoại lệ) với từ khóa 'when' là gì?**
> **A:** Nó cho phép bạn thêm một điều kiện logic vào khối catch để quyết định có bắt lỗi đó hay không.
> *Ví dụ:* `catch (HttpException e) when (e.GetHttpCode() == 404)`
> - Khối catch này chỉ chạy nếu lỗi là `HttpException` VÀ mã lỗi là 404. Nếu mã lỗi là 500, nó sẽ bỏ qua và tìm khối catch tiếp theo.

---

**Q6: Tại sao nên sử dụng 'using statement' thay vì 'try-finally' thủ công cho tài nguyên?**
> **A:** `using` statement là một cú pháp rút gọn (**syntactic sugar**) giúp code gọn gàng hơn. Nó tự động biên dịch thành khối `try-finally` và gọi phương thức `Dispose()` để giải phóng tài nguyên (như File, Database connection) ngay khi ra khỏi khối lệnh.