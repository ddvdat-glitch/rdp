# burh burh lmao chim to ckim nhỏ

Hệ thống Remote Desktop (RDP) chạy trên nền tảng **GitHub Actions** với cơ chế lưu trữ ổ đĩa ảo độc quyền, đồng bộ toàn bộ Profile, phần mềm, Registry và dữ liệu thẳng lên **GitHub Release** và **Git Branch** giữa các phiên làm việc mà không sợ mất mát[cite: 1, 2, 3, 4, 5].

---

## ✨ Các Tính Năng Nổi Bật

* **Ổ đĩa riêng biệt (`X:\`):** Co giãn động lên đến 45GB - 50GB, chứa toàn bộ hệ thống và dữ liệu[cite: 1, 2, 4, 5].
* **Đồng bộ thông minh:** Tự động sao lưu toàn bộ thư mục cá nhân (Desktop, Documents, Downloads, AppData) và các phần mềm cài đặt thêm ở `C:\Program Files`[cite: 1, 2, 4, 5].
* **Bảng điều khiển Web Quản Lý (`Port 8080`):** Cho phép sếp bấm **Lưu ngay**, **Khởi động phiên mới** hoặc **Tắt hẳn** trực tiếp ngay trong RDP hoặc qua trình duyệt điện thoại/máy tính[cite: 4, 5].
* **Bảo mật tuyệt đối qua Tailscale:** Kết nối mạng riêng ảo trực tiếp, không phơi cổng RDP ra ngoài Internet công cộng[cite: 1, 2, 3, 4, 5].
* **Tự động tiếp nối phiên:** Khi hết giờ, hệ thống tự động đóng gói dữ liệu và tự động gọi phiên chạy tiếp theo mà không cần thao tác thủ công[cite: 1, 2, 3, 4, 5].

---

## 🛠️ Chuẩn Bị Trước Khi Chạy (Secrets)

Trước khi kích hoạt Workflow, sếp cần tạo 3 **Repository Secrets** trong cài đặt của repo (`Settings -> Secrets and variables -> Actions -> New repository secret`):

1. **`PAT_TOKEN`**: Personal Access Token của GitHub (có quyền `repo` và `workflow`) dùng để đẩy dữ liệu lên Release và Git Branch.
2. **`TAILSCALE_AUTH_KEY`**: Khóa xác thực tài khoản Tailscale của sếp (được tạo từ trang quản trị Tailscale).
3. **`RDP_PASSWORD`** *(Tùy chọn)*: Mật khẩu cố định cho tài khoản RDP của sếp. Nếu để trống, hệ thống sẽ tự sinh ngẫu nhiên một mật khẩu mạnh và in ra ở log Bước 9[cite: 1, 2, 3, 4, 5].

---

## 🚀 Hướng Dẫn Sử Dụng

1. Vào tab **Actions** trên repository GitHub của sếp.
2. Chọn workflow **`siêu bá ki của đạt lor kim (github native persistence)`**.
3. Bấm **Run workflow**, tùy chỉnh các thông số:
   * **Thời lượng phiên (`duration`):** Chọn 1 giờ, 3 giờ hoặc 5 giờ[cite: 1, 2, 4, 5].
   * **Bản Windows (`windows_image`):** Chọn `windows-2022` hoặc `windows-2025` (Lưu ý: Giữ cố định một phiên bản giữa các lần chạy để app không lỗi Registry)[cite: 1, 2, 4, 5].
   * **Tên user (`rdp_user`):** Tên tài khoản đăng nhập RDP (Ví dụ: `vps` hoặc `AISTV-D`)[cite: 1, 2, 4, 5].
   * **Gói cài thêm (`choco_packages`):** Nhập tên các phần mềm muốn cài tự động qua Chocolatey, cách nhau bằng dấu cách (Ví dụ: `googlechrome vscode python git`)[cite: 1, 2, 4, 5].
4. Bấm **Run workflow** và đợi khoảng 2–3 phút để máy ảo khởi động xong.

---

## 🌐 Kết Nối & Quản Lý

* **Đăng nhập RDP:** Mở ứng dụng Remote Desktop trên máy tính/điện thoại, nhập địa chỉ **IP Tailscale** (cùng Port `3389`) kèm tài khoản và mật khẩu đã tạo[cite: 1, 2, 3, 4, 5].
* **Bảng điều khiển Web Quản Lý:** Trên Desktop của máy ảo có sẵn shortcut **`WEB-QUAN-LY-RDP`**, hoặc mở trình duyệt truy cập: `http://<IP-Tailscale>:8080`[cite: 4, 5].
  * 💾 **Lưu Dữ Liệu Ngay:** Đẩy toàn bộ dữ liệu mới nhất lên GitHub mà không cần tắt máy[cite: 4, 5].
  * 🔁 **Lưu & Khởi Động Phiên Mới:** Đóng gói toàn bộ ổ đĩa, lưu lên GitHub rồi tự động bật phiên tiếp theo[cite: 4, 5].
  * 🛑 **Lưu & Tắt Hẳn Server:** Lưu dữ liệu sạch sẽ lên GitHub rồi dừng hẳn, không tạo phiên mới[cite: 4, 5].

---

## ⚠️ Những Mục Không Được Lưu
* Các thư mục hoặc tệp tin tự tạo ở gốc ổ `C:\` hoặc ổ `D:\` (ngoài thư mục hệ thống chuẩn)[cite: 1, 2, 4, 5].
* Các tiến trình chạy ngầm cấp hệ thống (Windows Services như Docker, Database nặng) cần được cài đặt tự động qua `choco_packages` ở đầu phiên[cite: 1, 2, 4, 5].
