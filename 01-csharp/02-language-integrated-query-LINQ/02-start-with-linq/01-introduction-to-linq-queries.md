# Introduction to LINQ Queries

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Ba hành động riêng biệt (Distinct actions) của mọi thao tác truy vấn LINQ là gì?**
> **A:**
> 1.  **Obtain the data source:** Lấy nguồn dữ liệu.
> 2.  **Create the query:** Tạo câu truy vấn.
> 3.  **Execute the query:** Thực thi câu truy vấn.


---

**Q2: Biến truy vấn (Query variable) lưu trữ cái gì?**
> **A:** Biến truy vấn chỉ lưu trữ **thông tin** cần thiết để tạo ra kết quả (kế hoạch truy vấn), chứ **KHÔNG** lưu trữ dữ liệu kết quả thực tế.
> - Điều này có nghĩa là bạn có thể tạo truy vấn một lần và thực thi nó nhiều lần để lấy dữ liệu mới nhất.

---

**Q3: Deferred execution (Thực thi trì hoãn) là gì?**
> **A:** Là việc thao tác truy vấn **không** được thực hiện ngay tại thời điểm bạn khai báo biến truy vấn.
> - Truy vấn chỉ thực sự chạy khi bạn lặp qua biến truy vấn (ví dụ: dùng `foreach`).
> - Hầu hết các toán tử trả về `IEnumerable<T>` hoặc `IQueryable<T>` đều hoạt động theo cơ chế này.

---

**Q4: Immediate execution (Thực thi ngay lập tức) xảy ra khi nào?**
> **A:** Xảy ra khi:
> 1.  Truy vấn trả về một giá trị đơn (scalar result) như `Count()`, `Max()`, `Average()`, `First()`.
> 2.  Bạn ép buộc thực thi để lưu kết quả vào bộ nhớ đệm (**cache results**) bằng cách gọi `ToList()`, `ToArray()`, `ToDictionary()`.

---

**Q5: Streaming vs Non-streaming operators trong Deferred execution khác nhau thế nào?**
> **A:**
> - **Streaming:** Không cần đọc hết dữ liệu nguồn trước khi trả về kết quả. Nó xử lý từng phần tử và trả về ngay khi có thể (ví dụ: `Where`, `Select`).
> - **Non-streaming:** Phải đọc **toàn bộ** dữ liệu nguồn trước khi trả về kết quả đầu tiên (ví dụ: `OrderBy` - vì phải biết hết số thì mới sắp xếp được).

---

**Q6: LINQ to Objects là gì?**
> **A:** Là việc sử dụng LINQ để truy vấn trực tiếp các tập hợp trong bộ nhớ (**in-memory collections**) hỗ trợ `IEnumerable` hoặc `IEnumerable<T>` (như Array, List, Dictionary) mà không cần qua một nhà cung cấp trung gian (LINQ provider) hay API đặc biệt nào.

---

**Q7: Cách lưu trữ kết quả của một truy vấn vào bộ nhớ (Store results in memory)?**
> **A:** Vì truy vấn mặc định là thực thi lười (lazy), nếu bạn muốn lưu cứng kết quả lại để dùng sau (ví dụ: để sửa đổi mà không ảnh hưởng nguồn), hãy gọi `ToList()` hoặc `ToArray()`.
> *Ví dụ:* `List<int> numbers = query.ToList();`