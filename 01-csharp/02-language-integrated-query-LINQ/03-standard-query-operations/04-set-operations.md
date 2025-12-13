# Set operations (C#)

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Set operations (Phép toán tập hợp) trong LINQ là gì?**
> **A:** Là nhóm các phương thức dùng để so sánh hai tập hợp hoặc xử lý các phần tử trùng lặp, dựa trên quy tắc toán học về tập hợp.
> - Các phương thức chính: `Distinct`, `Except`, `Intersect`, `Union`.



---

**Q2: Phương thức 'Distinct' dùng để làm gì? (Kèm ví dụ)**
> **A:** `Distinct` loại bỏ các phần tử trùng lặp trong tập hợp, chỉ giữ lại các giá trị duy nhất (**unique values**).
>
> **Ví dụ:**
> ```csharp
> int[] factorsOf300 = { 2, 2, 3, 5, 5 };
>
> var uniqueFactors = factorsOf300.Distinct();
>
> Console.WriteLine(string.Join(", ", uniqueFactors));
> // Output: 2, 3, 5
> ```

---

**Q3: Phương thức 'Except' (Phép hiệu) dùng để làm gì? (Kèm ví dụ)**
> **A:** `Except` trả về các phần tử **có trong tập hợp thứ nhất nhưng KHÔNG có trong tập hợp thứ hai**. (Hiệu của tập A trừ tập B).
>
> **Ví dụ:**
> ```csharp
> string[] planets1 = { "Mercury", "Venus", "Earth", "Jupiter" };
> string[] planets2 = { "Mercury", "Earth", "Mars", "Jupiter" };
>
> // Lấy hành tinh có trong list 1 nhưng không có trong list 2
> var result = planets1.Except(planets2);
>
> foreach (var planet in result)
> {
>     Console.WriteLine(planet);
> }
> // Output: Venus
> // (Mercury, Earth, Jupiter bị loại vì có trong list 2)
> ```

---

**Q4: Phương thức 'Intersect' (Phép giao) dùng để làm gì? (Kèm ví dụ)**
> **A:** `Intersect` trả về các phần tử **xuất hiện ở cả hai tập hợp** (Phần chung).
>
> **Ví dụ:**
> ```csharp
> int[] id1 = { 44, 26, 92, 30, 71, 38 };
> int[] id2 = { 39, 59, 83, 47, 26, 44, 30 };
>
> // Tìm các ID xuất hiện ở cả 2 danh sách
> var both = id1.Intersect(id2);
>
> Console.WriteLine(string.Join(", ", both));
> // Output: 44, 26, 30
> ```

---

**Q5: Phương thức 'Union' (Phép hợp) khác gì với 'Concat'? (Kèm ví dụ)**
> **A:**
> - `Concat`: Nối đuôi hai danh sách lại với nhau (giữ nguyên phần tử trùng lặp).
> - `Union`: Gộp hai danh sách lại và **loại bỏ các phần tử trùng lặp** (trả về các phần tử duy nhất xuất hiện trong bất kỳ danh sách nào).
>
> **Ví dụ:**
> ```csharp
> int[] ints1 = { 5, 3, 9, 7, 5, 9, 3, 7 };
> int[] ints2 = { 8, 3, 6, 4, 4, 9, 1, 0 };
>
> // Gộp 2 mảng và loại bỏ trùng lặp
> var union = ints1.Union(ints2);
>
> Console.WriteLine(string.Join(", ", union));
> // Output: 5, 3, 9, 7, 8, 6, 4, 1, 0
> ```

---

**Q6: Lưu ý quan trọng khi dùng Set Operations với Object (Class)?**
> **A:** Các phương thức này mặc định sử dụng `Default Equality Comparer`.
> - Với các kiểu nguyên thủy (`int`, `string`): Nó so sánh giá trị -> OK.
> - Với `Class`: Nó so sánh tham chiếu (địa chỉ bộ nhớ). Hai object có cùng dữ liệu nhưng khác địa chỉ sẽ được coi là khác nhau.
> -> **Giải pháp:** Để `Distinct` hay `Union` hoạt động đúng với Class, bạn cần ghi đè `Equals()` và `GetHashCode()`, hoặc triển khai `IEquatable<T>`, hoặc dùng phiên bản `By` (như `DistinctBy` - từ .NET 6).