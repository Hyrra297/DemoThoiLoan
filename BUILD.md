# ThoiLoan Battle Demo — Hướng dẫn build

## 1. Chơi ngay trên trình duyệt (Web)

Mở file `demo/index.html` trực tiếp bằng Chrome / Edge:

```
File → Open File → chọn demo/index.html
```

Hoặc dùng VS Code Live Server, click chuột phải → "Open with Live Server".

---

## 2. Build APK Android

### Yêu cầu
- Android Studio (Electric Eel trở lên) hoặc Android SDK + Gradle
- JDK 17

### Cách build

```bash
cd demo/android
./gradlew assembleDebug
```

APK output: `demo/android/app/build/outputs/apk/debug/app-debug.apk`

### Cài trên máy thật / giả lập

```bash
adb install app/build/outputs/apk/debug/app-debug.apk
```

Hoặc mở bằng Android Studio → Run.

---

## 3. Cấu trúc file demo

```
demo/
├── index.html              ← Game HTML5 chính (mở bằng browser)
├── assets/
│   ├── buildings/
│   │   ├── cannon.png          ← Sprite Cannon (từ res/800_480/buildings/DEF_1_1)
│   │   ├── archer_tower.png    ← Sprite Archer Tower (DEF_2_1)
│   │   ├── mortar.png          ← Sprite Mortar (DEF_3_1)
│   │   ├── wizard_tower.png    ← Sprite Wizard Tower (DEF_5_1)
│   │   └── town_hall.png       ← Sprite Town Hall (TOW_1_3)
│   ├── star_on.png
│   └── star_off.png
└── android/
    ├── settings.gradle
    ├── build.gradle
    └── app/
        ├── build.gradle
        └── src/main/
            ├── AndroidManifest.xml
            ├── assets/             ← Copy của index.html + assets/
            └── java/vn/thoiloan/demo/
                └── MainActivity.java
```

---

## 4. Gameplay

| Quân | HP | DPS | Tốc độ | Đặc điểm |
|---|---|---|---|---|
| ⚔️ Barbarian | 45 | 8 | Nhanh | Cận chiến, giá rẻ |
| 🏹 Archer    | 20 | 7 | Nhanh | Tầm xa, linh hoạt |
| 🛡️ Giant     | 300 | 11 | Chậm | Tank, ưu tiên công trình phòng thủ |
| 🐉 Dragon    | 1700 | 120 | TB  | Bay, splash, mạnh nhất |

| Công trình | HP | DPS | Tầm bắn |
|---|---|---|---|
| 💣 Cannon       | 400  | 40  | 5 tile — bắn quân mặt đất |
| 🗼 Archer Tower | 380  | 30  | 6 tile — bắn tất cả |
| 🔥 Mortar       | 500  | 20  | 7 tile — splash, bắn mặt đất |
| 🧙 Wizard Tower | 620  | 60  | 5 tile — splash, bắn tất cả |
| 🏰 Town Hall    | 2800 | —   | Không bắn |

**Điều kiện thắng:**
- ⭐ 1 sao: Phá ≥50% công trình
- ⭐⭐ 2 sao: Phá ≥70%
- ⭐⭐⭐ 3 sao: Phá 100% (thời gian 3 phút)
