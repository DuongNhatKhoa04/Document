# How to: Use LINQ to query files and directories

**Version:** 1.0
**Updated:** 13/12/2025
**Author:** Vox

---

**Q1: Tại sao nên dùng LINQ để truy vấn File System thay vì cách truyền thống?**
> **A:**
> - **Ngắn gọn:** Thay thế các vòng lặp đệ quy hoặc `foreach` lồng nhau phức tạp.
> - **Mạnh mẽ:** Dễ dàng thực hiện các tác vụ phức tạp như lọc theo nhiều tiêu chí (đuôi file, kích thước, ngày tạo), sắp xếp, hoặc nhóm file.
> - **Đối tượng hóa:** LINQ làm việc tốt với mảng đối tượng `FileInfo` hoặc `DirectoryInfo`, cho phép truy cập thuộc tính (như `Length`, `LastWriteTime`) trực tiếp.

---

**Q2: Làm thế nào để tìm file có đuôi cụ thể (ví dụ .txt)? (Kèm code)**
> **A:** Sử dụng lớp `DirectoryInfo` để lấy danh sách file, sau đó dùng toán tử `Where`.
>
> **Ví dụ:** Tìm tất cả file `.txt` trong folder hệ thống.
> ```csharp
> string startFolder = @"C:\Program Files\dotnet";
> DirectoryInfo dir = new DirectoryInfo(startFolder);
>
> // Lấy tất cả file (bao gồm thư mục con)
> var fileList = dir.GetFiles("*.*", SearchOption.AllDirectories);
>
> // Truy vấn LINQ
> var txtFiles = from file in fileList
>                where file.Extension == ".txt"
>                select file;
>
> foreach (var file in txtFiles)
> {
>     Console.WriteLine(file.FullName);
> }
> ```

---

**Q3: Làm thế nào để tìm file có kích thước lớn nhất? (Kèm code)**
> **A:** Sử dụng `OrderByDescending` để sắp xếp theo dung lượng (`Length`), sau đó dùng `Take` hoặc `First`.
>
> **Ví dụ:**
> ```csharp
> var largestFile = (from file in fileList
>                    orderby file.Length descending
>                    select file).First();
>
> Console.WriteLine($"File lớn nhất: {largestFile.Name} ({largestFile.Length} bytes)");
> ```

---

**Q4: Làm thế nào để nhóm các file theo đuôi mở rộng? (Kèm code)**
> **A:** Sử dụng mệnh đề `group by`. Đây là cách tuyệt vời để thống kê xem mỗi loại file chiếm bao nhiêu số lượng.
>
> **Ví dụ:**
> ```csharp
> var query = from file in fileList
>             group file by file.Extension.ToLower() into fileGroup
>             orderby fileGroup.Count() descending // Sắp xếp nhóm nào nhiều file nhất lên đầu
>             select new 
>             { 
>                 Extension = fileGroup.Key, 
>                 Count = fileGroup.Count() 
>             };
>
> foreach (var item in query)
> {
>     Console.WriteLine($"{item.Extension}: {item.Count} files");
> }
> ```

---

**Q5: Tính tổng dung lượng (Size) của tất cả các file trong folder? (Kèm code)**
> **A:** Sử dụng phương thức tổng hợp `Sum()`.
>
> **Ví dụ:**
> ```csharp
> long totalSize = fileList.Sum(f => f.Length);
> Console.WriteLine($"Tổng dung lượng: {totalSize} bytes");
> ```

---

**Q6: Sự khác biệt quan trọng giữa 'GetFiles' và 'EnumerateFiles' là gì?**
> **A:** Đây là kiến thức hiệu năng quan trọng:
> - **GetFiles:** Trả về một **mảng** (`FileInfo[]`). Nó phải đợi tìm hết tất cả file rồi mới trả về kết quả. Nếu folder có hàng triệu file, nó sẽ rất chậm và tốn RAM.
> - **EnumerateFiles:** Trả về một **tập hợp** (`IEnumerable<FileInfo>`). Nó trả về kết quả dạng luồng (streaming). Bạn có thể bắt đầu xử lý file đầu tiên ngay lập tức mà không cần đợi tìm hết.
> -> **Khuyên dùng:** Nên dùng `EnumerateFiles` khi kết hợp với LINQ để tận dụng cơ chế **Deferred Execution**.