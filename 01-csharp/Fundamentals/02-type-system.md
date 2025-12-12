# 📘 C# TYPE SYSTEM

**Version:** 1.0
**Updated:** 12/12/2025
**Author:** Vox

---

# 📚 Mục lục

- [Overview](#i-overview)
- [Namespaces](#ii-namespaces)
- [Classes](#iii-classes)
- [Records](#iv-records)
- [Interfaces](#v-interfaces)
- [Generics](#vi-generics)
- [Tuples and anonymous types](#vii-tuples--anonymous-types)

---

# I. OVERVIEW

## 1. "C# là ngôn ngữ strongly typed nghĩa là gì?"

C# là ngôn ngữ **strongly typed**, nghĩa là:

* Mọi **biến**, **hằng**, **biểu thức** đều có **một kiểu xác định rõ ràng**.
* Mọi **phương thức** đều khai báo kiểu trả về và kiểu của từng tham số.
* Không có chuyển đổi kiểu ngầm định không an toàn.

Thư viện lớp của .NET cung cấp:

* Các **kiểu số** (numeric types)
* Các kiểu phức tạp mô tả: hệ thống file, kết nối mạng, collections, arrays, ngày tháng...

Một chương trình C# điển hình sử dụng:

* Các **kiểu có sẵn** từ class library
* Các **kiểu tự định nghĩa** mô tả domain của ứng dụng

---

## 2. "Thông tin mà một kiểu dữ liệu lưu trữ gồm những gì?"

Một type trong C# có thể chứa thông tin về:

* Bộ nhớ cần thiết để lưu biến
* Giá trị tối đa và tối thiểu
* Các thành viên: methods, fields, events…
* Kiểu cơ sở (base type)
* Interface mà nó implement
* Các phép toán hợp lệ

Compiler dùng những thông tin này để đảm bảo **type safety**.

Ví dụ:

```csharp
int a = 5;
int b = a + 2; // OK

bool test = true;

// Lỗi: không thể cộng int và bool
int c = a + test;
```

Ghi chú cho người học C/C++: **bool không chuyển đổi sang int trong C#**.

CLR nhúng metadata kiểu vào file thực thi và dùng metadata này lúc chạy để đảm bảo an toàn.

---

## 3. "Specifying types in variable declarations" – Cách khai báo kiểu cho biến

Khi khai báo biến hoặc hằng, bạn phải:

* Chỉ rõ **kiểu dữ liệu**, hoặc
* Dùng `var` để compiler tự suy luận kiểu.

Ví dụ:

```csharp
float temperature;
string name;
MyClass myClass;

char firstLetter = 'C';
var limit = 3;
int[] source = [0, 1, 2, 3, 4, 5];

var query = from item in source
            where item <= limit
            select item;
```

### Kiểu tham số và kiểu trả về của phương thức

```csharp
public string GetName(int ID)
{
    if (ID < names.Length)
        return names[ID];
    else
        return String.Empty;
}

private string[] names = ["Spencer", "Sally", "Doug"]; 
```

### Quy tắc quan trọng

* Không thể **khai báo lại biến** với kiểu khác.
* Không thể gán giá trị **khác kiểu** cho biến.
* Compiler tự thực hiện **implicit conversion** khi an toàn.
* **Explicit cast** bắt buộc khi có nguy cơ mất dữ liệu.

---

## 4. Built-in types – Các kiểu dựng sẵn trong C#

C# cung cấp các kiểu built‑in:

* Kiểu nguyên (integers)
* Kiểu dấu phẩy động (floating point)
* bool
* char
* decimal
* string
* object

Danh sách chi tiết: *Built-in types (Microsoft Docs)*.

---

## 5. Custom types – Kiểu tự định nghĩa

Bạn có thể tạo type bằng:

* `struct`
* `class`
* `interface`
* `enum`
* `record`

Class library .NET cũng chính là tập hợp của các custom types.

### Hướng dẫn chọn loại type phù hợp:

* <64 bytes → struct hoặc record struct
* Immutable → struct hoặc record struct
* Value semantics → record class hoặc record struct
* Chủ yếu chứa dữ liệu → record
* Có kế thừa → class hoặc record class
* Dùng polymorphism → class
* Chủ yếu chứa hành vi → class

---

## 6. The Common Type System (CTS)

Hai sự thật quan trọng về hệ thống kiểu .NET:

### 1) **Hỗ trợ kế thừa**

* Mọi type đều kế thừa từ **System.Object**.
* int = System.Int32
* string = System.String

### 2) **Mọi type đều là value type hoặc reference type**

* `struct`, `record struct` → value type
* `class`, `record`, `record class`, `delegate`, `interface`, `array` → reference type

CTS đảm bảo mọi ngôn ngữ .NET đều dùng chung hệ thống kiểu.

---

## 7. Classes vs Structs vs Records

### Class

* Reference type
* Lưu trên heap
* Gán biến → chia sẻ cùng object
* Hỗ trợ kế thừa

### Struct

* Value type
* Lưu trực tiếp dữ liệu
* Copy khi gán sang biến khác
* Không thể kế thừa struct khác
* Có thể implement interface(s)

### Record

* Có thể là reference type hoặc value type
* Hỗ trợ value-equality
* Phù hợp mô hình dữ liệu immutable

---

## 8. Value types

Giá trị lưu trực tiếp, không cần heap allocation.

### Hai loại:

#### 1) struct

Ví dụ:

```csharp
public struct Coords(int x, int y)
{
    public int X { get; init; } = x;
    public int Y { get; init; } = y;
}
```

#### 2) enum

Ví dụ:

```csharp
public enum FileMode
{
    CreateNew = 1,
    Create = 2,
    Open = 3,
    OpenOrCreate = 4,
    Truncate = 5,
    Append = 6,
}
```

---

## 9. Reference types

Bao gồm: class, record class, record, delegate, array, interface.

Ví dụ:

```csharp
MyClass myClass = new();
MyClass myClass2 = myClass; // cùng tham chiếu
```

### Interface

Không thể tạo instance trực tiếp.

```csharp
IMyInterface obj = new MyClass();
```

### Arrays

Luôn là reference type.

```csharp
int[] nums = [1, 2, 3, 4, 5];
int len = nums.Length;
```

Reference types hỗ trợ kế thừa đầy đủ.

---

## 10. Literal types – Kiểu của literal values

Compiler gán type cho literal.

Ví dụ:

```csharp
string s = "The answer is " + 5.ToString();

Type type = 12345.GetType(); // System.Int32
```

Bạn có thể dùng hậu tố để chỉ định kiểu:

* `4.56f` → float
* `4.56d` → double
* `10m` → decimal

---

## 11. Generic types

Generic type có **type parameter**.
Ví dụ:

```csharp
List<string> stringList = new List<string>();
stringList.Add("String example");
stringList.Add(4); // lỗi
```

Generic collections là **strongly typed collections**.

---

## 12. Implicit types, anonymous types, nullable types

### `var`

* Suy luận kiểu tại compile-time
* Không phải dynamic

### Anonymous types

Dùng cho dữ liệu tạm thời không cần đặt tên kiểu.

### Nullable value types

```csharp
int? age = null;
```

Hữu ích khi làm việc với database.

---

## 13. Compile-time type vs Run-time type

Biến có thể có **hai loại kiểu khác nhau**:

* Compile-time type: kiểu được khai báo
* Runtime type: kiểu thực sự của object được gán

Ví dụ:

```csharp
object msg = "hello";          // compile-time: object, runtime: string
IEnumerable<char> chars = "abc"; // runtime: string
```

Compile-time quyết định:

* Chọn phương thức (method resolution)
* Overload resolution
* Implicit/explicit cast hợp lệ

Runtime quyết định:

* Dispatch virtual methods
* Kiểm tra kiểu (is / switch)

---

# 🌟 II. NAMESPACES

---

## 1. "Namespace là gì trong C#?"

**Note:** What are namespaces?

**Trả lời:**
Namespace là cách C# dùng để **nhóm các kiểu (types)** liên quan lại với nhau và **tránh xung đột tên** trong chương trình.

Ví dụ:

```csharp
namespace SampleNamespace
{
    class MyClass { }
}
```

Namespaces giúp tổ chức code logic, dễ đọc, dễ quản lý — đặc biệt khi dự án lớn.

---

## 2. "Tại sao cần namespaces?"

Namespaces giúp:

* Tránh trùng tên giữa các class khác nhau
* Chia module theo chức năng
* Tổ chức code thành cấu trúc rõ ràng
* Tách các thành phần framework và code người dùng

Ví dụ: `System.IO.File` và `MyApp.IO.File` có thể tồn tại song song mà không xung đột.

---

## 3. "Cú pháp khai báo namespace"

Có hai dạng chính:

### **Dạng truyền thống (block):**

```csharp
namespace MyCompany.Project.Module
{
    class Example { }
}
```

### **Dạng file-scoped namespace (C# 10+):**

```csharp
namespace MyCompany.Project.Module;

class Example { }
```

Dạng file-scoped giúp giảm mức thụt lề và làm file ngắn gọn hơn.

---

## 4. "Nested namespaces – Namespace lồng nhau"

Bạn có thể khai báo namespace trong namespace khác:

```csharp
namespace Company
{
    namespace Product
    {
        class Example { }
    }
}
```

Hoặc viết gọn:

```csharp
namespace Company.Product
{
    class Example { }
}
```

---

## 5. "Sử dụng namespaces – từ khóa using"

Dùng `using` để truy cập type mà không cần viết đầy đủ tên namespace:

```csharp
using System;

Console.WriteLine("Hello world");
```

Không dùng `using`:

```csharp
System.Console.WriteLine("Hello world");
```

---

## 6. "Global using directives (C# 10+)"

Bạn có thể khai báo using dùng toàn dự án:

```csharp
global using System;
global using System.IO;
```

Ưu điểm: không phải thêm using đầu mỗi file.

---

## 7. "Alias namespaces – đặt tên tắt cho namespace"

Dùng từ khóa `using` để tạo alias:

```csharp
using ProjectModels = MyCompany.MyProject.Models;

ProjectModels.User user = new();
```

Điều này hữu ích khi namespaces dài hoặc trùng tên.

---

## 8. "Phạm vi (scope) của namespace"

Namespace có thể bao gồm:

* Class
* Struct
* Enum
* Interface
* Record
* Namespace con

Namespace **không** thể chứa biến hoặc logic thực thi.

---

## 9. "Namespace System là gì?"

`System` là namespace gốc của phần lớn các API .NET:

* `System.Console`
* `System.String`
* `System.Collections`
* `System.IO`
* ...

Nó là namespace quan trọng nhất trong .NET.

---

## 10. "Namespaces không ảnh hưởng đến Value type hay Reference type"

Ví dụ:

* `System.Int32` là value type
* `System.String` là reference type

Namespace **chỉ là vị trí logic**, không ảnh hưởng bản chất type.

---

## 11. "Namespaces và file organization"

Namespaces **không bắt buộc** phải trùng với cấu trúc folder, nhưng nên tuân theo quy ước:

```
Project
 ├── Models
 │     └── User.cs (namespace Project.Models)
 ├── Services
 │     └── AuthService.cs (namespace Project.Services)
```

Việc này giúp code dễ tìm và dễ quản lý.

---

## 12. "Có required namespaces không?"

Trong nhiều template .NET, compiler thêm một số **implicit global using**, ví dụ:

* `System`
* `System.Collections.Generic`
* `System.Linq`
* `System.Threading.Tasks`

Điều này làm code ngắn hơn trong .NET 6+.

---

# 🌟 III. CLASSES

---

## 1. "Class trong C# là gì?"

**Note:** What is a class?

**Trả lời:**
Class là **kiểu tham chiếu (reference type)** dùng để mô hình hóa dữ liệu và hành vi của một đối tượng trong chương trình.
Một class là **bản thiết kế** (blueprint) mô tả:

* Các **trường (fields)**
* Các **thuộc tính (properties)**
* Các **phương thức (methods)**
* Các **sự kiện (events)**

Object được tạo từ class bằng từ khóa `new`.

Ví dụ:

```csharp
public class Person
{
    public string Name;
    public int Age;
}

Person p = new Person();
```

---

## 2. "Class có những thành phần gì?"

**Note:** Members of a class

Một class có thể chứa:

* **Fields:** lưu trữ dữ liệu
* **Constructors:** khởi tạo object
* **Methods:** hành vi
* **Properties:** truy cập dữ liệu an toàn
* **Events:** thông báo thay đổi
* **Indexers, operators, nested types**

---

## 3. "Cách định nghĩa một class"

**Note:** Declaring classes

Ví dụ cơ bản:

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public void Introduce()
    {
        Console.WriteLine($"Hi, I'm {Name}.");
    }
}
```

---

## 4. "Tạo object từ class"

**Note:** Instantiating classes

Dùng từ khóa `new`:

```csharp
Person p = new Person();
p.Name = "Vox";
p.Introduce();
```

Class là reference type → biến chỉ lưu **tham chiếu** đến object.

```csharp
Person p2 = p;
p2.Name = "New Name";
// p.Name cũng thay đổi
```

---

## 5. "Constructors – Hàm tạo"

**Note:** Constructors

Constructor được gọi khi object được tạo:

```csharp
public class Car
{
    public string Model { get; }

    public Car(string model)
    {
        Model = model;
    }
}
```

Dùng:

```csharp
var c = new Car("Mazda");
```

---

## 6. "Static members và static classes"

**Note:** Static classes & members

### Static member

Thuộc về class, không thuộc object.

```csharp
public class MathUtil
{
    public static double Pi = 3.14;
}

double p = MathUtil.Pi;
```

### Static class

Không thể tạo instance.

```csharp
public static class Helpers
{
    public static void Print() => Console.WriteLine("Hello");
}
```

---

## 7. "Inheritance – kế thừa giữa các classes"

**Note:** Inheritance basics

Một class có thể kế thừa một class khác:

```csharp
class Animal { }
class Dog : Animal { }
```

Dog thừa hưởng các thành viên của Animal.

C# chỉ hỗ trợ **kế thừa đơn (single inheritance)**.

---

## 8. "Accessibility – các mức truy cập trong class"

**Note:** Access modifiers

Các từ khóa truy cập gồm:

* `public`
* `private`
* `protected`
* `internal`
* `protected internal`
* `private protected`

Ví dụ:

```csharp
class Person
{
    private int age;
    public string Name;
}
```

---

## 9. "Object lifetime – vòng đời của object"

**Note:** Object lifetime & garbage collection

* Object được cấp phát trên **heap** khi dùng `new`.
* CLR tự động thu thập rác (garbage collection).
* Không cần giải phóng bộ nhớ thủ công như C++.

---

## 10. "Partial classes"

**Note:** Partial classes

Cho phép chia class thành nhiều file:

```csharp
public partial class Person
{
    public void A() { }
}

public partial class Person
{
    public void B() { }
}
```

Hữu ích khi code dài hoặc có tool sinh code.

---

## 11. "Anonymous classes (anonymous types)"

**Note:** Anonymous types

Tạo object không có tên class:

```csharp
var person = new { Name = "Vox", Age = 25 };
```

Thường dùng trong LINQ.

---

## 12. "Classes vs Structs vs Records (summary)"

| Loại       | Reference / Value    | Dùng khi                  |
| ---------- | -------------------- | ------------------------- |
| **Class**  | Reference type       | Hành vi phức tạp, mutable |
| **Struct** | Value type           | Dữ liệu nhỏ, immutable    |
| **Record** | Reference hoặc Value | Mô hình dữ liệu, equality |

---

# 🌟 IV. RECORDS

---

## 1. "Record là gì trong C#?"

**Note:** What is a record?

**Trả lời:**
Record là một **kiểu dữ liệu đặc biệt** trong C# được thiết kế để:

* Mô hình hóa **dữ liệu** (data models) thay vì hành vi
* Hỗ trợ **value-based equality** (so sánh dựa trên giá trị, không phải tham chiếu)
* Dễ tạo các kiểu **immutable** (bất biến)

Record có thể là **reference type** hoặc **value type**:

* `record class` (reference type – mặc định)
* `record struct` (value type)

---

## 2. "Cú pháp khai báo record"

**Note:** Declaring records

### **Record class:**

```csharp
public record Person(string FirstName, string LastName);
```

### **Record struct:**

```csharp
public readonly record struct Point(int X, int Y);
```

Cú pháp ngắn gọn cho phép tạo model dữ liệu rất rõ ràng.

---

## 3. "Record hỗ trợ equality như thế nào?"

**Note:** Value-based equality

### Với record:

Hai record bằng nhau nếu **tất cả thuộc tính của chúng bằng nhau**.

Ví dụ:

```csharp
var p1 = new Person("Vox", "Nguyen");
var p2 = new Person("Vox", "Nguyen");

Console.WriteLine(p1 == p2); // True
```

### Với class thông thường:

```csharp
var c1 = new MyClass("Vox");
var c2 = new MyClass("Vox");

Console.WriteLine(c1 == c2); // False (so sánh tham chiếu)
```

→ **Record giúp so sánh dữ liệu dễ dàng và chính xác hơn.**

---

## 4. "Record có immutable không?"

**Note:** Immutability

Record **mặc định thiết kế để bất biến**.
Tuy nhiên, bạn vẫn có thể khai báo record mutable nếu muốn.

Ví dụ immutable:

```csharp
public record Person(string Name, int Age);
```

Ví dụ mutable:

```csharp
public record Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

---

## 5. "Vậy nondestructive mutation là gì?"

**Note:** with-expressions

Bạn có thể tạo object mới dựa trên object cũ bằng cú pháp `with`:

```csharp
var p1 = new Person("Vox", 25);
var p2 = p1 with { Age = 26 };
```

* Không thay đổi `p1`
* `p2` là bản sao mới có thuộc tính thay đổi

Đây gọi là **nondestructive mutation**.

---

## 6. "Record có thể kế thừa không?"

**Note:** Inheritance

### Record class hỗ trợ kế thừa:

```csharp
public record Animal(string Name);
public record Dog(string Name, string Breed) : Animal(Name);
```

### Record struct **không hỗ trợ kế thừa** (như struct).

---

## 7. "Positional record là gì?"

**Note:** Positional syntax

Cú pháp khai báo record ngắn gọn:

```csharp
public record Person(string FirstName, string LastName);
```

Compiler sẽ tự sinh:

* Constructor
* Deconstructor
* Các property dạng init-only
* Equality members
* ToString()

Bạn có thể mở rộng thêm thành phần nếu muốn.

---

## 8. "Record có thể chứa methods, events và other members không?"

**Note:** Members in records

Có. Record có thể chứa mọi loại thành viên giống class hoặc struct.

Ví dụ:

```csharp
public record Person(string Name)
{
    public void Print() => Console.WriteLine($"Hello {Name}");
}
```

---

## 9. "Deconstruction trong record là gì?"

**Note:** Deconstructors

```csharp
var person = new Person("Vox", "Nguyen");
var (first, last) = person;
```

→ Compiler tự tạo `Deconstruct(out string, out string)`.

---

## 10. "Record struct khác gì so với record class?"

**Note:** Record struct vs Record class

| Đặc điểm      | record class   | record struct |
| ------------- | -------------- | ------------- |
| Loại          | Reference type | Value type    |
| Equality      | Value-based    | Value-based   |
| Kế thừa       | Có             | Không         |
| Tính bất biến | Khuyến nghị    | Khuyến nghị   |

---

## 11. "Record phù hợp dùng khi nào?"

**Note:** When to use records

Dùng record khi:

* Bạn cần mô hình hóa dữ liệu bất biến
* Bạn cần value-equality
* Bạn dùng nhiều với pattern matching
* Bạn làm việc với DTOs, configuration models, view models

Không nên dùng khi:

* Bạn cần behavior phức tạp
* Bạn cần mutable objects nhiều

---

## 12. "Record có hỗ trợ 'primary constructor' như class không?"

**Note:** Primary constructors in records

Có. Record hỗ trợ đầy đủ primary constructor như class.

Ví dụ:

```csharp
public record Order(int Id, DateTime Created);
```

---

## 13. "Override trong record"

**Note:** Overriding synthesized members

Bạn có thể override các member compiler tự sinh:

```csharp
public record Person(string Name)
{
    public override string ToString() => $"Person: {Name}";
}
```

---

## 14. "Pattern matching với record"

**Note:** Pattern matching

Records hoạt động tuyệt vời với pattern matching:

```csharp
if (p1 is Person { Name: "Vox" })
{
    Console.WriteLine("Match!");
}
```

---

# 🌟 V. INTERFACES

---

## 1. "Interface là gì trong C#?"

**Note:** What is an interface?

**Trả lời:**
Interface là một **hợp đồng (contract)** mô tả **các thành viên mà một type phải triển khai**, nhưng **không cung cấp implementation** (ngoại trừ default interface members trong C# 8 trở lên).

Interface có thể chứa:

* Method signatures
* Properties
* Events
* Indexers
* Default implementations (C# 8+)

Interface **không thể chứa**:

* Fields
* Constructors
* Finalizers

Một class hoặc struct **có thể implement nhiều interface**, giúp hỗ trợ mô hình đa kế thừa (multiple inheritance of behavior).

---

## 2. "Khai báo interface như thế nào?"

**Note:** Declaring an interface

Ví dụ một interface đơn giản:

```csharp
public interface ILogger
{
    void Log(string message);
}
```

Class implement interface:

```csharp
public class ConsoleLogger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine(message);
    }
}
```

Struct cũng có thể implement interface:

```csharp
public struct FileLogger : ILogger
{
    public void Log(string message)
    {
        // Write to file
    }
}
```

---

## 3. "Explicit interface implementation" – triển khai tường minh

**Note:** Explicit interface implementation

Dùng khi:

* Interface có thành viên trùng tên hoặc trùng chữ ký
* Muốn **giấu** implementation khỏi API công khai

Ví dụ:

```csharp
public interface IControl
{
    void Paint();
}

public interface ISurface
{
    void Paint();
}

public class Sample : IControl, ISurface
{
    void IControl.Paint() => Console.WriteLine("Control");
    void ISurface.Paint() => Console.WriteLine("Surface");
}
```

Cách sử dụng:

```csharp
Sample s = new Sample();
// s.Paint(); ❌ lỗi – không truy cập được

((IControl)s).Paint();   // Control
((ISurface)s).Paint();   // Surface
```

---

## 4. "Default interface members" – thành viên mặc định (C# 8+)

**Note:** Default interface methods

Interface có thể cung cấp implementation mặc định:

```csharp
public interface ILogger
{
    void Log(string message);

    void LogError(string error)
        => Log($"ERROR: {error}");
}
```

Class implement không bắt buộc override:

```csharp
public class SimpleLogger : ILogger
{
    public void Log(string message)
        => Console.WriteLine(message);
}
```

Gọi:

```csharp
ILogger logger = new SimpleLogger();
logger.LogError("Oops");
```

---

## 5. "Interface inheritance" – interface có thể kế thừa interface khác

**Note:** Interface inheritance

Ví dụ:

```csharp
public interface IReadable
{
    void Read();
}

public interface IWritable
{
    void Write();
}

public interface IReadWrite : IReadable, IWritable
{
}
```

Class implement interface con:

```csharp
public class Document : IReadWrite
{
    public void Read() {}
    public void Write() {}
}
```

---

## 6. "Why use interfaces?" – Tại sao cần interface?

**Note:** Why use interfaces?

Interface mang lại các lợi ích:

* **Tách biệt abstraction và implementation**
* **Linh hoạt** – một class có thể implement nhiều interface
* **Giảm phụ thuộc (decoupling)** → dễ test hơn
* **Hỗ trợ dependency injection**
* **Thiết kế theo nguyên tắc SOLID** (đặc biệt là Interface Segregation)

Ví dụ mẫu DI:

```csharp
public class App
{
    private readonly ILogger _logger;
    public App(ILogger logger) => _logger = logger;
}
```

---

## 7. "Interface vs Abstract class"

**Note:** Difference between interface and abstract class

| Feature                | Interface         | Abstract class            |
| ---------------------- | ----------------- | ------------------------- |
| Constructors           | ❌ Không có        | ✔ Có                      |
| Fields                 | ❌ Không           | ✔ Có                      |
| Multiple inheritance   | ✔ Cho phép        | ❌ Không                   |
| Default implementation | ✔ C# 8+           | ✔                         |
| Use case               | Behavior contract | Base class + shared logic |

---

## 8. "Checking interface implementation" – kiểm tra object có implement interface không

**Note:** Checking interface support

```csharp
if (obj is ILogger logger)
    logger.Log("Hello");
```

Hoặc dùng `as`:

```csharp
ILogger? log = obj as ILogger;
if (log != null)
    log.Log("Hi");
```

---

## 9. "Interface với generic" (Generic interfaces)

**Note:** Generic interfaces

```csharp
public interface IRepository<T>
{
    T Get(int id);
    void Save(T item);
}

public class UserRepo : IRepository<User>
{
    public User Get(int id) => new();
    public void Save(User item) {}
}
```

---

## 10. "Interface và polymorphism"

**Note:** Polymorphism with interfaces

```csharp
public interface IShape
{
    double Area();
}

public class Circle : IShape
{
    public double Area() => Math.PI * 4;
}

public class Square : IShape
{
    public double Area() => 16;
}
```

Gọi polymorphism:

```csharp
IShape shape = new Circle();
Console.WriteLine(shape.Area());
```

---

# 🌟 VI. GENERICS

---

## 1. "Generics trong C# là gì?"

**Note:** What are generics?

**Trả lời:**
Generics cho phép bạn khai báo **kiểu dữ liệu có tham số hoá** (parameterized types). Thay vì cố định kiểu dữ liệu bên trong class, interface hoặc method, bạn có thể **trì hoãn việc xác định kiểu** cho đến khi tạo instance.

Ví dụ:

```csharp
List<int> numbers = new List<int>();
List<string> names = new List<string>();
```

Generics mang lại:

* **Hiệu năng tốt hơn** (không cần boxing/unboxing)
* **Type safety** – lỗi sai kiểu được phát hiện lúc compile
* **Tái sử dụng code**

---

## 2. "Khai báo generic class như thế nào?"

**Note:** Declaring generic classes

Ví dụ class generic:

```csharp
public class GenericList<T>
{
    private T[] _items = new T[10];
    private int _count;

    public void Add(T item)
    {
        _items[_count++] = item;
    }

    public T Get(int index) => _items[index];
}
```

Sử dụng:

```csharp
GenericList<int> list = new GenericList<int>();
list.Add(5);
int value = list.Get(0);
```

---

## 3. "Generic methods" – phương thức generic

**Note:** Generic methods

Phương thức có thể độc lập khai báo generic:

```csharp
public static void Swap<T>(ref T a, ref T b)
{
    T temp = a;
    a = b;
    b = temp;
}
```

Gọi:

```csharp
int x = 1, y = 2;
Swap<int>(ref x, ref y);
```

C# thường tự suy luận kiểu:

```csharp
Swap(ref x, ref y);
```

---

## 4. "Generic interfaces"

**Note:** Generic interfaces

Ví dụ:

```csharp
public interface IRepository<T>
{
    T Get(int id);
    void Add(T item);
}

public class UserRepository : IRepository<User>
{
    public User Get(int id) => new();
    public void Add(User item) {}
}
```

---

## 5. "Type constraints" – ràng buộc kiểu

**Note:** Constraints on type parameters

Dùng từ khoá `where` để giới hạn kiểu T.

### Các loại constraints:

#### ✔ `where T : struct`

T phải là **value type**:

```csharp
public void Process<T>() where T : struct {}
```

#### ✔ `where T : class`

T phải là **reference type**:

```csharp
public void Save<T>() where T : class {}
```

#### ✔ `where T : new()`

T phải có **constructor không tham số**:

```csharp
public T Create<T>() where T : new()
{
    return new T();
}
```

#### ✔ `where T : BaseClass`

T phải kế thừa từ BaseClass:

```csharp
public void Log<T>() where T : Logger {}
```

#### ✔ `where T : interface`

T phải implement interface:

```csharp
public void Print<T>() where T : IPrintable {}
```

#### ✔ Nhiều constraints cùng lúc

```csharp
public void Test<T>() where T : class, IPrintable, new() {}
```

---

## 6. "Covariance và Contravariance" (C# 4+)

**Note:** Variance in generics

Variance áp dụng cho **generic interfaces và delegates**.

### ✔ Covariance (`out`)

Cho phép **T derived → T base**

```csharp
IEnumerable<string> s = new List<string>();
IEnumerable<object> o = s; // OK
```

### ✔ Contravariance (`in`)

Cho phép **T base → T derived**

```csharp
IComparer<object> comp1 = ...;
IComparer<string> comp2 = comp1; // OK
```

### ✔ Invariance

List<T> **không hỗ trợ variance**:

```csharp
List<string> a = new();
List<object> b = a;  // ❌ lỗi
```

---

## 7. "Benefits of generics" – Tại sao dùng generics?

**Note:** Benefits of generics

Generics mang lại 3 lợi ích lớn:

### ✔ 1. Type safety

Lỗi sai kiểu được phát hiện tại compile-time.

```csharp
List<int> nums = new();
// nums.Add("abc"); ❌ lỗi compile
```

### ✔ 2. Hiệu năng tốt hơn

Tránh boxing/unboxing cho value types.

```csharp
List<int> nums = new();
```

Không cần:

```csharp
ArrayList list = new();
list.Add(5); // boxing
```

### ✔ 3. Tái sử dụng code

Một generic class xử lý nhiều loại kiểu dữ liệu.

---

## 8. "Built-in generic types" – các kiểu dựng sẵn

**Note:** Built-in generic types

Một số kiểu generic quan trọng trong .NET:

* `List<T>`
* `Dictionary<TKey, TValue>`
* `Queue<T>`
* `Stack<T>`
* `IEnumerable<T>`
* `Task<T>`
* `Nullable<T>` (`T?`)

Ví dụ:

```csharp
Dictionary<int, string> dict = new();
dict[1] = "Hello";
```

---

## 9. "Generic delegates"

**Note:** Generic delegates

Ví dụ các delegate generic phổ biến:

* `Func<T>`
* `Func<TInput, TOutput>`
* `Action<T>`
* `Predicate<T>`

Ví dụ:

```csharp
Func<int, int> square = x => x * x;
Console.WriteLine(square(5));
```

---

## 10. "Type inference" – suy luận kiểu

**Note:** Type inference in generics

Compiler có thể suy luận kiểu từ tham số:

```csharp
T Echo<T>(T value) => value;
var x = Echo(5);       // T = int
```

---

# 🌟 VII. TUPLES & ANONYMOUS TYPES
---

# PART A — ANONYMOUS TYPES

## 1. "Anonymous type là gì?"

**Note:** What are anonymous types?

**Trả lời:**
Anonymous type là **kiểu dữ liệu được compiler tạo tự động**, cho phép bạn tạo một object chứa một tập thuộc tính **mà không cần định nghĩa class**.

Anonymous type rất hữu ích khi:

* Dùng LINQ query
* Cần tạo object tạm thời
* Không muốn tạo class chỉ để chứa dữ liệu

Ví dụ:

```csharp
var person = new { Name = "Vox", Age = 21 };
```

Anonymous type luôn là **immutable** — giá trị của thuộc tính không thể thay đổi sau khi tạo.

---

## 2. "Cú pháp khởi tạo anonymous type"

**Note:** Declaring anonymous types

```csharp
var product = new
{
    Id = 1,
    Name = "Laptop",
    Price = 1800
};
```

Property name được compiler suy luận từ biểu thức:

```csharp
string name = "Vox";
var user = new { name };  // property "name"
```

---

## 3. "Anonymous types trong LINQ"

**Note:** Anonymous types in LINQ queries

Ví dụ dùng Select để trả về anonymous type:

```csharp
var results = from p in products
              select new
              {
                  p.Id,
                  p.Name,
                  Discounted = p.Price * 0.9
              };
```

---

## 4. "Anonymous types là reference type hay value type?"

**Note:** Are anonymous types reference types?

Anonymous types là **reference types**, và compiler tạo ra một class ẩn với:

* Auto-properties
* Immutable fields
* Value-based equality (so sánh theo thuộc tính)

---

## 5. "Equality của anonymous type"

**Note:** Anonymous type equality

Hai anonymous object bằng nhau khi:

* Chúng có **cùng cấu trúc thuộc tính**
* Và **giá trị các thuộc tính bằng nhau**

Ví dụ:

```csharp
var a = new { X = 1, Y = 2 };
var b = new { X = 1, Y = 2 };
Console.WriteLine(a.Equals(b)); // true
```

---

## 6. "Anonymous types và scope"

**Note:** Anonymous type scope limitations

Type của anonymous object chỉ tồn tại trong **phạm vi compile**. Nó không thể được dùng làm:

* Kiểu trả về public method
* Kiểu của field
* Kiểu generic argument trong API công khai

Sai:

```csharp
public new { Name = "A" } Create() => new { Name = "A" }; // ❌ không hợp lệ
```

Correct: sử dụng `object` hoặc `dynamic` nếu cần trả về kiểu không xác định.

---

# PART B — TUPLES (Bổ sung để hoàn chỉnh Section VI)

*Dù link Microsoft chỉ nói về anonymous types, nhưng mục của bạn yêu cầu "Tuples and Anonymous Types", nên phần Tuple được bổ sung đúng nội dung chuẩn .NET.*

---

## 7. "Tuple là gì?"

**Note:** What are tuples?

**Tuple** là cấu trúc dữ liệu nhẹ chứa nhiều giá trị.

Ví dụ:

```csharp
(string Name, int Age) person = ("Vox", 21);
Console.WriteLine(person.Name);
```

Tuple hỗ trợ:

* Truy cập bằng tên
* Truy cập bằng index (`person.Item1`)
* Deconstruction

---

## 8. "Tuple deconstruction"

**Note:** Deconstruction examples

```csharp
var (name, age) = ("Vox", 21);
Console.WriteLine(name);
```

Áp dụng với method:

```csharp
(string, int) GetInfo() => ("Vox", 21);
var (n, a) = GetInfo();
```

---

## 9. "Difference: Tuple vs Anonymous Type"

**Note:** Differences summary

| Feature               | Tuple                   | Anonymous Type |
| --------------------- | ----------------------- | -------------- |
| Mutable               | ✔ Có                    | ❌ Không        |
| Named fields          | ✔ Có                    | ✔ Có           |
| Value type / Ref type | Value type (ValueTuple) | Reference type |
| Deconstruction        | ✔ Hỗ trợ                | ✔ Hỗ trợ (ẩn)  |
| Dùng trong public API | ✔ Có thể                | ❌ Không        |

---

## 10. "Khi nào dùng tuple, khi nào dùng anonymous type?"

**Note:** Usage guidance

### Dùng **anonymous type** khi:

* Dùng trong LINQ
* Chỉ dùng nội bộ cục bộ
* Không cần return qua API

### Dùng **tuple** khi:

* Cần return nhiều giá trị từ method
* Cần truyền dữ liệu qua nhiều tầng
* Muốn mutable hoặc muốn deconstruction mạnh

---