# 🚀 Hướng dẫn Deploy locket-onl lên Render

## 📋 Yêu cầu
- Tài khoản GitHub: https://github.com
- Tài khoản Render: https://render.com

---

## ✅ Bước 1: Tạo Repository GitHub

### 1.1 Tạo repo mới
Truy cập: https://github.com/new

Điền thông tin:
- **Repository name**: `locket-onl`
- **Description**: `Share real-time photos with close friends`
- **Visibility**: `Public`
- **Initialize**: Để trống (không chọn)

Nhấp **"Create repository"**

### 1.2 Push code lên GitHub

Chạy các lệnh này trong Terminal:

```bash
# Di chuyển vào folder dự án
cd "c:\Users\nhanvu\OneDrive\Desktop\Client-Locket-Dio-1.4.0"

# Thiết lập remote (thay YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/locket-onl.git
git branch -M main

# Push code
git push -u origin main
```

Nhập GitHub username và token khi được hỏi.

---

## 🌐 Bước 2: Deploy trên Render

### 2.1 Kết nối Repository

1. Đăng nhập: https://dashboard.render.com
2. Nhấp **"New +"** → **"Web Service"**
3. Chọn **"Connect a repository"**
4. Tìm và chọn repository `locket-onl`
5. Nhấp **"Connect"**

### 2.2 Cấu hình Deployment

Điền các thông tin sau:

| Trường | Giá trị |
|--------|--------|
| **Name** | `locket-onl` |
| **Environment** | `Node` |
| **Region** | Chọn gần bạn nhất |
| **Build Command** | `npm install && npm run build` |
| **Start Command** | `npm start` |

### 2.3 Chọn Plan

- **Free Plan**: $0/tháng (sleeping after 15 min inactivity)
- **Paid Plan**: $7+/tháng (always running)

### 2.4 Deploy

Nhấp **"Create Web Service"** và chờ 5-10 phút.

**✅ Thành công!** Bạn sẽ nhận được URL: `https://locket-onl-XXXXX.onrender.com`

---

## 📝 Sau khi Deploy

### Auto-Deploy (Tự động deploy mỗi khi push)

```bash
# Chỉ cần push code bình thường
git add .
git commit -m "Update feature"
git push origin main
```

Render sẽ tự động build và deploy!

### Xem Logs

- Trong Render Dashboard → Logs tab
- Kiểm tra build progress và errors

---

## 🆘 Troubleshooting

### ❌ Build Failed

**Lỗi**: "npm: command not found" hoặc "vite: command not found"

**Giải pháp**:
- Kiểm tra Node.js version (phải ≥ 18)
- Chạy lại `npm install` trước khi deploy
- Kiểm tra `package.json` có hợp lệ không

### ❌ Application keeps restarting

**Nguyên nhân**: Server crash

**Giải pháp**:
- Xem Logs tab để tìm error
- Kiểm tra port binding (mặc định 3000)
- Đảm bảo `server.js` chạy được

### ❌ CSS/JavaScript không load

**Nguyên nhân**: Asset path không đúng

**Giải pháp**:
- Kiểm tra `dist/` folder tồn tại
- Verify build output: `npm run build` trên máy local
- Kiểm tra Express middleware trong `server.js`

### ❌ Timeout

**Nguyên nhân**: Build quá lâu

**Giải pháp**:
- Chờ thêm (có thể 10-15 phút)
- Nếu vẫn fail: Xóa node_modules, cài lại, push lại

---

## 📂 Files đã chuẩn bị

```
✅ render.yaml         - Cấu hình Render
✅ apps/main/server.js - Express server
✅ package.json        - Start script
```

---

## 💡 Mẹo

1. **Reduce deploy time**: Thêm `.renderignore` để loại bỏ files không cần thiết
2. **Monitor**: Render gửi email khi deploy fail
3. **Custom domain**: Sau khi deploy, bạn có thể thêm custom domain

---

## 📞 Hỗ trợ

- Render Docs: https://render.com/docs
- GitHub Issues: Báo cáo lỗi trên repository
- Render Support: https://support.render.com

---

**Bước tiếp theo**: Sau khi deploy thành công, hãy test website của bạn! 🎉
