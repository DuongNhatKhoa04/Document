# Standard query operators overview

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Standard Query Operators (Các toán tử truy vấn chuẩn) là gì?**
> **A:** Là tập hợp các phương thức tạo nên mẫu LINQ.
> - Hầu hết chúng là các **Extension Methods** nằm trong class `System.Linq.Enumerable` (cho LINQ to Objects) và `System.Linq.Queryable` (cho LINQ to SQL/Entities).
> - Chúng hoạt động trên các chuỗi dữ liệu (`IEnumerable<T>` hoặc `IQueryable<T>`).



---

**Q2: Các toán tử được phân loại dựa trên thời điểm thực thi (Execution Timing) như thế nào?**
> **A:** Có 2 loại chính:
> 1.  **Immediate Execution (Thực thi ngay lập tức):** Trả về một giá trị đơn (như `Count`, `Max`) hoặc một tập hợp cố định (như `ToList`). Truy vấn chạy ngay khi gọi phương thức.
> 2.  **Deferred Execution (Thực thi trì hoãn):** Trả về một chuỗi (`IEnumerable<T>`). Truy vấn chỉ chạy khi bạn duyệt qua kết quả (dùng `foreach`).

---

**Q3: Trong Deferred Execution, sự khác biệt giữa Streaming và Non-streaming là gì?**
> **A:**
> - **Streaming (Theo luồng):** Đọc một phần tử nguồn, xử lý, và trả về ngay (yield). Không cần đọc hết dữ liệu mới chạy. (Ví dụ: `Where`, `Select`). Tốn ít bộ nhớ.
> - **Non-streaming (Không theo luồng):** Bắt buộc phải đọc và nạp **toàn bộ** dữ liệu nguồn vào bộ nhớ để xử lý rồi mới trả về kết quả. (Ví dụ: `OrderBy`, `Reverse` - vì phải biết hết các số mới sắp xếp được).

---

**Q4: Các nhóm chức năng chính của toán tử LINQ?**
> **A:**
> - **Filtering (Lọc):** `Where`, `OfType`.
> - **Projection (Chiếu/Chuyển đổi):** `Select`, `SelectMany`.
> - **Partitioning (Phân vùng/Phân trang):** `Skip`, `Take`.
> - **Ordering (Sắp xếp):** `OrderBy`, `ThenBy`, `Reverse`.
> - **Grouping (Nhóm):** `GroupBy`, `ToLookup`.
> - **Set operations (Tập hợp):** `Distinct`, `Union`, `Intersect`.
> - **Aggregation (Tổng hợp):** `Count`, `Sum`, `Min`, `Max`, `Average`.

---

**Q5: Có phải tất cả toán tử đều có cú pháp Query Syntax (from...where...) không?**
> **A:** **Không**.
> - Một số toán tử như `Count`, `Take`, `Skip`, `Max`... **không có** từ khóa tương ứng trong cú pháp Query Syntax. Bạn bắt buộc phải dùng **Method Syntax** (gọi hàm).
> - Tuy nhiên, bạn có thể kết hợp cả hai (Mixed syntax).