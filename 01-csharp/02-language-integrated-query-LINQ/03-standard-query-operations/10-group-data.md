# Grouping Data (C#)

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Grouping (Nhóm) trong LINQ là gì?**
> **A:** Là thao tác sắp xếp dữ liệu vào các nhóm (buckets) dựa trên một giá trị chung gọi là **Key** (Khóa).
> - Ví dụ: Nhóm học sinh theo Lớp, nhóm sản phẩm theo Danh mục.
> - Kết quả trả về không phải là danh sách các phần tử lẻ tẻ, mà là một tập hợp các nhóm (`IEnumerable<IGrouping<TKey, TElement>>`).

---

**Q2: Cấu trúc của một nhóm 'IGrouping<Key, Element>' là gì?**
> **A:** Mỗi đối tượng `IGrouping` bao gồm 2 thành phần chính:
> 1.  **Key:** Giá trị chung dùng để nhóm (ví dụ: "Lớp 12A").
> 2.  **Sequence:** Bản thân `IGrouping` cũng là một danh sách (`IEnumerable`) chứa các phần tử thuộc nhóm đó. Bạn có thể lặp qua nó.

---

**Q3: Cú pháp Query Syntax (group...by) viết như thế nào? (Kèm ví dụ)**
> **A:** Cấu trúc: `group [phần_tử] by [khóa]`.
> - **Lưu ý:** Mệnh đề `group` thường kết thúc câu truy vấn (trừ khi dùng `into`).
>
> **Ví dụ:** Nhóm các số theo tính chẵn/lẻ.
> ```csharp
> int[] numbers = { 35, 44, 200, 84, 3987, 4, 199, 329, 446, 208 };
>
> var query = from number in numbers
>             group number by number % 2 == 0 ? "Số Chẵn" : "Số Lẻ";
>
> // Duyệt kết quả (Lặp lồng nhau)
> foreach (var group in query)
> {
>     Console.WriteLine($"Nhóm: {group.Key}"); // In ra Key (Số Chẵn/Lẻ)
>     
>     foreach (var number in group) // Lặp qua các số trong nhóm đó
>     {
>         Console.WriteLine($" - {number}");
>     }
> }
> ```

---

**Q4: Cú pháp Method Syntax (.GroupBy) viết như thế nào?**
> **A:** Sử dụng phương thức `.GroupBy(x => x.Key)`.
>
> **Ví dụ:** Nhóm từ theo chữ cái đầu tiên.
> ```csharp
> string[] words = { "blueberry", "chimpanzee", "abacus", "banana", "apple", "cheese" };
>
> var wordGroups = words.GroupBy(w => w[0]); // Key là ký tự đầu (char)
>
> foreach (var g in wordGroups)
> {
>     Console.WriteLine($"Bắt đầu bằng chữ '{g.Key}': có {g.Count()} từ.");
> }
> ```

---

**Q5: Từ khóa 'into' dùng để làm gì trong Grouping?**
> **A:** Dùng để lưu kết quả nhóm vào một biến tạm thời, cho phép bạn tiếp tục thực hiện các truy vấn khác (như lọc, sắp xếp, hoặc chọn) trên chính các nhóm đó.
>
> **Ví dụ:** Nhóm các số chẵn/lẻ, nhưng chỉ lấy nhóm nào có nhiều hơn 3 phần tử.
> ```csharp
> var query = from number in numbers
>             group number by number % 2 == 0 into numGroup // Lưu vào numGroup
>             where numGroup.Count() > 3                    // Lọc trên nhóm
>             select new { 
>                 Category = numGroup.Key ? "Even" : "Odd", 
>                 Count = numGroup.Count() 
>             };
> ```

---

**Q6: Sự khác biệt giữa 'GroupBy' và 'ToLookup'?**
> **A:**
> - **GroupBy:** Thực thi trì hoãn (**Deferred Execution**). Chỉ chạy khi bạn lặp qua.
> - **ToLookup:** Thực thi ngay lập tức (**Immediate Execution**). Duyệt toàn bộ nguồn dữ liệu và tạo ra một cấu trúc dữ liệu giống Dictionary nhưng cho phép trùng Key (Key -> List Values) và lưu vào bộ nhớ.