# Type Relationships in LINQ Query Operations

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Tại sao cần hiểu về mối quan hệ kiểu (Type Relationships) trong LINQ?**
> **A:** Vì LINQ là **strongly typed** (định kiểu mạnh). Dù bạn có dùng từ khóa `var`, trình biên dịch vẫn phải xác định chính xác kiểu dữ liệu ở mọi bước.
> - Hiểu luồng dữ liệu giúp bạn biết tại sao đầu vào là `Customer` nhưng đầu ra lại là `string` hoặc một đối tượng khác.



---

**Q2: Ba giai đoạn của dòng chảy kiểu dữ liệu trong LINQ là gì?**
> **A:**
> 1.  **Source:** Nguồn dữ liệu ban đầu (thường là `IEnumerable<SourceType>`).
> 2.  **Query Variable:** Biến lưu trữ truy vấn. Kiểu của nó phụ thuộc vào mệnh đề `select`. Nếu bạn chọn nguyên đối tượng, nó vẫn là `IEnumerable<SourceType>`. Nếu bạn chọn một thuộc tính, nó biến thành `IEnumerable<NewType>`.
> 3.  **Execution:** Trong vòng lặp `foreach`, biến lặp sẽ có kiểu cụ thể (`SourceType` hoặc `NewType`) để sử dụng.

---

**Q3: Phép chiếu (Projection) ảnh hưởng thế nào đến kiểu dữ liệu?**
> **A:** Mệnh đề `select` quyết định kiểu của biến truy vấn:
> - `select c`: Kiểu giữ nguyên (`IEnumerable<Customer>`).
> - `select c.Name`: Kiểu biến đổi thành chuỗi (`IEnumerable<string>`).
> - `select new { c.Name, c.Age }`: Kiểu biến đổi thành Anonymous Type (`IEnumerable<'a>`).

---

**Q4: Vai trò của từ khóa 'var' trong LINQ là gì?**
> **A:** `var` giúp code gọn gàng hơn, đặc biệt khi kiểu trả về là các generic phức tạp (như `IGrouping<string, List<Customer>>`) hoặc là Anonymous types.
> - **Lưu ý:** `var` không có nghĩa là biến không có kiểu (dynamic), mà là bảo trình biên dịch tự suy luận kiểu (`Strongly typed`).

---

**Q5: Trình biên dịch suy luận kiểu như thế nào?**
> **A:** Trình biên dịch dựa vào nguồn dữ liệu (`from c in customers`) để biết `c` là kiểu `Customer`. Sau đó dựa vào mệnh đề `select` để biết biến truy vấn sẽ trả về kiểu tập hợp gì.