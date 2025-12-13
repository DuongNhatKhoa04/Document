# Query expression basics

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Query expression (Biểu thức truy vấn) là gì?**
> **A:** Là một truy vấn được viết bằng **query syntax** (cú pháp khai báo giống SQL). Nó là cấu trúc ngôn ngữ hạng nhất (**first-class language construct**) trong C#.
> - Một biểu thức truy vấn phải bắt đầu bằng mệnh đề `from` và kết thúc bằng mệnh đề `select` hoặc `group`.

---

**Q2: Query variable (Biến truy vấn) khác gì với biến chứa kết quả?**
> **A:**
> - **Query variable:** Lưu trữ lệnh truy vấn (ví dụ: `IEnumerable<int> scoreQuery`). Nó không chứa dữ liệu thực tế.
> - **Result variable:** Lưu trữ dữ liệu kết quả thực sự sau khi truy vấn đã được thực thi (ví dụ: `var highScore = scoreQuery.Max()`).

---

**Q3: Cấu trúc bắt buộc của một Query expression?**
> **A:**
> 1.  **Bắt đầu:** Mệnh đề `from` (xác định nguồn dữ liệu và biến phạm vi).
> 2.  **Thân (Body):** Các mệnh đề tùy chọn như `where`, `orderby`, `join`, `let`, hoặc thêm các `from` khác.
> 3.  **Kết thúc:** Mệnh đề `select` (chọn dữ liệu trả về) hoặc `group` (nhóm dữ liệu).

---

**Q4: Mệnh đề 'from' hoạt động như thế nào?**
> **A:** Nó chỉ định nguồn dữ liệu (`in scores`) và một **range variable** (biến phạm vi - `score`).
> - Biến phạm vi đại diện cho từng phần tử trong chuỗi nguồn khi duyệt qua. Nó được định kiểu mạnh (**strongly typed**).
> *Ví dụ:* `from score in scores`

---

**Q5: Mệnh đề 'select' dùng để làm gì?**
> **A:** Dùng để xác định hình dạng (**shape**) và loại dữ liệu của kết quả trả về.
> - Bạn có thể trả về nguyên bản đối tượng (`select score`), hoặc biến đổi nó (`select score.ToString()`), hoặc tạo ra đối tượng mới (`select new { Name = c.Name }` - Projection).

---

**Q6: Mệnh đề 'group' dùng để làm gì?**
> **A:** Dùng để nhóm các phần tử lại dựa trên một khóa (**key**) nào đó. Kết quả trả về là một chuỗi các nhóm (`IGrouping<Key, Element>`).
> *Ví dụ:* `group country by country.Name[0]` (Nhóm quốc gia theo chữ cái đầu).

---

**Q7: Từ khóa 'into' (Continuation) dùng khi nào?**
> **A:** Dùng để lưu kết quả của mệnh đề `group` hoặc `select` vào một biến tạm thời để tiếp tục thực hiện thêm các truy vấn khác trên kết quả đó.
> *Ví dụ:* `group ... into countryGroup where countryGroup.Key >= 20 ...`

---

**Q8: Mệnh đề 'let' dùng để làm gì?**
> **A:** Dùng để lưu trữ kết quả của một biểu thức con (**sub-expression**) vào một biến phạm vi mới để dùng lại nhiều lần trong các mệnh đề sau, giúp code gọn và hiệu quả hơn.
> *Ví dụ:* `let firstName = name.Split(' ')[0]`

---

**Q9: Multiple 'from' clauses (Nhiều mệnh đề from) dùng khi nào?**
> **A:** Dùng khi muốn truy cập vào các tập hợp lồng nhau (**nested collections**) trong nguồn dữ liệu. Nó tương tự như vòng lặp `foreach` lồng nhau.
> *Ví dụ:*
> ```csharp
> from country in countries
> from city in country.Cities
> ```