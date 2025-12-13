# Sorting Data (C#)

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Sorting (Sắp xếp) trong LINQ hoạt động như thế nào?**
> **A:** Là thao tác sắp xếp lại các phần tử của một chuỗi dựa trên một hoặc nhiều thuộc tính (khóa sắp xếp).
> - **Lưu ý quan trọng:** Hầu hết các toán tử sắp xếp thuộc loại **Deferred Execution** (Trì hoãn) nhưng là **Non-streaming**. Tức là nó phải đọc hết dữ liệu vào bộ nhớ đệm để biết phần tử nào lớn nhất/nhỏ nhất rồi mới bắt đầu trả về kết quả.



---

**Q2: Làm thế nào để sắp xếp chính (Primary Sort)?**
> **A:** Sử dụng `OrderBy` (tăng dần) hoặc `OrderByDescending` (giảm dần).
>
> **Ví dụ:** Sắp xếp danh sách tên theo độ dài.
> ```csharp
> string[] words = { "the", "quick", "brown", "fox", "jumps" };
>
> // Method Syntax
> var query = words.OrderBy(w => w.Length);
>
> // Query Syntax
> var query2 = from w in words
>              orderby w.Length
>              select w;
>
> // Output: the, fox, quick, brown, jumps
> // (Lưu ý: "the" và "fox" cùng độ dài 3, thứ tự của chúng có thể giữ nguyên như ban đầu)
> ```

---

**Q3: Làm thế nào để sắp xếp phụ (Secondary Sort) - Xử lý khi giá trị bị trùng?**
> **A:** Khi hai phần tử có giá trị sắp xếp chính bằng nhau, ta dùng `ThenBy` hoặc `ThenByDescending` để định nghĩa tiêu chí phụ.
> - **Lưu ý:** `ThenBy` chỉ chạy được sau khi đã gọi `OrderBy`.
>
> **Ví dụ:** Sắp xếp theo độ dài (Tăng dần), nếu cùng độ dài thì sắp xếp theo bảng chữ cái (Tăng dần).
> ```csharp
> string[] words = { "apple", "grape", "banana", "kiwi", "cherry" };
>
> // Method Syntax: Chấm liên tiếp (.)
> var query = words.OrderBy(w => w.Length)
>                  .ThenBy(w => w);
>
> // Query Syntax: Dùng dấu phẩy (,)
> var query2 = from w in words
>              orderby w.Length, w // <--- Dấu phẩy ở đây
>              select w;
>
> // Output: kiwi, apple, grape, banana, cherry
> // (apple và grape cùng độ dài 5, nhưng apple đứng trước vì a < g)
> ```

---

**Q4: Lỗi thường gặp khi muốn sắp xếp nhiều tiêu chí là gì?**
> **A:** Đó là gọi `OrderBy` nhiều lần liên tiếp.
> - **SAI:** `list.OrderBy(x => x.Length).OrderBy(x => x.Name)` -> Lệnh `OrderBy` thứ 2 sẽ **xóa bỏ** hoàn toàn kết quả của lệnh thứ 1.
> - **ĐÚNG:** `list.OrderBy(x => x.Length).ThenBy(x => x.Name)` -> Giữ nguyên kết quả thứ 1 và chỉ sắp xếp lại những phần tử bị trùng.

---

**Q5: Phương thức 'Reverse' dùng để làm gì?**
> **A:** `Reverse` đơn giản là **đảo ngược** thứ tự của các phần tử trong danh sách hiện tại. Nó không quan tâm đến giá trị bên trong (không phải là sắp xếp giảm dần).
>
> **Ví dụ:**
> ```csharp
> char[] apple = { 'a', 'p', 'p', 'l', 'e' };
>
> var reversed = apple.Reverse();
>
> Console.WriteLine(string.Join("", reversed));
> // Output: elppa
> ```