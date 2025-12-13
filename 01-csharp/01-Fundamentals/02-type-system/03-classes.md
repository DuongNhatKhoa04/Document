# Introduction to classes

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Class trong C# là gì và nó thuộc loại kiểu dữ liệu nào?**
> **A:** **Class** (Lớp) là một cấu trúc cho phép bạn tạo ra các kiểu dữ liệu tùy chỉnh (**custom types**) của riêng mình. **Class** là một kiểu tham chiếu (**reference type**).

---

**Q2: Điều gì xảy ra khi bạn khai báo một biến kiểu Reference type mà chưa khởi tạo?**
> **A:** Biến đó sẽ chứa giá trị mặc định là **null** cho đến khi bạn tạo ra một instance (thể hiện) của class bằng toán tử **new**, hoặc gán cho nó một đối tượng tương thích đã được tạo ở nơi khác.

---

**Q3: Cú pháp cơ bản để khai báo một Class là gì?**
> **A:** Sử dụng từ khóa **class** theo sau là một định danh duy nhất (**identifier**).
> *Ví dụ:*
> ```csharp
> public class Customer
> {
>     // Fields, properties, methods and events go here...
> }
> ```
> *Lưu ý:* Từ khóa **public** là một access modifier (bổ trợ truy cập), cho phép class này được khởi tạo từ bất kỳ đâu.

---

**Q4: Sự khác biệt giữa Class và Object là gì?**
> **A:**
> - **Class:** Là một định nghĩa hay bản thiết kế (**blueprint**) của một kiểu đối tượng. Nó không phải là bản thân đối tượng đó.
> - **Object:** Là một thực thể cụ thể (**concrete entity**) dựa trên class đó, đôi khi được gọi là một **instance** (thể hiện) của class.

---

**Q5: Khi khởi tạo một object bằng từ khóa new, bộ nhớ được quản lý như thế nào?**
> **A:**
> 1.  Bộ nhớ được cấp phát trên **managed heap** (heap được quản lý) cho đối tượng cụ thể đó.
> 2.  Biến bạn khai báo chỉ giữ một tham chiếu (**reference**) đến vị trí bộ nhớ của đối tượng đó, chứ không chứa dữ liệu của đối tượng trực tiếp.
> 3.  Bộ nhớ này sẽ được tự động thu hồi bởi **Garbage Collection** (Trình thu gom rác) của CLR khi không còn được sử dụng.

---

**Q6: Điều gì xảy ra khi gán một biến object này cho một biến object khác (Ví dụ: object4 = object3)?**
> **A:** Cả hai biến sẽ cùng tham chiếu đến **cùng một đối tượng** trong bộ nhớ.
> - Bất kỳ thay đổi nào thực hiện qua biến này (`object3`) đều sẽ được phản ánh khi truy cập qua biến kia (`object4`). Đây là đặc tính cơ bản của **Reference types**.

---

**Q7: Constructor (Hàm dựng) dùng để làm gì?**
> **A:** **Constructor** là phương thức đặc biệt được gọi khi một đối tượng được tạo ra. Mục đích chính là để khởi tạo các giá trị ban đầu hữu ích cho các trường (**fields**) và thuộc tính (**properties**) của đối tượng.

---

**Q8: Primary constructor (Hàm dựng chính - từ C# 12) là gì?**
> **A:** Là cách định nghĩa constructor ngay trong phần khai báo class. Các tham số của primary constructor có sẵn trong toàn bộ thân class để khởi tạo field hoặc property.
> *Ví dụ:* `public class Container(int capacity) { ... }`

---

**Q9: Từ khóa required (bắt buộc) có tác dụng gì khi khai báo Property?**
> **A:** Nó bắt buộc người gọi (**caller**) phải thiết lập giá trị cho property đó ngay khi khởi tạo đối tượng (trong object initializer), nếu không trình biên dịch sẽ báo lỗi.

---

**Q10: Class Inheritance (Kế thừa lớp) trong C# hoạt động như thế nào?**
> **A:**
> - Một class có thể kế thừa từ một **base class** (lớp cơ sở) bằng cách sử dụng dấu hai chấm (`:`).
> - Class con (**derived class**) sẽ kế thừa tất cả dữ liệu và hành vi (trừ constructors) của base class.
> - **Quy tắc quan trọng:** Trong C#, một class chỉ có thể kế thừa trực tiếp từ **duy nhất một** base class (Single inheritance), nhưng có thể triển khai nhiều **interfaces**.

---

**Q11: Abstract class và Sealed class khác nhau thế nào?**
> **A:**
> - **Abstract class:** Không thể khởi tạo (cannot be instantiated), dùng làm lớp cơ sở cho các lớp khác kế thừa và triển khai.
> - **Sealed class:** Không cho phép các lớp khác kế thừa từ nó (ngăn chặn việc kế thừa).