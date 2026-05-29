# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Oxc](https://oxc.rs)
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/)

## React Compiler

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.
# PlaceGuide Frontend

## 1. Giới thiệu

Đây là phần frontend của hệ thống **PlaceGuide**.

PlaceGuide là web app hỗ trợ khách du lịch tìm kiếm quán ăn, xem thông tin quán, xem menu, nghe thuyết minh món ăn/quán ăn, lựa chọn món phù hợp, đặt món, thanh toán và đánh giá dịch vụ.

Frontend được xây dựng bằng **React + Vite** và kết nối với backend ASP.NET Core Web API.

---

## 2. Công nghệ sử dụng

Frontend sử dụng các công nghệ chính:

* React
* Vite
* JavaScript
* React Router DOM
* Axios
* TanStack React Query
* Zustand
* Lucide React

---

## 3. Yêu cầu cài đặt trước

Trước khi chạy frontend, máy cần cài:

### 3.1 Node.js

Kiểm tra Node.js:

```powershell
node -v
```

### 3.2 npm

Kiểm tra npm:

```powershell
npm -v
```

Nếu cả hai lệnh đều hiển thị phiên bản thì có thể chạy frontend.

---

## 4. Cấu trúc thư mục frontend

Thư mục frontend nằm trong project chính:

```text
PlaceGuide
│
├── backend
│
└── frontend
```

Cấu trúc thư mục frontend hiện tại:

```text
frontend
│
├── public
├── src
│   ├── api
│   ├── assets
│   ├── components
│   │   ├── common
│   │   ├── restaurant
│   │   ├── dish
│   │   ├── order
│   │   ├── payment
│   │   ├── review
│   │   └── audio
│   │
│   ├── layouts
│   ├── pages
│   │   ├── auth
│   │   ├── tourist
│   │   ├── owner
│   │   └── admin
│   │
│   ├── routes
│   ├── store
│   ├── hooks
│   └── utils
│
├── .env
├── index.html
├── package.json
└── vite.config.js
```

---

## 5. Cài đặt thư viện cho frontend

Khi clone project hoặc nhận source code từ người khác, vào thư mục frontend:

```powershell
cd frontend
```

Sau đó cài toàn bộ package đã khai báo trong `package.json`:

```powershell
npm install
```

Lệnh này sẽ tự động tải thư viện về thư mục:

```text
node_modules
```

Không cần copy thủ công thư mục `node_modules`.

---

## 6. Các package chính đang sử dụng

Frontend sử dụng các package sau:

```powershell
npm install axios react-router-dom @tanstack/react-query zustand lucide-react
```

Ý nghĩa từng package:

| Package                 | Mục đích                              |
| ----------------------- | ------------------------------------- |
| `axios`                 | Gọi API từ backend                    |
| `react-router-dom`      | Điều hướng giữa các trang             |
| `@tanstack/react-query` | Quản lý dữ liệu lấy từ API            |
| `zustand`               | Quản lý state như đăng nhập, giỏ hàng |
| `lucide-react`          | Sử dụng icon trong giao diện          |

---

## 7. File cấu hình môi trường

Frontend sử dụng file `.env` để lưu đường dẫn API backend.

File `.env` nằm trong thư mục:

```text
frontend/.env
```

Nội dung:

```env
VITE_API_BASE_URL=http://localhost:5096/api
```

Trong đó:

| Biến môi trường     | Ý nghĩa               |
| ------------------- | --------------------- |
| `VITE_API_BASE_URL` | Đường dẫn API backend |

Nếu backend chạy ở port khác, cần sửa lại port trong file `.env`.

Ví dụ backend chạy ở port `5000`:

```env
VITE_API_BASE_URL=http://localhost:5000/api
```

---

## 8. Chạy frontend ở môi trường development

Tại thư mục `frontend`, chạy:

```powershell
npm run dev
```

Nếu chạy thành công, terminal sẽ hiển thị dạng:

```text
Local: http://localhost:5173/
```

Mở trình duyệt và truy cập:

```text
http://localhost:5173
```

---

## 9. Build frontend

Khi cần build frontend để kiểm tra lỗi hoặc chuẩn bị deploy, chạy:

```powershell
npm run build
```

Sau khi build thành công, thư mục kết quả sẽ được tạo tại:

```text
frontend/dist
```

---

## 10. Chạy bản build preview

Sau khi build, có thể chạy thử bản build bằng lệnh:

```powershell
npm run preview
```

Terminal sẽ hiển thị một địa chỉ local để mở bản preview.

---

## 11. Các script trong package.json

Các script thường dùng:

| Lệnh              | Công dụng                              |
| ----------------- | -------------------------------------- |
| `npm run dev`     | Chạy frontend ở môi trường development |
| `npm run build`   | Build frontend                         |
| `npm run preview` | Chạy thử bản đã build                  |
| `npm install`     | Cài toàn bộ package cần thiết          |

---

## 12. Quy trình chạy frontend sau khi nhận source code

Người code sau thực hiện theo thứ tự:

```powershell
cd frontend
npm install
npm run dev
```

Sau đó mở trình duyệt tại địa chỉ mà terminal hiển thị, thường là:

```text
http://localhost:5173
```

---

## 13. Kết nối frontend với backend

Frontend cần backend chạy song song để gọi API.

Chạy backend trước:

```powershell
dotnet run --project backend\PlaceGuide.Api
```

Backend thường chạy tại:

```text
http://localhost:5096
```

Sau đó chạy frontend:

```powershell
cd frontend
npm run dev
```

Frontend thường chạy tại:

```text
http://localhost:5173
```

---

## 14. Lưu ý khi làm việc nhóm

Không commit thư mục:

```text
node_modules
dist
```

Các thư mục này có thể tạo lại bằng lệnh:

```powershell
npm install
npm run build
```

Nên commit các file quan trọng:

```text
package.json
package-lock.json
vite.config.js
.env.example
src
public
```

Nếu không muốn commit file `.env` thật, có thể tạo file mẫu:

```text
.env.example
```

Nội dung:

```env
VITE_API_BASE_URL=http://localhost:5096/api
```

Người nhận source sẽ copy `.env.example` thành `.env` và chỉnh lại cấu hình nếu cần.

---

## 15. Một số lỗi thường gặp

### 15.1 Lỗi `npm is not recognized`

Nguyên nhân: máy chưa cài Node.js hoặc chưa thêm Node.js vào PATH.

Cách xử lý:

* Cài Node.js.
* Mở lại terminal.
* Kiểm tra lại bằng lệnh:

```powershell
node -v
npm -v
```

---

### 15.2 Lỗi thiếu package

Nếu chạy project bị lỗi thiếu thư viện, chạy lại:

```powershell
npm install
```

---

### 15.3 Lỗi không truy cập được localhost

Nếu truy cập:

```text
http://localhost:5173
```

nhưng trình duyệt báo từ chối kết nối, cần kiểm tra frontend đã chạy chưa.

Chạy lại:

```powershell
npm run dev
```

Sau đó mở đúng địa chỉ mà terminal hiển thị.

---

### 15.4 Frontend không gọi được backend

Kiểm tra backend đã chạy chưa:

```powershell
dotnet run --project backend\PlaceGuide.Api
```

Kiểm tra file `.env`:

```env
VITE_API_BASE_URL=http://localhost:5096/api
```

Nếu backend đổi port thì sửa lại port trong `.env`.

Sau khi sửa `.env`, cần dừng frontend và chạy lại:

```powershell
npm run dev
```

---

## 16. Trạng thái hiện tại của frontend

Frontend hiện tại mới ở giai đoạn tạo khung.

Đã có:

* Project React + Vite.
* Cấu trúc thư mục cơ bản.
* File `.env`.
* Các package cần thiết cho routing, gọi API và quản lý state.

Chưa thực hiện:

* Chưa xây dựng giao diện chi tiết.
* Chưa tạo đầy đủ page.
* Chưa kết nối API thật.
* Chưa xử lý đăng nhập.
* Chưa xử lý giỏ hàng thật.
* Chưa xây dựng dashboard chủ quán.
* Chưa xây dựng trang admin.

---

## 17. Thứ tự phát triển frontend dự kiến

Thứ tự phát triển đề xuất:

```text
1. Tạo router chính.
2. Tạo layout cho khách du lịch, chủ quán và admin.
3. Tạo trang chủ.
4. Tạo trang danh sách quán ăn.
5. Tạo trang chi tiết quán ăn.
6. Tạo trang menu và món ăn.
7. Tạo giỏ hàng.
8. Tạo đăng nhập, đăng ký.
9. Tạo dashboard chủ quán.
10. Tạo trang quản lý admin.
11. Kết nối API backend.
12. Hoàn thiện giao diện và kiểm thử.
```

Frontend sẽ được phát triển theo từng module để dễ kiểm soát và dễ kết nối với backend.
