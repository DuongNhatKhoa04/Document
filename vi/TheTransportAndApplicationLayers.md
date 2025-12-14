# Tầng Giao vận và Ứng dụng (The Transport and Application Layers)

**Transport layer** và **Application layer** nằm ở trên cùng của mô hình TCP/IP.  
Cùng nhau, chúng biến việc chuyển giao gói tin nỗ lực tốt nhất (best-effort) từ tầng mạng thành các **dịch vụ hướng người dùng tin cậy** như duyệt web, email, và truyền tệp.

Chương này giải thích cách tầng giao vận cung cấp giao tiếp đầu-cuối và cách tầng ứng dụng sử dụng các dịch vụ đó, với cái nhìn cuối cùng về tất cả các tầng làm việc cùng nhau.

---

## 1. Tầng Giao vận (The Transport Layer)

**Transport layer** chịu trách nhiệm cho **giao tiếp đầu-cuối (end-to-end)** giữa các ứng dụng chạy trên các máy chủ khác nhau.

Các trách nhiệm chính:

- **Multiplexing và demultiplexing** – sử dụng **ports (cổng)** để cho phép nhiều ứng dụng chia sẻ một địa chỉ IP duy nhất.
- **Reliability (khi cần thiết)** – đảm bảo dữ liệu được chuyển giao mà không bị mất, trùng lặp, hoặc sai thứ tự.
- **Flow control (Kiểm soát luồng)** – ngăn chặn người gửi nhanh làm tràn ngập người nhận chậm.
- **Congestion control (Kiểm soát tắc nghẽn)** – phản ứng với tắc nghẽn bên trong mạng.
- **Segmentation và reassembly** – chia các thông điệp lớn thành các segments nhỏ hơn và lắp ráp lại chúng tại đích.

Hai giao thức giao vận chủ đạo là:

- **TCP (Transmission Control Protocol)** – hướng kết nối (connection-oriented), tin cậy.
- **UDP (User Datagram Protocol)** – không kết nối (connectionless), nỗ lực tốt nhất (best-effort).

---

## 2. Mổ xẻ một TCP Segment

Một **TCP segment** đóng gói dữ liệu ứng dụng với một TCP header.  
Ở cấp độ cao, các trường quan trọng bao gồm:

- **Source port** và **destination port** – xác định ứng dụng gửi và nhận.
- **Sequence number** – xác định vị trí của segment này trong luồng byte.
- **Acknowledgment number** – xác nhận việc nhận dữ liệu từ phía bên kia.
- **Data offset** – độ dài của TCP header.
- **Flags (control bits)** – quản lý thiết lập kết nối, ngắt kết nối, và độ tin cậy (SYN, ACK, FIN, RST, PSH, URG, v.v.).
- **Window size** – cho người gửi biết người nhận có thể chấp nhận bao nhiêu dữ liệu (kiểm soát luồng).
- **Checksum** – phát hiện lỗi cho header và payload.
- **Urgent pointer** (hiếm khi dùng) – làm nổi bật dữ liệu khẩn cấp.

TCP xử lý dữ liệu như một **luồng byte (byte stream)**, không phải là các thông điệp rời rạc. Số thứ tự và xác nhận đảm bảo tất cả các byte đến nơi và được lắp ráp lại theo đúng thứ tự.

---

## 3. Cờ điều khiển TCP và Bắt tay ba bước

### 3.1 Thiết lập kết nối – Bắt tay ba bước (Three-Way Handshake)

TCP là giao thức **hướng kết nối (connection-oriented)**. Trước khi truyền dữ liệu, cả hai bên thiết lập một kết nối sử dụng bắt tay ba bước:

1. **SYN** – Client gửi một segment với cờ SYN được bật và một **sequence number** khởi tạo.
2. **SYN-ACK** – Server trả lời bằng một segment có cả SYN và ACK được bật, xác nhận sequence number của client và gửi sequence number khởi tạo của chính nó.
3. **ACK** – Client xác nhận sequence number của server. Kết nối bây giờ đã được **thiết lập (established)**, và việc truyền dữ liệu có thể bắt đầu.

Quá trình này đảm bảo cả hai bên đồng ý về số thứ tự khởi tạo và sẵn sàng giao tiếp.

### 3.2 Ngắt kết nối (Connection Termination)

Ngắt kết nối thường là một trao đổi **bốn bước** sử dụng các cờ **FIN** và **ACK**:

1. Một bên gửi **FIN** để chỉ ra không còn dữ liệu để gửi.
2. Bên kia trả lời bằng **ACK**.
3. Khi bên thứ hai sẵn sàng đóng, nó gửi **FIN** của riêng mình.
4. Bên đầu tiên trả lời bằng **ACK** và cuối cùng chuyển sang trạng thái đóng hoàn toàn.

Việc tắt máy nhẹ nhàng này đảm bảo rằng tất cả dữ liệu đang truyền được chuyển giao trước khi kết nối kết thúc.

---

## 4. Gói tin TCP và UDP

### 4.1 TCP (Hướng kết nối, Tin cậy)

Đặc điểm:

- Thiết lập một **kết nối** với một cái bắt tay trước khi truyền dữ liệu.
- Sử dụng số thứ tự, xác nhận, và truyền lại để cung cấp **độ tin cậy**.
- Thực hiện **kiểm soát luồng** (window size) và **kiểm soát tắc nghẽn** (các thuật toán khác nhau).
- Phù hợp cho các ứng dụng nơi sự chính xác quan trọng hơn tốc độ, ví dụ:
  - Web (HTTP/HTTPS)
  - Email (SMTP, IMAP, POP3)
  - Truyền tệp (FTP, SFTP)
  - Truy cập từ xa (SSH)

### 4.2 UDP (Không kết nối, Nỗ lực tốt nhất)

Đặc điểm:

- **Không bắt tay**, không trạng thái kết nối, header tối thiểu.
- Không có độ tin cậy tích hợp, không sắp xếp thứ tự, hoặc kiểm soát tắc nghẽn.
- Overhead và độ trễ thấp hơn; ứng dụng xử lý bất kỳ độ tin cậy nào cần thiết.
- Các trường hợp sử dụng phổ biến:
  - Truyền thông thời gian thực (thoại, video, streaming)
  - Chơi game trực tuyến
  - Truy vấn DNS
  - Các giao thức yêu cầu/phản hồi nhẹ hoặc đơn giản

Trong thực tế, các nhà thiết kế ứng dụng chọn TCP hoặc UDP dựa trên sự đánh đổi giữa độ tin cậy và tốc độ.

---

## 5. Các trạng thái TCP Socket

Một **socket** là sự kết hợp của:

- IP cục bộ
- Cổng cục bộ
- IP từ xa
- Cổng từ xa

Các kết nối TCP di chuyển qua một loạt các **trạng thái (states)** khi chúng được tạo và ngắt.  
Một số trạng thái chính (góc nhìn khái niệm):

- **LISTEN** – Server đang chờ các kết nối đến trên một cổng cụ thể.
- **SYN-SENT** – Client đã gửi SYN và đang chờ SYN-ACK.
- **SYN-RECEIVED** – Server đã nhận SYN và gửi SYN-ACK.
- **ESTABLISHED** – Kết nối đã mở; dữ liệu có thể chảy theo cả hai hướng.
- **FIN-WAIT / CLOSE-WAIT / LAST-ACK** – Các trạng thái khác nhau quản lý việc tắt máy có trật tự.
- **TIME-WAIT** – Sau khi đóng, một bên chờ để đảm bảo các gói tin đến muộn bị loại bỏ.
- **CLOSED** – Không có kết nối hoạt động.

Hiểu các trạng thái socket là cần thiết để chẩn đoán các vấn đề như kết nối bị kẹt, cạn kiệt tài nguyên, hoặc cấu hình sai tường lửa.

---

## 6. Giao thức Hướng kết nối vs Không kết nối

Các giao thức giao vận có thể được nhóm thành hai loại khái niệm:

### 6.1 Hướng kết nối (Connection-Oriented) (ví dụ: TCP)

- Yêu cầu một **cái bắt tay** để thiết lập phiên.
- Duy trì **trạng thái** trên cả hai đầu (số thứ tự, kích thước cửa sổ, v.v.).
- Đảm bảo chuyển giao dữ liệu tin cậy, đúng thứ tự, hoặc báo lỗi rõ ràng nếu không đạt được.
- Overhead cao hơn, nhưng hành vi dễ dự đoán và mạnh mẽ.

### 6.2 Không kết nối (Connectionless) (ví dụ: UDP)

- Không thiết lập hoặc ngắt kết nối chính thức.
- Các đầu cuối **không** theo dõi trạng thái kết nối; mỗi gói tin là độc lập.
- Việc chuyển giao không được đảm bảo; gói tin có thể bị mất, trùng lặp, hoặc đến sai thứ tự.
- Overhead và độ trễ thấp, lý tưởng cho dữ liệu nhạy cảm về thời gian nơi sự mất mát nhỏ có thể chấp nhận được.

Sự lựa chọn giữa các mô hình này phụ thuộc vào nhu cầu của ứng dụng:  
chúng ta coi trọng **độ tin cậy** hơn, hay **tốc độ và sự đơn giản**?

---

## 7. Ports: System vs Ephemeral

Các cổng cho phép một máy chủ duy nhất chạy nhiều ứng dụng mạng cùng lúc.

### 7.1 Dải cổng (Cấp độ cao)

Theo truyền thống, số cổng được nhóm lại như sau:

- **Well-known / system ports** (0–1023)  
  - Dành riêng cho các dịch vụ và giao thức cốt lõi.  
  - Ví dụ: HTTP 80, HTTPS 443, SSH 22, DNS 53.

- **Registered ports** (1024–49151)  
  - Được gán cho các ứng dụng của người dùng hoặc nhà cung cấp.  
  - Ví dụ: MySQL 3306, RDP 3389.

- **Dynamic / ephemeral ports** (49152–65535, hoặc dải tương tự tùy OS)  
  - Được sử dụng tạm thời bởi các ứng dụng client khi khởi tạo kết nối.
  - Được cấp phát tự động bởi hệ điều hành khi các kết nối đi mới được tạo.

### 7.2 Cách sử dụng Cổng

Khi một client kết nối đến một server:

- **Server** lắng nghe trên một **system hoặc registered port** đã biết.
- **Client** sử dụng một **ephemeral port** tạm thời làm nguồn.
- Cùng nhau, bộ tuple (IP nguồn, cổng nguồn, IP đích, cổng đích, giao thức) định danh duy nhất kết nối đó.

---

## 8. Firewalls (Tường lửa)

**Firewall** là một thiết bị hoặc phần mềm bảo mật kiểm soát lưu lượng dựa trên các quy tắc đã cấu hình.

### 8.1 Lọc gói tin cơ bản (Basic Packet Filtering)

Ở mức độ đơn giản, một tường lửa có thể cho phép hoặc từ chối các gói tin dựa trên:

- Địa chỉ IP nguồn và đích.
- Cổng nguồn và đích.
- Giao thức (TCP, UDP, ICMP, v.v.).
- Giao diện hoặc hướng (vào vs ra).

Ví dụ: "Cho phép TCP port 443 từ Internet đến server này; chặn tất cả các cổng đến khác."

### 8.2 Kiểm tra trạng thái (Stateful Inspection)

Tường lửa hiện đại thường là **stateful**:

- Chúng theo dõi các kết nối đang hoạt động và chỉ cho phép các gói tin thuộc về một **phiên hợp lệ, đã thiết lập**.
- Ví dụ, chúng có thể tự động cho phép lưu lượng trả về cho một kết nối đi được khởi tạo từ mạng nội bộ, ngay cả khi lưu lượng vào trên cổng đó bị chặn.

Tường lửa là một điểm kiểm soát quan trọng để thực thi các chính sách bảo mật và bảo vệ ứng dụng khỏi truy cập trái phép.

---

## 9. Tầng Ứng dụng (The Application Layer)

**Application layer** là nơi các dịch vụ mạng hướng người dùng tồn tại.  
Nó bao gồm tất cả các giao thức mà ứng dụng sử dụng để giao tiếp qua mạng.

Ví dụ:

- **Web** – HTTP, HTTPS
- **Email** – SMTP, IMAP, POP3
- **Phân giải tên** – DNS
- **Dịch vụ tệp** – FTP, SFTP, SMB
- **Truy cập từ xa** – SSH, RDP

Trách nhiệm của tầng ứng dụng:

- Định nghĩa **định dạng thông điệp** và **lệnh** được sử dụng bởi các ứng dụng.
- Xử lý **xác thực**, **phiên**, và **biểu diễn dữ liệu** (ví dụ: JSON, XML, HTML).
- Cung cấp giao diện rõ ràng giữa các dịch vụ mạng và người dùng hoặc logic ứng dụng.

### 9.1 Tầng Ứng dụng và Mô hình OSI

Trong mô hình OSI, chức năng cấp ứng dụng được trải rộng qua ba tầng:

- **Application layer** – các dịch vụ hỗ trợ trực tiếp cho ứng dụng (ví dụ: HTTP, SMTP).
- **Presentation layer** – dịch dữ liệu, mã hóa, nén.
- **Session layer** – quản lý phiên, bao gồm thiết lập, quản lý, và ngắt.

Trong mô hình TCP/IP, các trách nhiệm này được gộp vào một **Application layer duy nhất**.
Mặc dù có sự khác biệt này, các mục tiêu khái niệm là giống nhau: chuyển giao dữ liệu ở dạng có ý nghĩa cho người dùng và quản lý các phiên giữa các điểm cuối giao tiếp.

---

## 10. Tất cả các Tầng hoạt động đồng bộ

Khi bạn truy cập một trang web, tất cả các tầng của mô hình TCP/IP hợp tác với nhau:

1. **Application Layer** - Trình duyệt của bạn sử dụng HTTP hoặc HTTPS để yêu cầu một trang từ web server.

2. **Transport Layer** - Trình duyệt mở một **kết nối TCP** đến địa chỉ IP của server trên cổng 80 hoặc 443.  
   - Bắt tay ba bước thiết lập kết nối, sau đó các thông điệp HTTP được trao đổi dưới dạng các TCP segments.

3. **Network Layer** - Mỗi TCP segment được đóng gói trong một **IP datagram** với địa chỉ IP nguồn và đích.  
   - Router chuyển tiếp các datagrams qua Internet dựa trên bảng định tuyến.

4. **Data Link Layer** - Trên mỗi liên kết vật lý, IP datagram được đóng gói trong một frame (ví dụ: Ethernet), sử dụng địa chỉ MAC để chuyển giao cục bộ.

5. **Physical Layer** - Các frames được chuyển đổi thành tín hiệu điện, quang, hoặc vô tuyến và truyền qua cáp hoặc môi trường không dây.

Tại đầu nhận, mỗi tầng thực hiện các thao tác ngược lại cho đến khi ứng dụng trên server nhìn thấy yêu cầu HTTP gốc. Phản hồi sau đó di chuyển ngược lại qua ngăn xếp đến trình duyệt của bạn.

---

## 11. Tóm tắt

Trong chương này bạn đã học cách tầng giao vận và ứng dụng hoàn thiện ngăn xếp mạng:

- **Transport layer** (TCP và UDP) cung cấp giao tiếp đầu-cuối giữa các ứng dụng, xử lý cổng, độ tin cậy, kiểm soát luồng, và kiểm soát tắc nghẽn.
- **TCP segments** chứa số thứ tự, xác nhận, và cờ điều khiển; **bắt tay ba bước** thiết lập kết nối tin cậy, và các trạng thái TCP socket mô tả vòng đời kết nối.
- Các giao thức **Connection-oriented** như TCP và **connectionless** như UDP cung cấp sự đánh đổi khác nhau giữa độ tin cậy và tốc độ.
- **Ports** phân biệt giữa nhiều ứng dụng trên cùng một máy chủ; các cổng well-known, registered, và ephemeral đều có vai trò cụ thể.
- **Firewalls** thực thi các chính sách bảo mật bằng cách kiểm tra tiêu đề gói tin và trạng thái kết nối.
- **Application layer** chứa các giao thức như HTTP, DNS, và SMTP, cung cấp giao diện giữa mạng và ứng dụng người dùng.
- Khi bạn truy cập bất kỳ dịch vụ mạng nào, tất cả các tầng—từ ứng dụng xuống vật lý—làm việc cùng nhau để chuyển giao dữ liệu một cách tin cậy và hiệu quả.

Các khái niệm này chuẩn bị cho bạn các chương tiếp theo về **các dịch vụ mạng**, **kết nối Internet**, và **xử lý sự cố**, nơi bạn sẽ thấy các giao thức này được triển khai và quản lý như thế nào trong môi trường thực tế.