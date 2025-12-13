# Quantifier operations in LINQ (C#)

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Quantifier operations (Toán tử định lượng) là gì?**
> **A:** Là các phương thức dùng để kiểm tra xem các phần tử trong một chuỗi có thỏa mãn một điều kiện nào đó hay không.
> - Đặc điểm chung: Chúng trả về `true` hoặc `false` (không trả về tập hợp).
> - Thời điểm thực thi: **Immediate Execution** (Thực thi ngay lập tức).

---

**Q2: Phương thức 'All' dùng để làm gì? (Kèm ví dụ)**
> **A:** `All` kiểm tra xem **tất cả** các phần tử trong nguồn dữ liệu có thỏa mãn điều kiện hay không.
> - Chỉ cần **một** phần tử không thỏa mãn, nó trả về `false` ngay lập tức.
> - Nếu tập hợp rỗng, `All` trả về `true`.
>
> **Ví dụ:** Kiểm tra xem tất cả tên có bắt đầu bằng chữ 'B' không.
> ```csharp
> string[] names = { "Bob", "Bill", "Ben", "Bruno" };
>
> bool allStartWithB = names.All(n => n.StartsWith("B"));
>
> Console.WriteLine(allStartWithB); // Output: True
> ```

---

**Q3: Phương thức 'Any' dùng để làm gì? (Kèm ví dụ)**
> **A:** `Any` có 2 cách dùng:
> 1.  **Không tham số:** Kiểm tra xem tập hợp có chứa **bất kỳ phần tử nào không** (tức là tập hợp không rỗng).
> 2.  **Có tham số (điều kiện):** Kiểm tra xem có **ít nhất một** phần tử thỏa mãn điều kiện hay không.
>
> **Ví dụ:**
> ```csharp
> int[] numbers = { 1, 2, 3, 4, 5 };
>
> // 1. Kiểm tra list có rỗng không?
> bool hasElements = numbers.Any(); // True
>
> // 2. Có số nào lớn hơn 10 không?
> bool hasLargeNumber = numbers.Any(n => n > 10); // False
> ```

---

**Q4: Phương thức 'Contains' khác gì với 'Any'? (Kèm ví dụ)**
> **A:**
> - `Any`: Kiểm tra dựa trên một **điều kiện logic** (biểu thức lambda).
> - `Contains`: Kiểm tra sự tồn tại của một **đối tượng/giá trị cụ thể**.
>
> **Ví dụ:**
> ```csharp
> int[] numbers = { 10, 20, 30 };
>
> // Kiểm tra xem số 20 có trong mảng không
> bool hasTwenty = numbers.Contains(20); // True
> ```

---

**Q5: Lưu ý về hiệu năng khi dùng Quantifier?**
> **A:** Vì các phương thức này trả về kết quả ngay lập tức khi tìm thấy bằng chứng:
> - `All`: Dừng ngay khi gặp phần tử sai (`false`).
> - `Any`: Dừng ngay khi gặp phần tử đúng (`true`).
> -> Chúng không nhất thiết phải duyệt hết toàn bộ danh sách (trừ trường hợp xấu nhất).