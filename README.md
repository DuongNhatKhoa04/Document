# 🌐 Tóm Tắt Kiến Thức Mạng Máy Tính Cốt Lõi

Tài liệu này tổng hợp các khái niệm quan trọng nhất về mạng máy tính, từ các tầng vật lý đến các dịch vụ mạng và bảo mật, tập trung vào kiến thức thực tế để cấu hình do mình tổng hợp. Các bạn có thể đọc kỹ hơn trong các folder.

---

## 📚 Mục Lục
1. [Layer 1 & 2: Physical & Data Link](#1-layer-1--2-physical--data-link)
2. [Layer 3: Network](#2-layer-3-network)
3. [Layer 4: Transport](#3-layer-4-transport)
4. [Network Services (Dịch vụ Mạng)](#4-network-services-dịch-vụ-mạng)
5. [Connecting to Internet & Wireless](#5-connecting-to-internet--wireless)

---

## 1. Layer 1 & 2: Physical & Data Link

Tầng này chịu trách nhiệm truyền tải dữ liệu giữa các thiết bị trong cùng một mạng nội bộ (LAN).

* **Switch:** Kết nối các thiết bị trong cùng LAN.
    * Sử dụng **địa chỉ MAC** để chuyển gói tin đến đúng cổng cụ thể.
    * *Lưu ý:* Switch thông minh hơn Hub vì không chuyển tin tràn lan (trừ gói tin broadcast).
* **MAC (Media Access Control):**
    * Là định danh vật lý **48-bit hex** (ví dụ: `00:1A:2B:3C:4D:5E`).
    * Dùng để nhận dạng cục bộ trong một **broadcast domain**.
* **Router:**
    * Thiết bị Layer 3 nhưng có giao diện Layer 1/2.
    * Kết nối các mạng khác nhau (ngăn cách broadcast domain).
    * Dùng **địa chỉ IP** để định tuyến.
* **NIC (Network Interface Card):** Card mạng gắn trên thiết bị, chứa địa chỉ MAC duy nhất.

### 📡 Các phương thức giao tiếp
| Loại | Mô tả |
| :--- | :--- |
| **Unicast** | **1 - 1** (Gửi từ 1 nguồn đến 1 đích). |
| **Multicast** | **1 - Nhóm** (Gửi từ 1 nguồn đến 1 nhóm đăng ký). |
| **Broadcast** | **1 - Tất cả** (Gửi đến mọi thiết bị trong subnet). <br> MAC đích mặc định: `FF:FF:FF:FF:FF:FF`. |

---

## 2. Layer 3: Network

Chịu trách nhiệm định danh logic và định tuyến gói tin giữa các mạng khác nhau.

* **IPv4:** Địa chỉ 32-bit, gồm 4 octet (ví dụ: `192.168.1.1`).
* **Subnet Mask:** Dãy số 32-bit để phân chia phần **Network** (bit 1) và phần **Host** (bit 0).
* **CIDR (Classless Inter-Domain Routing):** Ký hiệu hiện đại thay thế Class cũ.
    * Ví dụ: `192.168.1.0/24` (thay vì nói Class C).
* **ARP (Address Resolution Protocol):** Giao thức ánh xạ IP sang MAC.
    * **Request:** Broadcast (Hỏi cả mạng "Ai giữ IP này?").
    * **Reply:** Unicast (Trả lời "Là tôi, MAC của tôi đây").
    * Dữ liệu được lưu trong **ARP Table** để cache.

### 🧮 Subnetting & Tính toán IP
> **Công thức tính số IP sử dụng được:**
> $$N = 2^{(host\_bit)} - 2$$

* **Tại sao trừ 2?**
    1.  **Network Address** (Host bit toàn 0): Dùng để định danh mạng (VD: `.0`).
    2.  **Broadcast Address** (Host bit toàn 1): Dùng để gửi tin cho toàn mạng (VD: `.255`).

### 🚫 Các dải IP đặc biệt (Quan trọng)
| Loại | Dải IP / Ký hiệu | Ý nghĩa thực tế |
| :--- | :--- | :--- |
| **RFC 1918 (Private)** | `10.0.0.0/8`<br>`172.16.0.0/12`<br>`192.168.0.0/16` | Dùng tự do trong LAN. Phải qua **NAT** để ra Internet. (Tái sử dụng IP). |
| **Loopback** | `127.0.0.0/8`<br>(Thường là `127.0.0.1`) | Kiểm tra ngăn xếp mạng nội tại (Software stack). Nếu ping không được -> Lỗi Win/Driver. |
| **Link-local (APIPA)** | `169.254.0.0/16` | Tự gán khi **DHCP lỗi**. Máy không thấy Router, không ra được Net. |
| **Broadcast** | `255.255.255.255` | Dùng để tìm kiếm thiết bị/dịch vụ trong mạng cục bộ khi chưa biết IP. |

---

## 3. Layer 4: Transport

Quản lý luồng dữ liệu, đảm bảo độ tin cậy và phân phối đến đúng ứng dụng.

### 🆚 TCP vs UDP
| Đặc điểm | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| :--- | :--- | :--- |
| **Cơ chế** | Connection-oriented (Hướng kết nối). | Connectionless (Không kết nối). |
| **Độ tin cậy** | Cao (Có sửa lỗi, gửi lại). | Thấp (Best-effort). |
| **Tốc độ** | Chậm hơn (do overhead cao). | Rất nhanh. |
| **Ứng dụng** | Web, Email, File Transfer. | Game Online, DNS, VoIP, Stream. |
| **Quy trình** | **3-way Handshake** (SYN, SYN-ACK, ACK). | Gửi trực tiếp, không cần bắt tay. |

### 🚪 Ports & Firewall
* **Port:** Định danh ứng dụng trên một máy.
    * **System Ports (0-1023):** Web (`80`/`443`), SSH (`22`).
    * **Ephemeral Ports (49152+):** Cổng tạm thời Client dùng để gửi tin đi.
* **Firewall (Stateful Inspection):**
    * Tự động cho phép lưu lượng đi vào (**Inbound**) nếu nó là phản hồi của một kết nối mà Client bên trong đã khởi tạo trước đó (**Outbound**).

---

## 4. Network Services (Dịch vụ Mạng)

Các dịch vụ hạ tầng giúp mạng hoạt động trơn tru.

### 🌍 DNS (Domain Name System)
Phân giải **Tên miền** (Domain) sang **Địa chỉ IP**.
* **Quy trình:** Browser Cache -> OS Cache -> Recursive Resolver (ISP).
* **Truy vấn lặp (Iterative Queries):**
    1.  Hỏi **Root Server** (.)
    2.  Hỏi **TLD Server** (.com, .vn)
    3.  Hỏi **Authoritative Server** (nơi quản lý domain cụ thể).

### ⚙️ Các dịch vụ khác
* **DHCP (Dynamic Host Configuration Protocol):**
    * Tự động cấp phát: IP, Subnet Mask, Gateway, DNS.
    * Quy trình: **DORA** (Discover - Offer - Request - Acknowledge).
* **NAT (Network Address Translation):**
    * Dịch IP Private -> IP Public để truy cập Internet.
    * **PAT (Port Address Translation):** Nhiều máy LAN dùng chung 1 IP Public thông qua các cổng khác nhau.
* **VPN (Virtual Private Network):**
    * Tạo đường hầm mã hóa (**Encrypted Tunnel**) qua mạng công cộng.
    * Mục đích: Truy cập mạng nội bộ từ xa an toàn, ẩn IP thật.
* **Proxy:** Người trung gian (Middleman).
    * **Forward Proxy:** Bảo vệ Client (Lọc web, ẩn danh người dùng).
    * **Reverse Proxy:** Bảo vệ Server (Cân bằng tải, che giấu Server thật).

---

## 5. Connecting to Internet & Wireless

### 🌐 WAN (Wide Area Network)
* Kết nối các địa điểm xa nhau về mặt địa lý.
* Thường thuê hạ tầng của nhà mạng (ISP).

### 📶 Wireless (Wifi - 802.11)
Các thông số quan trọng khi cấu hình Wifi:

#### Băng tần (Bands) & Kênh (Channels)
| Băng tần | Đặc điểm | Kênh sạch (Non-overlapping) |
| :--- | :--- | :--- |
| **2.4 GHz** | Xuyên tường tốt, đi xa. Nhiễu cao. | **1, 6, 11** |
| **5 GHz** | Tốc độ cao, ít nhiễu. Xuyên tường kém. | Nhiều kênh hơn, ít trùng lặp. |

#### Bảo mật Wifi (Security)
* ✅ **WPA2-Personal (PSK):** Dùng mật khẩu chung (Phổ biến cho gia đình).
* ✅ **WPA2/WPA3-Enterprise:** Dùng User/Pass riêng, xác thực qua RADIUS (Doanh nghiệp).
* ❌ **Tránh:** WEP (Lỗi thời, dễ hack) và Open (Không mật khẩu).