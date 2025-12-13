# Top-level statements - programs without Main methods

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Top-level statements là gì và chúng giúp ích gì cho lập trình viên?**
> **A:** **Top-level statements** là tính năng cho phép bạn viết code thực thi trực tiếp tại thư mục gốc (root) của một file mà không cần bao bọc code trong một **class** hay phương thức **Main**.
> - Giúp giảm thiểu các đoạn code thủ tục (**boilerplate code**) không cần thiết.
> - Rất hữu ích cho các chương trình đơn giản, các tiện ích nhỏ (utilities) như **Azure Functions** hay **GitHub Actions**, và giúp người mới học C# dễ tiếp cận hơn.

---

**Q2: Quy tắc về số lượng file chứa Top-level statements trong một dự án là gì?**
> **A:** Một ứng dụng chỉ được phép có **duy nhất một entry point**. Do đó, trong một dự án, chỉ được phép có **một file duy nhất** chứa **top-level statements**.
> - Nếu có nhiều hơn một file chứa **top-level statements**, trình biên dịch sẽ báo lỗi (Compiler error CS8802).

---

**Q3: Có thể vừa dùng Top-level statements vừa khai báo phương thức Main không?**
> **A:** Bạn có thể viết phương thức **Main** một cách rõ ràng trong dự án, nhưng nó **không thể** đóng vai trò là entry point được nữa nếu đã có **top-level statements**.
> - Trình biên dịch sẽ bỏ qua phương thức **Main** đó và đưa ra cảnh báo (Warning CS7022).

---

**Q4: Thứ tự sắp xếp của using directives và type definitions trong file dùng Top-level statements như thế nào?**
> **A:**
> 1.  **using directives** phải nằm ở đầu file.
> 2.  Tiếp theo là các **top-level statements** (code thực thi).
> 3.  Cuối cùng là các khai báo **namespaces** và **type definitions** (như class, method). Chúng phải nằm **sau** các câu lệnh top-level.

---

**Q5: Top-level statements thuộc về namespace nào?**
> **A:** Các **top-level statements** ngầm định nằm trong **global namespace**.

---

**Q6: Làm thế nào để truy cập command-line arguments trong Top-level statements?**
> **A:** Bạn có thể sử dụng biến `args` để truy cập các đối số dòng lệnh.
> - Biến `args` này có sẵn (**available**) trong phạm vi top-level statements.
> - `args` không bao giờ là **null**, nhưng `args.Length` sẽ bằng 0 nếu không có đối số nào được cung cấp.

---

**Q7: Có thể sử dụng từ khóa await trong Top-level statements không?**
> **A:** Có. Bạn có thể gọi các phương thức bất đồng bộ (**async methods**) bằng cách sử dụng **await**.
> *Ví dụ:* `await Task.Delay(5000);`

---

**Q8: Làm thế nào để trả về mã thoát (Exit code) khi chương trình kết thúc?**
> **A:** Bạn sử dụng câu lệnh `return` với một giá trị kiểu `int`.
> *Ví dụ:* `return 0;` (để báo hiệu thành công).

---

**Q9: Thực chất trình biên dịch xử lý Top-level statements như thế nào (Implicit entry point method)?**
> **A:** Trình biên dịch sẽ tự động tạo ra một class `Program` và một phương thức entry point cho ứng dụng. Chữ ký (**signature**) của phương thức này phụ thuộc vào việc code của bạn có chứa từ khóa `await` hay câu lệnh `return` hay không.
> - Nếu có `await` và `return`: `static async Task<int> Main(string[] args)`
> - Nếu chỉ có `return`: `static int Main(string[] args)`
> - Nếu chỉ có `await`: `static async Task Main(string[] args)`
> - Nếu không có cả hai: `static void Main(string[] args)`
> *(Lưu ý: Tên phương thức thực tế do trình biên dịch tạo ra, bạn không thể tham chiếu trực tiếp đến nó).*