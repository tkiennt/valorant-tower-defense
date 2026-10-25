# Valorant: Defense of the Agents 🎯🛡️

<div align="center">

![Unity](https://img.shields.io/badge/Unity-2022+-black?style=for-the-badge&logo=unity&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-Cloud%20Auth%20%26%20Data-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Genre](https://img.shields.io/badge/Genre-2D%20Tower%20Defense-red?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

**Trò chơi chiến thuật thủ thành 2D xây dựng trên Unity Engine kết hợp hệ thống xác thực đám mây AWS**

</div>

---

## 🎮 1. Giới thiệu Trò chơi (Game Overview)

**Valorant: Defense of the Agents** là một tựa game chiến thuật phòng thủ tháp (Tower Defense) 2D độc đáo lấy cảm hứng từ vũ trụ các Đặc vụ (Agents) trong Valorant. Người chơi đóng vai trò người chỉ huy chiến thuật, bố trí các đặc vụ với vũ khí và kỹ năng đặc thù dọc theo các tuyến đường hành quân của kẻ địch nhằm bảo vệ căn cứ chiến lược (*The Spike Core*).

Dự án tích hợp giải pháp **AWS Cloud Architecture** trực tiếp vào game client, mang lại khả năng đăng ký, xác thực bảo mật người chơi và đồng bộ điểm số/tiến trình chơi lên đám mây.

---

## ⚔️ 2. Cơ chế Trò chơi & Tính năng Chính (Core Gameplay)

### 👥 1. Hệ thống Đặc vụ & Tháp phòng thủ (Agent Turret System)
- **Đặc vụ đa dạng:** Mỗi nhân vật sở hữu phong cách chiến đấu riêng biệt:
  - Tháp sát thương nhanh (Rapid-fire Weapon Turret).
  - Tháp sát thương diện rộng (AoE Splash Turret).
  - Tháp khống chế (`SlowTurret.cs`): Áp dụng hiệu ứng làm chậm tốc độ di chuyển của địch.
- **Trực quan hóa tầm bắn (`RangeVisualizer.cs` & `FOVVisualizer.cs`):** Hiển thị bán kính kiểm soát của từng đặc vụ theo thời gian thực khi triển khai hoặc nâng cấp.
- **Kinh tế trong trận (`BuildManager.cs` & `CurrencyDisplay.cs`):** Tích lũy tiền vàng (Creds) qua mỗi đợt tiêu diệt quái để mua thêm đặc vụ hoặc cường hóa chỉ số.

### 🌊 2. Hệ thống Màn chơi & Kẻ địch (Level Progression)
- **5 Màn chơi Chiến thuật:** Từ `LevelOneScene` đến `LevelFiveScene` với bản đồ địa hình (Pixel Art Maps) và lộ trình di chuyển phức tạp dần.
- **Cơ chế điều phối đợt tấn công (`EnemySpawner.cs`, `EnemyMovement.cs`):** Kẻ địch đa dạng về chỉ số máu, tốc độ và khả năng kháng hiệu ứng.
- **Quản lý Sinh mệnh & Thời gian (`Health.cs`, `TimeManager.cs`):** Theo dõi lượng máu căn cứ và tính năng tăng tốc trận đấu (1x / 2x speed).

### ☁️ 3. Tích hợp Đám mây AWS (Cloud Authentication & Storage)
- **Đăng ký & Đăng nhập Bảo mật (`AWSLoginManager.cs`, `AWSSignupManager.cs`):** Xác thực người chơi qua AWS Cognito / Lambda Functions.
- **Lưu trữ dữ liệu chơi (`CloudDataManager.cs`):** Lưu điểm số cao nhất, tiến trình mở khóa màn chơi và cấu hình cá nhân lên Cloud.

---

## 🛠 3. Kiến trúc Công nghệ (Tech Stack)

| Thành phần | Công nghệ / Công cụ | Mô tả chức năng |
| :--- | :--- | :--- |
| **Game Engine** | **Unity (2D URP)** | Universal Render Pipeline 2D cho đồ họa sắc nét |
| **Ngôn ngữ** | **C# (.NET 8/9 standard)** | Lập trình toàn bộ logic game, AI quái, cơ chế tháp |
| **Cloud Services** | **AWS SDK (.NET), Lambda** | Xử lý authentication và serverless backend |
| **Đồ họa & Nghệ thuật**| **Pixel Art & PNG Art** | Sprite nhân vật, vũ khí và tileset bản đồ độc quyền |
| **Văn bản & UI** | **TextMesh Pro (TMP)** | Hệ thống phông chữ và giao diện hiển thị tối ưu |

---

## 📂 4. Cấu trúc Dự án Unity (Project Structure)

```
valorant-tower-defense/
├── Assets/
│   ├── Code/                          # Toàn bộ mã nguồn C# điều khiển game
│   │   ├── AWSLoginManager.cs         # Xử lý đăng nhập đám mây
│   │   ├── AWSSignupManager.cs        # Xử lý đăng ký tài khoản
│   │   ├── BuildManager.cs            # Quản lý đặt tháp và lưới vị trí
│   │   ├── Tower.cs & SlowTurret.cs   # Logic bắn, sát thương, hiệu ứng tháp
│   │   ├── RangeVisualizer.cs         # Hiển thị vòng tròn tầm bắn
│   │   ├── EnemySpawner.cs            # Điều phối đợt tấn công kẻ thù
│   │   └── LevelManager.cs            # Điều hướng thắng/thua màn chơi
│   ├── Scenes/                        # Các màn chơi trong game
│   │   ├── LoginScene.unity           # Màn hình đăng nhập
│   │   ├── SignupScene.unity          # Màn hình đăng ký tài khoản
│   │   ├── HomeScene.unity            # Menu chính
│   │   ├── LevelChooseScene.unity     # Lựa chọn màn chơi
│   │   └── LevelOneScene -> LevelFiveScene.unity
│   ├── pixil_art/ & png_art/          # Tài nguyên đồ họa (Agents, Maps, Weapons, UI)
│   └── Settings/                      # Cấu hình UniversalRP và Renderer2D
└── Packages/                          # Các package Unity và thư viện AWS SDK
```

---

## 🚀 5. Hướng dẫn Mở và Chạy dự án (How to Run)

### Yêu cầu:
- Unity Hub & **Unity Editor phiên bản 2022.3 LTS** (hoặc mới hơn) hỗ trợ Universal Render Pipeline (URP).
- Visual Studio 2022 hoặc Rider với Workload *Game development with Unity*.

### Các bước khởi chạy:
1. Mở **Unity Hub** -> Chọn nút **Add** -> Chọn thư mục `valorant-tower-defense`.
2. Chờ Unity Editor biên dịch các script C# và import asset ban đầu.
3. Trong cửa sổ **Project**, điều hướng tới: `Assets/Scenes/LoginScene.unity` (hoặc `HomeScene.unity`).
4. Nhấn nút **Play (▶️)** trên thanh công cụ Unity để trải nghiệm game trực tiếp trên Editor.

---

## 👥 6. Tác giả & Đóng góp (Credits)

- **Dự án được phát triển bởi:** Nhóm dự án Valorant Defense.
- **Đóng góp:** Trung Kiên ([@tkiennt](https://github.com/tkiennt)):
  - Thiết kế và hoàn thiện toàn bộ phân hệ xác thực người chơi (`SignupScene.unity`, `SignupScene Manager`).
  - Xử lý hệ thống phông chữ TextMesh Pro, chuẩn hóa các trường nhập liệu (Input Validation).
  - Tối ưu hóa giao diện Menu, hiệu ứng tương tác người chơi và quy trình build game.
