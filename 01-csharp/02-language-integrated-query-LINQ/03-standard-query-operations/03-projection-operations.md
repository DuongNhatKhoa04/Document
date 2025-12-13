# Projection operations (C#)

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Projection (Phép chiếu) trong LINQ là gì?**
> **A:** **Projection** là hành động biến đổi (**transform**) một đối tượng thành một dạng mới.
> - Thay vì trả về toàn bộ đối tượng gốc, bạn có thể chỉ trả về một thuộc tính, thực hiện tính toán trên thuộc tính đó, hoặc tạo ra một đối tượng mới chứa tập hợp các giá trị bạn cần.
> - Phương thức chính: `Select` và `SelectMany`.

---

**Q2: Phương thức 'Select' được sử dụng như thế nào? (Kèm ví dụ)**
> **A:** `Select` dùng để áp dụng một phép biến đổi lên **từng phần tử** của chuỗi. Kết quả trả về có số lượng phần tử bằng với chuỗi gốc.
>
> **Ví dụ 1: Chỉ lấy một thuộc tính (Property projection)**
> ```csharp
> List<string> words = new() { "an", "apple", "a", "day" };
>
> // Chỉ lấy độ dài của từng từ
> var lengths = from word in words
>               select word.Length;
> // Output: 2, 5, 1, 3
> ```
>
> **Ví dụ 2: Tạo đối tượng mới (Object construction/Anonymous type)**
> ```csharp
> List<Customer> customers = GetCustomers();
>
> // Chỉ lấy Name và Email (tạo ra kiểu vô danh - Anonymous type)
> var contactInfo = from c in customers
>                   select new { Name = c.Name, Email = c.Email };
> ```

---

**Q3: Phương thức 'SelectMany' dùng để làm gì? (Kèm ví dụ)**
> **A:** `SelectMany` dùng để **làm phẳng** (flatten) các tập hợp lồng nhau (**one-to-many relationships**).
> - Nếu mỗi phần tử gốc chứa một danh sách con, `Select` sẽ trả về "Danh sách của các danh sách" (`List<List<T>>`).
> - `SelectMany` sẽ gộp tất cả các danh sách con đó thành một "Danh sách phẳng" duy nhất (`List<T>`).



> **Ví dụ:** Lấy tất cả các từ trong tất cả các câu.
> ```csharp
> List<string> phrases = new() { "an apple a day", "the quick brown fox" };
>
> // Sử dụng SelectMany để tách từng câu thành các từ và gộp lại
> var allWords = phrases.SelectMany(ph => ph.Split(' '));
>
> foreach (var word in allWords)
> {
>     Console.WriteLine(word);
> }
> // Output: "an", "apple", "a", "day", "the", "quick", "brown", "fox"
> ```

---

**Q4: Sự khác biệt cốt lõi giữa Select và SelectMany là gì?**
> **A:**
> - **Select:** Giữ nguyên cấu trúc phân cấp. Input 1 phần tử -> Output 1 phần tử.
> - **SelectMany:** Phá vỡ cấu trúc phân cấp (Flatten). Input 1 phần tử (chứa list con) -> Output N phần tử (từ list con đó).

---

**Q5: Phương thức 'Zip' là gì? (Kèm ví dụ)**
> **A:** `Zip` (như khóa kéo áo) dùng để gộp hai chuỗi dữ liệu lại với nhau dựa trên vị trí tương ứng của chúng. Nó sẽ dừng lại khi chuỗi ngắn hơn kết thúc.
>
> **Ví dụ:** Gộp danh sách Số và danh sách Chữ.
> ```csharp
> int[] numbers = { 1, 2, 3 };
> string[] words = { "One", "Two", "Three" };
>
> var numbersAndWords = numbers.Zip(words, (n, w) => n + "=" + w);
>
> // Output: "1=One", "2=Two", "3=Three"
> ```