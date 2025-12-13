# Main() and command-line arguments

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Vai trò cốt lõi của phương thức Main là gì?**
> **A:** Phương thức **Main** là điểm bắt đầu (**entry point**) của một ứng dụng C#. Khi chương trình khởi chạy, điều khiển chương trình (**program control**) bắt đầu và kết thúc tại đây.

---

**Q2: Các yêu cầu bắt buộc (Constraints) khi khai báo Main là gì?**
> **A:**
> 1.  Phải nằm bên trong một **class** hoặc **struct**.
> 2.  Phải được khai báo là **static**.
> 3.  Không bắt buộc phải là **public** (mặc định là **implicitly private** nếu không ghi rõ).

---

**Q3: Các kiểu trả về (Return types) hợp lệ của Main là gì?**
> **A:**
> - `void`: Khi không cần trả về giá trị.
> - `int`: Khi cần trả về mã thoát (**exit code**) cho hệ điều hành.
> - `Task`: Dùng cho **async Main** (không trả về giá trị).
> - `Task<int>`: Dùng cho **async Main** (trả về mã thoát).

---

**Q4: Tại sao cần sử dụng Async Main (Main bất đồng bộ)?**
> **A:** Việc khai báo `async Main` (với kiểu trả về `Task` hoặc `Task<int>`) cho phép bạn sử dụng từ khóa **await** bên trong **Main**. Điều này giúp code đơn giản hơn khi ứng dụng console cần gọi và chờ các **asynchronous operations** (tác vụ bất đồng bộ).

---

**Q5: Quy ước về giá trị trả về int (Exit code) của Main là gì?**
> **A:**
> - Giá trị `0`: Biểu thị thực thi thành công (**success**).
> - Giá trị khác 0: Biểu thị lỗi (**failure**).
> *Lưu ý:* Giá trị này được lưu trong biến môi trường (ví dụ: `%ERRORLEVEL%` trên Windows) để các script hoặc chương trình khác kiểm tra.

---

**Q6: Tham số string[] args trong Main chứa dữ liệu gì?**
> **A:** Nó chứa các đối số dòng lệnh (**command-line arguments**) được truyền vào khi chạy chương trình.
> - Mảng này được đánh chỉ số từ 0 (**zero-indexed**).
> - Tên của chương trình **không** nằm trong mảng `args` này (khác với C/C++).

---

**Q7: Mảng args có bao giờ bị null không?**
> **A:** Không. Mảng `args` **không bao giờ là null**. Vì vậy, bạn có thể truy cập thuộc tính `args.Length` một cách an toàn mà không cần kiểm tra null.

---

**Q8: Làm thế nào để sử dụng các đối số dòng lệnh nếu chúng là số (Numeric types)?**
> **A:** Mảng `args` luôn là kiểu `string`. Để sử dụng như số, bạn phải chuyển đổi (**convert**) chúng bằng cách dùng:
> - Lớp `Convert` (ví dụ: `Convert.ToInt64`).
> - Hoặc phương thức `Parse` (ví dụ: `int.Parse`, `long.Parse`).

---

**Q9: Điều gì xảy ra nếu có nhiều hơn một class chứa phương thức Main?**
> **A:** Trình biên dịch sẽ báo lỗi. Bạn phải chỉ định rõ class nào chứa **Main** được dùng làm **entry point** bằng tùy chọn biên dịch **StartupObject**.

---

**Q10: Sự tương tác giữa Top-level statements và phương thức Main như thế nào?**
> **A:** Bạn có thể dùng **top-level statements** làm entry point thay cho phương thức **Main**. Tuy nhiên, trong một dự án, chỉ được chọn một trong hai cách làm entry point (không thể vừa có file dùng top-level statements vừa có class chứa Main hoạt động cùng lúc).