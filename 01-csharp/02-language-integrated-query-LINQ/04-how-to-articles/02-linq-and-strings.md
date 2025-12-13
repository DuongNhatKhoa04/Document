# How to: Use LINQ to query strings

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Tại sao LINQ lại hoạt động được trên chuỗi (String)?**
> **A:** Vì trong C#, lớp `string` thực thi giao diện `IEnumerable<char>`.
> - Điều này có nghĩa là đối với LINQ, một chuỗi chỉ đơn giản là một danh sách các ký tự. Bạn có thể lọc số, tìm ký tự hoa, đếm ký tự...

---

**Q2: Làm thế nào để lọc các ký tự số ra khỏi một chuỗi? (Kèm code)**
> **A:** Sử dụng phương thức `Where` kết hợp với `char.IsDigit`.
>
> **Ví dụ:** Lọc lấy số điện thoại từ chuỗi hỗn độn.
> ```csharp
> string input = "Call me at 090-123-4567 after 5pm!";
>
> // Lọc chỉ lấy các ký tự là số
> var digits = input.Where(c => char.IsDigit(c));
>
> string phoneNumber = new string(digits.ToArray());
> Console.WriteLine(phoneNumber); 
> // Output: 09012345675
> ```

---

**Q3: Làm thế nào để đếm số lần xuất hiện của một từ trong văn bản? (Kèm code)**
> **A:** Đầu tiên bạn cần dùng `.Split()` để tách chuỗi thành mảng các từ, sau đó dùng LINQ để đếm.
>
> **Ví dụ:**
> ```csharp
> string text = "Historic Carved Stone of Dybbøl. Historically, the stone...";
>
> // Tách từ, loại bỏ dấu câu và khoảng trắng thừa
> string[] words = text.Split(new char[] { ' ', '.', ',' }, StringSplitOptions.RemoveEmptyEntries);
>
> // Tìm từ "stone" (không phân biệt hoa thường)
> var matchQuery = from word in words
>                  where word.ToLowerInvariant() == "stone"
>                  select word;
>
> Console.WriteLine($"Từ 'stone' xuất hiện {matchQuery.Count()} lần.");
> ```

---

**Q4: Làm thế nào để tìm các từ chung giữa hai câu (Intersection)? (Kèm code)**
> **A:** Sử dụng toán tử `Intersect`.
>
> **Ví dụ:**
> ```csharp
> string str1 = "hello world from C#";
> string str2 = "hello world from LINQ";
>
> var words1 = str1.Split(' ');
> var words2 = str2.Split(' ');
>
> // Tìm các từ xuất hiện ở cả 2 câu
> var commonWords = words1.Intersect(words2);
>
> Console.WriteLine(string.Join(", ", commonWords));
> // Output: hello, world, from
> ```

---

**Q5: Khi nào nên dùng LINQ so với Regex (Biểu thức chính quy)?**
> **A:**
> - **Dùng LINQ:** Khi logic xử lý đơn giản (sắp xếp, tìm từ cụ thể, lọc ký tự) hoặc cần kết hợp dữ liệu chuỗi với các nguồn dữ liệu khác. Code LINQ thường dễ đọc hơn.
> - **Dùng Regex:** Khi cần kiểm tra định dạng phức tạp (validate email, format ngày tháng) hoặc tìm kiếm mẫu (pattern matching) nâng cao mà LINQ viết sẽ rất dài dòng.