# Tầng Mạng (The Network Layer)

**Network layer** chịu trách nhiệm di chuyển các gói tin (packets) giữa các mạng khác nhau.
Trong khi tầng liên kết dữ liệu tập trung vào việc chuyển giao cục bộ trong một phân đoạn duy nhất, tầng mạng cho phép **giao tiếp đầu-cuối qua nhiều chặng**. Trên Internet, vai trò này chủ yếu được thực hiện bởi **Internet Protocol (IP)**.

---

## 1. Vai trò của Tầng Mạng

Ở cấp độ cao, tầng mạng cung cấp:

- **Logical addressing (Định địa chỉ logic)** – gán các địa chỉ IP để định danh máy chủ và mạng.
- **Routing (Định tuyến)** – chọn một đường đi qua các mạng được kết nối với nhau.
- **Forwarding (Chuyển tiếp)** – di chuyển các gói tin từ giao diện này sang giao diện khác dựa trên các quyết định định tuyến.
- **Fragmentation (Phân mảnh - cũ)** – chia nhỏ các gói tin khi chúng vượt quá đơn vị truyền tải tối đa (MTU) của một liên kết.

Các Router hoạt động chủ yếu ở tầng này. Chúng kiểm tra địa chỉ IP đích của một gói tin, tham khảo **bảng định tuyến (routing table)**, và chuyển tiếp gói tin đến gần đích hơn.

---

## 2. Địa chỉ IPv4

### 2.1 Cấu trúc Địa chỉ

Một **địa chỉ IPv4** là một giá trị 32-bit, thường được viết dưới dạng **thập phân có dấu chấm (dotted-decimal)**, chẳng hạn như `192.168.10.25`.

- 32 bits → bốn octet (mỗi octet 8 bit).
- Mỗi octet nằm trong khoảng 0–255.
- Về mặt khái niệm, một địa chỉ IP có hai phần:
  - **Network portion (Phần mạng)** – định danh mạng.
  - **Host portion (Phần máy chủ)** – định danh một thiết bị cụ thể trong mạng đó.

Ranh giới giữa mạng và máy chủ được xác định bởi một **subnet mask** hoặc **độ dài tiền tố (prefix length)** (ví dụ: `/24`).

### 2.2 Các lớp địa chỉ IPv4 (Góc nhìn lịch sử)

Ban đầu, các địa chỉ IPv4 được nhóm thành các **lớp (classes)** cố định:

- **Class A** – `0.0.0.0` đến `127.255.255.255` (mask mặc định `/8`).
- **Class B** – `128.0.0.0` đến `191.255.255.255` (mask mặc định `/16`).
- **Class C** – `192.0.0.0` đến `223.255.255.255` (mask mặc định `/24`).
- **Class D** – `224.0.0.0` đến `239.255.255.255` (multicast).
- **Class E** – `240.0.0.0` đến `255.255.255.255` (thử nghiệm).

Định địa chỉ theo lớp (Classful addressing) hầu như chỉ còn mang tính **lịch sử**. Các mạng hiện đại sử dụng **Classless Inter-Domain Routing (CIDR)**, cho phép độ dài tiền tố linh hoạt thay vì các lớp cố định. Tuy nhiên, việc hiểu về các lớp vẫn hữu ích khi đọc tài liệu cũ hoặc các mạng kế thừa.

---

## 3. IPv4 Datagram và Encapsulation

Đơn vị cơ bản tại tầng mạng là **IP datagram** (thường gọi là gói tin IP).

### 3.1 Encapsulation (Đóng gói)

Khi một ứng dụng gửi dữ liệu:

1. Dữ liệu được chuyển cho **Transport layer** (ví dụ: TCP hoặc UDP), tầng này thêm tiêu đề riêng của nó.
2. Segment kết quả được chuyển cho **Network layer**, tầng này đóng gói nó trong một tiêu đề IP, tạo thành một **IP datagram**.
3. Datagram sau đó được đóng gói trong một **Data link layer frame** (ví dụ: Ethernet frame) và truyền qua môi trường vật lý.

Mỗi router dọc đường đi sẽ mở gói (decapsulate) frame, kiểm tra **IP header** để xác định nơi gửi gói tin tiếp theo, và sau đó đóng gói lại (re-encapsulate) trong một frame mới cho liên kết tiếp theo.

### 3.2 Các trường chính trong IPv4 Header (Cấp độ cao)

Các trường quan trọng của IPv4 header bao gồm:

- **Source IP address** – nơi gói tin bắt nguồn.
- **Destination IP address** – nơi gói tin sẽ đến.
- **Time To Live (TTL)** – một bộ đếm giảm dần qua mỗi chặng (hop); khi nó về 0, gói tin bị loại bỏ. Điều này ngăn chặn các gói tin lưu thông mãi mãi.
- **Protocol** – chỉ định giao thức giao vận được đóng gói (ví dụ: TCP = 6, UDP = 17, ICMP).
- **Total Length** – kích thước của toàn bộ datagram.
- **Identification, Flags, Fragment Offset** – được sử dụng cho việc phân mảnh và lắp ráp lại khi một gói tin phải chia nhỏ qua các liên kết có MTU nhỏ hơn.
- **Header Checksum** – phát hiện lỗi cho chính IP header.

Các Router chủ yếu quan tâm đến các trường **địa chỉ đích**, **TTL**, và **protocol** trong quá trình chuyển tiếp.

---

## 4. Address Resolution Protocol (ARP)

Tại tầng mạng chúng ta sử dụng **địa chỉ IP**, nhưng tại tầng liên kết dữ liệu (Ethernet) chúng ta sử dụng **địa chỉ MAC**. **Address Resolution Protocol (ARP)** là cầu nối cho khoảng cách này.

- Khi một máy chủ muốn gửi gói tin đến một IP khác trên cùng mạng, nó phải biết **địa chỉ MAC đích**.
- Nếu nó chỉ biết IP, nó gửi một **ARP request** (broadcast) hỏi: "Ai có IP X.X.X.X? Hãy nói cho Y.Y.Y.Y biết."
- Máy chủ có IP đó trả lời bằng một **ARP reply** (unicast), cung cấp địa chỉ MAC của nó.
- Người gửi lưu trữ ánh xạ này trong một **bảng ARP (ARP table)** để sử dụng trong tương lai.

Router cũng sử dụng ARP để học địa chỉ MAC của các thiết bị lân cận trên các mạng được kết nối trực tiếp.

---

## 5. Subnetting và Subnet Masks

### 5.1 Tại sao phải Subnet?

**Subnetting** là quá trình chia một mạng IP lớn thành các mạng logic nhỏ hơn.

Lợi ích:

- Sử dụng tốt hơn không gian địa chỉ IPv4 hạn chế.
- Cải thiện hiệu suất và giảm lưu lượng broadcast.
- Tách biệt logic các phòng ban, vị trí, hoặc vùng bảo mật.
- Định tuyến rõ ràng hơn và xử lý sự cố dễ dàng hơn.

### 5.2 Subnet Masks và Độ dài Tiền tố

Một **subnet mask** là một số 32-bit chỉ ra phần nào của địa chỉ IP là phần mạng và phần nào là phần máy chủ.

- Viết dưới dạng thập phân có dấu chấm: ví dụ: `255.255.255.0`.
- Viết dưới dạng ký hiệu tiền tố: ví dụ: `/24`.
- Các bit được đặt là **1** đánh dấu **mạng**; các bit được đặt là **0** đánh dấu **máy chủ**.

Ví dụ:

- IP: `192.168.10.25`
- Mask: `255.255.255.0` → `/24`
- Mạng: `192.168.10.0`
- Phần máy chủ: 8 bit cuối cùng.

### 5.3 Toán nhị phân cơ bản (Khái niệm)

Các tính toán Subnetting dựa trên **nhị phân**:

- Mỗi octet là 8 bit, ví dụ: `255` = `11111111₂`, `0` = `00000000₂`.
- Mask là các số 1 liên tiếp theo sau là các số 0 (ví dụ: `/26` là `11111111.11111111.11111111.11000000`).
- Số lượng bit máy chủ xác định bao nhiêu địa chỉ IP có thể sử dụng trong một subnet:
  - `2^(host bits) − 2` (trừ đi địa chỉ mạng và địa chỉ quảng bá cho các subnet IPv4 truyền thống).

Bạn không cần thực hiện mọi phép tính bằng tay trong mạng thực tế, nhưng việc hiểu cấu trúc nhị phân giúp hành vi của CIDR và định tuyến trở nên rõ ràng hơn nhiều.

### 5.4 Classless Inter-Domain Routing (CIDR)

**CIDR** thay thế các ranh giới lớp bằng các tiền tố linh hoạt:

- Mạng được viết dưới dạng `<network address>/<prefix length>`, ví dụ: `10.0.0.0/8`, `192.168.10.0/24`, `172.16.0.0/16`.
- Cho phép các nhà cung cấp dịch vụ và doanh nghiệp phân bổ các khối địa chỉ phù hợp hơn với kích thước thực tế của họ.
- Cho phép **tổng hợp tuyến đường (route aggregation / supernetting)**, nơi nhiều mạng có thể được tóm tắt thành một tiền tố ngắn hơn duy nhất để giữ cho các bảng định tuyến nhỏ gọn.

CIDR là nền tảng cho định tuyến Internet có khả năng mở rộng.

---

## 6. Các nguyên tắc cơ bản về Định tuyến

### 6.1 Các khái niệm Định tuyến cơ bản

**Routing (Định tuyến)** là quá trình chọn một đường đi cho lưu lượng trong mạng, trong khi **Forwarding (Chuyển tiếp)** là hành động gửi các gói tin ra khỏi giao diện chính xác dựa trên đường đi đó.

Các ý tưởng chính:

- Mỗi router duy trì một **bảng định tuyến (routing table)**.
- Các tuyến đường thường bao gồm:
  - Mạng đích (trong ký hiệu CIDR).
  - Next hop (IP của router tiếp theo) hoặc giao diện đi ra.
  - Metric hoặc giá trị ưu tiên.
- Khi một gói tin đến, router thực hiện **khớp tiền tố dài nhất (longest prefix match)**:
  - Nó chọn tuyến đường có tiền tố khớp cụ thể nhất với IP đích.

Router có thể học các tuyến đường theo ba cách chính:

1. **Directly connected networks (Mạng kết nối trực tiếp)** – các giao diện được cấu hình với địa chỉ IP và mask.
2. **Static routes (Tuyến tĩnh)** – được cấu hình thủ công bởi quản trị viên.
3. **Dynamic routing protocols (Giao thức định tuyến động)** – router trao đổi thông tin tự động.

### 6.2 Bảng định tuyến

Một bảng định tuyến có thể chứa các mục như:

- Mạng kết nối trực tiếp: `192.168.10.0/24 via interface eth0`.
- Tuyến tĩnh: `10.0.0.0/8 via next hop 203.0.113.1`.
- Default route: `0.0.0.0/0 via ISP gateway`.

**Default route** đóng vai trò là "lưới hứng" cho các đích đến không được bao phủ bởi các mục cụ thể hơn và đặc biệt quan trọng trên các router biên và máy chủ đầu cuối.

### 6.3 Interior Gateway Protocols (IGPs)

Trong một tổ chức đơn lẻ hoặc **Hệ thống tự trị (Autonomous System - AS)**, các router thường sử dụng một **Interior Gateway Protocol (IGP)** để chia sẻ thông tin định tuyến.

Về mặt khái niệm, có hai họ chính:

- **Distance-vector protocols** - Router chia sẻ thông tin về "khoảng cách" đến các mạng (số hop hoặc metrics).  
  - Ví dụ kinh điển: RIP (Routing Information Protocol).

- **Link-state protocols** - Router xây dựng một bản đồ hoàn chỉnh về cấu trúc (topology) của mạng và tính toán đường đi tốt nhất bằng các thuật toán như đường đi ngắn nhất của Dijkstra.  
  - Ví dụ: OSPF (Open Shortest Path First), IS-IS.

Các IGP hướng tới sự **hội tụ nhanh (fast convergence)**, khả năng mở rộng bên trong tổ chức, và khả năng phục hồi.

### 6.4 Exterior Gateway Protocols, Autonomous Systems, và IANA

Trên Internet toàn cầu, các tổ chức khác nhau (ISP, doanh nghiệp lớn, nhà cung cấp nội dung) được đại diện như các **Autonomous Systems (AS)**. Để trao đổi các tuyến đường giữa các AS này, các mạng sử dụng một **Exterior Gateway Protocol (EGP)**.

- EGP chủ đạo là **BGP (Border Gateway Protocol)**.
- Mỗi AS có một **số AS (ASN)** duy nhất.
- Định tuyến giữa các AS xem xét các chính sách, mối quan hệ kinh doanh, và kỹ thuật lưu lượng, không chỉ là đường đi ngắn nhất.

Sự phối hợp toàn cầu của các khối địa chỉ IP và số AS được xử lý bởi **Internet Assigned Numbers Authority (IANA)** và các cơ quan đăng ký Internet khu vực. Điều này đảm bảo tính duy nhất và ngăn ngừa xung đột.

---

## 7. Không gian địa chỉ không định tuyến (Non-Routable Address Space)

Một số dải IPv4 nhất định là **không định tuyến được trên Internet công cộng** và được dành riêng cho các mục đích đặc biệt.

### 7.1 Dải địa chỉ riêng (RFC 1918)

Dành riêng cho các mạng nội bộ (private networks):

- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

Các địa chỉ này có thể được sử dụng tự do bên trong các tổ chức. Lưu lượng truy cập Internet thường được dịch qua **Network Address Translation (NAT)** tại biên mạng.

### 7.2 Các địa chỉ đặc biệt khác

- **Loopback** – `127.0.0.0/8` (thường là `127.0.0.1`) dùng để kiểm tra ngăn xếp mạng cục bộ.
- **Link-local** – `169.254.0.0/16` dùng để tự động định địa chỉ khi DHCP không khả dụng.
- **Broadcast** – `255.255.255.255` (quảng bá cục bộ) và địa chỉ quảng bá theo từng subnet.
- Nhiều dải dành riêng khác tồn tại cho tài liệu, thử nghiệm, và các mục đích đặc biệt khác.

Hiểu các dải này giúp tránh cấu hình sai và các vấn đề định tuyến.

---

## 8. Tiêu chuẩn và RFCs

Các giao thức Internet được ghi lại trong **Requests for Comments (RFCs)**, được duy trì bởi Internet Engineering Task Force (IETF).

- RFC mô tả các tiêu chuẩn, thực tiễn tốt nhất, và các ý tưởng thử nghiệm.
- Hành vi IPv4 cốt lõi, quy tắc định địa chỉ, và các giao thức định tuyến đều được định nghĩa trong các RFC cụ thể.
- Các kỹ sư mạng thường xuyên tham khảo RFC khi triển khai, gỡ lỗi, hoặc xác thực hành vi giao thức.

Mặc dù bạn không cần nhớ mọi RFC, điều quan trọng là phải biết rằng chúng là nguồn chính thức cho các thông số kỹ thuật giao thức.

---

## 9. Tóm tắt

Trong chương này, bạn đã học các khái niệm cấp cao xác định **Network layer**:

- IPv4 cung cấp **định địa chỉ logic** và tạo thành cơ sở của liên mạng toàn cầu.
- IP datagrams đóng gói các segment giao vận và được chuyển tiếp từng chặng qua các router.
- **ARP** phân giải địa chỉ IP thành địa chỉ MAC trên mạng cục bộ.
- **Subnetting**, **subnet masks**, và **CIDR** cho phép sử dụng linh hoạt, hiệu quả không gian IPv4.
- **Routing** sử dụng bảng định tuyến, tuyến tĩnh, và các giao thức động để di chuyển lưu lượng qua các cấu trúc mạng phức tạp.
- Các miền định tuyến riêng biệt (autonomous systems) trao đổi thông tin khả năng tiếp cận bằng BGP, trong khi mạng nội bộ sử dụng các IGP như OSPF hoặc RIP.
- Các dải địa chỉ **Private** và không định tuyến khác được dành riêng cho các mục đích đặc biệt và phải được xử lý cẩn thận tại biên mạng.
- Nền tảng cho tất cả những điều này, **RFCs** nắm giữ các tiêu chuẩn chính thức giúp Internet có khả năng tương tác.

Các khái niệm này cung cấp nền tảng cho chương tiếp theo, nơi bạn sẽ nghiên cứu **Transport layer và Application layer** và xem cách các ứng dụng xây dựng trên nền tảng IP để cung cấp các dịch vụ đầu-cuối.