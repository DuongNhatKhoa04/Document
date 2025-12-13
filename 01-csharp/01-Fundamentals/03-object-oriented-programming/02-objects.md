# Objects - create instances of types

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Object (Đối tượng) là gì trong mối quan hệ với Type definition?**
> **A:**
> - **Type definition (Class/Struct):** Giống như một bản thiết kế (**blueprint**).
> - **Object:** Là một khối bộ nhớ (**block of memory**) được cấp phát và cấu hình dựa trên bản thiết kế đó.
> - **Client code:** Là code sử dụng các biến object này để gọi phương thức hoặc truy cập thuộc tính.

---

**Q2: Việc khởi tạo Class instances (Reference types) hoạt động như thế nào?**
> **A:**
> - Các instance của class được tạo bằng toán tử **new**.
> - Biến của class giữ một tham chiếu (**reference**) đến địa chỉ của đối tượng trên **managed heap**.
> - Khi gán `object2 = object1`, cả hai biến cùng trỏ đến **cùng một đối tượng**. Thay đổi `object2` sẽ làm thay đổi `object1`.
> - Bộ nhớ được tự động thu hồi bởi **Garbage Collection**.

---

**Q3: Việc khởi tạo Struct instances (Value types) hoạt động như thế nào?**
> **A:**
> - Biến của struct chứa toàn bộ bản sao (**copy**) của đối tượng.
> - Khi gán `struct2 = struct1`, dữ liệu được sao chép sang `struct2`. Hai biến hoàn toàn độc lập. Thay đổi `struct2` **không** ảnh hưởng đến `struct1`.
> - Bộ nhớ thường được cấp phát trên **thread stack** và tự động giải phóng khi ra khỏi phạm vi (scope).

---

**Q4: Làm thế nào để kiểm tra hai đối tượng có cùng định danh (Identity) hay không?**
> **A:** Để xác định xem hai biến class có trỏ đến **cùng một vị trí trong bộ nhớ** hay không (tức là cùng Identity), bạn sử dụng phương thức tĩnh:
> `Object.ReferenceEquals(obj1, obj2)`

---

**Q5: Value equality (So sánh bằng giá trị) là gì?**
> **A:** Là việc kiểm tra xem giá trị của một hoặc nhiều trường trong hai đối tượng có tương đương nhau không.
> - Với **Structs**: Phương thức `Equals` mặc định sẽ kiểm tra xem tất cả các trường có giá trị bằng nhau không.
> - Với **Classes**: Bạn thường phải tự ghi đè (**override**) phương thức `Equals` hoặc toán tử `==` để định nghĩa thế nào là "bằng nhau" (nếu không mặc định nó sẽ so sánh reference).
> - **Records**: Mặc định sử dụng value equality.

---

**Q6: Có phải lúc nào cấp phát trên Stack (Struct) cũng nhanh hơn Heap (Class) không?**
> **A:** Không hẳn. Trong hầu hết các trường hợp, không có sự khác biệt đáng kể về hiệu năng. Việc cấp phát và thu hồi bộ nhớ trên **managed heap** đã được tối ưu hóa rất cao trong .NET Runtime.