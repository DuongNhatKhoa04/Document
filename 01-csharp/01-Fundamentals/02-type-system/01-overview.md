# The C# Type System

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: C# là ngôn ngữ lập trình thuộc loại nào về mặt định kiểu (Type system)?**
> **A:** C# là một ngôn ngữ định kiểu mạnh (**strongly typed language**).
> - Mỗi biến (**variable**) và hằng số (**constant**) đều có một kiểu (**type**).
> - Mọi biểu thức (**expression**) đánh giá ra một giá trị cũng đều có một kiểu.

---

**Q2: Thông tin được lưu trữ trong một Type bao gồm những gì?**
> **A:** Thông tin của một **Type** có thể bao gồm:
> - Không gian lưu trữ (**storage space**) mà một biến của kiểu đó yêu cầu.
> - Giá trị tối đa và tối thiểu (**maximum and minimum values**) mà nó có thể biểu diễn.
> - Các thành viên (**members**) mà nó chứa (như phương thức, trường, sự kiện...).
> - Kiểu cơ sở (**base type**) mà nó kế thừa.
> - Các giao diện (**interfaces**) mà nó triển khai.
> - Các phép toán (**operations**) được phép thực hiện.

---

**Q3: Trình biên dịch (Compiler) sử dụng thông tin kiểu để làm gì?**
> **A:** Trình biên dịch sử dụng thông tin kiểu để đảm bảo tính an toàn kiểu (**type safety**) cho tất cả các hoạt động trong code của bạn.
> *Ví dụ:* Nếu bạn cộng một biến kiểu `int` với một biến kiểu `bool`, trình biên dịch sẽ báo lỗi vì phép toán này không hợp lệ.

---

**Q4: Có những cách nào để chỉ định kiểu khi khai báo biến?**
> **A:**
> 1.  **Chỉ định rõ ràng:** Ghi rõ tên kiểu (ví dụ: `float temperature;`, `string name;`).
> 2.  **Suy luận kiểu (Type inference):** Sử dụng từ khóa **var** để trình biên dịch tự suy luận kiểu dựa trên giá trị khởi tạo (ví dụ: `var limit = 3;` -> kiểu `int`).

---

**Q5: Common Type System (CTS) trong .NET là gì?**
> **A:** **Common Type System (CTS)** là một hệ thống phân cấp kiểu thống nhất, nơi tất cả các kiểu (bao gồm cả các kiểu số tích hợp sẵn như `int`) cuối cùng đều dẫn xuất (**derive**) từ một kiểu cơ sở duy nhất là `System.Object` (từ khóa trong C# là **object**).
> - Điều này đảm bảo các ngôn ngữ .NET khác nhau có thể chia sẻ và hiểu cùng một hệ thống kiểu.

---

**Q6: Hai loại kiểu chính (Main categories) trong CTS là gì?**
> **A:**
> 1.  **Value types** (Kiểu tham trị).
> 2.  **Reference types** (Kiểu tham chiếu).

---

**Q7: Đặc điểm và danh sách các Value types?**
> **A:**
> - Biến thuộc **Value types** chứa trực tiếp giá trị của chúng (**contain their values directly**).
> - Khi gán cho biến mới, dữ liệu sẽ được sao chép (**copied**). Hai biến chứa hai bản sao riêng biệt.
> - **Gồm có:** `struct` và `enum`. (Lưu ý: Các kiểu số tích hợp sẵn như `int`, `byte`, `float` thực chất là `struct` nên chúng là **Value types**).

---

**Q8: Đặc điểm và danh sách các Reference types?**
> **A:**
> - Biến thuộc **Reference types** chỉ chứa tham chiếu (**reference**) đến dữ liệu (địa chỉ bộ nhớ), không chứa dữ liệu thực sự.
> - Khi gán cho biến mới, chỉ sao chép tham chiếu. Cả hai biến cùng trỏ đến cùng một vùng dữ liệu. Thay đổi biến này sẽ ảnh hưởng biến kia.
> - **Gồm có:** `class`, `interface`, `delegate`, `record` (mặc định là record class).

---

**Q9: Literal value là gì?**
> **A:** **Literal value** là một giá trị cố định (**fixed value**) xuất hiện trực tiếp trong mã nguồn.
> *Ví dụ:* `4.5` (double literal), `'a'` (char literal), `"Hello"` (string literal).

---

**Q10: Generic types (Kiểu generic) là gì?**
> **A:** **Generic types** là các kiểu cho phép sử dụng các tham số kiểu (**type parameters**) thay vì một kiểu dữ liệu cụ thể. Điều này giúp code linh hoạt và tái sử dụng được nhiều lần mà không làm mất đi tính an toàn kiểu.
> *Ví dụ:* `List<int>` (danh sách chứa số nguyên), `List<string>` (danh sách chứa chuỗi).

---

**Q11: Implicit types (Kiểu ngầm định) và Anonymous types (Kiểu ẩn danh) là gì?**
> **A:**
> - **Implicit types:** Sử dụng từ khóa **var**, trình biên dịch tự xác định kiểu lúc biên dịch.
> - **Anonymous types:** Cho phép tạo ra các đối tượng có tập hợp các thuộc tính "chỉ đọc" (**read-only properties**) mà không cần định nghĩa một `class` hay `struct` rõ ràng trước đó.