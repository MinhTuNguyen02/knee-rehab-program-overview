# 🏥 Knee Rehab Program System (KRPS)

**Hệ thống Quản lý & Theo dõi Phục hồi Chức năng Đầu gối Toàn diện**

## 📖 Giới thiệu dự án

**KRPS (Knee Rehab Program System)** là giải pháp Full-stack Web Application giúp số hóa quy trình đánh giá sức khỏe đầu gối, phân loại mức độ nghiêm trọng và kết nối trực tuyến giữa bệnh nhân với đội ngũ y tế.

### 🎯 Mục tiêu giải quyết:

* **Số hóa quy trình đánh giá:** Thay thế biểu mẫu giấy truyền thống bằng bài kiểm tra tương tác trực tuyến (Self-Assessment).

* **Phân loại tự động (Traffic-Light Zone):** Đánh giá tức thì mức độ nghiêm trọng (🟢 **Green** / 🟡 **Amber** / 🔴 **Red**) dựa trên chỉ số Đau (Pain) và Chức năng khớp (Function) để ưu tiên chăm sóc.

* **Tương tác Real-time:** Kênh trao đổi trực tiếp giữa Bệnh nhân và Bác sĩ/Nhân viên y tế qua hệ thống Chat đa phương tiện (Text, Ảnh, Sticker, Reaction, Read Receipt, Chuỗi ngày tương tác - Streak).

* **Theo dõi & Tự động hóa:** Cung cấp Dashboard phân tích số liệu trực quan cho phòng khám và hệ thống Cronjob tự động nhắc nhở bệnh nhân tái đánh giá qua Email & Push Notification (FCM).

## 🎥 Video Demo

*([**Link Video Demo Google Drive**](https://drive.google.com/file/d/149VNcCCXVGMD3Jn9N_d0Y7JyDEgF6ZZ-/view?usp=drive_link))*

## 📦 Cấu trúc dự án (Repositories)

Hệ thống được thiết kế theo kiến trúc tách biệt gồm **1 Backend API trung tâm** và **3 ứng dụng Frontend chuyên biệt**:

| **#** | **Tên thành phần** | **Link Repository** | **Công nghệ chính** | **Đối tượng & Vai trò** | 
| **1** | **API Server** | [🔗 knee-rehab-program-api](https://github.com/MinhTuNguyen02/knee-rehab-program-api) | NestJS 11, TypeORM, PostgreSQL, Socket.IO, FCM | Xử lý toàn bộ Business Logic, RESTful API, WebSocket Gateway, Cron Jobs & Dual Auth. | 
| **2** | **Web Assessment** | [🔗 knee-rehab-program-assess](https://github.com/MinhTuNguyen02/knee-rehab-program-assess) | Next.js 16, React 19, TailwindCSS 4 | Cổng đánh giá sức khỏe đầu gối công khai (Public), phân loại Zone và thu thập thông tin Opt-in. | 
| **3** | **Clinical Portal** | [🔗 knee-rehab-program-clinical-portal](https://github.com/MinhTuNguyen02/knee-rehab-program-clinical-portal) | Next.js 16, SWR, Recharts, Socket.IO Client | Cổng quản trị dành cho Bác sĩ/Admin: Xem thống kê, quản lý bệnh nhân (Leads), nhân sự & Chat. | 
| **4** | **Patient Portal** | [🔗 knee-rehab-program-patient-portal](https://github.com/MinhTuNguyen02/knee-rehab-program-patient-portal) | Next.js 16, shadcn/ui, SWR, Socket.IO Client | Cổng cá nhân của Bệnh nhân: Theo dõi lịch sử phục hồi, biểu đồ tiến triển và nhắn tin với bác sĩ. | 

## 🏗️ Kiến trúc hệ thống

```
                         ┌─────────────────────────────┐
                         │       Web Assessment        │
                         │     (Next.js - Public)      │
                         └──────────────┬──────────────┘
                                        │ REST API
     ┌──────────────────┐               ▼               ┌──────────────────┐
     │  Clinical Portal │◄──────── REST + WS ─────────► │    API Server    │
     │    (Next.js)     │                               │     (NestJS)     │
     │   Staff/Admin    │                               │                  │
     └──────────────────┘                               │  ┌────────────┐  │
                                                        │  │ PostgreSQL │  │
     ┌──────────────────┐                               │  └────────────┘  │
     │  Patient Portal  │◄──────── REST + WS ─────────► │  ┌────────────┐  │
     │    (Next.js)     │                               │  │ Cloudinary │  │
     │     Patients     │                               │  └────────────┘  │
     └──────────────────┘                               │  ┌────────────┐  │
                                                        │  │  Firebase  │  │
                                                        │  │   (FCM)    │  │
                                                        │  └────────────┘  │
                                                        │  ┌────────────┐  │
                                                        │  │    SMTP    │  │
                                                        │  │  (Mailer)  │  │
                                                        │  └────────────┘  │
                                                        └──────────────────┘

```

## ✨ Tính năng nổi bật

### 1. 📋 Web Assessment (Public Site)

* **Interactive Sliders:** Tự đánh giá mức độ đau (Pain 0–5) và chức năng khớp (Function 0–5), tính điểm theo thời gian thực.

* **Traffic-Light Classification:** Tự động xếp loại kết quả vào vùng 🟢 Xanh / 🟡 Vàng / 🔴 Đỏ kèm khuyến nghị y tế tương ứng.

* **Opt-in Flow & Onboarding:** Đăng ký tham gia chương trình (hỗ trợ cả bệnh nhân mới và tái khám), tự động khởi tạo hồ sơ và gửi Email chào mừng kèm mật khẩu tạm thời.

### 2. 👨‍⚕️ Clinical Portal (Dành cho Staff / Admin)

* **Analytics Dashboard:** Thống kê tổng lượt đánh giá, tỷ lệ chuyển đổi (Opt-in conversion rate), biểu đồ phân bổ theo Zone và lịch sử hoạt động 7 ngày gần nhất.

* **Quản lý Hồ sơ & Đánh giá:** Tra cứu danh sách bài đánh giá và hồ sơ bệnh nhân (Leads) với bộ lọc thông minh và phân trang **Cursor-based pagination** tối ưu hiệu năng.

* **Quản lý Nhân sự:** Phân quyền, kích hoạt/vô hiệu hóa tài khoản nhân viên và hỗ trợ xuất dữ liệu ra file Excel (`.xlsx`).

* **Real-time Inbox:** Giao diện quản lý hội thoại tập trung, hỗ trợ phản hồi bệnh nhân tức thì.

### 3. 🧑‍🦽 Patient Portal (Dành cho Bệnh nhân)

* **Theo dõi Tiến độ:** Biểu đồ trực quan hóa quá trình phục hồi qua các lần đánh giá, xem lại chi tiết lịch sử từng bài kiểm tra.

* **Bảo mật Tài khoản:** Cơ chế bắt buộc đổi mật khẩu trong lần đăng nhập đầu tiên (Force Change Password), khôi phục mật khẩu qua Email.

* **Tùy chỉnh Thông báo:** Chủ động bật/tắt nhận thông báo nhắc nhở tái khám định kỳ.

### 4. 💬 Hệ thống Giao tiếp & Điểm nhấn Kỹ thuật (Backend & Real-time)

* **Real-time Chat toàn diện (Socket.IO):**

  * Kiến trúc chia phòng (`Room-based`) kết hợp xác thực JWT ngay tại bước Handshake.

  * Đầy đủ tính năng hiện đại: Gửi văn bản, hình ảnh (tối ưu qua CDN), Sticker, Emoji Reactions, trả lời tin nhắn (`Reply-to`), trạng thái đang nhập (`Typing indicator`), đã xem (`Read receipts`) và trạng thái Online/Offline.

  * **Chat Streak:** Tính chuỗi ngày tương tác liên tiếp giữa bệnh nhân và nhân viên y tế.

  * **Virtualized List:** Ứng dụng `@tanstack/react-virtual` và Optimistic UI giúp cuộn hàng nghìn tin nhắn mượt mà không độ trễ.

* **Dual Authentication System:** Tách biệt hoàn toàn 2 luồng xác thực `StaffJwtStrategy` và `PatientJwtStrategy` cùng các Guard riêng biệt, ngăn chặn tuyệt đối việc leo thang đặc quyền.

* **Đa kênh Thông báo (Multi-channel Notifications):**

  * **Push Notification (FCM):** Hỗ trợ đa thiết bị (Multicast), tự động dọn dẹp token hết hạn.

  * **Automated Cron Jobs:** Tự động gửi email nhắc tái khám (Ngày 14 & Ngày 30), dọn dẹp thông báo cũ sau 30 ngày và cập nhật chuỗi Streak mỗi ngày.

## 🛠️ Công nghệ sử dụng

### **Backend (`knee-rehab-program-api`)**

* **Core Framework:** NestJS v11 (Modular Architecture, Dependency Injection)

* **Database & ORM:** PostgreSQL, TypeORM v0.3

* **Real-time:** Socket.IO (`@nestjs/websockets`)

* **Security & Auth:** Passport JWT (Dual Strategy), Bcrypt, Helmet, Rate Limiting (`@nestjs/throttler`), CORS Whitelist, Input Sanitization (`class-validator`, `escape-html`)

* **Services & Utilities:** Firebase Admin SDK (FCM), Cloudinary (Stream Media Upload), Nodemailer (`@nestjs-modules/mailer`), `@nestjs/schedule` (Cron), `xlsx`, Swagger/OpenAPI.

### **Frontend (3 Ứng dụng Next.js)**

* **Core:** Next.js 16 (App Router, API Proxy Routes), React 19, TypeScript

* **Styling & UI:** TailwindCSS v4, shadcn/ui, Radix UI, Lucide & Phosphor Icons

* **State & Data Fetching:** SWR v2 (Stale-While-Revalidate), Socket.IO Client v4

* **Forms & Visualization:** React Hook Form, Recharts v3, `@tanstack/react-virtual`, `emoji-picker-react`, `react-hot-toast`.

## 🚀 Hướng dẫn khởi chạy tổng quan

Để chạy toàn bộ hệ thống ở môi trường Local, vui lòng clone các repository tương ứng và khởi chạy theo thứ tự sau:

1. **Khởi chạy Backend (`knee-rehab-program-api`):**

   * Cấu hình biến môi trường `.env` (PostgreSQL, JWT Secrets, Cloudinary, Firebase, SMTP).

   * Chạy migration/khởi tạo database và khởi động server.

   * Xem tài liệu Swagger API tại: `http://localhost:<PORT>/api`

2. **Khởi chạy 3 ứng dụng Frontend:**

   * Cấu hình `.env.local` trỏ tới URL của API Server và Firebase Config.

   * Chạy `npm install && npm run dev` trên từng ứng dụng (`assess`, `clinical-portal`, `patient-portal`).

*(Chi tiết cài đặt và biến môi trường của từng phần được hướng dẫn cụ thể trong file `README.md` của từng repository con).*
