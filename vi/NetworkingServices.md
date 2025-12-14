# Các dịch vụ Mạng (Networking Services)

Bên trên các giao thức giao vận và mạng cốt lõi, các mạng trong thế giới thực dựa vào một tập hợp các **dịch vụ mạng (networking services)**. Các dịch vụ này làm cho Internet trở nên hữu dụng, có khả năng mở rộng và an toàn hơn.

Chương này bao gồm những dịch vụ quan trọng nhất:

- **DNS** – chuyển đổi tên thành địa chỉ IP.
- **DHCP** – tự động gán cấu hình IP.
- **NAT** – mở rộng không gian địa chỉ IPv4.
- **VPNs và proxies** – thêm sự riêng tư, bảo mật và kiểm soát.

---

## 1. Phân giải tên và Hệ thống tên miền (DNS)

### 1.1 Tại sao chúng ta cần DNS?

Con người thích các **tên** như `www.example.com`.  
Tuy nhiên, router và máy chủ chuyển tiếp lưu lượng bằng **địa chỉ IP**.

**Hệ thống tên miền (DNS)** là cơ sở dữ liệu phân tán ánh xạ **tên miền** sang **địa chỉ IP** và các thông tin khác. Nếu không có DNS, người dùng sẽ phải nhớ các địa chỉ số, và việc thay đổi IP của một máy chủ sẽ làm hỏng cấu hình của mọi client.

DNS cung cấp:

- Một không gian tên phân cấp, toàn cầu (`example.com`, `sub.example.com`).
- Ánh xạ linh hoạt từ tên sang địa chỉ IPv4/IPv6.
- Các bản ghi bổ sung cho định tuyến email, khám phá dịch vụ, và hơn thế nữa.

### 1.2 Các bước của Phân giải tên

Khi bạn gõ một URL vào trình duyệt, một số thành phần hợp tác để phân giải tên đó:

1. **Application** kiểm tra bộ nhớ đệm của chính nó (browser cache).
2. **Operating system resolver** kiểm tra bộ nhớ đệm DNS cục bộ và cấu hình (ví dụ: `/etc/hosts`).
3. Nếu không tìm thấy, yêu cầu được gửi đến một **recursive resolver** (thường là máy chủ DNS do ISP hoặc tổ chức của bạn vận hành).
4. Recursive resolver có thể:
   - Trả lời từ bộ nhớ đệm của chính nó, hoặc
   - Thực hiện **truy vấn lặp (iterative queries)** thay cho bạn:
     - Hỏi một **root server** xem máy chủ **Top-Level Domain (TLD)** nào cần liên hệ.
     - Hỏi máy chủ TLD (ví dụ: `.com`) xem **authoritative server** nào xử lý `example.com`.
     - Hỏi authoritative server để lấy bản ghi cụ thể (ví dụ: `www.example.com`).
5. Câu trả lời được lưu trong bộ nhớ đệm ở mỗi bước trong một khoảng thời gian xác định (**Time To Live - TTL**) để giảm tải và tăng tốc độ cho các truy vấn trong tương lai.

Người dùng chỉ thấy một độ trễ ngắn trước khi trang web tải, nhưng bên dưới DNS thực hiện quy trình nhiều bước này một cách nhanh chóng và hiệu quả.

### 1.3 DNS và UDP

DNS thường sử dụng **UDP port 53** nhất:

- Overhead thấp của UDP là lý tưởng cho các thông điệp yêu cầu/phản hồi ngắn.
- Các thông điệp DNS nằm gọn trong một UDP datagram duy nhất trong trường hợp phổ biến.

Trong một số tình huống, DNS sử dụng **TCP**:

- Khi phản hồi quá lớn cho một gói tin UDP đơn lẻ (ví dụ: nhiều bản ghi).
- Cho các hoạt động cụ thể như **zone transfers** giữa các máy chủ DNS.

Từ góc độ ứng dụng, điều này là trong suốt; thư viện resolver xử lý các chi tiết giao vận.

---

## 2. DNS trong Thực tế

### 2.1 Các loại Bản ghi Tài nguyên (Resource Record Types)

Một DNS **zone** chứa các **bản ghi tài nguyên (Resource Records - RRs)**, mỗi bản ghi lưu trữ thông tin cụ thể.

Các loại bản ghi phổ biến (góc nhìn cấp cao):

- **A** – Ánh xạ tên sang địa chỉ IPv4.
- **AAAA** – Ánh xạ tên sang địa chỉ IPv6.
- **CNAME** – Canonical name; một bí danh trỏ tên này sang tên khác.
- **MX** – Mail exchanger; chỉ định máy chủ thư cho một tên miền.
- **NS** – Name server; xác định các máy chủ DNS có thẩm quyền cho một zone.
- **TXT** – Văn bản tự do; thường dùng cho xác minh và bảo mật (SPF, DKIM).
- **SRV** – Service locator; chỉ định máy chủ và cổng cho các dịch vụ cụ thể.

Client thường yêu cầu các bản ghi A/AAAA, nhưng quản trị viên làm việc với nhiều loại bản ghi để hỗ trợ email, xác thực và các dịch vụ nâng cao.

### 2.2 Giải phẫu một Tên miền

Một tên miền có tính **phân cấp**, đọc từ phải sang trái:

- `www.mail.example.com`
  - `.com` – **Top-Level Domain (TLD)**.
  - `example` – **Second-level domain**, được đăng ký cho một tổ chức.
  - `mail` – Subdomain được tạo bởi tổ chức đó.
  - `www` – Nhãn máy chủ hoặc dịch vụ.

Mỗi cấp độ đại diện cho quyền kiểm soát hành chính. Các tổ chức có thể tạo các subdomains để tổ chức các dịch vụ, địa điểm hoặc phòng ban (`eu.example.com`, `api.example.com`, v.v.).

### 2.3 DNS Zones

Một **zone** là một phần của không gian tên DNS được quản lý bởi một tổ chức hoặc quản trị viên cụ thể.

Các khái niệm chính:

- Một zone chứa các bản ghi cho một hoặc nhiều **domains**.
- **Authoritative DNS servers** lưu trữ dữ liệu zone và cung cấp các câu trả lời chính thức.
- Zones có thể được chia nhỏ hoặc ủy quyền (delegated):
  - `example.com` có thể được quản lý bởi một nhóm.
  - `us.example.com` có thể được ủy quyền cho một nhóm khác với các máy chủ riêng của họ.
- **Zone transfers** (AXFR/IXFR qua TCP) đồng bộ hóa dữ liệu giữa các máy chủ có thẩm quyền chính (primary) và phụ (secondary) để dự phòng.

Thiết kế phân tán này cho phép DNS mở rộng ra toàn bộ Internet trong khi vẫn cho phép kiểm soát cục bộ.

---

## 3. Dynamic Host Configuration Protocol (DHCP)

### 3.1 Tổng quan về DHCP

Việc gán thủ công địa chỉ IP và cài đặt cho mọi thiết bị là không khả thi khi mở rộng quy mô.  
**Dynamic Host Configuration Protocol (DHCP)** tự động hóa quy trình này.

DHCP có thể cung cấp:

- Địa chỉ IP và subnet mask.
- Default gateway.
- DNS servers.
- Các tùy chọn khác (NTP servers, tên miền, v.v.).

### 3.2 DHCP trong Hoạt động (Quy trình DORA khái niệm)

Khi một client tham gia mạng và cần cấu hình IP, một trình tự điển hình là:

1. **Discover** – Client phát quảng bá thông điệp DHCPDISCOVER để tìm các máy chủ DHCP khả dụng.
2. **Offer** – Một hoặc nhiều server phản hồi bằng DHCPOFFER, đề xuất một địa chỉ IP và cấu hình.
3. **Request** – Client chọn một lời đề nghị và gửi DHCPREQUEST, cho biết lựa chọn của nó.
4. **Acknowledge** – Server được chọn gửi DHCPACK, xác nhận việc cho thuê.

Các ý tưởng chính:

- Địa chỉ được cho thuê trong một **thời gian thuê (lease time)** có thể cấu hình và có thể được gia hạn.
- DHCP có thể dành riêng các địa chỉ cố định cho các địa chỉ MAC cụ thể (“DHCP reservations”).
- DHCP thường được chuyển giao qua UDP (client port 68, server port 67).

DHCP đơn giản hóa triệt để cấu hình client và giúp tránh xung đột IP.

---

## 4. Network Address Translation (NAT)

### 4.1 Cơ bản về NAT

**Network Address Translation (NAT)** cho phép nhiều thiết bị nội bộ với **địa chỉ IP riêng (private IP addresses)** chia sẻ một số lượng nhỏ hơn các **địa chỉ IP công cộng (public IP addresses)**.

Tại router biên (thường gọi là NAT gateway):

- Các gói tin đi ra có **IP nguồn** được thay thế bằng IP công cộng của router.
- Router giữ một **bảng dịch (translation table)** để khớp lưu lượng trả về với đúng máy chủ nội bộ.

Lợi ích:

- Bảo tồn địa chỉ IPv4 khan hiếm.
- Ẩn cấu trúc địa chỉ nội bộ khỏi Internet công cộng (riêng tư và bảo mật cơ bản).
- Cho phép định địa chỉ nội bộ linh hoạt độc lập với việc gán của ISP.

### 4.2 NAT và Tầng Giao vận (PAT)

Hầu hết các mạng gia đình và doanh nghiệp nhỏ thực sự sử dụng **Port Address Translation (PAT)**, một dạng của NAT cũng dịch cả **transport ports**:

- Nhiều client nội bộ có thể chia sẻ một IP công cộng duy nhất.
- Thiết bị NAT viết lại:
  - IP nguồn và cổng nguồn cho các gói tin đi ra.
  - IP đích và cổng đích cho các phản hồi đi vào.
- Ánh xạ `(internal IP, internal port)` ↔ `(public IP, public port)` được lưu trong một bảng.

Hệ quả:

- Các kết nối đi ra (Outbound) thường hoạt động mà không cần cấu hình đặc biệt.
- Các kết nối **đi vào (Inbound)** (lưu lượng không mong muốn từ Internet) bị chặn trừ khi bạn thiết lập **port forwarding**, sử dụng các giao thức hỗ trợ NAT traversal, hoặc sử dụng VPN.

### 4.3 Cạn kiệt địa chỉ IPv4 (Bối cảnh cấp cao)

NAT trở nên phổ biến do **cạn kiệt địa chỉ IPv4**:

- IPv4 cung cấp khoảng 4.3 tỷ địa chỉ, không đủ cho mọi thiết bị trên Trái đất.
- Không gian địa chỉ riêng cộng với NAT kéo dài bể chứa khả dụng nhưng gây ra sự phức tạp và phá vỡ kết nối đầu-cuối nghiêm ngặt.
- **IPv6** được thiết kế để giải quyết vấn đề này lâu dài với không gian địa chỉ lớn hơn nhiều, nhưng NAT sẽ vẫn còn phù hợp trong nhiều năm trong quá trình chuyển đổi.

---

## 5. VPNs và Dịch vụ Proxy

### 5.1 Mạng riêng ảo (VPNs)

Một **Virtual Private Network (VPN)** tạo ra một **đường hầm mã hóa (encrypted tunnel)** qua một mạng công cộng hoặc không tin cậy.

Mục tiêu cấp cao:

- Cho phép người dùng từ xa truy cập an toàn vào các mạng riêng (mạng nội bộ doanh nghiệp, mạng gia đình).
- Bảo vệ dữ liệu khỏi bị nghe trộm trên các mạng không tin cậy (ví dụ: Wi-Fi công cộng).
- Đôi khi cung cấp một vị trí IP công cộng hiển thị khác vì lý do chính sách hoặc truy cập.

Các khái niệm:

- Các điểm cuối VPN đóng gói lưu lượng riêng (gói tin IP) bên trong các gói tin bên ngoài được mã hóa.
- Các công nghệ phổ biến: IPsec, SSL/TLS-based VPNs (ví dụ: OpenVPN, WireGuard).
- Khi đã kết nối, client thường hoạt động như thể nó đang ở vật lý trên mạng từ xa, sử dụng địa chỉ riêng và truy cập các dịch vụ nội bộ.

### 5.2 Dịch vụ Proxy

Một **proxy server** đóng vai trò trung gian cho các yêu cầu từ client đến các server khác.

Các loại (khái niệm):

- **Forward proxy** - Client gửi yêu cầu đến proxy; proxy lấy nội dung thay cho họ.  
  - Được sử dụng để lọc nội dung, bộ nhớ đệm, kiểm soát truy cập, hoặc ẩn IP của client khỏi đích đến.

- **Reverse proxy** - Đứng trước một hoặc nhiều server và nhận yêu cầu từ Internet.  
  - Thực hiện cân bằng tải, bộ nhớ đệm, chấm dứt TLS (TLS termination), và lọc bảo mật.  
  - Các client bên ngoài chỉ nhìn thấy địa chỉ của proxy, không thấy các server backend riêng lẻ.

Sự khác biệt so với VPN:

- Một VPN thường mang tất cả hoặc hầu hết lưu lượng mạng từ một thiết bị; một proxy thường chỉ xử lý các giao thức hoặc ứng dụng cụ thể (ví dụ: HTTP).
- VPN tạo ra các giao diện ảo và các tuyến đường; proxy hoạt động ở tầng ứng dụng.

---

## 6. Tóm tắt

Trong chương này, bạn đã khám phá các **dịch vụ mạng** nằm trên ngăn xếp giao thức cốt lõi:

- **DNS** phân giải tên thân thiện với con người thành địa chỉ IP và sử dụng các bản ghi tài nguyên, zones, và bộ nhớ đệm để mở rộng quy mô toàn cầu.
- **DHCP** tự động cung cấp cấu hình IP cho client, đơn giản hóa việc quản lý mạng.
- **NAT** (và PAT) mở rộng không gian địa chỉ IPv4 và thay đổi cách các kết nối đi qua Internet, đặc biệt ảnh hưởng đến lưu lượng đi vào và khả năng tiếp cận đầu-cuối.
- **VPNs** và **proxies** cung cấp các đường hầm an toàn, sự riêng tư, cân bằng tải, và kiểm soát.

Các dịch vụ này là cần thiết để vận hành các mạng thực tế.  
Các chương tiếp theo sẽ chỉ ra cách các thiết bị kết nối với Internet và cách xử lý sự cố trên toàn bộ ngăn xếp.