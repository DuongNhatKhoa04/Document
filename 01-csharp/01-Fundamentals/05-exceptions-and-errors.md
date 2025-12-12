# 📘 C# EXCEPTIONS AND ERRORS — EXCEPTIONS & EXCEPTION HANDLING

**Version:** 1.0
**Updated:** 12/12/2025
**Author:** Vox

---

- [📘 C# EXCEPTIONS AND ERRORS — EXCEPTIONS \& EXCEPTION HANDLING](#-c-exceptions-and-errors--exceptions--exception-handling)
- [I. EXCEPTIONS AND EXCEPTION HANDLING](#i-exceptions-and-exception-handling)
  - [1. "Exception trong C# là gì?"](#1-exception-trong-c-là-gì)
  - [2. "Tại sao cần exception handling?"](#2-tại-sao-cần-exception-handling)
  - [3. "Cấu trúc try-catch cơ bản"](#3-cấu-trúc-try-catch-cơ-bản)
    - [Giải thích:](#giải-thích)
  - [4. "Bắt nhiều loại exception"](#4-bắt-nhiều-loại-exception)
  - [5. "finally dùng để làm gì?"](#5-finally-dùng-để-làm-gì)
  - [6. "throw exception — khi nào nên tự ném lỗi?"](#6-throw-exception--khi-nào-nên-tự-ném-lỗi)
  - [7. "Exception filtering — catch when"](#7-exception-filtering--catch-when)
  - [8. "Các exception phổ biến trong .NET"](#8-các-exception-phổ-biến-trong-net)
  - [9. "try-catch có làm chậm chương trình không?"](#9-try-catch-có-làm-chậm-chương-trình-không)
  - [10. "Best practices khi xử lý exception"](#10-best-practices-khi-xử-lý-exception)
  - [11. Tóm tắt nhanh](#11-tóm-tắt-nhanh)
- [II. USE EXCEPTIONS](#ii-use-exceptions)
  - [1. "Khi nào nên dùng exception?"](#1-khi-nào-nên-dùng-exception)
  - [2. "Thay thế exception bằng kiểm tra điều kiện"](#2-thay-thế-exception-bằng-kiểm-tra-điều-kiện)
  - [3. "Khi nào nên bắt (catch) exception?"](#3-khi-nào-nên-bắt-catch-exception)
  - [4. "Throw vs throw; — sự khác nhau?"](#4-throw-vs-throw--sự-khác-nhau)
    - [✔ `throw;`](#-throw)
    - [❌ `throw ex;`](#-throw-ex)
  - [5. "Trong .NET có guideline đặt tên exception không?"](#5-trong-net-có-guideline-đặt-tên-exception-không)
  - [6. "Các loại lỗi nên dùng exception nào?"](#6-các-loại-lỗi-nên-dùng-exception-nào)
  - [7. "Avoid using exceptions for flow control" — Vì sao?](#7-avoid-using-exceptions-for-flow-control--vì-sao)
  - [8. "Use exceptions for exceptional situations" — Best practices](#8-use-exceptions-for-exceptional-situations--best-practices)
  - [9. "Don't overuse custom exceptions"](#9-dont-overuse-custom-exceptions)
  - [10. Tóm tắt nhanh](#10-tóm-tắt-nhanh)
- [III. EXCEPTION HANDLING](#iii-exception-handling)
  - [1. "Exception handling là gì?"](#1-exception-handling-là-gì)
  - [2. "Cấu trúc try-catch cơ bản"](#2-cấu-trúc-try-catch-cơ-bản)
    - [Ý nghĩa:](#ý-nghĩa)
  - [3. "Bắt nhiều loại exception"](#3-bắt-nhiều-loại-exception)
  - [4. "Catch-all handler — nên hay không?"](#4-catch-all-handler--nên-hay-không)
  - [5. "Sử dụng finally"](#5-sử-dụng-finally)
  - [6. "Combining try-catch-finally"](#6-combining-try-catch-finally)
  - [7. "Exception filters — catch when"](#7-exception-filters--catch-when)
  - [8. "Throw exception từ catch block"](#8-throw-exception-từ-catch-block)
    - [Ném lại exception cũ:](#ném-lại-exception-cũ)
    - [Ném exception mới:](#ném-exception-mới)
  - [9. "Exception propagation — lan truyền exception"](#9-exception-propagation--lan-truyền-exception)
  - [10. "Exception handling trong async/await"](#10-exception-handling-trong-asyncawait)
    - [Bắt lỗi trong async:](#bắt-lỗi-trong-async)
    - [Task lưu exception trong Task.Exception:](#task-lưu-exception-trong-taskexception)
  - [11. "Exception handling trong iterator (yield)"](#11-exception-handling-trong-iterator-yield)
  - [12. "Các trường hợp đặc biệt cần handler riêng"](#12-các-trường-hợp-đặc-biệt-cần-handler-riêng)
    - [Null values:](#null-values)
    - [Task cancellation:](#task-cancellation)
    - [Overflow:](#overflow)
  - [13. Best practices](#13-best-practices)
  - [14. Tóm tắt nhanh](#14-tóm-tắt-nhanh)
- [IV. CREATE AND THROW EXCEPTIONS](#iv-create-and-throw-exceptions)
  - [1. "Khi nào cần tạo exception mới?"](#1-khi-nào-cần-tạo-exception-mới)
  - [2. "Quy tắc đặt tên exception"](#2-quy-tắc-đặt-tên-exception)
  - [3. "Cách ném exception bằng throw"](#3-cách-ném-exception-bằng-throw)
    - [Ném exception mới:](#ném-exception-mới-1)
    - [Ném exception với inner exception:](#ném-exception-với-inner-exception)
  - [4. "throw; vs throw ex; — khác nhau như thế nào?"](#4-throw-vs-throw-ex--khác-nhau-như-thế-nào)
    - [✔ `throw;`](#-throw-1)
    - [❌ `throw ex;`](#-throw-ex-1)
  - [5. "Argument validation — kiểm tra tham số và ném lỗi"](#5-argument-validation--kiểm-tra-tham-số-và-ném-lỗi)
  - [6. "Tạo custom exception đầy đủ — best practices"](#6-tạo-custom-exception-đầy-đủ--best-practices)
  - [7. "Tạo exception dùng when để lọc lỗi"](#7-tạo-exception-dùng-when-để-lọc-lỗi)
  - [8. "Ví dụ đầy đủ — tạo và ném exception tùy chỉnh"](#8-ví-dụ-đầy-đủ--tạo-và-ném-exception-tùy-chỉnh)
  - [9. "Exception trong constructor"](#9-exception-trong-constructor)
  - [10. Tóm tắt nhanh](#10-tóm-tắt-nhanh-1)

---

# I. EXCEPTIONS AND EXCEPTION HANDLING

---

## 1. "Exception trong C# là gì?"

**Exception** là lỗi phát sinh trong lúc chương trình đang chạy (*run-time error*).
Khi xảy ra exception, .NET sẽ:

* Ngừng thực thi bình thường
* Tìm một "exception handler" phù hợp
* Nếu không tìm thấy → chương trình **bị crash**

Exception là cơ chế mạnh mẽ giúp bạn xử lý lỗi đúng cách thay vì để chương trình dừng đột ngột.

---

## 2. "Tại sao cần exception handling?"

Exception handling giúp bạn:

* Giữ chương trình **ổn định**, không bị crash
* Phân tách logic xử lý lỗi ra khỏi logic chính
* Xử lý lỗi ở nơi phù hợp nhất trong luồng thực thi

Ví dụ thực tế:

* Mở file không tồn tại
* Mất kết nối mạng
* Null reference

---

## 3. "Cấu trúc try-catch cơ bản"

```csharp
try
{
    int x = int.Parse("abc");
}
catch (FormatException ex)
{
    Console.WriteLine("Sai định dạng!");
}
```

### Giải thích:

* **try**: chứa code có thể gây lỗi
* **catch**: xử lý lỗi tương ứng

---

## 4. "Bắt nhiều loại exception"

```csharp
try
{
    DoWork();
}
catch (IOException)
{
    Console.WriteLine("Lỗi IO");
}
catch (UnauthorizedAccessException)
{
    Console.WriteLine("Không đủ quyền");
}
catch (Exception ex)
{
    Console.WriteLine($"Lỗi khác: {ex.Message}");
}
```

⚠ **Thứ tự quan trọng**: bắt từ exception cụ thể → đến exception chung.

---

## 5. "finally dùng để làm gì?"

`finally` luôn chạy dù có xảy ra exception hay không.

Thường dùng để giải phóng tài nguyên:

```csharp
FileStream fs = null;
try
{
    fs = File.OpenRead("data.txt");
}
finally
{
    fs?.Dispose();
}
```

---

## 6. "throw exception — khi nào nên tự ném lỗi?"

Bạn tự ném exception khi chương trình rơi vào trạng thái không hợp lệ.

```csharp
if (age < 0)
    throw new ArgumentOutOfRangeException(nameof(age));
```

Ném lại exception đang bắt:

```csharp
catch (Exception)
{
    throw;
}
```

(Khác với `throw ex`, vì `throw;` giữ nguyên stack trace.)

---

## 7. "Exception filtering — catch when"

Bạn có thể thêm điều kiện khi bắt exception:

```csharp
try
{
    Process(order);
}
catch (OrderException ex) when (ex.Severity == "Low")
{
    Console.WriteLine("Lỗi nhẹ, tiếp tục chạy.");
}
```

Điều kiện sai → catch **không xử lý** exception đó.

---

## 8. "Các exception phổ biến trong .NET"

| Exception                   | Ý nghĩa                                     |
| --------------------------- | ------------------------------------------- |
| `NullReferenceException`    | Truy cập object null                        |
| `ArgumentException`         | Tham số không hợp lệ                        |
| `InvalidOperationException` | Thao tác không hợp lệ ở trạng thái hiện tại |
| `FormatException`           | Sai định dạng dữ liệu                       |
| `IOException`               | Lỗi truy cập I/O                            |
| `IndexOutOfRangeException`  | Truy cập mảng vượt chỉ số                   |

---

## 9. "try-catch có làm chậm chương trình không?"

Có — nhưng chỉ khi **exception thật sự xảy ra**.
Việc đặt nhiều try-catch **không gây overhead đáng kể**.

Vì vậy, dùng exception cho lỗi bất ngờ (exceptional cases), không dùng cho luồng logic bình thường.

---

## 10. "Best practices khi xử lý exception"

✔ Bắt exception **cụ thể**, tránh bắt chung `Exception` trừ khi thực sự cần thiết
✔ Không dùng exception cho flow control
✔ Luôn dọn tài nguyên qua `finally` hoặc `using`
✔ Ghi log đầy đủ khi có lỗi bất ngờ
✔ Throw exception mới khi cần nhưng giữ nguyên stack trace

---

## 11. Tóm tắt nhanh

* Exception là lỗi runtime
* try-catch dùng để xử lý và ngăn crash
* finally luôn chạy
* throw dùng để ném lỗi thủ công
* Lọc exception với when
* Không lạm dụng exception

---

# II. USE EXCEPTIONS

---

## 1. "Khi nào nên dùng exception?"

Exceptions chỉ nên được sử dụng cho **tình huống bất thường** (exceptional cases), không phải cho luồng logic bình thường.

✔ Dùng exception khi:

* Lỗi không thể tiếp tục thực thi
* Dữ liệu đầu vào không hợp lệ
* Hệ thống bên ngoài (file, network, DB) gặp sự cố

❌ Không dùng exception khi:

* Chỉ để kiểm tra điều kiện logic
* Điều kiện có thể dự đoán và kiểm tra trước

Ví dụ không nên dùng:

```csharp
try
{
    if (list.Count == 0) throw new Exception();
}
catch
{
    // tránh cách viết này!
}
```

---

## 2. "Thay thế exception bằng kiểm tra điều kiện"

Ví dụ tốt:

```csharp
if (age < 0)
    throw new ArgumentOutOfRangeException(nameof(age));
```

Ví dụ tốt hơn nếu không cần exception:

```csharp
if (list.Count == 0)
    return; // tránh dùng exception để xử lý logic bình thường
```

---

## 3. "Khi nào nên bắt (catch) exception?"

Chỉ catch exception khi:

* Bạn có thể xử lý lỗi và cho chương trình tiếp tục
* Bạn có hành động hợp lý để xử lý lỗi (ghi log, retry…)

Không catch nếu:

* Bạn không thể xử lý
* Bạn chỉ catch để che giấu lỗi

Ví dụ **không nên làm**:

```csharp
catch (Exception)
{
    // Nuốt exception → rất nguy hiểm
}
```

---

## 4. "Throw vs throw; — sự khác nhau?"

Trong catch, nếu bạn cần ném lại exception:

### ✔ `throw;`

Giữ nguyên stack trace → được khuyến nghị.

### ❌ `throw ex;`

Làm mất stack trace gốc → tránh dùng.

Ví dụ đúng:

```csharp
catch (Exception)
{
    throw; // giữ nguyên stack trace
}
```

---

## 5. "Trong .NET có guideline đặt tên exception không?"

Có. Khi tạo exception mới:

* Tên class nên kết thúc bằng **Exception**
* Từ khóa mô tả lỗi (ví dụ: InvalidShapeException)

Ví dụ:

```csharp
public class InvalidOrderException : Exception
{
    public InvalidOrderException(string message) : base(message) {}
}
```

---

## 6. "Các loại lỗi nên dùng exception nào?"

| Tình huống                     | Nên dùng exception                                 |
| ------------------------------ | -------------------------------------------------- |
| Tham số sai                    | `ArgumentException`, `ArgumentOutOfRangeException` |
| Lỗi định dạng                  | `FormatException`                                  |
| Trạng thái object không hợp lệ | `InvalidOperationException`                        |
| File không tồn tại             | `FileNotFoundException`                            |
| Truy cập trái phép             | `UnauthorizedAccessException`                      |

---

## 7. "Avoid using exceptions for flow control" — Vì sao?

Vì exception tốn chi phí xử lý (slow path).
Dùng exception cho logic bình thường sẽ:

* Làm code khó hiểu
* Giảm performance
* Che giấu lỗi thật

Ví dụ ❌ sai:

```csharp
try
{
    var x = dict[key];
}
catch
{
    // dùng exception để kiểm tra key tồn tại → KHÔNG NÊN
}
```

Ví dụ ✔ đúng:

```csharp
if (dict.TryGetValue(key, out var x))
{
    // OK
}
```

---

## 8. "Use exceptions for exceptional situations" — Best practices

✔ Dùng exception khi:

* Lỗi nghiêm trọng, không thể tiếp tục
* Tình huống bất ngờ, không dự đoán trước
* Bạn muốn buộc caller xử lý lỗi

✔ Throw exception có ý nghĩa, thông điệp rõ ràng

✔ Catch và xử lý ở mức logic phù hợp

---

## 9. "Don't overuse custom exceptions"

Chỉ tạo custom exception khi:

* Lỗi mang tính domain-specific
* Không có exception .NET có sẵn mô tả đúng lỗi

Ví dụ hợp lý:

```csharp
public class OrderNotPaidException : Exception
{
    public OrderNotPaidException(string message) : base(message) {}
}
```

Ví dụ KHÔNG nên làm:

```csharp
public class MyException : Exception {} // tên mơ hồ, vô nghĩa
```

---

## 10. Tóm tắt nhanh

* Exception chỉ dùng cho lỗi bất thường
* Không dùng exception cho flow control
* Catch có mục đích rõ ràng
* Throw exception giữ nguyên stack trace (`throw;`)
* Dùng exception .NET có sẵn khi phù hợp
* Chỉ tạo custom exception khi cần thiết

---

# III. EXCEPTION HANDLING

---

## 1. "Exception handling là gì?"

**Exception handling** là cơ chế cho phép bạn:

* Phát hiện lỗi trong khi chạy chương trình
* Xử lý lỗi đúng cách
* Cho phép chương trình tiếp tục hoặc dừng an toàn

C# cung cấp ba khối chính:

* `try`
* `catch`
* `finally`

---

## 2. "Cấu trúc try-catch cơ bản"

```csharp
try
{
    int x = int.Parse("abc");
}
catch (FormatException ex)
{
    Console.WriteLine("Sai định dạng!");
}
```

### Ý nghĩa:

* Mã trong `try` có thể gây lỗi
* `catch` chỉ chạy khi lỗi phù hợp xảy ra

---

## 3. "Bắt nhiều loại exception"

```csharp
try
{
    ProcessFile();
}
catch (FileNotFoundException)
{
    Console.WriteLine("Không tìm thấy file!");
}
catch (IOException)
{
    Console.WriteLine("Lỗi IO!");
}
catch (Exception ex)
{
    Console.WriteLine($"Lỗi khác: {ex.Message}");
}
```

⚠ **Quan trọng:** Thứ tự catch là từ cụ thể → tổng quát.

---

## 4. "Catch-all handler — nên hay không?"

Dạng catch bắt mọi lỗi:

```csharp
catch (Exception ex)
{
    Log(ex);
}
```

Dùng khi:

* Bạn muốn log tất cả lỗi
* Bạn muốn dọn tài nguyên và tắt ứng dụng an toàn

Không nên dùng để che lỗi.

---

## 5. "Sử dụng finally"

`finally` **luôn thực thi** dù có exception hay không.

Ví dụ dọn tài nguyên:

```csharp
FileStream? fs = null;
try
{
    fs = File.OpenRead("data.txt");
}
catch
{
    Console.WriteLine("Lỗi!");
}
finally
{
    fs?.Dispose();
}
```

`finally` đặc biệt quan trọng với:

* File stream
* Network connections
* Database connections

---

## 6. "Combining try-catch-finally"

```csharp
try
{
    DoWork();
}
catch (InvalidOperationException)
{
    Console.WriteLine("Không thể thực hiện thao tác này!");
}
finally
{
    Cleanup();
}
```

---

## 7. "Exception filters — catch when"

Bạn có thể lọc exception bằng điều kiện:

```csharp
catch (OrderException ex) when (ex.Severity == Severity.Low)
{
    Console.WriteLine("Lỗi nhẹ, tiếp tục chạy.");
}
```

Nếu điều kiện sai → handler **bị bỏ qua**.

---

## 8. "Throw exception từ catch block"

### Ném lại exception cũ:

```csharp
catch (Exception)
{
    throw; // giữ nguyên stack trace
}
```

### Ném exception mới:

```csharp
catch (Exception ex)
{
    throw new CustomException("Lỗi xảy ra", ex);
}
```

---

## 9. "Exception propagation — lan truyền exception"

Nếu một exception **không được catch**, nó sẽ lan lên call stack:

* Từ method con → method cha → method cao hơn
* Dừng lại khi gặp handler phù hợp

Nếu không có handler → ứng dụng **crash**.

---

## 10. "Exception handling trong async/await"

### Bắt lỗi trong async:

```csharp
try
{
    await DoWorkAsync();
}
catch (HttpRequestException ex)
{
    Console.WriteLine("Lỗi mạng!");
}
```

### Task lưu exception trong Task.Exception:

```csharp
var task = DoWorkAsync();
try
{
    await task;
}
catch
{
    Console.WriteLine(task.Exception);
}
```

---

## 11. "Exception handling trong iterator (yield)"

Iterator có thể ném exception, và cần catch bên ngoài:

```csharp
foreach (var item in GetItems())
{
    // exception có thể xảy ra tại đây
}
```

Hoặc bên trong iterator:

```csharp
IEnumerable<int> GetItems()
{
    try
    {
        yield return 1;
        throw new Exception();
    }
    finally
    {
        Console.WriteLine("Iterator cleanup");
    }
}
```

---

## 12. "Các trường hợp đặc biệt cần handler riêng"

### Null values:

```csharp
ArgumentNullException.ThrowIfNull(obj);
```

### Task cancellation:

```csharp
catch (OperationCanceledException)
{
    Console.WriteLine("Task bị hủy");
}
```

### Overflow:

```csharp
checked
{
    int x = int.MaxValue + 1; // gây OverflowException
}
```

---

## 13. Best practices

✔ Bắt đúng exception, không bắt quá rộng
✔ Luôn dọn tài nguyên trong `finally` hoặc `using`
✔ Không nuốt exception
✔ Ghi log đầy đủ
✔ Không dùng exception cho luồng điều khiển logic
✔ Giữ nguyên stack trace khi ném lại lỗi

---

## 14. Tóm tắt nhanh

* try-catch giúp xử lý lỗi an toàn
* catch lọc theo exception type
* finally luôn chạy
* throw để ném lỗi thủ công
* Exception filters giúp bắt lỗi có điều kiện
* Async/await xử lý lỗi giống try-catch bình thường

---

# IV. CREATE AND THROW EXCEPTIONS

---

## 1. "Khi nào cần tạo exception mới?"

Bạn nên tạo exception tùy chỉnh (**custom exception**) khi:

* Lỗi thuộc về **domain logic** của ứng dụng
* Không có exception .NET nào mô tả chính xác lỗi

Ví dụ hợp lý:

```csharp
public class OrderNotPaidException : Exception
{
    public OrderNotPaidException(string message) : base(message) {}
}
```

Không nên tạo exception mơ hồ:

```csharp
public class MyException : Exception {} // vô nghĩa
```

---

## 2. "Quy tắc đặt tên exception"

Microsoft khuyến nghị:

* Tên class kết thúc bằng **Exception**
* Mô tả lỗi rõ ràng, chính xác

Ví dụ tốt:

* `InvalidTemperatureException`
* `UserNotFoundException`
* `PaymentDeclinedException`

---

## 3. "Cách ném exception bằng throw"

### Ném exception mới:

```csharp
throw new InvalidOperationException("Không thể hoàn thành thao tác.");
```

### Ném exception với inner exception:

Dùng khi bạn muốn giữ thông tin lỗi gốc:

```csharp
try
{
    ProcessFile();
}
catch (IOException ex)
{
    throw new DataLoadException("Không thể tải dữ liệu.", ex);
}
```

Inner exception rất quan trọng trong debugging.

---

## 4. "throw; vs throw ex; — khác nhau như thế nào?"

### ✔ `throw;`

* Ném lại lỗi **giữ nguyên stack trace**
* Khuyến nghị dùng

### ❌ `throw ex;`

* Reset stack trace → khó debug

Ví dụ đúng:

```csharp
catch (Exception)
{
    throw; // giữ nguyên thông tin lỗi gốc
}
```

---

## 5. "Argument validation — kiểm tra tham số và ném lỗi"

C# cung cấp helper methods từ .NET 6:

```csharp
ArgumentNullException.ThrowIfNull(name);
ArgumentOutOfRangeException.ThrowIfNegative(age);
```

Ví dụ manual validation:

```csharp
if (age < 0)
    throw new ArgumentOutOfRangeException(nameof(age), "Tuổi không hợp lệ.");
```

---

## 6. "Tạo custom exception đầy đủ — best practices"

Mẫu exception tùy chỉnh chuẩn theo guideline Microsoft:

```csharp
[Serializable]
public class InvalidOrderStateException : Exception
{
    public InvalidOrderStateException() {}
    public InvalidOrderStateException(string message) : base(message) {}
    public InvalidOrderStateException(string message, Exception inner) : base(message, inner) {}
    protected InvalidOrderStateException(SerializationInfo info, StreamingContext context) : base(info, context) {}
}
```

Bao gồm:

* Constructor mặc định
* Constructor message
* Constructor message + inner
* Constructor hỗ trợ serialization

---

## 7. "Tạo exception dùng when để lọc lỗi"

```csharp
catch (OrderException ex) when (ex.Severity == Severity.Critical)
{
    throw new CriticalOrderException("Đơn hàng lỗi nghiêm trọng.", ex);
}
```

---

## 8. "Ví dụ đầy đủ — tạo và ném exception tùy chỉnh"

```csharp
public class TemperatureSensor
{
    public void Read(int temperature)
    {
        if (temperature < -50 || temperature > 150)
            throw new TemperatureOutOfRangeException(temperature);
    }
}

public class TemperatureOutOfRangeException : Exception
{
    public int Temperature { get; }

    public TemperatureOutOfRangeException(int temperature)
        : base($"Nhiệt độ {temperature} nằm ngoài phạm vi.")
        => Temperature = temperature;
}
```

---

## 9. "Exception trong constructor"

Constructor có thể ném lỗi nếu object ở trạng thái không hợp lệ:

```csharp
public class Person
{
    public Person(string name)
    {
        if (string.IsNullOrWhiteSpace(name))
            throw new ArgumentException("Tên không hợp lệ", nameof(name));
    }
}
```

---

## 10. Tóm tắt nhanh

| Khái niệm                     | Ý nghĩa                            |
| ----------------------------- | ---------------------------------- |
| **Custom exception**          | Exception mô tả lỗi domain         |
| **Inner exception**           | Giữ lỗi gốc khi ném lỗi mới        |
| **throw;**                    | Ném lại lỗi giữ nguyên stack trace |
| **Argument validation**       | Kiểm tra tham số đúng quy tắc      |
| **Serialization constructor** | Cần cho exception tùy chỉnh chuẩn  |

---
