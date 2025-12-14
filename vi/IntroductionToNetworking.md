# Giới thiệu về Mạng (Introduction to Networking)

Mạng máy tính cho phép máy tính và các thiết bị khác chia sẻ dữ liệu, dịch vụ và tài nguyên.  
Chương đầu tiên này cung cấp cho bạn cái nhìn tổng quan về cách các mạng hiện đại được cấu trúc, những thiết bị nào giúp chúng hoạt động và điều gì xảy ra với các bit khi chúng di chuyển trên dây dẫn.

---

## Mục tiêu học tập

Sau khi học chương này, bạn sẽ có thể:

- Giải thích mục đích của các mô hình mạng và tại sao chúng ta sử dụng các tầng (layers).
- Mô tả **Mô hình 5 tầng TCP/IP** và **Mô hình 7 tầng OSI**.
- Nhận diện các thiết bị mạng phổ biến: cáp, hub, switch, router, server và client.
- Mô tả những gì xảy ra tại **Physical layer** (Tầng vật lý) và **Data link layer** (Tầng liên kết dữ liệu) của một mạng.
- Nhận biết vai trò của địa chỉ MAC và Ethernet frames trong giao tiếp cục bộ.

---

## 1. Các mô hình Mạng (Network Models)

### 1.1 Tại sao phải sử dụng các tầng?

Mạng trong thế giới thực rất phức tạp. Để quản lý sự phức tạp này, mạng được mô tả bằng cách sử dụng các **mô hình phân tầng (layered models)**. Mỗi tầng có một trách nhiệm rõ ràng và chỉ tương tác với tầng ngay phía trên và bên dưới nó. Điều này mang lại một số lợi ích:

- Dễ dàng thiết kế và xử lý sự cố (troubleshooting).
- Khả năng thay thế hoặc nâng cấp một tầng mà không cần thiết kế lại các tầng khác.
- Một ngôn ngữ chung cho các nhà cung cấp, kỹ sư và các tổ chức tiêu chuẩn.

Hai mô hình đặc biệt quan trọng là: **Mô hình 5 tầng TCP/IP** và **Mô hình 7 tầng OSI**.

### 1.2 Mô hình mạng 5 tầng TCP/IP

Mô hình TCP/IP là mô hình thực tế phù hợp nhất với cách Internet hoạt động ngày nay.
Từ dưới lên trên, 5 tầng bao gồm:

1. **Physical layer (Tầng vật lý)** - Xử lý việc truyền tải thực tế các bit qua môi trường truyền dẫn (đồng, quang, vô tuyến, v.v.).  
   - Định nghĩa các mức điện áp, thời gian, đầu nối và phương pháp tín hiệu.

2. **Data link layer (Tầng liên kết dữ liệu)** - Cung cấp việc chuyển giao giữa các nút (node-to-node) trên một phân đoạn mạng vật lý duy nhất.  
   - Sử dụng địa chỉ MAC và frames; xử lý việc truy cập vào môi trường truyền dẫn và phát hiện lỗi cơ bản.

3. **Network layer (Tầng mạng)** - Cung cấp định địa chỉ logic (logical addressing) và định tuyến (routing) giữa các mạng.  
   - Sử dụng địa chỉ IP và các giao thức định tuyến để di chuyển các gói tin (packets) qua nhiều chặng (hops).

4. **Transport layer (Tầng giao vận)** - Cung cấp giao tiếp đầu-cuối (end-to-end) giữa các ứng dụng trên các máy chủ khác nhau.  
   - Triển khai các khái niệm như cổng (ports), kết nối, độ tin cậy (TCP), hoặc chuyển giao nỗ lực tốt nhất (UDP).

5. **Application layer (Tầng ứng dụng)** - Bao gồm tất cả các giao thức và dịch vụ mà ứng dụng sử dụng trực tiếp: HTTP, DNS, SMTP, v.v.  
   - Chịu trách nhiệm trình bày dữ liệu dưới dạng mà người dùng và ứng dụng hiểu được.

Khi dữ liệu di chuyển xuống ngăn xếp (stack) ở phía người gửi, mỗi tầng sẽ thêm tiêu đề (header) của riêng nó (gọi là **encapsulation** - đóng gói).
Ở phía người nhận, các tiêu đề được loại bỏ theo thứ tự ngược lại (gọi là **decapsulation** - mở gói).

### 1.3 Mô hình mạng OSI

**Mô hình OSI (Open Systems Interconnection)** là một mô hình khái niệm chi tiết hơn với **bảy** tầng:

1. Physical  
2. Data Link  
3. Network  
4. Transport  
5. Session  
6. Presentation  
7. Application  

Ba tầng trên cùng (Session, Presentation, Application) mô tả cách các ứng dụng thiết lập, quản lý và định dạng các phiên giao tiếp. Trong thực tế, nhiều trách nhiệm của chúng được gộp lại trong tầng Application của mô hình TCP/IP, nhưng mô hình OSI vẫn rất hữu ích cho việc giảng dạy và xử lý sự cố vì nó cung cấp một khung làm việc rõ ràng, chi tiết.

### 1.4 So sánh TCP/IP và OSI

- Cả hai mô hình đều bắt đầu với các tầng **Physical**, **Data Link**, **Network**, và **Transport** khá tương đồng nhau.
- Mô hình OSI chia các mối quan tâm cấp ứng dụng thành ba tầng (Session, Presentation, Application), trong khi mô hình TCP/IP gộp chúng thành một tầng **Application** duy nhất.
- Khi xử lý sự cố, các kỹ sư thường nói những câu như "đây là vấn đề Layer 2" hoặc "đây có vẻ là vấn đề Layer 3", ám chỉ các tầng của OSI như một cách gọi tắt.

---

## 2. Các thiết bị Mạng cơ bản

Mạng hiện đại dựa vào sự kết hợp của các phương tiện vật lý và các thiết bị tích cực. Ở cấp độ cao, bạn sẽ gặp các khối xây dựng sau.

### 2.1 Cáp (Cables)

**Cáp** cung cấp đường dẫn vật lý mà các bit di chuyển qua.

- **Cáp đồng xoắn đôi (Twisted-pair copper)** (ví dụ: Cat5e, Cat6) được sử dụng rộng rãi cho Ethernet trong mạng cục bộ.  
  Các cặp dây được xoắn lại để giảm nhiễu điện từ.  
- **Cáp quang (Fiber-optic cables)** sử dụng ánh sáng thay vì điện, cho phép tốc độ cao hơn nhiều và khoảng cách xa hơn.  
- Mỗi loại cáp có quy định về chiều dài tối đa và đặc tính hiệu suất; việc chọn đúng loại là rất quan trọng cho một mạng tin cậy.

### 2.2 Hub và Switch

- **Hub** là một thiết bị đơn giản, cũ kỹ, lặp lại các tín hiệu điện đầu vào ra tất cả các cổng khác. Nó hoạt động hoàn toàn ở **Physical layer**, tạo ra một miền xung đột (collision domain) duy nhất, và hiếm khi được sử dụng ngày nay do hiệu quả kém và khả năng mở rộng thấp.
- **Switch** là một thiết bị thông minh hơn hoạt động ở **Data link layer**. Nó:
  - Học các **địa chỉ MAC** và xây dựng một bảng chuyển tiếp (forwarding table).
  - Chỉ chuyển tiếp các frames đến đúng cổng thay vì phát quảng bá (broadcasting) đến tất cả các cổng.
  - Giảm đáng kể xung đột và cải thiện hiệu suất so với Hub.

Trong các mạng Ethernet hiện đại, Switch là cách tiêu chuẩn để kết nối các máy chủ trong cùng một LAN.

### 2.3 Routers

**Router** kết nối nhiều mạng lại với nhau và hoạt động chủ yếu ở **Network layer**.

- Sử dụng **địa chỉ IP** và bảng định tuyến (routing tables) để quyết định nơi gửi gói tin tiếp theo.
- Tách biệt các miền quảng bá (broadcast domains), cung cấp lựa chọn đường đi, và thường triển khai tường lửa cơ bản, NAT, và các chức năng biên khác.
- "Wi-Fi routers" tại nhà thường kết hợp nhiều chức năng: router, switch, điểm truy cập không dây (wireless access point), và đôi khi là modem.

### 2.4 Servers và Clients

- **Server (Máy chủ)** là một máy cung cấp dịch vụ hoặc tài nguyên (trang web, tệp tin, cơ sở dữ liệu, xác thực, v.v.) cho các thiết bị khác trên mạng.
- **Client (Máy khách)** là một máy yêu cầu và tiêu thụ các dịch vụ này (trình duyệt web, ứng dụng email, ứng dụng di động, v.v.).
- Trong nhiều môi trường, một máy vật lý duy nhất có thể đóng vai trò vừa là client vừa là server, tùy thuộc vào vai trò của nó trong cuộc giao tiếp.

---

## 3. Tầng Vật lý (The Physical Layer)

**Physical layer** xoay quanh việc đưa các bit riêng lẻ từ thiết bị này sang thiết bị khác.

### 3.1 Di chuyển Bit qua môi trường truyền dẫn

- Dữ liệu được mã hóa thành tín hiệu điện, xung ánh sáng, hoặc sóng vô tuyến tùy thuộc vào môi trường.  
- Tầng vật lý định nghĩa cách biểu diễn các số 0 và 1 (line coding), thời gian bit (bit timing), và cách các thiết bị phát hiện xung đột hoặc lỗi liên kết.
- Việc truyền tải có thể là **simplex** (một chiều), **half-duplex** (hai chiều, nhưng không cùng lúc), hoặc **full-duplex** (hai chiều cùng lúc).

### 3.2 Cáp xoắn đôi và Duplexing

Cáp Ethernet xoắn đôi sử dụng nhiều cặp dây:

- Các cặp khác nhau xử lý tín hiệu gửi và nhận.  
- Cấu hình **duplex** thích hợp (half vs full) là cần thiết để tránh xung đột và các vấn đề hiệu suất.
- Các Switch và card mạng (NIC) hiện đại thường tự động đàm phán (auto-negotiate) tốc độ và duplex, nhưng sự không khớp vẫn có thể xảy ra trong các môi trường cấu hình sai.

### 3.3 Ethernet qua Cáp xoắn đôi và Cáp chéo (Crossover Cables)

- **Cáp thẳng (Straight-through cables)** kết nối các thiết bị khác loại (ví dụ: host với switch, switch với router) trong các tiêu chuẩn cũ, với dây truyền ở một bên khớp với dây nhận ở bên kia.
- **Cáp chéo (Crossover cables)** theo truyền thống được sử dụng để kết nối trực tiếp các thiết bị tương tự (switch-với-switch, host-với-host) bằng cách đảo ngược các cặp truyền và nhận.
- Ngày nay, hầu hết các giao diện hiện đại đều hỗ trợ **auto-MDI/MDI-X**, tự động điều chỉnh cho cả hai cấu hình, làm cho cáp chéo phần lớn không còn cần thiết nhưng vẫn quan trọng để hiểu về mặt lịch sử.

### 3.4 Cổng mạng và Patch Panels

- **Network ports** trên ổ cắm tường, switch và router cung cấp các điểm kết nối tiêu chuẩn cho cáp mạng.
- **Patch panels** tập hợp nhiều đường cáp vào một vị trí duy nhất, có tổ chức (ví dụ: một tủ rack). Các cáp nhảy ngắn (patch cables) kết nối các cổng trên panel với các cổng của switch.
- Việc dán nhãn và quản lý cáp đúng cách ở cấp độ này là rất quan trọng cho các mạng có khả năng mở rộng và bảo trì.

### 3.5 Công cụ làm cáp

Kỹ thuật viên mạng dựa vào một số công cụ tại tầng vật lý:

- **Kìm bấm cáp (Cable crimpers)** để gắn đầu nối (ví dụ: RJ-45) vào cáp đồng.
- **Kìm tuốt dây (Cable strippers)** để chuẩn bị vỏ cáp mà không làm hỏng các cặp dây bên trong.
- **Máy test cáp và chứng nhận (Cable testers and certifiers)** để xác minh sơ đồ chân (pin-out), tính liên tục và hiệu suất.
- **Tone generator and probe** để dò tìm đường đi của cáp trong môi trường phức tạp.

---

## 4. Tầng Liên kết dữ liệu (The Data Link Layer)

**Data link layer** nằm ngay phía trên tầng vật lý và chịu trách nhiệm chuyển giao tin cậy các frames giữa các nút trên cùng một phân đoạn mạng.

### 4.1 Ethernet và Địa chỉ MAC

Ethernet là công nghệ chủ đạo tại tầng liên kết dữ liệu trong các mạng LAN có dây.

- Mỗi card mạng (NIC) có một **MAC (Media Access Control) address**, thường là một giá trị 48-bit viết dưới dạng thập lục phân (ví dụ: `00:1A:2B:3C:4D:5E`).
- Địa chỉ MAC được sử dụng cho **nhận dạng cục bộ** trên một miền quảng bá đơn lẻ.
- Switch xây dựng một **bảng địa chỉ MAC (MAC address table)** ánh xạ các địa chỉ MAC tới các cổng cụ thể của switch, cho phép chúng chuyển tiếp frames một cách hiệu quả.

### 4.2 Unicast, Multicast, và Broadcast

Ethernet hỗ trợ ba loại chuyển giao frame cơ bản:

- **Unicast** - Giao tiếp một-một.  
  - Frame được gửi đến một địa chỉ MAC đích duy nhất; switch chỉ chuyển tiếp nó đến đúng cổng.

- **Multicast** - Giao tiếp một-nhiều.  
  - Frame được gửi đến một địa chỉ MAC multicast đặc biệt; các máy chủ đã tham gia nhóm multicast sẽ xử lý frame, những máy khác sẽ bỏ qua.

- **Broadcast** - Giao tiếp một-tất cả trên mạng cục bộ.  
  - Địa chỉ MAC đích là địa chỉ quảng bá (`FF:FF:FF:FF:FF:FF`); tất cả các máy chủ trên LAN đều nhận và xử lý frame.  
  - Broadcast là cần thiết cho một số giao thức (ví dụ: ARP) nhưng phải được hạn chế vì lưu lượng broadcast quá mức có thể làm giảm hiệu suất.

### 4.3 Mổ xẻ một Ethernet Frame

Một **Ethernet frame** bao bọc dữ liệu của tầng trên với thông tin của tầng liên kết dữ liệu. Ở cấp độ cao, một frame chứa:

- **Destination MAC address (MAC đích)** - **Source MAC address (MAC nguồn)** - **EtherType / Length field** (chỉ định giao thức nào được đóng gói, chẳng hạn như IPv4 hoặc IPv6)  
- **Payload** (gói tin tầng mạng và bất kỳ dữ liệu tầng cao hơn nào)  
- **Frame Check Sequence (FCS)** để phát hiện lỗi

Tại tầng này, Ethernet cung cấp:

- **Framing** – điểm bắt đầu và kết thúc rõ ràng của mỗi đơn vị dữ liệu.  
- **Local delivery** – di chuyển các frames từ NIC này sang NIC khác trên cùng một phân đoạn mạng.  
- **Error detection** – các frames bị hỏng được phát hiện và loại bỏ.

---

## 5. Tóm tắt

Chương mở đầu này đã thiết lập nền tảng cho phần còn lại của các ghi chú mạng của bạn:

- Chúng ta sử dụng **các mô hình mạng phân tầng** để quản lý sự phức tạp và chuẩn hóa giao tiếp.
- **Mô hình 5 tầng TCP/IP** là mô hình thực tế của Internet, trong khi **Mô hình 7 tầng OSI** là một tài liệu tham khảo khái niệm chi tiết hơn.
- Các thiết bị mạng cơ bản—**cáp, hub, switch, router, server, và client**—làm việc cùng nhau để di chuyển dữ liệu và cung cấp dịch vụ.
- Tại **Physical layer**, các bit thô di chuyển dưới dạng tín hiệu điện hoặc ánh sáng qua các phương tiện khác nhau, sử dụng cáp có cấu trúc và các công cụ chuyên dụng.
- Tại **Data link layer**, **Ethernet** sử dụng **địa chỉ MAC** và **frames** để cung cấp việc chuyển giao cục bộ tin cậy, sử dụng các mô hình giao tiếp unicast, multicast, và broadcast.

Trong chương tiếp theo, bạn sẽ đi sâu hơn vào **Network layer**, nơi địa chỉ IP và định tuyến cho phép giao tiếp qua nhiều mạng được kết nối với nhau.