# Use exceptions

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Cấu trúc cơ bản để xử lý ngoại lệ bao gồm những khối (blocks) nào?**
> **A:**
> - **try block:** Chứa đoạn code có thể ném ra ngoại lệ.
> - **catch block:** Chứa code xử lý khi ngoại lệ cụ thể xảy ra.
> - **finally block:** Chứa code dọn dẹp tài nguyên (**cleanup code**), chạy bất kể ngoại lệ có xảy ra hay không.

---

**Q2: Nguyên tắc sắp xếp các khối catch khi muốn bắt nhiều loại ngoại lệ khác nhau là gì?**
> **A:** Bạn phải bắt các ngoại lệ cụ thể (**specific exceptions**) trước, và các ngoại lệ tổng quát (**generic exceptions**) sau.
> - Trình biên dịch sẽ báo lỗi nếu bạn đặt khối catch cho `System.Exception` (lớp cha) lên trước khối catch cho `System.IO.FileNotFoundException` (lớp con), vì khối catch của lớp con sẽ không bao giờ được chạm tới (**unreachable**).

---

**Q3: Mục đích chính của khối finally là gì?**
> **A:** Để đảm bảo các tài nguyên hệ thống (như file streams, kết nối database, đồ họa) được giải phóng (**released**) chính xác ngay cả khi chương trình gặp lỗi.
> *Ví dụ:* Đóng file (`file.Close()`) trong khối `finally`.

---

**Q4: Câu lệnh 'using' (using statement) liên quan gì đến xử lý ngoại lệ?**
> **A:** Câu lệnh **using** là một cú pháp thuận tiện (**convenient syntax**) thay thế cho khối `try-finally` khi làm việc với các đối tượng thực thi giao diện `IDisposable`.
> - Nó đảm bảo phương thức `Dispose()` của đối tượng được gọi tự động khi code thoát khỏi khối `using`, giúp dọn dẹp tài nguyên gọn gàng mà không cần viết `finally` thủ công.

---

**Q5: Có thể truy cập thông tin gì từ biến exception trong khối catch?**
> **A:** Bạn có thể truy cập các thuộc tính như:
> - **Message:** Thông điệp mô tả lỗi.
> - **StackTrace:** Chuỗi thể hiện ngăn xếp cuộc gọi nơi lỗi xảy ra.
> - **InnerException:** Chứa thông tin về lỗi gốc ban đầu (nếu lỗi hiện tại được bọc bên ngoài một lỗi khác).

---

**Q6: Điều gì xảy ra nếu một ngoại lệ xảy ra trong khối try mà không có khối catch nào phù hợp ở đó?**
> **A:** Ngoại lệ đó sẽ thoát ra khỏi phương thức hiện tại và đẩy ngược lên (**propagate up**) ngăn xếp cuộc gọi (**call stack**) để tìm khối `catch` ở phương thức gọi nó. Nếu lên đến tận cùng (`Main`) mà vẫn không ai bắt, chương trình sẽ dừng lại.