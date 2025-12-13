# Discards - C# Fundamentals

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Discards trong C# là gì?**
> **A:** **Discards** (Biến loại bỏ) là các biến giữ chỗ (**placeholder variables**) được sử dụng có chủ đích khi bạn muốn bỏ qua kết quả của một biểu thức.
> - Chúng tương đương với các biến chưa được gán (**unassigned variables**); chúng không có giá trị.
> - Ký tự đại diện cho discard là dấu gạch dưới `_`.

---

**Q2: Mục đích chính của việc sử dụng Discards là gì?**
> **A:** Để thông báo rõ ràng cho trình biên dịch và người đọc code rằng: "Tôi có chủ ý bỏ qua giá trị này". Điều này giúp code sạch hơn, dễ bảo trì hơn và tránh việc khai báo các biến thừa không cần thiết.

---

**Q3: Kịch bản sử dụng Discards với Tuple Deconstruction (Phân rã Tuple) như thế nào?**
> **A:** Khi phân rã một Tuple, nếu bạn chỉ quan tâm đến một vài phần tử và muốn bỏ qua các phần tử còn lại, hãy dùng `_`.
> *Ví dụ:* `var (_, _, area) = city.GetCityInformation(cityName);` (Chỉ lấy giá trị thứ 3 là `area`, bỏ qua 2 giá trị đầu).

---

**Q4: Discards hoạt động thế nào với Pattern matching (trong switch expression)?**
> **A:** Trong biểu thức `switch`, `_` đóng vai trò là mẫu khớp với mọi thứ (**matches everything**), thường dùng làm trường hợp mặc định (**default case**) để xử lý các giá trị không khớp với các case cụ thể trước đó.
> *Ví dụ:* `_ => "Unknown"`

---

**Q5: Có thể dùng Discards với tham số 'out' không?**
> **A:** Có. Đây là cách rất phổ biến để kiểm tra tính hợp lệ mà không cần lấy giá trị thực tế.
> *Ví dụ:* `if (DateTime.TryParse(dateString, out _)) { ... }`
> - Ở đây ta chỉ cần biết chuỗi có phải ngày tháng hợp lệ không (trả về `true`/`false`), không cần lấy giá trị `DateTime` output.

---

**Q6: Standalone discard (Discard độc lập) là gì?**
> **A:** Là việc sử dụng `_` như một lệnh độc lập để bỏ qua hoàn toàn một đối tượng trả về, ví dụ như bỏ qua một `Task` trả về từ phương thức bất đồng bộ để tránh cảnh báo của compiler.
> *Ví dụ:* `_ = Task.Run(() => { ... });`

---

**Q7: Lưu ý quan trọng khi sử dụng ký tự '_' là gì?**
> **A:** `_` cũng là một tên biến hợp lệ trong C#. Nếu trong phạm vi (**scope**) hiện tại đã có một biến tên là `_` đang được sử dụng, thì `_` sẽ được hiểu là biến đó chứ KHÔNG phải là discard. Điều này có thể gây ra lỗi gán nhầm giá trị ngoài ý muốn.