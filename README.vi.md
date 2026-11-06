<div align="center">

# AntiLostNavigator

**Biết mình đang ở đâu. Biết mình cần đi hướng nào. Biết cách quay về.**

[![Expo](https://img.shields.io/badge/Expo-SDK%2054-000020?logo=expo&logoColor=white)](https://expo.dev/)
[![React Native](https://img.shields.io/badge/React%20Native-0.81-61DAFB?logo=react&logoColor=black)](#)
[![React](https://img.shields.io/badge/React-19.1-61DAFB?logo=react&logoColor=black)](#)
[![Android](https://img.shields.io/badge/Android-first-3DDC84?logo=android&logoColor=black)](#)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

[English](README.md) · **Tiếng Việt**

</div>

---

## Giới thiệu

AntiLostNavigator là ứng dụng hỗ trợ định hướng ngoài trời dành cho trekking, dã ngoại và những hành trình có nguy cơ mất kết nối di động. Ứng dụng giúp người dùng lưu các mốc quan trọng, xác định hướng đi tới từng mốc bằng GPS và la bàn, đồng thời tiếp tục xem bản đồ ngay cả khi không còn Internet.

Ứng dụng **không** thay thế bản đồ địa hình, thiết bị cứu hộ hoặc kỹ năng sinh tồn. Mục tiêu của AntiLostNavigator là cung cấp một lớp hỗ trợ định hướng đơn giản, rõ ràng và hoạt động cục bộ trên điện thoại khi người dùng cần tìm đường trở lại.

```text
Chuẩn bị hành trình → lấy GPS → lưu waypoint → di chuyển → bản đồ offline + la bàn
→ tính hướng/khoảng cách → mũi tên chỉ hướng → tới mốc / chọn mốc tiếp theo
```

![Luồng hoạt động của AntiLostNavigator](docs/antilost-workflow.png)

---

## Cách ứng dụng hỗ trợ

| Vấn đề ngoài thực địa | Cách AntiLostNavigator hỗ trợ |
|:--|:--|
| Không có Internet | Dùng tile bản đồ offline đã bundle và cache cục bộ |
| Không nhớ đường quay về | Lưu waypoint và breadcrumbs để chọn lại các điểm đã đi qua |
| Không biết đi hướng nào | Tính bearing, khoảng cách và hiển thị hướng tới waypoint |
| GPS dao động | Theo dõi liên tục và chỉ lưu mốc khi độ chính xác đạt mức phù hợp |
| Cầm điện thoại bị nghiêng | Kết hợp Magnetometer và DeviceMotion để bù nghiêng la bàn |
| Muốn kiểm tra hành trình | Lưu dữ liệu cục bộ bằng SQLite để xem lại trong ứng dụng |

Luồng sử dụng điển hình: chờ GPS ổn định, lưu điểm xuất phát/nơi cắm trại/nguồn nước/điểm rẽ dưới dạng waypoint, sau đó dùng bản đồ offline và la bàn khi mất kết nối.

---

## Tính năng

- **Dẫn đường tới waypoint** — trạng thái GPS, độ chính xác vị trí, hướng hiện tại, hướng tới mốc, khoảng cách và cảnh báo lệch hướng
- **Lưu mốc chính xác hơn** — chờ vị trí ổn định trong thời gian ngắn trước khi cho người dùng lưu tên, ghi chú và ảnh của mốc
- **Bản đồ offline** — bộ tile Việt Nam đã bundle cho các mức zoom chính, hỗ trợ lớp vệ tinh và đường phố; các mức zoom cao hơn có thể dùng cache cục bộ khi dữ liệu đã có trên thiết bị
- **Thời gian và dữ liệu mặt trời** — giờ UTC, giờ địa phương và thông tin mọc/lặn mặt trời để ước lượng điều kiện ánh sáng trong hành trình
- **Lưu trữ cục bộ** — waypoint, breadcrumb và dữ liệu GPS lưu trên thiết bị bằng SQLite
- **Giao diện đa ngôn ngữ** — có tiếng Anh, tiếng Việt và các chuỗi bản địa hoá bổ sung trong ứng dụng
- **Android-first với Expo** — thiết kế cho development build native và APK release

---

## Công nghệ

| Thành phần | Sử dụng |
|:--|:--|
| Framework | Expo SDK 54 |
| Runtime | React Native 0.81.5, React 19.1 |
| Vị trí | `expo-location` |
| Cảm biến | `expo-sensors` — Magnetometer và DeviceMotion |
| Cơ sở dữ liệu cục bộ | `expo-sqlite` |
| Lưu tile và file | `expo-file-system` |
| Đồ họa | `react-native-svg` |
| Bộ dựng bản đồ | Custom SVG-based offline map renderer |
| Nền tảng mục tiêu | Android-first, Expo native workflow |

---

## Yêu cầu môi trường

- **Node.js 20+**
- **JDK 17** và **Android SDK** để build native Android
- Thiết bị Android hoặc máy ảo Android
- Tuỳ chọn: tài khoản **Expo / EAS** để build cloud và phát hành
- Để kiểm thử GPS, la bàn và bản đồ offline chính xác, nên dùng thiết bị Android thật

> Expo Go phù hợp để kiểm tra nhanh giao diện và logic, nhưng hành vi cảm biến native, vị trí và bản đồ offline nên kiểm thử bằng development build hoặc APK trên thiết bị thật.

---

## Cách chạy

```bash
git clone https://github.com/Namtran592005/AntiLostNavigator.git
cd AntiLostNavigator

npm install
npx expo start
```

Chạy native Android trên thiết bị hoặc máy ảo:

```bash
npx expo run:android
```

Build bản release cục bộ:

```bash
npx expo prebuild --platform android
npx expo run:android --variant release
```

Các thư mục native sinh tự động và file build không được commit vào repository. APK/AAB nên được lưu ở kênh phát hành riêng như GitHub Releases.

---

## Cấu trúc dự án

```text
.
├── App.js                        # Logic, màn hình và style chính
├── app.json                      # Metadata Expo và quyền native
├── index.js                      # Entry point
├── metro.config.js               # Cấu hình asset tile cho Metro
├── eas.json                      # Profile build EAS
├── assets/
│   ├── icon.png
│   ├── splash-icon.png
│   ├── beep.mp3
│   └── tiles/                    # Tile bản đồ offline đã bundle
├── docs/
│   ├── antilost-workflow.mmd     # Nguồn biểu đồ hoạt động
│   └── antilost-workflow.png     # Biểu đồ dùng trong README
├── package.json
├── LICENSE
├── README.md                     # Tiếng Anh (mặc định)
└── README.vi.md                  # Tiếng Việt
```

---

## Quyền và riêng tư

AntiLostNavigator cần quyền vị trí vì GPS là dữ liệu cốt lõi của chức năng dẫn đường. Ứng dụng cũng yêu cầu quyền camera, media và bộ nhớ để chụp/chọn ảnh mốc và lưu ảnh.

GPS, waypoint, breadcrumb và dữ liệu chuyến đi được lưu cục bộ trên thiết bị để hỗ trợ hoạt động offline. Người dùng nên xem lại các quyền Android trước khi sử dụng.

Lưu ý độ chính xác:

- Độ chính xác GPS phụ thuộc vào thiết bị, điều kiện bầu trời, môi trường và chất lượng tín hiệu.
- La bàn có thể bị ảnh hưởng bởi kim loại, nam châm, loa hoặc thiết bị điện tử gần điện thoại.
- Khi hướng hiển thị không ổn định, hãy di chuyển khỏi nguồn nhiễu và hiệu chỉnh cảm biến bằng chuyển động hình số tám.
- Không nên chỉ dựa vào AntiLostNavigator trong các chuyến đi nguy hiểm. Người dùng nên mang theo bản đồ dự phòng, pin dự phòng, đèn, nước, thiết bị liên lạc và thông báo lịch trình cho người khác trước khi khởi hành.

---

## Phiên bản stable

| Trường | Giá trị |
|:--|:--|
| App version | `1.0.0` |
| Android version code | `1` |
| iOS build number | `1` |
| Expo SDK | `54` |

---

## Đóng góp

Issue và pull request được hoan nghênh. Khi báo lỗi, hãy mô tả thiết bị, phiên bản Android, trạng thái kết nối mạng, độ chính xác GPS và liệu lỗi có xảy ra trong chế độ bản đồ offline hay không.

---

## Giấy phép

Mã nguồn được cấp phép theo [MIT License](LICENSE).

Bản quyền © 2026 [@Namtran592005](https://github.com/Namtran592005).

Giấy phép MIT chỉ áp dụng cho mã nguồn. Tile bản đồ đã bundle, ảnh vệ tinh, dữ liệu đường phố, icon, ảnh chụp và các tài nguyên bên thứ ba khác vẫn tuân theo điều khoản upstream riêng. Nếu phân phối lại ứng dụng kèm tile bản đồ, cần kiểm tra và giữ lại yêu cầu nguồn/ghi nhận liên quan.

---

## Tham chiếu

- [Tài liệu Expo](https://docs.expo.dev/) — tài liệu chính thức của Expo
- [Tài liệu React Native](https://reactnative.dev/docs/getting-started) — tài liệu chính thức của React Native
