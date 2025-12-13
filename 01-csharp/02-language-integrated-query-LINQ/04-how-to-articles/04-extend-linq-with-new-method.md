# Write your own extensions to LINQ

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Tại sao lại cần mở rộng (extend) LINQ?**
> **A:** Mặc dù LINQ cung cấp rất nhiều phương thức chuẩn (như `Average`, `Max`, `Where`...), đôi khi bạn cần một phép tính đặc thù (ví dụ: tính trung vị `Median`, tính độ lệch chuẩn) hoặc một bộ lọc riêng biệt.
> - Việc viết **Extension Method** cho `IEnumerable<T>` giúp bạn gọi phương thức tùy chỉnh của mình tự nhiên như các phương thức LINQ chuẩn (`list.MyCustomMethod()`).

---

**Q2: Nguyên tắc cơ bản để viết một Extension Method cho LINQ là gì?**
> **A:**
> 1.  Tạo một **Static Class**.
> 2.  Tạo một **Static Method**.
> 3.  Tham số đầu tiên của phương thức phải có từ khóa `this` đứng trước kiểu dữ liệu muốn mở rộng (thường là `IEnumerable<T>`).

---

**Q3: Ví dụ: Viết phương thức tính trung vị (Median) cho kiểu Double?**
> **A:** Trung vị là giá trị nằm giữa danh sách đã sắp xếp.
>
> ```csharp
> public static class EnumerableExtension
> {
>     public static double Median(this IEnumerable<double> source)
>     {
>         if (source == null || !source.Any())
>         {
>             throw new InvalidOperationException("Nguồn dữ liệu không được rỗng.");
>         }
>
>         // 1. Sắp xếp danh sách
>         var sortedList = source.OrderBy(number => number).ToList();
>
>         // 2. Tìm vị trí giữa
>         int itemIndex = sortedList.Count / 2;
>
>         // 3. Tính toán
>         if (sortedList.Count % 2 == 0)
>         {
>             // Nếu chẵn phần tử: trung bình cộng của 2 số giữa
>             return (sortedList[itemIndex] + sortedList[itemIndex - 1]) / 2;
>         }
>         else
>         {
>             // Nếu lẻ phần tử: lấy số chính giữa
>             return sortedList[itemIndex];
>         }
>     }
> }
>
> // Cách dùng:
> double[] numbers = { 1.9, 2, 8, 4, 5.7, 6, 7.2, 0 };
> var median = numbers.Median(); // Output: 4.85
> ```

---

**Q4: Làm thế nào để tạo Overload hỗ trợ nhiều kiểu dữ liệu khác nhau (như int)?**
> **A:** Bạn có thể viết thêm một overload nhận `IEnumerable<int>` và bên trong gọi lại hàm `Median` của double.
>
> ```csharp
> // Overload cho int
> public static double Median(this IEnumerable<int> source)
> {
>     // Ép kiểu từng phần tử sang double và gọi hàm Median gốc
>     return (from number in source select (double)number).Median();
> }
> ```

---

**Q5: Làm thế nào để hỗ trợ Generic (Tổng quát) với Selector?**
> **A:** Để tính Median cho một danh sách đối tượng bất kỳ (ví dụ `List<Product>`), bạn cần một tham số `Func<T, double>` để người dùng chỉ định trường nào cần tính toán.
>
> ```csharp
> // Generic Overload
> public static double Median<T>(this IEnumerable<T> source, Func<T, double> selector)
> {
>     // Áp dụng selector để lấy ra danh sách double, sau đó gọi Median gốc
>     return source.Select(selector).Median();
> }
>
> // Cách dùng:
> string[] items = { "one", "two", "three", "four", "five" };
> // Tính trung vị độ dài của các chuỗi
> var medianLength = items.Median(s => s.Length); 
> ```

---

**Q6: Làm thế nào để viết Custom Query Method trả về một chuỗi mới (dạng Streaming)?**
> **A:** Sử dụng từ khóa `yield return` để trả về từng phần tử một cách lười biếng (**lazy evaluation**).
>
> **Ví dụ:** Phương thức trả về các phần tử ở vị trí chẵn (Alternate Elements).
> ```csharp
> public static IEnumerable<T> AlternateElements<T>(this IEnumerable<T> source)
> {
>     int index = 0;
>     foreach (T element in source)
>     {
>         if (index % 2 == 0) // Chỉ lấy phần tử ở vị trí chẵn (0, 2, 4...)
>         {
>             yield return element;
>         }
>         index++;
>     }
> }
> ```

---

**Q7: Cú pháp "Extension Block" mới trong C# 14 (Preview) là gì?**
> **A:** Từ C# 14, bạn có thể gom nhóm các extension methods lại gọn gàng hơn bằng từ khóa `extension`.
> *Lưu ý: Đây là tính năng rất mới, có thể chưa chạy được trên các phiên bản .NET cũ.*
> ```csharp
> extension(IEnumerable<double> source)
> {
>     public double Median() { ... }
> }
> ```