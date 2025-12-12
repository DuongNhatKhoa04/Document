# 📘 C# PROGRAMMING CONCEPTS

**Version:** 1.0
**Updated:** 12/12/2025
**Author:** Vox

---

# I. COVARIANCE AND CONTRAVARIANCE

---

## 1. "Covariance và Contravariance là gì?"

Hai khái niệm này mô tả **khả năng chuyển đổi kiểu** trong hệ thống kế thừa khi sử dụng:

* Generic type parameters
* Delegates
* Interfaces

Chúng giúp bạn **sử dụng kiểu dẫn xuất (derived type)** ở nơi yêu cầu kiểu cơ sở (base type), hoặc ngược lại, mà vẫn đảm bảo an toàn kiểu.

### Tóm tắt nhanh

| Khái niệm                 | Cho phép gì?                               |
| ------------------------- | ------------------------------------------ |
| **Covariance (`out`)**    | Dùng *kiểu dẫn xuất* thay cho *kiểu cơ sở* |
| **Contravariance (`in`)** | Dùng *kiểu cơ sở* thay cho *kiểu dẫn xuất* |

Ví dụ:
Covariant → "đi xuống" (derived)
Contravariant → "đi lên" (base)

---

## 2. Covariance trong Generic Interfaces (từ khóa `out`)

Cho phép trả về kiểu dẫn xuất khi interface yêu cầu kiểu cơ sở.

Ví dụ:

```csharp
IEnumerable<object> objs = new List<string>(); // OK nhờ covariance
```

`string` kế thừa `object`, nên `IEnumerable<string>` được phép gán vào `IEnumerable<object>`.

### Khai báo interface covariant

```csharp
interface ICovariant<out T> { T GetItem(); }
```

---

## 3. Contravariance trong Generic Interfaces (từ khóa `in`)

Cho phép sử dụng kiểu cơ sở khi interface yêu cầu kiểu dẫn xuất.

Ví dụ:

```csharp
IComparer<string> cmp = new CustomObjectComparer(); // object comparer vẫn dùng cho string
```

### Khai báo interface contravariant

```csharp
interface IContravariant<in T> { void SetValue(T item); }
```

---

## 4. Covariance trong Delegates

Covariance cho phép delegate có **return type** là kiểu dẫn xuất.

Ví dụ:

```csharp
public class Animal {}
public class Dog : Animal {}

delegate Animal AnimalCreator();

Dog CreateDog() => new Dog();

AnimalCreator creator = CreateDog; // OK (Dog → Animal)
```

---

## 5. Contravariance trong Delegates

Contravariance cho phép delegate nhận **tham số** kiểu cơ sở thay vì kiểu dẫn xuất.

Ví dụ:

```csharp
delegate void Processor<in T>(T item);

void ProcessAnimal(Animal a) { }

Processor<Dog> p = ProcessAnimal; // OK (Animal ← Dog)
```

---

## 6. Generic Delegate Variance

Bạn có thể dùng `in` hoặc `out` trong generic delegate để mô tả hướng chuyển đổi.

Ví dụ:

```csharp
public delegate TOutput Converter<in TInput, out TOutput>(TInput input);
```

Điều này cho phép viết code linh hoạt và an toàn hơn.

---

## 7. Khi nào nên dùng covariance và contravariance?

### Dùng covariance khi:

* Chỉ **trả về** T (không nhận T làm input)
* Làm việc với collections chỉ đọc (`IEnumerable<T>`)

### Dùng contravariance khi:

* Chỉ **nhận vào** T (không trả về T)
* Làm việc với API xử lý input (comparers, processors…)

---

## 8. Ví dụ tổng hợp

```csharp
interface IProducer<out T>
{
    T Produce();
}

interface IConsumer<in T>
{
    void Consume(T item);
}

class Animal {}
class Dog : Animal {}
```

```csharp
IProducer<Animal> producer = new DogProducer(); // covariance
IConsumer<Dog> consumer = new AnimalConsumer(); // contravariance
```

---

## 9. Lưu ý quan trọng

* Chỉ áp dụng khi interface/delegate **được khai báo** với `in` hoặc `out`.
* Không áp dụng với **class generic** thông thường.
* Giúp code tổng quát (generic) linh hoạt mà vẫn **type-safe**.

---

# II. VARIANCE IN GENERIC INTERFACES

---

## 1. Interface hỗ trợ `in` và `out`

C# cho phép dùng variance trong **generic interfaces** thông qua từ khóa:

* `out` → covariance (chỉ xuất – return)
* `in` → contravariance (chỉ nhập – input)

Giúp interface linh hoạt khi dùng với hệ thống kế thừa.

---

## 2. Covariance (`out`) trong interface

Cho phép dùng kiểu **dẫn xuất** thay thế kiểu **cơ sở**.

Ví dụ:

```csharp
IEnumerable<object> objs = new List<string>(); // OK
```

Khai báo interface:

```csharp
public interface ICovariant<out T>
{
    T GetItem();
}
```

Chỉ cho phép **return T**, không được nhận T trong tham số.

---

## 3. Contravariance (`in`) trong interface

Cho phép dùng kiểu **cơ sở** thay thế kiểu **dẫn xuất**.

Ví dụ:

```csharp
IComparer<string> cmp = new ObjectComparer(); // OK vì string → object
```

Khai báo interface:

```csharp
public interface IContravariant<in T>
{
    void SetValue(T value);
}
```

Chỉ cho phép **input T**, không được return T.

---

## 4. Tóm tắt áp dụng

| Từ khóa | Nghĩa         | Áp dụng        |
| ------- | ------------- | -------------- |
| `out`   | Covariant     | Chỉ return T   |
| `in`    | Contravariant | Chỉ nhận vào T |

---

# III. VARIANCE IN DELEGATES

---

## 1. Delegate hỗ trợ variance là gì?

Delegates có thể:

* Covariant ở **kiểu trả về**
* Contravariant ở **tham số**

Điều này làm delegate linh hoạt hơn khi liên quan đến kế thừa.

---

## 2. Covariance trong return type

Cho phép method trả về **derived type** khi delegate yêu cầu **base type**.

Ví dụ:

```csharp
class Animal {}
class Dog : Animal {}

delegate Animal Creator();
Dog CreateDog() => new Dog();
Creator creator = CreateDog; // OK
```

---

## 3. Contravariance trong parameter type

Cho phép method nhận **base type** khi delegate yêu cầu **derived type**.

Ví dụ:

```csharp
class Animal {}
class Cat : Animal {}

delegate void Processor(Cat c);
void ProcessAnimal(Animal a) {}

Processor p = ProcessAnimal; // OK
```

---

## 4. Variance trong Generic Delegates

Bạn có thể chỉ định `in` hoặc `out` trong khai báo delegate:

```csharp
public delegate TResult Converter<in TInput, out TResult>(TInput input);
```

→ Input contravariant, output covariant.

---

## 5. Khi nào dùng variance trong delegates?

### Dùng covariance khi:

* Delegate **trả về** kiểu liên quan đến kế thừa.

### Dùng contravariance khi:

* Delegate **nhận vào** kiểu nằm trong hierarchy.

---

## 6. Ví dụ tổng hợp

```csharp
delegate Animal AnimalFactory();
delegate void AnimalHandler(Dog d);

AnimalFactory factory = () => new Dog(); // covariance
AnimalHandler handler = (Animal a) => {}; // contravariance
```

---

# IV. ITERATORS

Iterators cho phép bạn **duyệt qua các phần tử** trong collection mà không cần tạo cấu trúc trả về riêng như mảng hoặc danh sách.
Bạn chỉ cần dùng từ khóa **`yield`** để tạo iterator block.

---

## 1. "Iterator là gì?"

Iterator là **phương thức**, **toán tử get** hoặc **block** dùng `yield return` để trả về từng phần tử một của một tập hợp.

Iterator tự động:

* Tạo object thực thi `IEnumerator`
* Quản lý trạng thái lần lặp tiếp theo
* Tiết kiệm bộ nhớ (trả về từng phần tử khi cần)

---

## 2. "yield return" hoạt động như thế nào?

`yield return` tạm dừng phương thức, trả về một phần tử, và lưu trạng thái để tiếp tục lần gọi tiếp theo.

Ví dụ đơn giản:

```csharp
public static IEnumerable<int> GetNumbers()
{
    yield return 1;
    yield return 2;
    yield return 3;
}
```

Sử dụng:

```csharp
foreach (var n in GetNumbers())
    Console.WriteLine(n);
```

---

## 3. "yield break" dùng để làm gì?

Dùng để **kết thúc iterator sớm**.

```csharp
yield break;
```

---

## 4. Iterator với vòng lặp

Ví dụ lặp từ 0 đến 4:

```csharp
public static IEnumerable<int> Counter()
{
    for (int i = 0; i < 5; i++)
        yield return i;
}
```

---

## 5. Iterator trong property

Bạn có thể dùng iterator trong `get` accessor:

```csharp
public IEnumerable<int> Values
{
    get
    {
        yield return 10;
        yield return 20;
    }
}
```

---

## 6. Khi nào nên dùng iterator?

Dùng iterator khi:

* Dữ liệu **lớn** và không muốn tạo danh sách mới
* Dữ liệu được **tạo theo yêu cầu** (lazy evaluation)
* Tạo **pipeline xử lý dữ liệu tuần tự**

Không dùng iterator khi:

* Cần random-access (indexing)
* Dữ liệu cần cache lại hoàn toàn

---

## 7. Iterator và IEnumerable / IEnumerator

Iterator block tự động tạo class giống như:

* Triển khai `IEnumerable`
* Trả về enumerator triển khai `IEnumerator`

Bạn **không phải viết tay** state machine.

---

## 8. Ví dụ iterator phức tạp hơn

```csharp
public static IEnumerable<int> FilterEven(IEnumerable<int> numbers)
{
    foreach (var n in numbers)
        if (n % 2 == 0)
            yield return n;
}
```

---

## 9. Iterator cho cây (tree traversal)

Iterator rất hữu ích cho cấu trúc đệ quy:

```csharp
public IEnumerable<Node> Traverse(Node node)
{
    yield return node;
    foreach (var child in node.Children)
        foreach (var c in Traverse(child))
            yield return c;
}
```

---

## 10. Tóm tắt nhanh

| Tính năng        | Ý nghĩa                                   |
| ---------------- | ----------------------------------------- |
| `yield return`   | Trả về từng phần tử và lưu lại trạng thái |
| `yield break`    | Kết thúc iterator                         |
| Hỗ trợ `foreach` | Tự động tạo IEnumerator                   |
| Lazy evaluation  | Chỉ tạo giá trị khi cần                   |

---
