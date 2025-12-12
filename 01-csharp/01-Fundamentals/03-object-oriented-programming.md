# 📘 C# OBJECT-ORIENTED PROGRAMMING (OOP)

**Version:** 1.0
**Updated:** 12/12/2025
**Author:** Vox

---

- [📘 C# OBJECT-ORIENTED PROGRAMMING (OOP)](#-c-object-oriented-programming-oop)
- [I. CLASSES, STRUCTS, AND RECORDS](#i-classes-structs-and-records)
  - [1. "Object-Oriented Programming trong C# là gì?"](#1-object-oriented-programming-trong-c-là-gì)
  - [2. "Class là gì?"](#2-class-là-gì)
    - [Ví dụ class đơn giản:](#ví-dụ-class-đơn-giản)
    - [Đặc điểm của class:](#đặc-điểm-của-class)
  - [3. "Struct là gì?"](#3-struct-là-gì)
    - [Ví dụ struct:](#ví-dụ-struct)
    - [Đặc điểm của struct:](#đặc-điểm-của-struct)
  - [4. "Record là gì?"](#4-record-là-gì)
    - [Ví dụ record:](#ví-dụ-record)
    - [Đặc điểm:](#đặc-điểm)
  - [5. "Khi nào dùng class, struct, record?"](#5-khi-nào-dùng-class-struct-record)
    - [Khi nào dùng **class**:](#khi-nào-dùng-class)
    - [Khi nào dùng **struct**:](#khi-nào-dùng-struct)
    - [Khi nào dùng **record**:](#khi-nào-dùng-record)
- [II. OBJECTS — CREATE INSTANCES OF TYPES](#ii-objects--create-instances-of-types)
  - [1. "Object trong C# là gì?"](#1-object-trong-c-là-gì)
  - [2. "Tạo object trong C# như thế nào?"](#2-tạo-object-trong-c-như-thế-nào)
    - [Cách 1 — Dùng `new` với kiểu mặc định:](#cách-1--dùng-new-với-kiểu-mặc-định)
    - [Cách 2 — Khởi tạo bằng constructor:](#cách-2--khởi-tạo-bằng-constructor)
    - [Cách 3 — Object initializer:](#cách-3--object-initializer)
  - [3. "Object có thể chứa những gì?"](#3-object-có-thể-chứa-những-gì)
  - [4. "Object initializer hoạt động thế nào?"](#4-object-initializer-hoạt-động-thế-nào)
  - [5. "Anonymous objects là gì?"](#5-anonymous-objects-là-gì)
  - [6. "Record khi tạo object có gì đặc biệt?"](#6-record-khi-tạo-object-có-gì-đặc-biệt)
  - [7. "Struct khi tạo object có gì đặc biệt?"](#7-struct-khi-tạo-object-có-gì-đặc-biệt)
  - [8. "Reference types khi tạo object có gì đặc biệt?"](#8-reference-types-khi-tạo-object-có-gì-đặc-biệt)
  - [9. "Object lifetime — vòng đời object trong C# được quản lý thế nào?"](#9-object-lifetime--vòng-đời-object-trong-c-được-quản-lý-thế-nào)
  - [10. "Tóm tắt — nên dùng loại object nào?"](#10-tóm-tắt--nên-dùng-loại-object-nào)
- [III. INHERITANCE — DERIVE TYPES TO CREATE MORE SPECIALIZED BEHAVIOR](#iii-inheritance--derive-types-to-create-more-specialized-behavior)
  - [1. "Inheritance trong C# là gì?"](#1-inheritance-trong-c-là-gì)
  - [2. "Base class và derived class là gì?"](#2-base-class-và-derived-class-là-gì)
  - [3. "Override và virtual là gì?"](#3-override-và-virtual-là-gì)
  - [4. "sealed là gì?"](#4-sealed-là-gì)
  - [5. "base keyword dùng để làm gì?"](#5-base-keyword-dùng-để-làm-gì)
  - [6. "Constructor của base class gọi như thế nào?"](#6-constructor-của-base-class-gọi-như-thế-nào)
  - [7. "Inherited members — Derived class kế thừa những gì?"](#7-inherited-members--derived-class-kế-thừa-những-gì)
  - [8. "Hiding vs overriding — sự khác nhau?"](#8-hiding-vs-overriding--sự-khác-nhau)
    - [**override**](#override)
    - [**new (method hiding)**](#new-method-hiding)
  - [9. "Inheritance chỉ áp dụng cho class?"](#9-inheritance-chỉ-áp-dụng-cho-class)
  - [10. "Polymorphism liên quan gì đến inheritance?"](#10-polymorphism-liên-quan-gì-đến-inheritance)
  - [11. Tóm tắt nhanh](#11-tóm-tắt-nhanh)
- [IV. POLYMORPHISM — DYNAMIC BEHAVIOR THROUGH INHERITANCE](#iv-polymorphism--dynamic-behavior-through-inheritance)
  - [1. "Polymorphism trong C# là gì?"](#1-polymorphism-trong-c-là-gì)
  - [2. "Polymorphism hoạt động dựa trên cơ chế nào?"](#2-polymorphism-hoạt-động-dựa-trên-cơ-chế-nào)
  - [3. "Ví dụ cơ bản về polymorphism"](#3-ví-dụ-cơ-bản-về-polymorphism)
  - [4. "Polymorphism giúp ích gì trong thực tế?"](#4-polymorphism-giúp-ích-gì-trong-thực-tế)
  - [5. "new vs override — khác nhau thế nào?"](#5-new-vs-override--khác-nhau-thế-nào)
    - [✔ override](#-override)
    - [✔ new (method hiding)](#-new-method-hiding)
  - [6. "Polymorphism hoạt động cho record không?"](#6-polymorphism-hoạt-động-cho-record-không)
  - [7. "Abstract methods và polymorphism"](#7-abstract-methods-và-polymorphism)
  - [8. "Interface có hỗ trợ polymorphism không?"](#8-interface-có-hỗ-trợ-polymorphism-không)
  - [9. "Overriding ToString, Equals, GetHashCode" — có phải polymorphism không?](#9-overriding-tostring-equals-gethashcode--có-phải-polymorphism-không)
  - [10. Polymorphism \& run-time type resolution](#10-polymorphism--run-time-type-resolution)
  - [11. Tóm tắt nhanh](#11-tóm-tắt-nhanh-1)


---

# I. CLASSES, STRUCTS, AND RECORDS

## 1. "Object-Oriented Programming trong C# là gì?"

Lập trình hướng đối tượng (OOP) trong C# là mô hình dựa trên việc xây dựng **object** – những thực thể kết hợp **dữ liệu** và **hành vi** liên quan.

C# hỗ trợ đầy đủ các nguyên lý OOP:

* **Encapsulation** (bao đóng)
* **Inheritance** (kế thừa)
* **Polymorphism** (đa hình)

C# cung cấp ba loại cấu trúc chính dùng để tạo kiểu tùy chỉnh:

* **class** → tham chiếu (reference type)
* **struct** → giá trị (value type)
* **record** → kiểu dữ liệu ưu tiên so sánh theo giá trị

---

## 2. "Class là gì?"

**Class** là blueprint để tạo ra object. Là *reference type*, lưu trên heap.

### Ví dụ class đơn giản:

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public void SayHello()
    {
        Console.WriteLine($"Hello, I'm {Name}");
    }
}
```

### Đặc điểm của class:

* Cho phép kế thừa từ class khác.
* Hỗ trợ polymorphism qua virtual, override, interface.
* Object được tạo bằng `new` và biến lưu **tham chiếu**.

---

## 3. "Struct là gì?"

**Struct** là value type, dùng cho dữ liệu nhỏ và bất biến.

### Ví dụ struct:

```csharp
public struct Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }
}
```

### Đặc điểm của struct:

* Lưu trực tiếp dữ liệu, **copy** khi gán sang biến khác.
* Không hỗ trợ kế thừa (chỉ implement interface).
* Thích hợp cho dữ liệu nhỏ, immutable.
* Không cần `new` để khởi tạo (nhưng khuyến khích dùng).

---

## 4. "Record là gì?"

**Record** là cú pháp đặc biệt hỗ trợ so sánh theo giá trị, phù hợp cho mô hình dữ liệu.

Records có hai dạng:

* **record class** → reference type
* **record struct** → value type

### Ví dụ record:

```csharp
public record Person(string Name, int Age);
```

### Đặc điểm:

* Tự động sinh `Equals`, `GetHashCode`, `ToString`.
* Hỗ trợ **non-destructive mutation** qua `with` expression:

```csharp
var p1 = new Person("Alice", 20);
var p2 = p1 with { Age = 21 };
```

---

## 5. "Khi nào dùng class, struct, record?"

### Khi nào dùng **class**:

* Object có vòng đời phức tạp.
* Cần kế thừa.
* Dữ liệu lớn hoặc thay đổi thường xuyên.

### Khi nào dùng **struct**:

* < 64 bytes.
* Dữ liệu bất biến.
* Có semantics của giá trị.

### Khi nào dùng **record**:

* Chủ yếu dùng để lưu dữ liệu.
* Cần equality theo value.
* Cần khả năng clone chỉnh sửa (`with`).

---

# II. OBJECTS — CREATE INSTANCES OF TYPES

---

## 1. "Object trong C# là gì?"

Object là **instance (thể hiện)** của một class, struct, hoặc record. Khi bạn tạo object, bạn đang tạo một thực thể thật sự chứa:

* **Dữ liệu** → fields, properties
* **Hành vi** → methods

Object là trọng tâm của lập trình hướng đối tượng trong C#.

---

## 2. "Tạo object trong C# như thế nào?"

### Cách 1 — Dùng `new` với kiểu mặc định:

```csharp
var person = new Person();
person.Name = "Bob";
person.Age = 30;
```

### Cách 2 — Khởi tạo bằng constructor:

```csharp
var person = new Person("Alice", 25);
```

### Cách 3 — Object initializer:

```csharp
var p = new Person
{
    Name = "Chris",
    Age = 20
};
```

---

## 3. "Object có thể chứa những gì?"

Object được tạo từ class/struct/record và có thể chứa:

* **Fields** – dữ liệu thô
* **Properties** – dữ liệu có getter/setter
* **Methods** – hành vi
* **Events** – mô hình pub/sub
* **Indexers** – cho phép object hoạt động như mảng

Ví dụ:

```csharp
public class BankAccount
{
    public string Owner { get; set; }
    private decimal balance;

    public void Deposit(decimal amount) => balance += amount;
    public decimal GetBalance() => balance;
}
```

---

## 4. "Object initializer hoạt động thế nào?"

Dùng `{}` để gán giá trị cho property trong lúc khởi tạo:

```csharp
var account = new BankAccount
{
    Owner = "Vox"
};
```

Kết hợp với constructor:

```csharp
var account = new BankAccount("Vox")
{
    Balance = 1000
};
```

---

## 5. "Anonymous objects là gì?"

Anonymous objects là object **không có kiểu đặt tên**.

Ví dụ:

```csharp
var product = new { Name = "Laptop", Price = 1200 };
```

Đặc điểm:

* Compiler tự sinh kiểu
* Thuộc tính **immutable**
* Dùng nhiều trong LINQ

Ví dụ LINQ:

```csharp
var result = from p in products
             select new { p.Name, p.Price };
```

---

## 6. "Record khi tạo object có gì đặc biệt?"

Record hỗ trợ **value equality** và cung cấp cú pháp constructor rút gọn:

```csharp
var person = new Person("Alice", 30);
```

Clone object bằng `with`:

```csharp
var p2 = person with { Age = 31 };
```

---

## 7. "Struct khi tạo object có gì đặc biệt?"

Struct là **value type** → copy khi gán:

```csharp
Point p1 = new Point(1, 2);
Point p2 = p1;  // copy dữ liệu
```

Thay đổi `p2` **không ảnh hưởng** `p1`.

---

## 8. "Reference types khi tạo object có gì đặc biệt?"

Class, record class, array, delegate, interface → đều là reference types.

```csharp
var a = new Person("Tom", 20);
var b = a; // cùng tham chiếu
b.Name = "Jerry";
```

→ `a.Name` cũng thay đổi.

---

## 9. "Object lifetime — vòng đời object trong C# được quản lý thế nào?"

CLR cấp phát object trên heap. **Garbage Collector** tự giải phóng khi object không còn được tham chiếu.

Dọn dẹp tài nguyên bằng `IDisposable`:

```csharp
using var conn = new SqlConnection(...);
```

`using` đảm bảo giải phóng tài nguyên dù có lỗi xảy ra.

---

## 10. "Tóm tắt — nên dùng loại object nào?"

| Loại               | Đặc điểm                   | Khi nên dùng                |
| ------------------ | -------------------------- | --------------------------- |
| **Class**          | reference type             | entity phức tạp, có hành vi |
| **Struct**         | value type                 | dữ liệu nhỏ, immutable      |
| **Record class**   | reference + value equality | data models                 |
| **Record struct**  | value type + equality      | immutable data              |
| **Anonymous type** | không đặt tên              | LINQ, data tạm thời         |

---

# III. INHERITANCE — DERIVE TYPES TO CREATE MORE SPECIALIZED BEHAVIOR

---

## 1. "Inheritance trong C# là gì?"

**Inheritance (kế thừa)** là cơ chế cho phép bạn tạo một kiểu mới (**derived class**) mở rộng hoặc chuyên biệt hóa hành vi của một kiểu khác (**base class**).

Kế thừa giúp:

* Tái sử dụng code
* Tạo cấu trúc phân cấp (hierarchy)
* Cho phép polymorphism

Ví dụ thực tế: *Car* kế thừa từ *Vehicle*.

---

## 2. "Base class và derived class là gì?"

* **Base class**: lớp cha chứa logic chung.
* **Derived class**: lớp con mở rộng hoặc thay đổi hành vi.

Ví dụ:

```csharp
public class Animal
{
    public void Eat() => Console.WriteLine("Eating...");
}

public class Dog : Animal
{
    public void Bark() => Console.WriteLine("Barking...");
}
```

Dùng:

```csharp
var dog = new Dog();
dog.Eat();   // từ Animal
dog.Bark();  // của Dog
```

---

## 3. "Override và virtual là gì?"

Base class có thể khai báo phương thức là **virtual** → Derived class có thể **override**.

Ví dụ:

```csharp
public class Shape
{
    public virtual double Area() => 0;
}

public class Circle : Shape
{
    public double Radius { get; }
    public Circle(double r) => Radius = r;

    public override double Area() => Math.PI * Radius * Radius;
}
```

Tính đa hình:

```csharp
Shape s = new Circle(5);
Console.WriteLine(s.Area());
```

---

## 4. "sealed là gì?"

Dùng `sealed` để **ngăn không cho kế thừa tiếp**.

```csharp
public sealed class PremiumAccount : BankAccount
{
}
```

---

## 5. "base keyword dùng để làm gì?"

Dùng `base` để:

* Gọi constructor của lớp cha
* Gọi phương thức hoặc property bị override

Ví dụ:

```csharp
public class Person
{
    public string Name { get; }
    public Person(string name) => Name = name;
}

public class Student : Person
{
    public int Grade { get; }

    public Student(string name, int grade)
        : base(name) // gọi Person(name)
    {
        Grade = grade;
    }
}
```

---

## 6. "Constructor của base class gọi như thế nào?"

Derived class **bắt buộc** phải gọi một constructor của base class.
Nếu base class không có constructor mặc định, bạn phải chỉ rõ:

```csharp
public class Employee : Person
{
    public Employee(string name) : base(name) {}
}
```

---

## 7. "Inherited members — Derived class kế thừa những gì?"

Derived class kế thừa:

* Fields
* Properties
* Methods
* Events

Ngoại trừ:

* Constructor **không được kế thừa**
* Private members vẫn tồn tại nhưng **không truy cập trực tiếp**

---

## 8. "Hiding vs overriding — sự khác nhau?"

### **override**

* Thay đổi hành vi của phương thức virtual trong base class

### **new (method hiding)**

* Tạo phương thức mới có cùng tên → không liên quan đến base method

Ví dụ:

```csharp
public class Base
{
    public void Show() => Console.WriteLine("Base.Show");
}

public class Derived : Base
{
    public new void Show() => Console.WriteLine("Derived.Show");
}
```

---

## 9. "Inheritance chỉ áp dụng cho class?"

Đúng. Struct **không hỗ trợ kế thừa** từ struct khác.
Tuy nhiên:

* Class và struct **đều** có thể implement interface.

---

## 10. "Polymorphism liên quan gì đến inheritance?"

Polymorphism cho phép dùng **kiểu base** để tham chiếu object của **kiểu derived**.

Ví dụ:

```csharp
List<Shape> shapes = [
    new Circle(5),
    new Rectangle(3, 4)
];

foreach (var s in shapes)
    Console.WriteLine(s.Area());
```

Kết quả gọi đúng method override ở class con.

---

## 11. Tóm tắt nhanh

| Khái niệm         | Ý nghĩa                                 |
| ----------------- | --------------------------------------- |
| **Base class**    | Lớp cha chứa hành vi chung              |
| **Derived class** | Lớp con mở rộng hoặc thay đổi hành vi   |
| **virtual**       | Cho phép override                       |
| **override**      | Thay đổi hành vi từ base                |
| **sealed**        | Ngăn kế thừa tiếp                       |
| **base keyword**  | Gọi constructor hoặc method của lớp cha |
| **Polymorphism**  | Hành vi động trên base reference        |

---

# IV. POLYMORPHISM — DYNAMIC BEHAVIOR THROUGH INHERITANCE

---

## 1. "Polymorphism trong C# là gì?"

**Polymorphism** (đa hình) cho phép bạn:

* Gọi phương thức của object **thông qua kiểu tham chiếu của base class**, nhưng
* Hành vi thực thi thuộc về **kiểu thực tế (run-time type)** của object đó.

Nói ngắn gọn: *một interface chung – nhiều hành vi khác nhau*.

Ví dụ quen thuộc:

* `Shape` có `Draw()`
* `Circle`, `Rectangle` override `Draw()` theo cách riêng

---

## 2. "Polymorphism hoạt động dựa trên cơ chế nào?"

Trong C#, polymorphism dựa trên hai từ khóa:

* **virtual** — cho phép override phương thức trong class con
* **override** — thay đổi hành vi của base method

---

## 3. "Ví dụ cơ bản về polymorphism"

```csharp
public class Shape
{
    public virtual void Draw() => Console.WriteLine("Drawing a shape");
}

public class Circle : Shape
{
    public override void Draw() => Console.WriteLine("Drawing a circle");
}

public class Rectangle : Shape
{
    public override void Draw() => Console.WriteLine("Drawing a rectangle");
}
```

Sử dụng:

```csharp
List<Shape> shapes = [ new Circle(), new Rectangle(), new Shape() ];

foreach (var s in shapes)
    s.Draw();
```

Output:

```
Drawing a circle
Drawing a rectangle
Drawing a shape
```

→ Dù biến có kiểu **Shape**, C# vẫn gọi đúng method của **kiểu thật**.

---

## 4. "Polymorphism giúp ích gì trong thực tế?"

* Tạo code linh hoạt và dễ mở rộng (open/closed principle)
* Dễ dàng thay đổi hành vi runtime
* Cho phép xử lý nhiều loại đối tượng qua cùng 1 API

Ví dụ kinh điển: `Stream` trong .NET

```csharp
Stream stream = File.OpenRead("data.bin");
```

`stream.Read()` hoạt động khác tùy loại stream.

---

## 5. "new vs override — khác nhau thế nào?"

### ✔ override

* Thay thế hành vi của base
* Yêu cầu base method phải `virtual`, `abstract`, hoặc `override`

### ✔ new (method hiding)

* Che giấu (hide) method, không liên quan override

Ví dụ:

```csharp
public class Base
{
    public virtual void Show() => Console.WriteLine("Base.Show");
}

public class Derived : Base
{
    public new void Show() => Console.WriteLine("Derived.Show");
}
```

Trong trường hợp này:

```csharp
Base b = new Derived();
b.Show(); // Base.Show
```

→ vì nó KHÔNG phải override.

---

## 6. "Polymorphism hoạt động cho record không?"

Có. **Record class** hoạt động như class bình thường, hỗ trợ override.

**Record struct** là value-type nhưng cũng hỗ trợ override `virtual` members của base class (nếu có).

---

## 7. "Abstract methods và polymorphism"

Abstract method **bắt buộc** phải override trong derived class → đảm bảo polymorphism.

Ví dụ:

```csharp
public abstract class Animal
{
    public abstract void Speak();
}

public class Dog : Animal
{
    public override void Speak() => Console.WriteLine("Woof!");
}
```

Bạn không thể tạo instance của abstract class:

```csharp
Animal animal = new Dog();
animal.Speak();
```

---

## 8. "Interface có hỗ trợ polymorphism không?"

Có. Interface là một dạng polymorphism đặc biệt dựa trên **contract**, không dựa trên kế thừa class.

Ví dụ:

```csharp
public interface ILogger
{
    void Log(string message);
}

public class ConsoleLogger : ILogger
{
    public void Log(string message) => Console.WriteLine(message);
}
```

Dùng:

```csharp
ILogger logger = new ConsoleLogger();
logger.Log("Hello");
```

---

## 9. "Overriding ToString, Equals, GetHashCode" — có phải polymorphism không?

Đúng. Đây là ví dụ điển hình của polymorphism trong .NET.

Mọi class đều kế thừa `object`, nên bạn có thể override:

* `ToString()` → biểu diễn chuỗi
* `Equals()` → so sánh
* `GetHashCode()` → dùng cho từ điển/hashing

```csharp
public override string ToString() => $"Person: {Name}";
```

---

## 10. Polymorphism & run-time type resolution

Khi gọi method, C# quyết định như sau:

| Loại                    | Quyết định khi nào? |
| ----------------------- | ------------------- |
| **Overload resolution** | Compile-time        |
| **Override resolution** | Run-time            |

Polymorphism dùng **run-time type** để xác định hành vi.

---

## 11. Tóm tắt nhanh

| Khái niệm             | Ý nghĩa                                   |
| --------------------- | ----------------------------------------- |
| **virtual**           | Cho phép override                         |
| **override**          | Thay đổi hành vi base method              |
| **new**               | Che giấu method, KHÔNG override           |
| **abstract method**   | Bắt buộc override                         |
| **interface**         | Polymorphism dựa trên contract            |
| **run-time dispatch** | Gọi đúng method theo kiểu thật của object |

---
