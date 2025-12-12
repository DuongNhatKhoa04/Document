# 📘 C# PROGRAM STRUCTURE

**Version:** 1.0
**Updated:** 12/12/2025
**Author:** Vox

---

# 🌟 I. PROGRAM STRUCTURE – CẤU TRÚC CHUNG CỦA MỘT CHƯƠNG TRÌNH C#

## 1. “Một chương trình C# được cấu trúc như thế nào?”

**Note:** Overview – Program Structure

**Trả lời:**
Một chương trình C# được tổ chức thành các phần tử như:

* Namespaces
* Types (class, struct, interface, enum…)
* Type members (fields, methods, properties…)
* Statements
* Expressions

Chương trình có thể bao gồm không hoặc nhiều namespace; mỗi namespace có thể chứa nhiều type; và mỗi type có thể chứa nhiều member.

---

## 2. “Dòng using nằm ở đâu và có tác dụng gì?”

**Note:** Using directives

**Trả lời:**
`using` đặt ở đầu file để cho phép sử dụng type từ namespace khác mà không cần viết đầy đủ tên.

```csharp
using System;
```

---

## 3. “Namespace trong C# dùng để làm gì?”

**Note:** Namespace declarations

**Trả lời:**
Dùng để tổ chức code thành từng nhóm logic. Một namespace có thể chứa nhiều type hoặc namespace con.

```csharp
namespace SampleNamespace
{
}
```

---

## 4. “Type declaration nghĩa là gì?”

**Note:** Type declarations

**Trả lời:**
Khai báo một loại dữ liệu mới như:

* class
* struct
* interface
* enum

Mỗi type có thể chứa: fields, methods, properties, events…

---

## 5. “Type members là gì?”

**Note:** Members

**Trả lời:**
Các thành phần nằm trong một type gồm:

* Fields
* Constants
* Methods
* Properties
* Events
* Indexers
* Operators
* Constructors / Finalizers
* Nested types

---

## 6. “Entry point của chương trình C# là gì?”

**Note:** Main method

**Trả lời:**
Entry point là nơi chương trình bắt đầu chạy.

```csharp
static void Main() { }
```

Hoặc dạng trả về int:

```csharp
static int Main() => 0;
```

.NET 6+ cho phép sử dụng top-level statements để viết code mà không cần khai báo Main thủ công.

---

## 7. “Statements trong chương trình là gì?”

**Note:** Statements

**Trả lời:**
Statements là các câu lệnh trong method và được thực thi tuần tự từ trên xuống. Bao gồm:

* Declaration statements
* Expression statements
* Selection statements (if, switch)
* Iteration statements (for, while)
* Jump statements (return, break)

---

## 8. “Compilation của C# diễn ra thế nào?”

**Note:** Compilation and execution

**Trả lời:**
Quy trình chạy chương trình gồm:

1. Compiler biên dịch code thành IL (Intermediate Language).
2. IL được đóng gói vào assembly (.exe hoặc .dll).
3. CLR sử dụng JIT compiler để chuyển IL thành mã máy.

---

## 9. “Variable scope trong chương trình C# là gì?”

**Note:** Scope

**Trả lời:**
Phạm vi tồn tại của biến hoặc thành viên:

* Biến trong block `{ }` chỉ tồn tại trong block.
* Biến trong method tồn tại trong thời gian method chạy.
* Member của class tồn tại theo vòng đời object.

---

## 10. “Top-level statements là gì?”

**Note:** Top-level statements

**Trả lời:**
Là cách viết chương trình không cần khai báo `Program` hoặc `Main`.

```csharp
using System;
Console.WriteLine("Hello World!");
```

Compiler sẽ tự tạo Main phía sau.

---

# 🌟 II. MAIN METHOD & COMMAND-LINE ARGUMENTS

## 1. “Main method là gì và tại sao nó quan trọng?”

**Note:** Overview – The Main method

**Trả lời:**
`Main` là entry point của ứng dụng và phải là `static`. Có thể trả về `void` hoặc `int`, có tham số hoặc không.

---

## 2. “Có những dạng khai báo Main nào?”

**Note:** Main method signatures

**Trả lời:**
**Không tham số:**

```csharp
static void Main() { }
static int Main() { return 0; }
```

**Có tham số:**

```csharp
static void Main(string[] args) { }
static int Main(string[] args) { return 0; }
```

---

## 3. “Command-line arguments là gì?”

**Note:** Command-line arguments overview

**Trả lời:**
Là các chuỗi ký tự truyền từ terminal vào chương trình.

Ví dụ:

```bash
dotnet run one two three
```

Trong code:

* args[0] == "one"
* args[1] == "two"
* args[2] == "three"

---

## 4. “Làm sao in command-line arguments?”

**Note:** Examples

**Trả lời:**

```csharp
static void Main(string[] args)
{
    foreach (string arg in args)
        Console.WriteLine(arg);
}
```

---

## 5. “Main trả về int để làm gì?”

**Note:** Return values

**Trả lời:**

* 0 → thành công
* khác 0 → lỗi

---

## 6. “Có thể dùng async Main không?”

**Note:** Async Main

**Trả lời:**

```csharp
static async Task Main()
{
    await Task.Delay(1000);
}
```

---

## 7. “Top-level statements thay đổi Main như thế nào?”

**Note:** Top-level statements as entry point

**Trả lời:**

```csharp
Console.WriteLine("Hello World");
```

Compiler tạo:

```csharp
static void Main(string[] args)
{
    Console.WriteLine("Hello World");
}
```

---

## 8. “Muốn parse command-line arguments nâng cao thì sao?”

**Note:** System.CommandLine

**Trả lời:**
Microsoft khuyến nghị dùng thư viện:

```
System.CommandLine
```

Hỗ trợ: options, flags, subcommands, auto-help.

---

# 🌟 III. TOP-LEVEL STATEMENTS

## 1. “Top-level statements là gì?”

**Note:** What are top-level statements?

Cho phép viết chương trình không cần `Main` hoặc class `Program`.

---

## 2. “Tại sao C# có top-level statements?”

**Note:** Purpose

Mục đích:

* Đơn giản hóa việc học
* Giảm noise
* Dễ viết script và demo nhỏ

---

## 3. “Nếu dùng top-level statements thì Main ở đâu?”

**Note:** Generated Main method

Compiler tự sinh Main tương đương:

```csharp
internal class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hi");
    }
}
```

---

## 4. “Có được dùng nhiều file chứa top-level statements không?”

**Note:** Rules – only one file allowed

Không. Một project chỉ được có **1 file** chứa top-level statements.

---

## 5. “Có thể trộn top-level statements với type declarations không?”

**Note:** Can appear with type declarations

Hợp lệ:

```csharp
Console.WriteLine("Hello");

class MyClass
{
    public void Test() => Console.WriteLine("Inside class");
}
```

Quy tắc: top-level statements phải nằm trước mọi type.

---

## 6. “Có thể dùng async trong top-level statements không?”

**Note:** Async support

```csharp
HttpClient client = new();
string text = await client.GetStringAsync("https://example.com");
Console.WriteLine(text);
```

---

## 7. “Scope hoạt động ra sao?”

**Note:** Scope rules

* Biến top-level không thể truy cập từ type phía dưới.
* Type phía dưới có thể được dùng ở top-level.
* Top-level statements không được tham chiếu ngược lại vào type phía dưới.

---

## 8. “Tiếp tục dùng Main truyền thống được không?”

**Note:** Compatibility

Có. Top-level statements không bắt buộc.

---

## 9. “Arguments hoạt động thế nào với top-level?”

**Note:** Args generation

Compiler tự tạo:

```csharp
string[] args
```
Có thể dùng trực tiếp:

```csharp
Console.WriteLine(args.Length);
```

---
