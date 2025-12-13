# Deconstructing tuples and other types

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Deconstruction (Phân rã) là gì?**
> **A:** Là quá trình trích xuất các trường hoặc thuộc tính của một đối tượng (như Tuple, Record) và gán chúng vào các biến riêng lẻ trong một câu lệnh duy nhất.
> *Ví dụ:* `var (city, population, area) = QueryCityData("New York");`

---

**Q2: Có những cách nào để phân rã một Tuple?**
> **A:**
> 1.  **Khai báo kiểu rõ ràng:** `(string city, int population, double area) = ...`
> 2.  **Dùng từ khóa var:** `var (city, population, area) = ...` (Trình biên dịch tự suy luận kiểu).
> 3.  **Dùng biến đã khai báo trước:**
>     ```csharp
>     string city;
>     int pop;
>     double area;
>     (city, pop, area) = QueryCityData(...);
>     ```

---

**Q3: Deconstructing user-defined types (Phân rã kiểu do người dùng định nghĩa) hoạt động như thế nào?**
> **A:** Để một class, struct hoặc interface có thể phân rã được, bạn phải định nghĩa một (hoặc nhiều) phương thức có tên là **Deconstruct** trả về `void` và sử dụng các tham số đầu ra (**out parameters**) cho mỗi giá trị muốn trích xuất.
> *Ví dụ:*
> ```csharp
> public void Deconstruct(out string fname, out string lname)
> {
>     fname = FirstName;
>     lname = LastName;
> }
> ```

---

**Q4: Phương thức Deconstruct có bắt buộc phải là instance method không?**
> **A:** Không. Nó có thể là:
> - Một **instance method** (phương thức của đối tượng).
> - Hoặc một **extension method** (phương thức mở rộng) có tên `Deconstruct`. Điều này giúp bạn thêm khả năng phân rã cho cả những class mà bạn không sở hữu mã nguồn.

---

**Q5: Deconstructing records (Phân rã Record) có gì đặc biệt?**
> **A:** Đối với các loại **positional record** (record có primary constructor), trình biên dịch sẽ **tự động** tạo sẵn phương thức `Deconstruct` cho bạn dựa trên các tham số vị trí.
> *Ví dụ:* Với `public record Person(string Name, int Age);`, bạn có thể viết ngay `var (n, a) = person;` mà không cần viết thêm code gì.