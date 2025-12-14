# Kết nối Internet (Connecting to the Internet)

Mạng hiện đại sử dụng nhiều loại **phương tiện vật lý** và **công nghệ truy cập** để kết nối với Internet. Chương này xem xét cách các điểm cuối thực sự kết nối, từ dial-up cũ kỹ đến cáp quang, các liên kết WAN giữa các địa điểm, và các mạng không dây và di động ngày nay.

---

## 1. POTS và Dial-up

### 1.1 Dịch vụ điện thoại cũ (POTS)

Các kết nối Internet tiêu dùng sớm nhất sử dụng **mạng điện thoại analog** hiện có, thường được gọi là **POTS – Plain Old Telephone Service**.

Đặc điểm:

- Được thiết kế ban đầu cho **thoại**, không phải dữ liệu.
- Sử dụng dây đồng xoắn đôi từ cơ sở khách hàng đến tổng đài điện thoại.
- Băng thông hạn chế và chịu ảnh hưởng của nhiễu analog và suy giảm tín hiệu.

### 1.2 Dial-up và Modems

**Dial-up Internet** sử dụng **modems** (modulator–demodulator) để mã hóa dữ liệu số thành các âm thanh analog có thể di chuyển qua đường dây POTS.

Các tính chất cấp cao:

- Tốc độ thường từ 56 kbps trở xuống – **rất chậm** theo tiêu chuẩn hiện đại.
- Kết nối yêu cầu quay số điện thoại; đường dây bị bận trong khi kết nối.
- Độ trễ và độ tin cậy bị hạn chế, nhưng nó đã làm cho việc truy cập Internet đại chúng ban đầu trở nên khả thi.

Dial-up phần lớn đã lỗi thời ngày nay, nhưng hiểu về nó cung cấp bối cảnh cho lý do tại sao các công nghệ băng thông rộng mới hơn lại cần thiết.

---

## 2. Kết nối Băng thông rộng (Broadband Connections)

### 2.1 Băng thông rộng là gì?

**Broadband** đề cập đến truy cập Internet tốc độ cao, "luôn bật" hỗ trợ:

- Tốc độ dữ liệu cao hơn nhiều so với dial-up.
- Sử dụng đồng thời **thoại và dữ liệu** trên cùng một đường dây (hoặc phương tiện riêng biệt).
- Chia sẻ quyền truy cập cho nhiều thiết bị trong gia đình và doanh nghiệp.

Các công nghệ băng thông rộng phổ biến bao gồm **T-carrier**, **DSL**, **cable**, và **fiber**.

### 2.2 Công nghệ T-Carrier

Hệ thống **T-carrier** là các mạch kỹ thuật số theo truyền thống được sử dụng bởi các nhà cung cấp viễn thông:

- **T1** cung cấp 1.544 Mbps, bao gồm 24 kênh kỹ thuật số.
- **T3** cung cấp 44.736 Mbps, tổng hợp nhiều đường T1.

Các ý tưởng chính:

- Cung cấp kết nối điểm-điểm (point-to-point) dành riêng giữa các địa điểm.
- Trong lịch sử rất phổ biến cho các liên kết WAN doanh nghiệp và truy cập Internet tốc độ cao ban đầu.
- Thường được thay thế ngày nay bởi các dịch vụ dựa trên Ethernet và cáp quang nhưng vẫn hữu ích để biết.

### 2.3 Digital Subscriber Lines (DSL)

**DSL (Digital Subscriber Line)** sử dụng các dải tần số cao hơn trên các cặp dây điện thoại đồng hiện có để cung cấp băng thông rộng mà không can thiệp vào thoại analog.

Các khái niệm cấp cao:

- **Asymmetric DSL (ADSL)** – băng thông tải xuống cao hơn tải lên, tối ưu hóa cho duyệt web và tiêu thụ phương tiện.
- **VDSL và VDSL2** – các biến thể DSL mới hơn cung cấp tốc độ cao hơn trên khoảng cách ngắn hơn.
- Tốc độ phụ thuộc nhiều vào **chất lượng đường dây** và **khoảng cách** từ thiết bị của nhà cung cấp.

DSL cho phép các công ty viễn thông nâng cấp khách hàng từ dial-up lên băng thông rộng sử dụng cơ sở hạ tầng đồng hiện có.

### 2.4 Cable Broadband

**Cable broadband** tận dụng **cáp đồng trục** được lắp đặt ban đầu cho truyền hình cáp:

- Sử dụng các tiêu chuẩn như **DOCSIS** để truyền dữ liệu.
- Thường cung cấp tốc độ cao hơn DSL, đặc biệt là theo hướng tải xuống.
- Mạng thường được **chia sẻ** giữa nhiều thuê bao trong một khu vực lân cận, vì vậy băng thông khả dụng có thể thay đổi theo mức sử dụng.

Cable modem kết nối thiết bị của khách hàng với mạng lai cáp quang-đồng trục của nhà cung cấp.

### 2.5 Kết nối Cáp quang (Fiber)

**Fiber-optic broadband** là tiêu chuẩn vàng hiện tại cho tốc độ truy cập và độ tin cậy.

Đặc điểm:

- Sử dụng ánh sáng qua sợi thủy tinh; chống nhiễu điện từ.
- Hỗ trợ băng thông rất cao (hàng trăm Mbps đến đa Gbps) và khoảng cách xa.
- Các mô hình triển khai phổ biến:
  - **FTTH/FTTP (Fiber to the Home/Premises)**
  - **FTTC (Fiber to the Curb/Cabinet)** với cáp đồng cho đoạn cuối cùng.

Cáp quang ngày càng phổ biến ở các khu vực đô thị và ngoại ô và củng cố phần lớn trục xương sống Internet toàn cầu.

### 2.6 Các giao thức Băng thông rộng (Góc nhìn cấp cao)

Bất kể phương tiện truyền dẫn, các dịch vụ băng thông rộng thường dựa vào các giao thức cấp cao hơn như:

- **PPP và PPPoE** – đóng gói PPP qua Ethernet để xác thực và cấu hình.
- **DOCSIS** – định nghĩa cách dữ liệu được truyền qua mạng cáp.
- Nhiều công nghệ dựa trên **Ethernet** và **MPLS** cho các mạng nhà mạng.

Người dùng cuối thường chỉ thấy một kết nối Ethernet từ modem hoặc router của họ, trong khi các giao thức này hoạt động ở hậu trường.

---

## 3. Mạng diện rộng (WANs)

### 3.1 Khái niệm WAN

Một **Wide Area Network (WAN)** kết nối các địa điểm tách biệt về mặt địa lý:

- Văn phòng công ty, trung tâm dữ liệu, chi nhánh, và nhà cung cấp đám mây.
- Thường được xây dựng bằng các dịch vụ mua từ các nhà mạng viễn thông.

Sự khác biệt chính so với LAN:

- Khoảng cách xa hơn, độ trễ cao hơn.
- Các liên kết thường được **thuê** hoặc cung cấp như một dịch vụ thay vì sở hữu hoàn toàn.
- Độ tin cậy, dự phòng, và thỏa thuận cấp độ dịch vụ (SLAs) là rất quan trọng.

### 3.2 Công nghệ WAN (Cấp độ cao)

Các khối xây dựng WAN phổ biến bao gồm:

- **Leased lines / private circuits** – kết nối điểm-điểm dành riêng.
- **MPLS (Multiprotocol Label Switching)** – công nghệ nhà mạng cung cấp mạng riêng ảo trên cơ sở hạ tầng chia sẻ.
- **Metro Ethernet** – các dịch vụ dựa trên Ethernet kết nối các địa điểm ở quy mô đô thị.
- **Satellite và microwave links** – được sử dụng khi cơ sở hạ tầng có dây không thực tế.

Việc lựa chọn công nghệ phụ thuộc vào băng thông yêu cầu, khoảng cách, chi phí và tính khả dụng.

### 3.3 Các giao thức WAN (Khái niệm)

Trong lịch sử, WAN sử dụng các giao thức như:

- **Frame Relay**, **ATM**, và **HDLC** trên các liên kết nối tiếp.
- **PPP (Point-to-Point Protocol)** cho framing tầng liên kết, xác thực, và cấu hình IP trên các liên kết điểm-điểm.

Nhiều trong số này là di sản ngày nay, được thay thế bằng các giải pháp dựa trên Ethernet và IP, nhưng chúng minh họa cách WAN đã phát triển.

### 3.4 Point-to-Point VPNs

Các tổ chức ngày càng sử dụng **point-to-point VPNs** qua Internet công cộng thay vì các mạch dành riêng:

- Đường hầm an toàn, được mã hóa giữa các địa điểm hoặc giữa một địa điểm và nhà cung cấp đám mây.
- Đạt được ngữ nghĩa mạng riêng trong khi tận dụng kết nối công cộng giá rẻ.
- Thường được triển khai với các công nghệ như IPsec hoặc các thiết bị VPN site-to-site hiện đại.

Từ góc độ của các router nội bộ, một đường hầm VPN hoạt động giống như một liên kết WAN riêng.

---

## 4. Mạng không dây (Wireless Networking)

### 4.1 Giới thiệu về Công nghệ Mạng không dây

Mạng không dây thay thế cáp đồng hoặc quang bằng **sóng vô tuyến**:

- Cung cấp tính di động và triển khai linh hoạt.
- Hoạt động theo nhiều tiêu chuẩn và băng tần khác nhau (Wi-Fi, Bluetooth, di động, v.v.).
- Yêu cầu lập kế hoạch cẩn thận về **vùng phủ sóng**, **dung lượng**, và **bảo mật**.

### 4.2 Wi-Fi và Họ 802.11

**Wi-Fi** là tên thông thường cho các tiêu chuẩn mạng LAN không dây IEEE **802.11**.

Các tính năng cấp cao:

- Hoạt động chủ yếu trong các băng tần **2.4 GHz**, **5 GHz**, và **6 GHz** mới hơn.
- Các tiêu chuẩn như 802.11n, 802.11ac, và **802.11ax (Wi-Fi 6)** giới thiệu thông lượng cao hơn và hiệu quả tốt hơn.
- Sử dụng các điểm truy cập (access points) để cung cấp vùng phủ sóng và quản lý truy cập cho nhiều client.

**Wi-Fi 6** cải thiện:

- Hiệu suất trong môi trường mật độ cao (sân vận động, văn phòng, chung cư).
- Hiệu quả thông qua các công nghệ như OFDMA và lập lịch cải tiến.
- Thời lượng pin cho client thông qua các cơ chế tiết kiệm năng lượng tốt hơn.

### 4.3 "Súp bảng chữ cái" và Các giao thức truyền dữ liệu IoT

Thế giới không dây bao gồm nhiều giao thức chuyên biệt, thường được biết đến bằng các từ viết tắt:

- **Bluetooth / Bluetooth Low Energy (BLE)** – mạng khu vực cá nhân phạm vi ngắn.
- **Zigbee, Thread, Z-Wave** – mạng lưới công suất thấp cho cảm biến và tự động hóa gia đình.
- **LoRaWAN, Sigfox, NB-IoT** – công nghệ tầm xa, tốc độ bit thấp cho các thiết bị IoT.

Các giao thức này đánh đổi tốc độ lấy **phạm vi**, **hiệu quả năng lượng**, hoặc **sự đơn giản**, tùy thuộc vào trường hợp sử dụng.

### 4.4 Cấu hình Mạng không dây

Các mô hình triển khai Wi-Fi phổ biến:

- **Infrastructure mode** – mô hình tiêu chuẩn với điểm truy cập và client.
- **Ad hoc mode** – giao tiếp ngang hàng không có cơ sở hạ tầng trung tâm.
- **Mesh networks** – nhiều điểm truy cập chuyển tiếp lưu lượng để phủ sóng rộng hơn.
- **Hotspots** – truy cập công cộng được cung cấp bởi ISP, địa điểm, hoặc thiết bị di động.

Thiết kế mạng cân bằng giữa vùng phủ sóng, dung lượng và hành vi chuyển vùng (roaming).

### 4.5 Kênh không dây (Wireless Channels)

Mạng không dây chia sẻ không khí, vì vậy **lập kế hoạch kênh** là rất quan trọng:

- Các kênh khác nhau tương ứng với các lát tần số khác nhau trong một băng tần.
- Trong 2.4 GHz, chỉ một vài kênh là không chồng chéo, vì vậy nhiễu là phổ biến.
- Băng tần 5 GHz và 6 GHz cung cấp nhiều kênh không chồng chéo hơn và thông lượng tiềm năng cao hơn.
- Lựa chọn kênh thích hợp và kiểm soát công suất phát giúp giảm nhiễu và cải thiện hiệu suất.

### 4.6 Bảo mật không dây

Vì tín hiệu vô tuyến có thể được nhận bởi bất kỳ ai trong phạm vi, **bảo mật** là mối quan tâm hàng đầu.

Các ý tưởng chính:

- **Authentication (Xác thực)** – xác minh ai được phép tham gia mạng.
- **Encryption (Mã hóa)** – bảo vệ dữ liệu đang truyền khỏi bị nghe trộm.
- **Network segmentation (Phân đoạn mạng)** – tách biệt lưu lượng khách, doanh nghiệp và quản lý.

Các thực tiễn tốt nhất tránh các cơ chế cũ như mạng mở và WEP, và thay vào đó dựa vào các phương pháp mã hóa hiện đại.

### 4.7 Giao thức và Mã hóa (Cấp độ cao)

Các cơ chế bảo mật Wi-Fi phổ biến:

- **WPA2-Personal (PSK)** – mật khẩu chia sẻ; phù hợp cho mạng gia đình.
- **WPA2-Enterprise / WPA3-Enterprise** – sử dụng 802.1X và máy chủ RADIUS cho xác thực từng người dùng và khóa động.
- **WPA3** – giới thiệu mật mã mạnh hơn và bảo vệ tốt hơn chống lại các cuộc tấn công ngoại tuyến.

Ngoài Wi-Fi, nhiều giao thức không dây (Bluetooth, di động, IoT) bao gồm các sơ đồ mã hóa và xác thực riêng để bảo vệ dữ liệu.

### 4.8 Mạng di động (Cellular Networking)

Mạng di động cung cấp kết nối không dây diện rộng sử dụng phổ tần được cấp phép và một mạng lưới các trạm gốc.

Tổng quan cấp cao:

- **GSM/2G → 3G → 4G LTE → 5G** – mỗi thế hệ cải thiện tốc độ, độ trễ và dung lượng.
- Thiết bị di động kết nối với **cell (tế bào)** gần nhất, chuyển giao giữa các cells khi chúng di chuyển.
- **SIM (Subscriber Identity Module)** xác định an toàn thuê bao với mạng.
- Các nhà mạng cung cấp dịch vụ dữ liệu, thoại và tin nhắn, thường được tích hợp với Internet.

Mạng di động là cần thiết cho truy cập Internet di động, IoT và băng thông rộng ở những khu vực hạn chế cơ sở hạ tầng có dây.

### 4.9 Mạng thiết bị di động

Thiết bị di động thường sử dụng sự kết hợp của:

- **Wi-Fi** – cho truy cập tốc độ cao cục bộ (nhà, văn phòng, điểm phát sóng công cộng).
- **Dữ liệu di động** – cho kết nối diện rộng.
- **Tethering / hotspot** – tính năng chia sẻ kết nối của một thiết bị với các thiết bị khác.

Cân nhắc:

- Chuyển vùng giữa các mạng và vùng phủ sóng.
- Giới hạn dữ liệu và sự khác biệt về hiệu suất giữa Wi-Fi và di động.
- Các thực tiễn bảo mật khi sử dụng mạng công cộng hoặc không tin cậy.

---

## 5. Tóm tắt

Chương này đã khám phá cách các thiết bị kết nối vật lý và logic với **Internet**:

- Các kết nối **POTS và dial-up** cũ đã giới thiệu truy cập Internet đại chúng nhưng hiện đã được thay thế bằng các công nghệ băng thông rộng nhanh hơn.
- Các tùy chọn **Broadband**—T-carrier, DSL, cáp, và quang—cung cấp kết nối tốc độ cao, luôn bật sử dụng các phương tiện và giao thức khác nhau.
- **WANs** kết nối các địa điểm qua khoảng cách lớn sử dụng leased lines, MPLS, Metro Ethernet, và ngày càng nhiều **point-to-point VPNs** qua Internet công cộng.
- **Mạng không dây** (Wi-Fi, giao thức IoT, di động) mang lại tính di động và linh hoạt, trong khi lập kế hoạch kênh, mã hóa và xác thực giữ cho các mạng này an toàn.

Cùng nhau, các công nghệ này hình thành tầng truy cập của Internet, làm cầu nối giữa người dùng cuối, tổ chức và cơ sở hạ tầng mạng toàn cầu được mô tả trong các chương trước.