# 📘 C# FUNCTION TECHNIQUES — PATTERN MATCHING

**Version:** 1.0
**Updated:** 12/12/2025
**Author:** Vox

---

- [📘 C# FUNCTION TECHNIQUES — PATTERN MATCHING](#-c-function-techniques--pattern-matching)
- [I. PATTERN MATCHING](#i-pattern-matching)
  - [1. "Pattern matching trong C# là gì?"](#1-pattern-matching-trong-c-là-gì)
  - [2. "Type patterns — Kiểm tra kiểu của object"](#2-type-patterns--kiểm-tra-kiểu-của-object)
  - [3. "Constant patterns — So khớp với giá trị cụ thể"](#3-constant-patterns--so-khớp-với-giá-trị-cụ-thể)
  - [4. "Relational patterns — So sánh bằng \<, \>, \<=, \>="](#4-relational-patterns--so-sánh-bằng----)
  - [5. "Logical patterns — Kết hợp nhiều pattern"](#5-logical-patterns--kết-hợp-nhiều-pattern)
  - [6. "Property patterns — Kiểm tra property bên trong object"](#6-property-patterns--kiểm-tra-property-bên-trong-object)
  - [7. "Positional patterns — Match với deconstructors"](#7-positional-patterns--match-với-deconstructors)
  - [8. "List patterns — Áp dụng cho mảng và collection"](#8-list-patterns--áp-dụng-cho-mảng-và-collection)
  - [9. "`var` patterns — always match"](#9-var-patterns--always-match)
  - [10. "Pattern matching trong switch expressions"](#10-pattern-matching-trong-switch-expressions)
  - [11. "Pattern matching với when — guard clauses"](#11-pattern-matching-với-when--guard-clauses)
  - [12. Tóm tắt nhanh](#12-tóm-tắt-nhanh)
- [II. DISCARDS](#ii-discards)
  - [1. "Discards trong C# là gì?"](#1-discards-trong-c-là-gì)
  - [2. "Dùng discards khi deconstruct object"](#2-dùng-discards-khi-deconstruct-object)
  - [3. "Dùng discards với pattern matching"](#3-dùng-discards-với-pattern-matching)
  - [4. "Dùng discards trong switch expressions"](#4-dùng-discards-trong-switch-expressions)
  - [5. "Dùng discards với out parameters"](#5-dùng-discards-với-out-parameters)
  - [6. "Dùng discards trong tuple assignment"](#6-dùng-discards-trong-tuple-assignment)
  - [7. "Discards trong lambda expression"](#7-discards-trong-lambda-expression)
  - [8. "Khi nào dùng discards?"](#8-khi-nào-dùng-discards)
  - [9. Tóm tắt nhanh](#9-tóm-tắt-nhanh)
- [III. DECONSTRUCTING TUPLES AND OTHER TYPES](#iii-deconstructing-tuples-and-other-types)
  - [1. "Deconstruction trong C# là gì?"](#1-deconstruction-trong-c-là-gì)
  - [2. "Deconstruct một tuple"](#2-deconstruct-một-tuple)
  - [3. "Deconstruct bằng discards"](#3-deconstruct-bằng-discards)
  - [4. "Deconstruct các type tùy chỉnh (records, classes, structs)"](#4-deconstruct-các-type-tùy-chỉnh-records-classes-structs)
  - [5. "Deconstruct object theo property patterns"](#5-deconstruct-object-theo-property-patterns)
  - [6. "Tạo custom deconstruction cho class/struct"](#6-tạo-custom-deconstruction-cho-classstruct)
  - [7. "Deconstruction với var và kiểu rõ ràng"](#7-deconstruction-với-var-và-kiểu-rõ-ràng)
    - [Dùng var:](#dùng-var)
    - [Khai báo kiểu rõ ràng:](#khai-báo-kiểu-rõ-ràng)
  - [8. "Deconstruction trong foreach"](#8-deconstruction-trong-foreach)
  - [9. "Deconstruction \& extension methods"](#9-deconstruction--extension-methods)
  - [10. Tóm tắt nhanh](#10-tóm-tắt-nhanh)


---

# I. PATTERN MATCHING

---

## 1. "Pattern matching trong C# là gì?"

Pattern matching là kỹ thuật cho phép bạn:

* Kiểm tra **hình dạng**, **kiểu**, hoặc **giá trị** của dữ liệu.
* Trích xuất dữ liệu phù hợp từ object.
* Viết code rõ ràng hơn, súc tích hơn.

Sử dụng nhiều trong functional programming để thay thế `if` / `switch` dài dòng.

---

## 2. "Type patterns — Kiểm tra kiểu của object"

Ví dụ:

```csharp
object obj = "hello";

if (obj is string s)
{
    Console.WriteLine(s.ToUpper());
}
```

C# tự cast `obj` sang `string` thành biến `s` nếu đúng kiểu.

---

## 3. "Constant patterns — So khớp với giá trị cụ thể"

```csharp
int x = 10;

string result = x switch
{
    0 => "Zero",
    10 => "Ten",
    _ => "Other"
};
```

---

## 4. "Relational patterns — So sánh bằng <, >, <=, >="

```csharp
int age = 25;

string category = age switch
{
    < 13 => "Child",
    < 20 => "Teen",
    < 60 => "Adult",
    _ => "Senior"
};
```

---

## 5. "Logical patterns — Kết hợp nhiều pattern"

C# hỗ trợ:

* `and`
* `or`
* `not`

Ví dụ:

```csharp
int n = 5;

bool ok = n is > 0 and < 10;
```

---

## 6. "Property patterns — Kiểm tra property bên trong object"

Ví dụ:

```csharp
Person p = new("Alice", 30);

string label = p switch
{
    { Age: < 18 } => "Minor",
    { Age: >= 18 and < 60 } => "Adult",
    _ => "Senior"
};
```

Property patterns hoạt động cả với **record**, **class** và **struct**.

---

## 7. "Positional patterns — Match với deconstructors"

```csharp
public record Point(int X, int Y);

var p = new Point(3, 4);

string pos = p switch
{
    (0, 0) => "Origin",
    (var x, var y) when x == y => "On diagonal",
    _ => "Other"
};
```

C# tự gọi `Deconstruct()` khi pattern matching.

---

## 8. "List patterns — Áp dụng cho mảng và collection"

```csharp
int[] nums = [1, 2, 3, 4];

bool matched = nums is [1, 2, ..];
```

Các cú pháp:

* `[a, b]` — match 2 phần tử
* `[a, ..]` — bắt đầu bằng a
* `[.., b]` — kết thúc bằng b
* `[a, .., b]` — bắt đầu a, kết thúc b

---

## 9. "`var` patterns — always match"

Dùng để bắt giá trị, không kiểm tra điều kiện.
Ví dụ:

```csharp
object o = 42;

var r = o switch
{
    var x => $"Value: {x}"
};
```

---

## 10. "Pattern matching trong switch expressions"

Switch expressions giúp code ngắn và rõ ràng hơn:

```csharp
string GetColorName(ConsoleColor c) => c switch
{
    ConsoleColor.Red => "Red",
    ConsoleColor.Green => "Green",
    ConsoleColor.Blue => "Blue",
    _ => "Unknown"
};
```

---

## 11. "Pattern matching với when — guard clauses"

```csharp
int score = 95;

string grade = score switch
{
    var v when v >= 90 => "A",
    var v when v >= 75 => "B",
    _ => "C"
};
```

---

## 12. Tóm tắt nhanh

| Pattern                | Ý nghĩa                 |
| ---------------------- | ----------------------- |
| **Type pattern**       | Kiểm tra & cast kiểu    |
| **Constant pattern**   | Match literal           |
| **Relational pattern** | So sánh < > <= >=       |
| **Logical pattern**    | Kết hợp pattern         |
| **Property pattern**   | Match theo property     |
| **Positional pattern** | Match tuple/deconstruct |
| **List pattern**       | Match mảng/collection   |
| **Var pattern**        | Bắt giá trị, luôn true  |

---

# II. DISCARDS

---

## 1. "Discards trong C# là gì?"

**Discards** là biến đặc biệt được biểu diễn bằng dấu gạch dưới `_` dùng để:

* Bỏ qua giá trị bạn *không cần dùng*
* Không chiếm bộ nhớ như biến thông thường
* Không được đọc lại (unreadable variable)

Discards giúp code rõ ràng hơn và tránh tạo biến không cần thiết.

---

## 2. "Dùng discards khi deconstruct object"

Nếu bạn chỉ cần một vài thành phần khi deconstruct:

```csharp
var (x, _) = GetPoint();
```

Hoặc bỏ tất cả:

```csharp
var _ = GetPoint();
```

Ví dụ đầy đủ:

```csharp
public record Point(int X, int Y);
var p = new Point(3, 4);
var (a, _) = p;   // chỉ dùng giá trị X
```

---

## 3. "Dùng discards với pattern matching"

```csharp
if (obj is Person { Age: _ })
{
    Console.WriteLine("It is a Person");
}
```

Hoặc:

```csharp
if (obj is Person(_, _))
{
    Console.WriteLine("Matched");
}
```

Khi bạn không quan tâm đến giá trị property.

---

## 4. "Dùng discards trong switch expressions"

```csharp
string Classify(object obj) => obj switch
{
    Person(_, _) => "A person",
    _ => "Unknown"
};
```

Discards ở đây giúp mô tả cấu trúc mà không cần dùng giá trị.

---

## 5. "Dùng discards với out parameters"

Ví dụ với `int.TryParse`:

```csharp
if (int.TryParse("123", out _))
    Console.WriteLine("OK");
```

Bạn chỉ muốn biết kết quả thành công hay thất bại, không cần giá trị.

---

## 6. "Dùng discards trong tuple assignment"

```csharp
(_, int y) = (10, 20);
Console.WriteLine(y); // 20
```

Discards bỏ qua giá trị 10.

---

## 7. "Discards trong lambda expression"

Khi bạn buộc phải khai báo tham số nhưng *không dùng nó*:

```csharp
Func<int, int> f = _ => 5;
```

Mọi input đều trả về 5, và `_` không dùng đến.

---

## 8. "Khi nào dùng discards?"

| Tình huống       | Ví dụ                  | Ý nghĩa                     |
| ---------------- | ---------------------- | --------------------------- |
| Deconstruction   | `(var x, _) = ...`     | Bỏ giá trị không cần thiết  |
| out parameters   | `TryParse(..., out _)` | Không lưu giá trị trả về    |
| Pattern matching | `Person(_, _)`         | Không quan tâm đến property |
| Lambdas          | `_ => ...`             | Không cần dùng tham số      |
| Tuples           | `(_, y) = ...`         | Bỏ thành phần tuple         |

---

## 9. Tóm tắt nhanh

* `_` là **discard variable**
* Không thể đọc lại `_`
* Có thể dùng `_` nhiều lần trong cùng một biểu thức
* Giúp code ngắn, rõ ràng, tránh tạo biến thừa

---

# III. DECONSTRUCTING TUPLES AND OTHER TYPES

---

## 1. "Deconstruction trong C# là gì?"

**Deconstruction** là kỹ thuật giúp bạn "tách" (unpack) một object hoặc tuple thành nhiều biến riêng biệt.

Cú pháp:

```csharp
(var a, var b) = tupleOrObject;
```

Deconstruction làm code gọn, rõ ràng, đặc biệt khi làm việc với tuples và records.

---

## 2. "Deconstruct một tuple"

Tuples hỗ trợ deconstruction mặc định.

```csharp
var point = (3, 4);
(var x, var y) = point;
Console.WriteLine(x); // 3
Console.WriteLine(y); // 4
```

Bạn cũng có thể bỏ kiểu:

```csharp
(var x, var y) = (10, 20);
```

---

## 3. "Deconstruct bằng discards"

Bạn có thể bỏ qua giá trị không cần dùng:

```csharp
(_, var y) = (10, 20);
Console.WriteLine(y); // 20
```

---

## 4. "Deconstruct các type tùy chỉnh (records, classes, structs)"

Các type tùy chỉnh hỗ trợ deconstruction thông qua method **Deconstruct**.

Ví dụ với record:

```csharp
public record Person(string Name, int Age);

var p = new Person("Alice", 30);
var (name, age) = p;
```

Ngầm hiểu:

```csharp
public void Deconstruct(out string name, out int age)
{
    name = Name;
    age = Age;
}
```

---

## 5. "Deconstruct object theo property patterns"

```csharp
Person p = new("Bob", 40);

var (name, age) = p;   // dùng Deconstruct
Console.WriteLine(name);
```

Dùng trong switch expression:

```csharp
string label = p switch
{
    ("Bob", 40) => "Matched Bob",
    _ => "Other"
};
```

---

## 6. "Tạo custom deconstruction cho class/struct"

Bạn có thể tự định nghĩa Deconstruct method:

```csharp
public class Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y) => (X, Y) = (x, y);

    public void Deconstruct(out int x, out int y)
    {
        x = X;
        y = Y;
    }
}
```

Dùng:

```csharp
var p = new Point(5, 6);
var (x, y) = p;
```

---

## 7. "Deconstruction với var và kiểu rõ ràng"

### Dùng var:

```csharp
var (a, b) = (1, 2);
```

### Khai báo kiểu rõ ràng:

```csharp
(int a, int b) = (3, 4);
```

---

## 8. "Deconstruction trong foreach"

```csharp
var points = new List<(int X, int Y)> { (1, 2), (3, 4) };

foreach (var (x, y) in points)
    Console.WriteLine($"{x}, {y}");
```

Hoặc với type tùy chỉnh có Deconstruct:

```csharp
foreach (var (name, age) in people)
    Console.WriteLine($"{name} is {age}");
```

---

## 9. "Deconstruction & extension methods"

Bạn có thể mở rộng bất kỳ type nào bằng cách thêm Deconstruct():

```csharp
public static class Extensions
{
    public static void Deconstruct(this DateTime dt, out int year, out int month, out int day)
    {
        year = dt.Year;
        month = dt.Month;
        day = dt.Day;
    }
}
```

Dùng:

```csharp
var (year, month, day) = DateTime.Now;
```

---

## 10. Tóm tắt nhanh

| Khái niệm                  | Ý nghĩa                                    |
| -------------------------- | ------------------------------------------ |
| **Tuple deconstruction**   | Tách tuple thành nhiều biến                |
| **Custom Deconstruct**     | Tạo deconstruction cho class/struct/record |
| **Discard `_`**            | Bỏ giá trị không cần                       |
| **Switch deconstruction**  | Dùng tuple hoặc patterns trong switch      |
| **Foreach deconstruction** | Tách mỗi phần tử khi lặp                   |
| **Extension Deconstruct**  | Mở rộng type có sẵn                        |

---
