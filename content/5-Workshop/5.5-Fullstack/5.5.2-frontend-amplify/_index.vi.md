---
title : "Deploy Frontend (Amplify)"
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

#### 1. Chuẩn bị GitLab Repository

Bạn cần đưa mã nguồn frontend lên GitLab cá nhân để Amplify có thể lấy code về build. Có 2 cách để thực hiện:
**Cách 1: Tạo Repo mới và Push code (Khuyên dùng)**
1.  Đăng nhập vào GitLab cá nhân và tạo một **New project/repository** (trống).
2.  Mở Terminal trên máy tính, di chuyển vào thư mục `frontend`:
    ```bash
    cd frontend
    ```
3.  Xóa cấu hình git cũ (nếu có):
    *   **Windows (PowerShell)**: `Remove-Item -Recurse -Force .git`
    *   **Mac/Linux**: `rm -rf .git`
4.  Khởi tạo git mới và đẩy code lên:
    ```bash
    git init
    git add .
    git commit -m "Initial deploy"
    git remote add origin <URL-Repo-GitLab-Cua-Ban>
    git branch -M main
    git push -uf origin main
    ```
**Cách 2: Fork từ Repo mẫu**
*   Truy cập: [https://gitlab.com/manh-25/contract-demo](https://gitlab.com/manh-25/contract-demo)
*   Bấm nút **Fork** để sao chép về tài khoản của bạn.
#### 2. Tạo App trên AWS Amplify
1.  Truy cập dịch vụ **AWS Amplify** trên Console.
2.  Kéo xuống dưới cùng trang, chọn **Create new app**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.33.png)
3.  Tại màn hình "Start building with Amplify", chọn **GitLab** -> Bấm **Next**.
4.  Kết nối tài khoản GitLab và chọn Repository bạn vừa push (nhánh `main`).
![alt text](/images/5-Workshop/5.3-Infrastructure/3.34.png)

#### 3. Cấu hình Build Settings
1.  Đặt tên cho App (App name).
2.  Trong phần **Build settings**, bấm nút **Edit YML file**.
![alt text](/images/5-Workshop/5.3-Infrastructure/3.35.png)

3.  Xóa toàn bộ nội dung mặc định và **Ghi đè (Paste)** đoạn code sau vào (để sử dụng `bun` giúp tốc độ build nhanh hơn):
```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - curl -fsSL https://bun.sh/install | bash
        - export BUN_INSTALL="$HOME/.bun"
        - export PATH="$BUN_INSTALL/bin:$PATH"
        - bun install
    build:
      commands:
        - export BUN_INSTALL="$HOME/.bun"
        - export PATH="$BUN_INSTALL/bin:$PATH"
        - bun run build
  artifacts:
    baseDirectory: dist
    files:
      - "**/*"
  cache:
    paths:
      - node_modules/**/*
```

#### 4. Cấu hình Biến môi trường
1.  Bấm vào **Advanced settings** -> Kéo xuống phần **Environment variables**.
2.  Bấm **Add new variable** để thêm lần lượt 4 biến sau.
3.  **Lấy giá trị (Value) ở đâu?** -> Hãy mở một tab trình duyệt khác để lấy thông tin:

    *   **Vào dịch vụ Amazon Cognito:** Chọn User Pool có tên `ai-contract-backend-user-pool-dev`.
        *   `VITE_COGNITO_REGION` = `ap-southeast-1`
        *   `VITE_COGNITO_USER_POOL_ID` = Copy **User pool ID**.
        *   `VITE_COGNITO_CLIENT_ID` = Vào tab **App integration**, kéo xuống dưới cùng copy **Client ID**.
  
    ![alt text](/images/5-Workshop/5.3-Infrastructure/3.36.png)

    *   **Vào dịch vụ Lambda:** Chọn hàm `ai-contract-backend-dev-api`.
        *   `VITE_API_URL` = Copy **API Endpoint** (trong phần Configuration -> Triggers hoặc API Gateway).

    ![alt text](/images/5-Workshop/5.3-Infrastructure/3.37.png) 
    ![alt text](/images/5-Workshop/5.3-Infrastructure/3.38.png)


4.  Sau khi điền đủ 4 biến, bấm **Next**.

#### 5. Deploy và Kiểm tra
1.  Tại màn hình Review, kiểm tra lại thông tin và bấm **Save and deploy**.
2.  Chờ khoảng 3-5 phút để Amplify thực hiện các bước: Provision -> Build -> Deploy.
3.  Khi cả 3 bước đều xanh, link truy cập ứng dụng sẽ hiện ra ở phần **Domain** (ví dụ: `https://main.d123...amplifyapp.com`).

👉 **Bấm vào link để trải nghiệm ứng dụng Smart Contract Assistant của bạn!**

 ![alt text](/images/5-Workshop/5.3-Infrastructure/3.39.png)