# Filtering Data in C# with LINQ

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Filtering (Lọc) trong LINQ là gì?**
> **A:** Là thao tác hạn chế tập kết quả trả về, chỉ giữ lại các phần tử thỏa mãn một điều kiện nhất định (**predicate**).
> - Kết quả trả về luôn là một tập hợp con của tập hợp gốc (số lượng phần tử $\le$ số lượng ban đầu).



---

**Q2: Hai phương thức lọc chuẩn (Standard operators) là gì?**
> **A:**
> 1.  **Where:** Lọc dựa trên một điều kiện logic (predicate).
> 2.  **OfType:** Lọc dựa trên khả năng ép kiểu dữ liệu (chỉ lấy các phần tử thuộc một kiểu cụ thể).

---

**Q3: Phương thức 'Where' hoạt động như thế nào? (Kèm ví dụ)**
> **A:** `Where` duyệt qua từng phần tử, kiểm tra biểu thức điều kiện (trả về `bool`). Nếu `true` thì giữ lại, `false` thì loại bỏ.
>
> **Ví dụ:** Lọc các từ có độ dài > 3 ký tự.
> ```csharp
> string[] words = { "the", "quick", "brown", "fox", "jumps" };
>
> // 1. Query Syntax
> var query = from word in words
>             where word.Length > 3
>             select word;
>
> // 2. Method Syntax (Lambda)
> var methodQuery = words.Where(word => word.Length > 3);
>
> // Kết quả cả 2 đều là: "quick", "brown", "jumps"
> ```

---

**Q4: Phương thức 'OfType' dùng khi nào? (Kèm ví dụ)**
> **A:** `OfType<T>` rất hữu ích khi bạn làm việc với các tập hợp không định kiểu (**non-generic collections** như `ArrayList`) hoặc tập hợp chứa nhiều loại đối tượng hỗn hợp. Nó sẽ chọn ra các phần tử có thể ép về kiểu `T` và bỏ qua các phần tử khác.
>
> **Ví dụ:** Chỉ lấy các số nguyên (`int`) từ một mảng hỗn hợp.
> ```csharp
> object[] things = { "Hello", 10, "World", 20, 3.5, true };
>
> // Chỉ lấy các phần tử là int
> var intValues = things.OfType<int>();
>
> foreach (var n in intValues)
> {
>     Console.WriteLine(n); // Output: 10, 20
> }
> ```

---

**Q5: Có thể sử dụng nhiều điều kiện trong mệnh đề 'where' không?**
> **A:** Có.
> - Trong **Query Syntax**: Sử dụng toán tử `&&` (AND) hoặc `||` (OR).
> - Trong **Method Syntax**: Bạn có thể nối chuỗi nhiều hàm `.Where()` liên tiếp hoặc dùng toán tử logic trong lambda.
>
> ```csharp
> // Lọc số chẵn VÀ lớn hơn 5
> var result = numbers.Where(n => n % 2 == 0 && n > 5);
> // Hoặc
> var result2 = numbers.Where(n => n % 2 == 0).Where(n => n > 5);
> ```