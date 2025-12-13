# Overview of object oriented techniques in C#

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Bản chất của Type (Class, Struct, Record) và Object khác nhau thế nào?**
> **A:**
> - **Type Definition (Class, Struct, Record):** Giống như một bản thiết kế (**blueprint**) chỉ định những gì loại đó có thể làm.
> - **Object:** Là một khối bộ nhớ (**block of memory**) được cấp phát và cấu hình dựa trên bản thiết kế đó.

---

**Q2: Encapsulation (Đóng gói) là gì?**
> **A:** **Encapsulation** thường được gọi là trụ cột đầu tiên của OOP. Nó cho phép một class hoặc struct chỉ định mức độ truy cập (**accessibility**) của mỗi thành viên đối với code bên ngoài.
> - Các thành viên không dành cho bên ngoài sử dụng sẽ bị ẩn đi để hạn chế lỗi coding hoặc các khai thác nguy hiểm.

---

**Q3: Trong C# có biến toàn cục (Global variables) hoặc phương thức toàn cục không?**
> **A:** **Không**. Trong C#, tất cả phương thức, trường, hằng số... đều phải được khai báo bên trong một **class** hoặc **struct** (kể cả phương thức `Main`).

---

**Q4: Có những Access Modifiers (Bổ trợ truy cập) nào để kiểm soát Encapsulation?**
> **A:**
> - `public`: Truy cập từ bất cứ đâu.
> - `private`: Chỉ truy cập trong nội bộ class/struct đó (đây là mặc định).
> - `protected`: Truy cập trong nội bộ class và các class kế thừa (**derived classes**).
> - `internal`: Truy cập trong cùng assembly.
> - `protected internal`: Kết hợp protected hoặc internal.
> - `private protected`: Kết hợp protected và internal (trong cùng assembly và phải kế thừa).

---

**Q5: Inheritance (Kế thừa) hoạt động với loại Type nào?**
> **A:** Chỉ **Classes** (và record classes) mới hỗ trợ kế thừa. **Structs** không hỗ trợ kế thừa.
> - Class kế thừa từ một **Base class** sẽ tự động có tất cả các thành viên public, protected và internal của base class (trừ constructors và finalizers).

---

**Q6: Abstract class và Sealed class là gì?**
> **A:**
> - **Abstract class:** Một hoặc nhiều phương thức chưa có triển khai (**implementation**). Không thể khởi tạo trực tiếp, chỉ dùng làm base class.
> - **Sealed class:** Ngăn chặn các class khác kế thừa từ nó.

---

**Q7: Interface đóng vai trò gì trong kỹ thuật hướng đối tượng?**
> **A:** **Interface** định nghĩa một tập hợp các phương thức mà một Type phải thực hiện.
> - Một Class hoặc Struct có thể triển khai **nhiều Interfaces** (Multiple interfaces implementation), dù chỉ được kế thừa một Base class.

---

**Q8: Static class là gì?**
> **A:** **Static class** là class chỉ chứa các thành viên tĩnh (**static members**) và không thể khởi tạo bằng từ khóa `new`. Nó được nạp vào bộ nhớ một lần duy nhất khi chương trình chạy.
> *(Lưu ý: Structs và Records không thể khai báo là static class, nhưng có thể chứa static members).*

---

**Q9: Extension Methods (Phương thức mở rộng) là gì?**
> **A:** Cho phép bạn "mở rộng" một class có sẵn mà không cần tạo class kế thừa, bằng cách tạo một type riêng biệt chứa các phương thức có thể được gọi như thể chúng thuộc về type gốc.

---

**Q10: Polymorphism (Đa hình) được nhắc đến như thế nào trong bối cảnh Inheritance?**
> **A:** (Được chi tiết hóa ở bài sau, nhưng về cơ bản): Cho phép các class con (**derived classes**) được đối xử như class cha (**base class**). Các phương thức có thể được ghi đè (**override**) để thay đổi hành vi cụ thể.