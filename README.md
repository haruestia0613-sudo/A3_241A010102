# 📱 Lab A3: Thiết kế giao diện với XML Layout & tài nguyên (A3_241A010102)

Bài tập thực hành học phần **Lập trình trên các thiết bị di động** — Màn hình Đăng nhập & Thẻ hồ sơ sinh viên. Bài lab tập trung thiết kế giao diện bằng XML Layout (LinearLayout & ConstraintLayout), tổ chức tài nguyên dùng chung, hỗ trợ đa màn hình (màn hình ngang `layout-land`), chế độ tối (Dark Theme) và tối ưu hóa kiểu dáng bằng Styles.

---

## 👨‍💻 Thông tin sinh viên
- **Họ và tên:** Lê Huỳnh Thành Đạt
- **Mã số sinh viên (MSSV):** 241A010102
- **Lớp:** CNTT - LTDD
- **Phiên bản Android Studio:** Android Studio Quail 4 | 2026.1.4 Patch 1
- **Môi trường / Thiết bị thử nghiệm:** TDR API 37.2 — **Android Version:** Android 17.0 (“CinnamonBun”) | x86_64

---

## 🎯 Mục tiêu bài lab
1. **Phân biệt View và ViewGroup:** Hiểu cách Android thổi (inflate) file XML thành cây đối tượng Java.
2. **Thiết kế giao diện bằng 2 cách:** Dựng cùng một giao diện màn hình Đăng nhập bằng `LinearLayout` lồng nhau và `ConstraintLayout` phẳng.
3. **Tổ chức tài nguyên chuẩn:** Tách tài nguyên ra `strings.xml`, `colors.xml`, `dimens.xml` và vẽ hình bằng các file `drawable/*.xml` với đơn vị chuẩn `dp` / `sp`.
4. **Hỗ trợ đa cấu hình màn hình:** Thiết kế giao diện 2 cột dành cho màn hình xoay ngang với `res/layout-land` giữ nguyên ID view.
5. **Nâng cao trải nghiệm UI:** Hỗ trợ Chế độ tối (Dark Theme) và tối ưu hóa mã nguồn XML bằng `styles`.

---

## 🛠️ Công nghệ & Cấu hình
- **Ngôn ngữ lập trình:** Java
- **Giao diện:** XML (`LinearLayout`, `ConstraintLayout`, `FrameLayout`, `ScrollView`, `MaterialCardView`, `TextInputLayout`)
- **Build System & Minimum SDK:** Gradle 9.6.0, Minimum SDK API 24 (Android 7.0)
- **Cấu trúc tài nguyên dự án:**
    - `res/values/`: `strings.xml`, `colors.xml`, `dimens.xml`, `themes.xml` (chứa styles).
    - `res/values-night/`: `colors.xml` hỗ trợ Chế độ tối.
    - `res/drawable/`: `bg_header.xml`, `bg_avatar.xml`, `bg_stat.xml`.
    - `res/layout-land/`: `activity_main.xml` thiết kế riêng cho màn hình xoay ngang.

---

## 📊 So sánh hai bản Layout (LinearLayout vs ConstraintLayout)

| Tiêu chí | Bản LinearLayout | Bản ConstraintLayout |
| :--- | :--- | :--- |
| **Số tầng lồng nhau** *(Component Tree)* | Nhiều tầng (3–4 tầng lồng nhau) | 1 tầng phẳng (tất cả view nằm trực tiếp trong root) |
| **Số dòng XML** | Nhiều hơn (do phải khai báo thêm các ViewGroup trung gian) | Ít hơn / Gọn hơn (giảm thiểu thẻ chứa phụ) |
| **Độ dễ đọc / dễ sửa** | Dễ đọc khi đơn giản; khó sửa khi giao diện phức tạp/lồng sâu | Dễ sửa và linh hoạt hơn nhờ các đường ràng buộc (constraints) |
| **Hiển thị khi màn hình rộng** | Các thành phần bị kéo giãn theo chiều dọc/ngang, khó cân đối | Giữ nguyên tỉ lệ và vị trí tương quan nhờ ràng buộc và Guideline |

---

## 🌟 Chức năng nâng cao đã hoàn thành
- [x] **NC1: Hỗ trợ Chế độ tối (Dark Theme):** Khai báo bảng màu tương phản dịu mắt ở `res/values-night/colors.xml`, tự động đổi nền (#121212) và màu chữ khi bật Dark Mode mà không làm lệch bố cục.
- [x] **NC3: Tách Style chữ dùng lại (Styles optimization):** Tối ưu hóa mã nguồn XML bằng cách gom nhóm các thuộc tính định dạng chữ lặp đi lặp lại vào thẻ `<style>` trong `themes.xml` / `styles.xml`.

---

## ❓ Câu hỏi ôn tập

1. **Khác nhau giữa `padding` vs `layout_margin` \| `gravity` vs `layout_gravity`:**
    - `padding` là khoảng cách từ viền vào bên trong nội dung view; `layout_margin` là khoảng cách từ viền ra bên ngoài tới các view xung quanh.
    - `gravity` căn chỉnh vị trí nội dung bên trong view; `layout_gravity` căn chỉnh vị trí của chính view đó trong view cha.
2. **Cách dùng `dp` vs `sp` & Vì sao không dùng `px`?**
    - `dp` dùng cho kích thước/khoảng cách (width, height, margin, padding); `sp` dùng riêng cho cỡ chữ.
    - Không dùng `px` vì phụ thuộc vào độ phân giải màn hình gây vỡ/méo giao diện trên thiết bị có mật độ điểm ảnh cao; `dp` và `sp` tự co giãn linh hoạt theo màn hình hệ thống.
3. **Chia đôi 50/50 chiều ngang trong LinearLayout:**
    - Đặt `android:layout_width="0dp"` cho cả 2 view.
    - Đặt `android:layout_weight="1"` cho cả 2 view.
4. **2 lý do thay LinearLayout lồng nhau bằng ConstraintLayout:**
    - **Tăng tốc độ vẽ:** Tạo cây layout phẳng (Flat Hierarchy), hệ thống chỉ cần đo đạc 1 lần thay vì đệ quy nhiều tầng gây giật lag.
    - **Dễ bảo trì:** Ràng buộc linh hoạt giúp giảm bớt thẻ XML thừa và dễ tinh chỉnh bố cục.
5. **Cơ chế chọn `res/layout-land` & Xoay màn hình:**
    - Hệ thống tự chọn dựa trên *Configuration Qualifiers*; khi xoay ngang máy, Android tự nhận diện qualifier `-land` để nạp XML tương ứng.
    - Xoay màn hình làm thay đổi cấu hình (*Configuration Change*), Android mặc định hủy và tạo lại Activity để nạp lại đúng layout mới.

---

## 📌 Hướng dẫn cài đặt & Chạy ứng dụng
1. **Clone repository:**
   ```bash
   git clone [https://github.com/haruestia0613-sudo/A3_241A010102.git](https://github.com/haruestia0613-sudo/A3_241A010102.git)
   cd A3_241A010102