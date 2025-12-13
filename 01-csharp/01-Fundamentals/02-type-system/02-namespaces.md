# Declare namespaces to organize types

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Namespace là gì và mục đích chính của nó trong C#?**
> **A:** **Namespace** (Không gian tên) là một cơ chế dùng để tổ chức code. Nó có hai mục đích chính:
> 1.  **.NET** sử dụng namespace để tổ chức rất nhiều class của nó (ví dụ: `System.Console` thì `System` là namespace, `Console` là class).
> 2.  Giúp bạn kiểm soát phạm vi (**scope**) của tên class và method trong các dự án lớn, tránh xung đột tên (**naming conflicts**).

---

**Q2: Làm thế nào để sử dụng một class mà không cần gõ tên đầy đủ (Fully qualified name)?**
> **A:** Bạn sử dụng từ khóa **using** (chỉ thị using directive).
> *Ví dụ:* Thay vì viết `System.Console.WriteLine("Hello");`, bạn khai báo `using System;` ở đầu file và chỉ cần viết `Console.WriteLine("Hello");`.

---

**Q3: Cú pháp khai báo namespace theo kiểu truyền thống (Block-scoped) là gì?**
> **A:** Bạn sử dụng từ khóa `namespace` theo sau là tên namespace và cặp dấu ngoặc nhọn `{ }` bao bọc lấy phần code bên trong.
> *Ví dụ:*
> ```csharp
> namespace SampleNamespace
> {
>     class SampleClass { ... }
> }
> ```

---

**Q4: Cú pháp khai báo namespace kiểu mới (File-scoped) là gì và lợi ích của nó?**
> **A:** Bạn khai báo namespace kết thúc bằng dấu chấm phẩy `;` thay vì dùng ngoặc nhọn. Namespace này sẽ áp dụng cho toàn bộ các type trong file đó.
> *Ví dụ:* `namespace SampleNamespace;`
> - **Lợi ích:** Cú pháp đơn giản hơn, tiết kiệm không gian chiều ngang (thụt đầu dòng) và bớt đi các dấu ngoặc nhọn lồng nhau, giúp code dễ đọc hơn.

---

**Q5: Tính năng Implicit global using directives (có từ .NET 6) là gì?**
> **A:** Đối với các dự án sử dụng SDK như `Microsoft.NET.Sdk` hoặc `Microsoft.NET.Sdk.Web`, hệ thống sẽ tự động thêm các chỉ thị `global using` cho các namespace phổ biến nhất (như `System`, `System.Linq`, `System.Collections.Generic`...) mà không cần bạn phải khai báo thủ công trong từng file.

---

**Q6: Namespace "root" trong C# là gì?**
> **A:** **Global namespace** được coi là namespace "gốc" (root).
> - Bạn có thể dùng `global::System` để luôn tham chiếu chính xác đến namespace `System` của .NET, đảm bảo không bị nhầm lẫn với bất kỳ namespace nào khác trùng tên do người dùng tự tạo.

---

**Q7: Các tính chất cơ bản (Properties) của Namespaces là gì?**
> **A:**
> - Chúng giúp tổ chức các dự án code lớn.
> - Chúng được phân cách bởi dấu chấm (`.`) (ví dụ: `System.Collections.Generic`).
> - Chỉ thị **using** giúp loại bỏ yêu cầu phải chỉ định tên namespace cho mọi class.

---