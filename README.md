<div align="center">

<h1>💳 PaymentPlugin for Minecraft</h1>

<p>Siêu plugin nạp tiền cho server Minecraft – nạp Ngân hàng (VietQR), Thẻ cào (card2k), Top nạp, Mốc thưởng, BossBar mục tiêu & PlaceholderAPI.</p>

<p>
  <img alt="Java" src="https://img.shields.io/badge/Java-17%2B-ff3f3f?logo=openjdk&labelColor=1e1e1e" />
  <img alt="Paper" src="https://img.shields.io/badge/Paper-1.16%2B-3eb489?logo=papertrail&labelColor=1e1e1e" />
  <img alt="PlayerPoints" src="https://img.shields.io/badge/PlayerPoints-Required-fabc2a?labelColor=1e1e1e" />
  <img alt="PlaceholderAPI" src="https://img.shields.io/badge/PlaceholderAPI-Optional-5865f2?labelColor=1e1e1e" />
  <img alt="License" src="https://img.shields.io/badge/License-REQUIRED_KEY-ff66aa?labelColor=1e1e1e" />
</p>

</div>

---

- ✨ Trải nghiệm nạp “một chạm” qua QR/Bank và thẻ cào.
- 🧠 Tự động đối soát giao dịch, xử lý sai mệnh giá, retry thông minh.
- 🏆 Top nạp, 🎁 mốc thưởng, 📊 BossBar mục tiêu donate toàn server.
- 🧩 PlaceholderAPI: dễ dàng đổ dữ liệu vào scoreboard/tablist/menu.
- 💎 Hỗ trợ Bedrock (Geyser/Floodgate) với form/GUI riêng.


Mục lục
- [Tính năng nổi bật](#tính-năng-nổi-bật)
- [Yêu cầu hệ thống](#yêu-cầu-hệ-thống)
- [Cài đặt nhanh](#cài-đặt-nhanh)
- [Cấu hình chi tiết](#cấu-hình-chi-tiết)
  - [Nạp thẻ (card)](#nạp-thẻ-card--card2k)
  - [Nạp Ngân hàng (API)](#nạp-ngân-hàng-api)
  - [VietQR](#vietqr)
  - [Quy đổi điểm, lệnh thưởng](#quy-đổi-điểm-lệnh-thưởng)
  - [Database](#database)
  - [BossBar mục tiêu donate](#bossbar-mục-tiêu-donate)
  - [Ngày thưởng/Bonus](#ngày-thưởngbonus)
- [Lệnh & Quyền hạn](#lệnh--quyền-hạn)
- [PlaceholderAPI](#placeholderapi)
- [Khắc phục sự cố](#khắc-phục-sự-cố)
- [Build từ mã nguồn](#build-từ-mã-nguồn)
- [Hỗ trợ & Liên hệ](#hỗ-trợ--liên-hệ)


Tính năng nổi bật
- 💳 Nạp qua QR/Ngân hàng (sepay, payos, sieuthicode…)
- 🪪 Nạp thẻ cào theo chuẩn Nencer – card2k, gachthe1s, naptudong
- 🔁 Tự động kiểm tra giao dịch chờ (pending) + retry thông minh
- 🧭 Xử lý sai mệnh giá: cảnh báo, chờ kết quả chốt, cộng điểm theo mệnh giá thực
- 🧮 Tùy chỉnh quy đổi điểm theo mệnh giá; lệnh thưởng sau nạp
- 🏆 Top nạp + 🎯 mốc thưởng + 📊 BossBar mục tiêu (server-wide)
- 🧩 PlaceholderAPI: bảng điểm, tablist, menu cực tiện
- 🎮 GUI riêng cho Java & Bedrock (nếu có Geyser/Floodgate)
- 🔒 Kiểm tra license trước khi khởi động (yêu cầu license-key)


Yêu cầu hệ thống
- Máy chủ: Paper/Spigot 1.16+ (khuyến nghị 1.20.x)
- Java 17+
- Bắt buộc: PlayerPoints (để cộng điểm)
- Tuỳ chọn: PlaceholderAPI, Floodgate/Geyser (Bedrock)


Cài đặt nhanh
1) Cài dependency:
   - PlayerPoints (bắt buộc)
   - PlaceholderAPI (khuyến nghị)
   - Floodgate/Geyser (nếu hỗ trợ Bedrock)
2) Thả PaymentPlugin.jar vào plugins/ và khởi động server.
3) Điền license-key và cấu hình cần thiết trong plugins/PaymentPlugin/config.yml.
4) Dùng lệnh: /naptheadmin reload để nạp lại cấu hình.


Cấu hình chi tiết

Nạp thẻ (card)
Sử dụng card2k ,gachthe1s ,naptudong ,thesieure.

```yaml
card:
  api_type: 'card2k' # cũng hỗ trợ 'gachthe1s', 'naptudong'
  api_url: "http://card2k.com/chargingws/v2" # card2k dùng http
  partner_id: "81144044513"
  partner_key: "YOUR_PARTNER_KEY"
  connection_timeout: 15000
  read_timeout: 15000
  max_retries: 3
  conversion_rate: 1000
  ssl_trust_all: false
  signature_uppercase: false
  debug_mode: true
  callback_url: ""
  include_callback_in_signature: false
  pending_check_interval: 60
  pending_max_checks: 5
  error_messages:
    '1': "Thẻ hợp lệ. Nạp thẻ thành công!"
    '2': "Thẻ đúng nhưng sai mệnh giá. Bạn sẽ nhận được số points theo mệnh giá thực tế."
    '3': "Thẻ không hợp lệ, đã sử dụng hoặc sai thông tin."
    '4': "Hệ thống nạp thẻ đang bảo trì. Vui lòng thử lại sau."
    '99': "Thẻ đang được xử lý. Vui lòng đợi trong giây lát..."
    '100': "Gửi thẻ thất bại. Vui lòng liên hệ admin."
```

- status 1: cộng điểm ngay
- status 2: sai mệnh giá → cảnh báo + chờ check để chốt số điểm thực
- status 99: đang xử lý → hệ thống tự check lại nhiều lần
- status 3/4/100: lỗi → hiển thị thông báo thân thiện

Bật/tắt loại thẻ trong GUI:

```yaml
card-types:
  viettel: true
  mobifone: true
  vinaphone: true
  vietnammobile: true
  garena: true
  zing: false
  vcoin: true
  gate: false
```


Nạp Ngân hàng (API)
Ví dụ cấu hình sepay:

```yaml
api:
  provider: "sepay"
  sepay:
    url: "https://my.sepay.vn/userapi/transactions/list"
    token: "YOUR_SEPAY_TOKEN"
    connection_timeout: 15000
    read_timeout: 15000
    max_retries: 3
```

Plugin sẽ quét lịch sử giao dịch, đối chiếu transaction code VietQR và cộng điểm tự động.


VietQR
```yaml
vietqr:
  account: "" # Số tài khoản
  bin: ""     # Mã BIN (VD 970436)
  name: ""    # Tên chủ tài khoản
  template: "compact"
  connection_timeout: 15000
  read_timeout: 15000
  max_retries: 3
```
Nếu thiếu cấu hình, plugin sẽ dùng QR động fallback.


Quy đổi điểm, lệnh thưởng
- Quy đổi chung (bank): conversion.rate, ví dụ 1000 VND = 1 point
- Quy đổi thẻ (card): card.conversion_rate (mặc định 1000)

```yaml
donate-amounts:
  10000: 10
  20000: 20
  50000: 50
  100000: 100
  200000: 200

donate-commands:
  '50000':
    - 'give %PLAYER% diamond 5'
  '100000':
    - 'give %PLAYER% diamond_block 1'
```


Database
- Mặc định: SQLite (plugins/PaymentPlugin/data.db)
- Hỗ trợ: MySQL, H2

```yaml
database:
  type: sqlite # sqlite|mysql|h2|file
  options:
    prefix: payment_
  mysql:
    host: localhost
    port: 3306
    database: payment_plugin
    username: root
    password: your_password
    useSSL: false
    allowPublicKeyRetrieval: true
    connectionTimeout: 30000
    socketTimeout: 30000
    characterEncoding: UTF-8
    useUnicode: true
    autoReconnect: true
    maxReconnects: 3
```


BossBar mục tiêu donate
- Sửa plugins/PaymentPlugin/bossbar.yml để đặt mục tiêu & phần thưởng server-wide.
- Tổng donate toàn server sẽ được load từ DB và cập nhật động.


Ngày thưởng/Bonus
```yaml
special-bonus:
  enabled: true
  events:
    '01-01':
      name: "&cTết Dương Lịch"
      bonus-percentage: 20
    '02-09':
      name: "&aQuốc Khánh"
      bonus-percentage: 25
```


Lệnh & Quyền hạn

Lệnh phổ biến
- /napbank <số tiền> — nạp qua ngân hàng/QR
- /napthe [lichsu] — mở GUI nạp thẻ; xem lịch sử bằng tham số lichsu
- /mocnap — mở mốc thưởng
- /topnap — mở bảng xếp hạng top nạp
- /ntmenu — mở menu (Bedrock)
- /napthedt <loại> <mệnh giá> <seri> <mã> — nạp thẻ cho Bedrock
- /naptheadmin <reload|help|version|status> — quản trị

Quyền hạn
- paymentplugin.admin — dùng lệnh quản trị


PlaceholderAPI
- Plugin tự đăng ký expansion "paymentpl" nếu PlaceholderAPI có mặt.

Theo người chơi
- %paymentpl_player_donate%, %paymentpl_donate% — tổng donate (VND)
- %paymentpl_player_donate_formatted% — donate đã format
- %paymentpl_player_rank%, %paymentpl_rank% — hạng donate (0 nếu chưa xếp hạng)
- %paymentpl_points%, %paymentpl_player_points% — điểm PlayerPoints hiện tại
- %paymentpl_points_formatted% — điểm đã format

Top server
- %paymentpl_top_name_1%, %paymentpl_top_amount_1% (đổi 1 thành 2..10)
- %paymentpl_top_list% — liệt kê name:amount theo top

Tổng donate toàn server
- %paymentpl_total_donate%, %paymentpl_server_total_donate%

Hệ thống
- %paymentpl_api_calls%, %paymentpl_api_errors%, %paymentpl_uptime%


Khắc phục sự cố
- PlayerPoints not found → Cài PlayerPoints rồi khởi động lại.
- Placeholder không hiển thị → Cài PlaceholderAPI, kiểm tra console có lỗi không.
- Thẻ 99/2 quá lâu → Đợi phản hồi đối tác, kiểm tra card.pending_check_interval & pending_max_checks.
- QR VietQR không tạo → Kiểm tra vietqr.account/bin/name hoặc dùng QR động fallback.
- SSL lỗi khi gọi API → Không bật card.ssl_trust_all trên production. Chỉ dùng tạm để test.
- License invalid → Điền license-key hợp lệ vào config.yml.


Build từ mã nguồn
- Maven 3.8+ & JDK 17+

```bash
mvn -q -DskipTests package
```
Jar nằm ở target/PaymentPlugin-<version>.jar


Hỗ trợ & Liên hệ
- Gặp sự cố? Hãy gửi log/ảnh console + phiên bản server/Java/các plugin liên quan.
- Đóng góp ý tưởng, phản hồi tính năng – luôn hoan nghênh!


Bản quyền
- © Aryaisme. Yêu cầu license-key hợp lệ để sử dụng.


