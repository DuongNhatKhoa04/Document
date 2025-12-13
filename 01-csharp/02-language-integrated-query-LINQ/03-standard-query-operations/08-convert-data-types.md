# Converting Data Types (C#)

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Mục đích chính của các phương thức chuyển đổi (Conversion Methods) là gì?**
> **A:**
> 1.  **Materialization (Hiện thực hóa):** Ép buộc truy vấn thực thi ngay lập tức và lưu trữ kết quả vào bộ nhớ (ví dụ: `ToList`, `ToArray`).
> 2.  **Type Casting (Ép kiểu phần tử):** Chuyển đổi kiểu dữ liệu của các phần tử trong chuỗi (ví dụ: `Cast`, `OfType`).
> 3.  **Interface Hiding:** Chuyển đổi kiểu của biến truy vấn (ví dụ: `AsEnumerable`) để thay đổi cách thực thi (ví dụ: chuyển từ LINQ to SQL sang LINQ to Objects).



---

**Q2: Phương thức 'ToArray', 'ToList' dùng để làm gì? (Kèm ví dụ)**
> **A:** Chúng ép buộc truy vấn thực thi ngay lập tức (**Immediate Execution**) và trả về một Mảng (`Array`) hoặc Danh sách (`List<T>`) chứa kết quả.
> - Dùng khi bạn muốn lưu trữ kết quả để sử dụng nhiều lần mà không muốn chạy lại truy vấn.
>
> **Ví dụ:**
> ```csharp
> string[] fruits = { "Apple", "Banana", "Mango" };
>
> // Truy vấn chưa chạy (Deferred)
> var query = from f in fruits where f.Length > 5 select f;
>
> // Truy vấn chạy NGAY LẬP TỨC và lưu vào List (Materialized)
> List<string> fruitList = query.ToList();
> ```

---

**Q3: Sự khác biệt giữa 'ToDictionary' và 'ToLookup'? (Kèm ví dụ)**
> **A:** Cả hai đều chuyển đổi danh sách thành cấu trúc `Key-Value`.
> - **ToDictionary:** Tỷ lệ 1-1. Mỗi Key là duy nhất. Nếu dữ liệu nguồn có 2 phần tử trùng Key -> **Lỗi** (Exception).
> - **ToLookup:** Tỷ lệ 1-n. Mỗi Key chứa một danh sách các giá trị. Nếu trùng Key -> Nó gom các giá trị vào cùng một Key (giống `GroupBy` nhưng chạy ngay lập tức).
>
> **Ví dụ:**
> ```csharp
> class Product { public int Id; public string Category; public string Name; }
> List<Product> products = GetProducts();
>
> // 1. ToDictionary: Tạo từ điển tìm nhanh theo ID (ID phải duy nhất)
> Dictionary<int, Product> dict = products.ToDictionary(p => p.Id);
> var prod = dict[101]; // Tìm cực nhanh
>
> // 2. ToLookup: Gom sản phẩm theo Category
> ILookup<string, Product> lookup = products.ToLookup(p => p.Category);
> // Lấy tất cả sản phẩm thuộc nhóm "Electronics"
> var electronics = lookup["Electronics"]; 
> ```

---

**Q4: Phương thức 'Cast<T>' và 'OfType<T>' khác nhau thế nào?**
> **A:** Cả hai đều dùng để ép kiểu các phần tử trong chuỗi.
> - **Cast<T>:** Cố gắng ép kiểu tất cả phần tử. Nếu gặp phần tử không ép được -> **Ném lỗi** (`InvalidCastException`).
> - **OfType<T>:** Chỉ lấy những phần tử ép kiểu thành công, bỏ qua các phần tử khác -> **An toàn** (Safe filtering).
>
> **Ví dụ:**
> ```csharp
> object[] mixed = { "Hello", 123, "World", 456 };
>
> // Dùng Cast: Sẽ lỗi vì không thể ép "Hello" sang int
> // var numbers = mixed.Cast<int>(); // -> Exception!
>
> // Dùng OfType: Chỉ lấy số, bỏ qua chuỗi
> var safeNumbers = mixed.OfType<int>(); // -> 123, 456
> ```

---

**Q5: Phương thức 'AsEnumerable' dùng khi nào?**
> **A:** Dùng để ẩn đi các phương thức đặc thù của một provider (như Entity Framework) và quay về sử dụng các phương thức chuẩn của LINQ to Objects.
> - Thường dùng để ngắt việc sinh câu lệnh SQL và thực hiện phần còn lại của truy vấn trên bộ nhớ Client (Client-side evaluation).
>
> **Ví dụ:**
> ```csharp
> // db.Students là IQueryable (chạy SQL trên server)
> var query = db.Students
>     .Where(s => s.Age > 18)   // Chạy SQL: WHERE Age > 18
>     .AsEnumerable()           // Kéo dữ liệu về RAM
>     .Select(s => HeavyCalculation(s)); // Hàm C# này chạy trên RAM máy client
> ```