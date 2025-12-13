# Compiler-generated exceptions

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Compiler-generated exceptions (hay Standard Exceptions) là gì?**
> **A:** Đây là các ngoại lệ được .NET Runtime tự động ném ra khi một hoạt động cơ bản thất bại. Bạn thường không ném chúng thủ công mà chúng xuất hiện do lỗi logic trong code.

---

**Q2: NullReferenceException (Lỗi tham chiếu Null) xảy ra khi nào?**
> **A:** Xảy ra khi bạn cố gắng truy cập thành viên (thuộc tính, phương thức) của một đối tượng có giá trị là **null**.
> - Đây là lỗi phổ biến nhất trong lập trình C#.
> - *Nguyên nhân:* Quên khởi tạo đối tượng hoặc không kiểm tra null trước khi sử dụng.

---

**Q3: IndexOutOfRangeException (Lỗi chỉ số ngoài phạm vi) là gì?**
> **A:** Xảy ra khi bạn cố gắng truy cập một phần tử trong mảng (**array**) hoặc tập hợp (**collection**) bằng một chỉ số (index) nhỏ hơn 0 hoặc lớn hơn/bằng tổng số phần tử.

---

**Q4: StackOverflowException và OutOfMemoryException khác nhau thế nào?**
> **A:** Đây là hai lỗi nghiêm trọng thường không thể phục hồi (**fatal errors**):
> - **StackOverflowException:** Xảy ra khi ngăn xếp thực thi bị tràn, thường do để đệ quy vô hạn (**infinite recursion**) hoặc đệ quy quá sâu. Lỗi này **không thể bắt được** bằng khối `try-catch` (chương trình sẽ bị tắt ngay lập tức).
> - **OutOfMemoryException:** Xảy ra khi CLR không thể cấp phát đủ bộ nhớ (RAM) cho đối tượng mới.

---

**Q5: Các lỗi liên quan đến tính toán số học (Arithmetic)?**
> **A:**
> - **DivideByZeroException:** Xảy ra khi chia một số nguyên (**integer**) cho 0. (Lưu ý: Chia số thực `float`/`double` cho 0 sẽ ra `Infinity` chứ không ném lỗi này).
> - **OverflowException:** Xảy ra khi kết quả của một phép toán vượt quá giá trị tối đa hoặc tối thiểu mà kiểu dữ liệu đó có thể lưu trữ (trong bối cảnh `checked`).

---

**Q6: ArgumentException và các lớp con của nó dùng khi nào?**
> **A:** Dùng để báo lỗi khi đối số (**argument**) truyền vào phương thức không hợp lệ.
> - **ArgumentNullException:** Khi tham số không được phép null nhưng lại truyền vào null.
> - **ArgumentOutOfRangeException:** Khi giá trị tham số nằm ngoài khoảng cho phép (ví dụ: tuổi âm).