# C# & Unity Interview Questions – High-Level Answers  
*Dành cho Unity Intern / Junior Developer*

---

## 📌 Mục lục
1. [Câu hỏi C# cơ bản](#i-câu-hỏi-c-cơ-bản-core-fundamentals)  
2. [OOP trong C#](#ii-câu-hỏi-oop-trong-c-rất-quan-trọng-khi-dùng-unity)  
3. [Câu hỏi nâng cao](#iii-câu-hỏi-nâng-cao-hơn-vẫn-phù-hợp-intern)  
4. [LINQ](#iv-linq-c-cực-hay-dùng-trong-xử-lý-data-game)  
5. [C# trong Unity](#v-liên-quan-đến-c-trong-unity)

---

# I. Câu hỏi C# cơ bản (Core Fundamentals)

## 1. C# là gì? Nó khác gì so với C++/Java?
**Answer:**
- C# là ngôn ngữ hiện đại của Microsoft chạy trên .NET/CLR.  
- Cú pháp thân thiện, hướng đối tượng mạnh.  
- Khác C++: không quản lý memory thủ công.  
- Khác Java: nhiều cú pháp mới & tích hợp sâu hệ sinh thái .NET.

---

## 2. CLR (Common Language Runtime) là gì?
**Answer:**
- Runtime của .NET quản lý memory, GC, JIT.  
- Đảm bảo code chạy an toàn và tối ưu.  
- Cung cấp cơ chế thực thi đa ngôn ngữ.

---

## 3. Biến và hằng khác nhau?
**Answer:**
- Biến: thay đổi được.  
- const: cố định tại compile-time.  
- readonly: cố định sau khi khởi tạo runtime.

---

## 4. Value type vs Reference type?
**Answer:**
- Value type lưu trực tiếp giá trị.  
- Reference type lưu tham chiếu đến object.  
- Value type nhanh và nhẹ hơn.

---

## 5. Stack và Heap khác nhau?
**Answer:**
- Stack: nhanh, dùng cho value type và biến local.  
- Heap: lưu object lớn, do GC quản lý.  
- Stack tối ưu nhưng dung lượng nhỏ.

---

## 6. Null là gì? NullReferenceException khi nào xảy ra?
**Answer:**
- null nghĩa là không trỏ tới object nào.  
- Lỗi xảy ra khi truy cập thuộc tính/hàm trên null.  
- Thường do quên khởi tạo object.

---

## 7. Boxing & Unboxing là gì?
**Answer:**
- Boxing: chuyển value type thành object → heap.  
- Unboxing: lấy value type từ object.  
- Gây overhead và tốn GC.

---

## 8. Từ khóa var hoạt động thế nào?
**Answer:**
- Compiler suy ra kiểu tại compile-time.  
- Không phải kiểu “mờ” hay dynamic.  
- Vẫn đảm bảo an toàn kiểu.

---

## 9. dynamic khác gì var?
**Answer:**
- var: xác định kiểu tại compile-time.  
- dynamic: xác định kiểu tại runtime.  
- dynamic linh hoạt nhưng dễ lỗi runtime.

---

# 2. Cấu trúc điều khiển

## 10. for, foreach, while, do…while?
**Answer:**
- for: dùng khi biết số lần lặp.  
- foreach: duyệt collection dễ và an toàn.  
- while: lặp khi điều kiện còn đúng.  
- do-while: chạy ít nhất 1 lần.

---

## 11. break, continue, return?
**Answer:**
- break: thoát vòng lặp.  
- continue: bỏ iteration hiện tại.  
- return: thoát hàm.

---

## 12. switch-case có hỗ trợ pattern matching?
**Answer:**
- Có từ C# 7+.  
- Hỗ trợ type pattern, property pattern.  
- Mạnh mẽ và linh hoạt hơn switch truyền thống.

---

# 3. Hàm & Tham số

## 13. Pass by value vs ref/out?
**Answer:**
- Value: truyền bản sao.  
- ref: truyền tham chiếu đã khởi tạo.  
- out: truyền tham chiếu, bắt buộc gán trong hàm.

---

## 14. Overload là gì?
**Answer:**
- Cùng tên hàm nhưng khác tham số.  
- Quyết định tại compile-time.  
- Giúp API linh hoạt.

---

## 15. Optional parameters là gì?
**Answer:**
- Tham số có giá trị mặc định.  
- Giảm số overload không cần thiết.  
- Code gọn hơn.

---

# II. Câu hỏi OOP trong C# (rất quan trọng khi dùng Unity)

## 16. 4 tính chất OOP
**Answer:**
- Encapsulation: che giấu dữ liệu.  
- Inheritance: tái sử dụng logic.  
- Polymorphism: hành vi tùy thuộc object.  
- Abstraction: che chi tiết, chỉ lộ cần thiết.

---

## 17. virtual, override
**Answer:**
- virtual: method cho phép override.  
- override: ghi đè method cha.  
- Cơ chế polymorphism runtime.

---

## 18. Abstract class vs Interface?
**Answer:**
- Abstract: có code mẫu + abstract.  
- Interface: chỉ chứa định nghĩa hành vi.  
- Abstract phù hợp chia sẻ logic chung.

---

## 19. Khi nào dùng interface?
**Answer:**
- Khi cần hợp đồng chung cho nhiều class.  
- Khi cần DI, dễ test.  
- Giảm phụ thuộc giữa các module.

---

## 20. Từ khóa base dùng khi nào?
**Answer:**
- Gọi method cha hoặc constructor cha.  
- Tránh lặp code.  
- Quan trọng khi override.

---

## 21. C# có hỗ trợ đa kế thừa?
**Answer:**
- Không cho class.  
- Cho phép implement nhiều interface.  
- Giữ thiết kế đơn giản và rõ ràng.

---

## 22. Compile-time vs Runtime Polymorphism?
**Answer:**
- Compile-time: overload.  
- Runtime: override qua virtual.  
- Tùy mục đích sử dụng.

---

## 23. Overload vs Override?
**Answer:**
- Overload: khác tham số.  
- Override: ghi đè logic class cha.  
- Hai khái niệm khác nhau.

---

## 24. Auto-property là gì?
**Answer:**
- Property có backing field tự động.  
- Code sạch, ít boilerplate.  
- Dùng khi không cần logic đặc biệt.

---

## 25. Getter/Setter?
**Answer:**
- Getter để lấy giá trị.  
- Setter để gán giá trị.  
- Kiểm soát truy cập dữ liệu.

---

## 26. private set là gì?
**Answer:**
- Bên ngoài chỉ đọc được.  
- Chỉ class nội bộ được phép gán.  
- Dùng cho tính bất biến.

---

## 27. Access modifiers
**Answer:**
- public: truy cập mọi nơi.  
- private: chỉ trong class.  
- protected: class và class con.  
- internal: trong cùng assembly.

---

# III. Câu hỏi nâng cao hơn (vẫn phù hợp Intern)

## 28. Class vs Struct?
**Answer:**
- Class: reference type, heap.  
- Struct: value type, stack.  
- Struct nhẹ, không tạo GC.

---

## 29. Khi nào dùng struct trong game?
**Answer:**
- Data nhỏ (Position, Velocity).  
- High-performance code.  
- Tránh allocation trong Update().

---

## 30. GC hoạt động thế nào?
**Answer:**
- Quét và thu hồi object không dùng nữa.  
- Chia generations để tối ưu.  
- Gây pause ngắn (GC spikes).

---

## 31. Hạn chế GC spikes trong Unity?
**Answer:**
- Tránh new object trong Update.  
- Dùng object pooling.  
- Tránh boxing, dùng struct khi hợp lý.

---

## 32. Tại sao string immutable?
**Answer:**
- An toàn, dễ cache và optimize.  
- Hỗ trợ hashing hiệu quả.  
- Tránh lỗi khi chia sẻ nhiều nơi.

---

## 33. Khi nào dùng try-catch?
**Answer:**
- Xử lý lỗi không mong muốn.  
- Không dùng trong loop hoặc Update.  
- Dùng ở boundary code (I/O, network).

---

## 34. finally dùng làm gì?
**Answer:**
- Luôn chạy dù có lỗi.  
- Dùng giải phóng tài nguyên.  
- Chống leak resource.

---

## 35. throw vs throw ex?
**Answer:**
- throw: giữ nguyên stack trace.  
- throw ex: mất trace → khó debug.  
- Nên dùng throw.

---

## 36. Generics là gì?
**Answer:**
- Code cho nhiều kiểu nhưng vẫn an toàn kiểu.  
- Tránh boxing/unboxing.  
- Rất phổ biến trong Unity.

---

## 37. Tại sao generics tối ưu hơn?
**Answer:**
- Tránh boxing → giảm GC.  
- Không cần cast.  
- An toàn kiểu & hiệu năng tốt.

---

## 38. Ví dụ List<T>, Dictionary<K,V>
**Answer:**
- List<T>: danh sách tuyến tính.  
- Dictionary<K,V>: lookup nhanh O(1).  
- Dùng nhiều cho game data.

---

## 39. Delegate là gì?
**Answer:**
- Là biến trỏ tới hàm.  
- Nền tảng của event.  
- Tạo cơ chế callback.

---

## 40. Event khác delegate?
**Answer:**
- Event đóng gói delegate.  
- Chỉ publisher mới raise event.  
- An toàn và tránh lạm dụng.

---

## 41. Action & Func
**Answer:**
- Action: hàm không trả về.  
- Func: hàm có trả về.  
- Cú pháp gọn gàng.

---

## 42. Anonymous function là gì?
**Answer:**
- Hàm không tên.  
- Dùng với delegate/Event.  
- Giảm code lặp.

---

## 43. Lambda expression là gì?
**Answer:**
- Cú pháp ngắn gọn của anonymous function.  
- Rất mạnh trong LINQ.  
- Code dễ đọc hơn.

---

# IV. LINQ (C# cực hay dùng trong xử lý data game)

## 44. LINQ là gì?
**Answer:**
- Thư viện truy vấn dữ liệu dạng SQL-like.  
- Hỗ trợ filter/map/sort.  
- Code sạch và dễ bảo trì.

---

## 45. Select, Where, OrderBy?
**Answer:**
- Select: chuyển đổi dữ liệu.  
- Where: lọc dữ liệu.  
- OrderBy: sắp xếp.

---

## 46. IEnumerable vs List
**Answer:**
- IEnumerable: lazy, duyệt tuần tự.  
- List: chứa đầy đủ dữ liệu, truy cập nhanh.  
- IEnumerable tiết kiệm memory.

---

## 47. Deferred execution là gì?
**Answer:**
- Query chỉ chạy khi được duyệt.  
- Linh hoạt và tối ưu hiệu năng.  
- Tránh tính toán không cần thiết.

---

# V. Liên quan đến C# trong Unity

## 48. Awake(), Start(), Update()
**Answer:**
- Awake: khởi tạo object.  
- Start: chạy khi object active.  
- Update: chạy mỗi frame.

---

## 49. Update vs FixedUpdate vs LateUpdate
**Answer:**
- Update: logic per-frame.  
- FixedUpdate: vật lý (timestep cố định).  
- LateUpdate: chạy sau Update, ổn định camera.

---

## 50. Tại sao MonoBehaviour cần thiết?
**Answer:**
- Giúp script gắn vào GameObject.  
- Cho phép Unity quản lý lifecycle.  
- Hỗ trợ coroutine, event Unity.

---

## 51. Unity Serializable là gì?
**Answer:**
- Cho phép hiển thị và lưu dữ liệu trong Inspector.  
- Hữu ích cho config/game data.  
- Dùng cho class và struct.

---

## 52. [SerializeField] dùng làm gì?
**Answer:**
- Expose biến private lên Inspector.  
- Đảm bảo encapsulation.  
- Tránh lộ API không cần thiết.

---

## 53. Coroutine là gì?
**Answer:**
- Hàm chạy qua nhiều frame.  
- Không block game loop.  
- Rất hữu dụng cho hiệu ứng, delay.

---

## 54. Khi nào dùng coroutine?
**Answer:**
- Timer, animations, vfx.  
- Chờ sự kiện hoặc thời gian.  
- Tránh nhét logic delay vào Update.

---

## 55. yield return null?
**Answer:**
- Chờ đến frame tiếp theo.  
- Tạm dừng coroutine mà không block game.  
- Dùng cho hiệu ứng theo frame.

---

## 56. yield return new WaitForSeconds()
**Answer:**
- Tạm dừng trong X giây.  
- Không block CPU.  
- Dùng cho cooldown, delay, animations.

---

## 57. ScriptableObject là gì?
**Answer:**
- Asset dùng để chứa data tách khỏi scene.  
- Không phụ thuộc GameObject.  
- Tối ưu memory và workflow.

---

## 58. Khi nào dùng ScriptableObject?
**Answer:**
- Config game, item database, player stats.  
- Dùng chung nhiều scene.  
- Dễ share & maintain data.

---

## 59. Tại sao tránh new object trong Update()?
**Answer:**
- Tạo GC liên tục → tụt FPS.  
- Không phù hợp trong game loop.  
- Nên pooling hoặc reuse.

---

## 60. Khi nào dùng struct thay class?
**Answer:**
- Dữ liệu nhỏ, bất biến.  
- Performance-critical code.  
- Tránh allocation heap.

---

## 61. Object Pooling là gì?
**Answer:**
- Tái sử dụng object thay vì tạo/hủy liên tục.  
- Giảm load GC.  
- Cực kỳ quan trọng cho game tốc độ cao.

---
