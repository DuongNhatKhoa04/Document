# Partitioning data (C#)

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Partitioning (Phân vùng) trong LINQ là gì?**
> **A:** Là thao tác chia một chuỗi đầu vào thành hai phần riêng biệt và chỉ lấy một phần trong số đó.
> - Khác với **Filtering** (`Where` - kiểm tra từng phần tử), **Partitioning** hoạt động dựa trên vị trí hoặc điều kiện dừng.
> - Các phương thức chính: `Skip`, `Take`, `SkipWhile`, `TakeWhile`.

---

**Q2: 'Take' và 'Skip' hoạt động như thế nào? (Kèm ví dụ)**
> **A:**
> - **Take(n):** Lấy `n` phần tử đầu tiên của chuỗi.
> - **Skip(n):** Bỏ qua `n` phần tử đầu tiên và lấy phần còn lại.
>
> **Ví dụ:**
> ```csharp
> int[] numbers = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
>
> // Lấy 3 phần tử đầu tiên
> var first3 = numbers.Take(3); 
> // Output: 0, 1, 2
>
> // Bỏ qua 3 phần tử đầu, lấy phần còn lại
> var allButFirst3 = numbers.Skip(3); 
> // Output: 3, 4, 5, 6, 7, 8, 9
> ```

---

**Q3: Ứng dụng quan trọng nhất của Skip/Take là gì?**
> **A:** **Phân trang (Pagination)**.
> - Công thức kinh điển để lấy dữ liệu cho trang `pageNumber` với kích thước `pageSize`:
> ```csharp
> int pageSize = 10;
> int pageNumber = 2; // Muốn lấy trang 2
>
> var pageData = sourceData
>     .Skip((pageNumber - 1) * pageSize) // Bỏ qua trang 1
>     .Take(pageSize);                   // Lấy dữ liệu trang 2
> ```

---

**Q4: 'TakeWhile' và 'SkipWhile' khác gì với 'Where'? (Kèm ví dụ)**
> **A:** Đây là điểm rất dễ nhầm lẫn.
> - **Where:** Duyệt qua **TOÀN BỘ** danh sách để tìm mọi phần tử thỏa mãn.
> - **TakeWhile:** Lấy các phần tử liên tục thỏa mãn điều kiện, nhưng sẽ **DỪNG NGAY LẬP TỨC** khi gặp phần tử đầu tiên sai điều kiện (ngắt mạch).
>
> **Ví dụ:**
> ```csharp
> int[] numbers = { 1, 2, 3, 99, 4, 5 }; // Số 99 làm gãy chuỗi tăng dần
>
> // Lấy các số nhỏ hơn 10 (Gặp 99 sẽ dừng ngay)
> var result = numbers.TakeWhile(n => n < 10);
>
> Console.WriteLine(string.Join(", ", result));
> // Output: 1, 2, 3
> // (Số 4 và 5 dù nhỏ hơn 10 cũng không được lấy vì chuỗi đã bị ngắt tại 99)
> ```

---

**Q5: Phương thức 'Chunk' (từ .NET 6) dùng để làm gì?**
> **A:** `Chunk(size)` dùng để chia nhỏ một danh sách lớn thành các mảng con (chunks) có kích thước cố định `size`.
> - Rất hữu ích khi xử lý Batch Processing (ví dụ: gửi 100 email một lần).
>
> **Ví dụ:**
> ```csharp
> int[] numbers = { 1, 2, 3, 4, 5, 6, 7 };
>
> var chunks = numbers.Chunk(3);
>
> foreach (var chunk in chunks)
> {
>     Console.WriteLine($"Chunk: {string.Join(",", chunk)}");
> }
> // Output:
> // Chunk: 1,2,3
> // Chunk: 4,5,6
> // Chunk: 7
> ```