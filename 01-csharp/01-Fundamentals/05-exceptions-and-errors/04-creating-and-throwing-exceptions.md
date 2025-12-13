# Create and throw exceptions

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Khi nào lập trình viên nên chủ động ném ngoại lệ (throw exceptions)?**
> **A:**
> 1.  Khi phương thức không thể hoàn thành chức năng của nó (ví dụ: tham số đầu vào không hợp lệ).
> 2.  Khi có một lời gọi không phù hợp với trạng thái của đối tượng (ví dụ: ghi vào file chỉ đọc).
> 3.  Khi một đối số gây ra lỗi, bạn nên bắt lỗi gốc và ném ra một ngoại lệ mới rõ ràng hơn (ví dụ: `ArgumentException`) bao bọc lấy lỗi cũ.

---

**Q2: Thuộc tính InnerException dùng để làm gì?**
> **A:** Khi bạn ném một ngoại lệ mới để phản hồi lại một ngoại lệ khác vừa xảy ra, bạn nên truyền ngoại lệ gốc vào tham số `InnerException` của ngoại lệ mới. Điều này giúp giữ lại thông tin về nguyên nhân gốc rễ (**root cause**) của lỗi để phục vụ việc debug.

---

**Q3: Những ngoại lệ hệ thống nào KHÔNG nên tự ý ném ra từ code của bạn?**
> **A:** Bạn không nên ném các ngoại lệ cấp thấp của hệ thống như:
> - `System.Exception`
> - `System.SystemException`
> - `System.NullReferenceException`
> - `System.IndexOutOfRangeException`
> -> **Lý do:** Các lỗi này nên được dành riêng cho CLR ném ra khi có lỗi hệ thống thực sự. Bạn nên dùng các ngoại lệ cụ thể hơn như `ArgumentNullException` hoặc `InvalidOperationException`.

---

**Q4: Cách định nghĩa một lớp ngoại lệ tùy chỉnh (Custom Exception Class) chuẩn là gì?**
> **A:**
> 1.  Tạo class kế thừa từ `System.Exception`.
> 2.  Đặt tên class kết thúc bằng hậu tố "Exception" (ví dụ: `InvalidDepartmentException`).
> 3.  Cung cấp ít nhất 3 constructors chuẩn:
>     - Constructor không tham số (`public InvalidDepartmentException()`).
>     - Constructor nhận message (`public InvalidDepartmentException(string message)`).
>     - Constructor nhận message và inner exception (`public InvalidDepartmentException(string message, Exception inner)`).

---

**Q5: Lưu ý đặc biệt khi ném ngoại lệ trong phương thức async (Task-returning methods) là gì?**
> **A:**
> - Các ngoại lệ ném ra trong phần `async` sẽ được lưu trữ trong `Task` trả về và chỉ bung ra khi `Task` đó được `await`.
> - **Khuyến nghị:** Nên kiểm tra và ném lỗi tham số (Argument validation) **trước** khi bước vào phần xử lý bất đồng bộ để lỗi được ném ra ngay lập tức (synchronously), giúp người gọi phát hiện lỗi sớm hơn.

---

**Q6: Có nên dùng Exception để điều hướng luồng chương trình bình thường (Normal flow control) không?**
> **A:** **Tuyệt đối không**. Exception chỉ nên dùng để báo cáo và xử lý các tình huống lỗi (**error conditions**). Việc dùng Exception để điều khiển logic (như check if-else) sẽ làm giảm hiệu năng và gây khó hiểu cho code.