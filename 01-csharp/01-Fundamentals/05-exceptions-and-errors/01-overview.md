# Exceptions and Exception Handling

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Exception (Ngoại lệ) trong C# là gì?**
> **A:** **Exception** là một sự kiện xảy ra trong quá trình thực thi chương trình làm gián đoạn luồng lệnh bình thường.
> - Trong C#, ngoại lệ là các đối tượng (**types**) kế thừa từ lớp cơ sở `System.Exception`.

---

**Q2: Bốn từ khóa chính (Keywords) để xử lý ngoại lệ là gì?**
> **A:**
> 1.  **try:** Chứa đoạn code có thể gây ra lỗi (actions that may not succeed).
> 2.  **catch:** Chứa đoạn code để xử lý lỗi nếu nó xảy ra trong khối `try`.
> 3.  **finally:** Chứa đoạn code **luôn luôn được thực thi**, bất kể lỗi có xảy ra hay không (thường dùng để dọn dẹp tài nguyên như đóng file, stream).
> 4.  **throw:** Dùng để ném ra (tạo ra) một ngoại lệ theo cách thủ công.

---

**Q3: Cơ chế "Call stack bubbling" hoạt động như thế nào khi có lỗi xảy ra?**
> **A:** Khi một ngoại lệ được ném ra:
> - CLR (Common Language Runtime) sẽ lùi lại ngăn xếp cuộc gọi (**unwind the stack**).
> - Nó tìm kiếm phương thức nào có chứa khối **catch** phù hợp với loại ngoại lệ đó.
> - Nó sẽ thực thi khối **catch** đầu tiên tìm thấy.
> - Nếu không tìm thấy khối catch nào phù hợp trong toàn bộ call stack, CLR sẽ **chấm dứt chương trình** (terminate the process) và hiển thị thông báo lỗi.


---

**Q4: Những thông tin gì được chứa trong một Exception object?**
> **A:** Đối tượng ngoại lệ chứa thông tin chi tiết về lỗi, bao gồm:
> - Trạng thái của ngăn xếp cuộc gọi (**stack trace**) tại thời điểm lỗi.
> - Mô tả văn bản về lỗi (**text description**).

---

**Q5: Có nên catch mọi loại Exception không?**
> **A:** **Không**.
> - Đừng catch một ngoại lệ trừ khi bạn có thể xử lý nó và đưa ứng dụng về trạng thái ổn định đã biết (**known state**).
> - Nếu bạn catch `System.Exception` (lớp cha của mọi lỗi), hãy chắc chắn ném lại nó (**rethrow**) bằng từ khóa `throw` ở cuối khối catch, trừ khi bạn thực sự muốn "nuốt" lỗi đó (điều này thường không được khuyến khích).

---

**Q6: Ngoại lệ có thể được sinh ra từ những nguồn nào?**
> **A:**
> - Từ Common Language Runtime (**CLR**).
> - Từ các thư viện .NET hoặc thư viện bên thứ ba (**third-party libraries**).
> - Từ chính code của ứng dụng (**application code**) bằng từ khóa `throw`.