# Hướng dẫn Deploy lên Render

## Yêu cầu
- Tài khoản GitHub (https://github.com)
- Tài khoản Render (https://render.com)

## Các bước Deploy

### 1. Tạo Repository GitHub

#### Step 1: Tạo repository mới
1. Vào https://github.com/new
2. Điền thông tin:
   - **Repository name**: `locket-onl` (hoặc tên khác tùy ý)
   - **Description**: `Share real-time photos with close friends`
   - **Public/Private**: Chọn Public (để Render có thể access)
   - **Initialize**: Chọn "Add .gitignore" → "Node"
3. Nhấp "Create repository"

#### Step 2: Push code lên GitHub
```bash
# Đặt remote URL
git remote add origin https://github.com/YOUR_USERNAME/locket-onl.git

# Đặt default branch là main (nếu cần)
git branch -M main

# Push code lên
git push -u origin main
```

**Lưu ý**: Thay `YOUR_USERNAME` bằng username GitHub của bạn

#### Step 3: Thiết lập SSH (tùy chọn, nhưng khuyến nghị)
Nếu bạn muốn tránh nhập password mỗi lần push:
```bash
# Tạo SSH key (nếu chưa có)
ssh-keygen -t ed25519 -C "your_email@example.com"

# Copy key vào GitHub Settings → SSH and GPG keys
```

### 2. Tạo Web Service trên Render

1. **Đăng nhập vào Render Dashboard**: https://dashboard.render.com
2. **Nhấp vào "New +"** → Chọn **"Web Service"**
3. **Kết nối GitHub Repository**:
   - Chọn repository `Client-Locket-Dio-1.4.0`
   - Chọn branch (thường là `main`)

### 3. Cấu hình Deploy

Điền các thông tin sau:

| Trường | Giá trị |
|-------|--------|
| **Name** | `locket-dio` (hoặc tên khác) |
| **Environment** | `Node` |
| **Build Command** | `npm install && npm run build` |
| **Start Command** | `npm start` |
| **Plan** | `Free` (hoặc paid) |

### 4. Thêm Environment Variables (nếu cần)

Nếu ứng dụng cần các biến môi trường (API keys, Firebase config, v.v.):

1. Trong trang cấu hình Web Service, tìm phần **"Environment"**
2. Nhấp **"Add Environment Variable"**
3. Thêm các biến như:
   - `NODE_ENV` = `production`
   - `VITE_API_URL` = (URL API của bạn nếu có)
   - Các biến khác theo nhu cầu

### 5. Deploy

1. Nhấp **"Create Web Service"**
2. Render sẽ tự động build và deploy
3. Chờ quá trình hoàn thành (thường 5-10 phút)
4. Sau khi thành công, bạn sẽ nhận được URL public (ví dụ: `https://locket-dio.onrender.com`)

## Cấu hình Auto-Deploy

Render sẽ tự động deploy lại mỗi khi bạn push code mới lên branch đã chọn.

## Troubleshooting

### Lỗi Build
- Kiểm tra build logs trên Render dashboard
- Đảm bảo `npm install` chạy thành công
- Kiểm tra Node.js version: Render hỗ trợ Node 18+

### Ứng dụng Crash sau Deploy
- Kiểm tra logs: Nhấp vào **"Logs"** trong Web Service
- Kiểm tra Environment Variables có đầy đủ không
- Kiểm tra PORT binding trong `server.js`

### Ứng dụng không tải CSS/Assets
- Đảm bảo Vite build thành công
- Kiểm tra đường dẫn assets trong dist folder

## Các file đã tạo:

- `render.yaml` - Cấu hình deployment
- `apps/main/server.js` - Express server để serve static files
- Cập nhật `package.json` - Thêm Express dependency

## Ghi chú

- Render free plan sẽ sleep nếu không có request trong 15 phút
- Để production-ready, nên upgrade lên paid plan
- Mỗi deployment tương ứng với một commit/push lên GitHub
