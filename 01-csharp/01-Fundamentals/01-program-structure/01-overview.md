# General Structure of a C# Program

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Cấu trúc cơ bản của các C# programs là gì?**
> **A:** Các **C# programs** bao gồm một hoặc nhiều tệp (files). Mỗi tệp chứa không hoặc nhiều **namespaces**. Một **namespace** chứa các **types** (như **classes**, **structs**, **interfaces**, **enumerations**, **delegates**) hoặc các **namespaces** khác.

---

**Q2: Điểm bắt đầu (Entry point) của chương trình khi sử dụng top-level statements được xác định như thế nào?**
> **A:** Khi sử dụng **top-level statements**, điểm bắt đầu của chương trình là dòng văn bản đầu tiên trong tệp đó. Chỉ **một tệp duy nhất** trong ứng dụng được phép có **top-level statements**.


---

**Q3: Nếu không dùng top-level statements, điểm bắt đầu truyền thống là gì?**
> **A:** Điểm bắt đầu là một **static method** tên là **Main**. Chương trình bắt đầu từ dấu ngoặc nhọn mở `{` của phương thức **Main**.
> *Ví dụ signature:* `static void Main(string[] args) { ... }`

---

**Q4: C# thuộc loại ngôn ngữ lập trình nào?**
> **A:** C# là một **compiled language** (ngôn ngữ biên dịch).

---

**Q5: Quy trình biên dịch và chạy chương trình C# thông thường diễn ra như thế nào?**
> **A:**
> 1.  Sử dụng lệnh **dotnet build** để biên dịch (compile) các tệp nguồn (source files) thành một gói nhị phân (**binary package**).
> 2.  Sử dụng lệnh **dotnet run** để chạy chương trình.
> *Lưu ý:* Lệnh **dotnet run** có thể tự động biên dịch chương trình trước khi chạy nếu cần thiết.

---

**Q6: Tính năng "File-based apps" (có từ C# 14 và .NET 10) là gì?**
> **A:** Tính năng này cho phép chạy một chương trình chứa trong một tệp `*.cs` duy nhất mà không cần tạo project phức tạp. Bạn có thể chạy trực tiếp bằng lệnh: `dotnet run hello-world.cs`.

---

**Q7: "File-based apps" hỗ trợ tính năng gì cho môi trường Unix?**
> **A:** Nó hỗ trợ chuỗi **#!** (shebang) ở dòng đầu tiên (ví dụ: `#!/usr/bin/env dotnet`). Nếu bạn cấp quyền thực thi (`+x`), bạn có thể chạy tệp C# trực tiếp từ dòng lệnh như một script (ví dụ: `./hello-world.cs`).

---

**Q8: C# programs được xây dựng dựa trên hai khái niệm nền tảng nào?**
> **A:** **Expressions** (biểu thức) và **Statements** (câu lệnh).

---

**Q9: Expression là gì? Hãy nêu các ví dụ cụ thể trong tài liệu.**
> **A:** Một **expression** là sự kết hợp của các giá trị (**values**), biến (**variables**), toán tử (**operators**), và lời gọi phương thức (**method calls**) để đánh giá thành một giá trị đơn (**single value**). **Expressions** trả về kết quả và có thể được dùng ở bất cứ đâu mong đợi một giá trị.
> *Ví dụ:*
> - `42` (literal value)
> - `x + y` (arithmetic operation)
> - `Math.Max(a, b)` (method call)
> - `new Person("John")` (object creation)

---

**Q10: Statement là gì? Hãy nêu các ví dụ cụ thể trong tài liệu.**
> **A:** Một **statement** là một chỉ dẫn hoàn chỉnh (**complete instruction**) thực hiện một hành động (**perform an action**). **Statements** không trả về giá trị mà dùng để điều khiển luồng chương trình (**program flow**), khai báo biến (**declare variables**), hoặc thực hiện thao tác.
> *Ví dụ:*
> - `int x = 42;` (declaration statement)
> - `Console.WriteLine("Hello");` (expression statement - bao đóng một method call expression)
> - `if (condition) { /* code */ }` (conditional statement)
> - `return result;` (return statement)

---

**Q11: Sự khác biệt cốt lõi (Key distinction) giữa Expression và Statement là gì?**
> **A:** **Expressions** đánh giá thành giá trị (**evaluate to values**), trong khi **statements** thực hiện hành động (**perform actions**).
> *Lưu ý:* Một số cấu trúc như lời gọi phương thức (**method calls**) có thể đóng vai trò cả hai (ví dụ: `Math.Max(a, b)` là expression khi gán giá trị, nhưng là statement khi đứng độc lập).

---
