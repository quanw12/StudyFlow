# StudyFlow - Hệ thống Quản lý Học tập Thông minh

**Tác giả:** Nguyễn Kiều Anh Quân  
**Mô tả:** Ứng dụng web hỗ trợ sinh viên tổ chức môn học, ghi chú thông minh và quản lý deadline một cách hiệu quả.

---

## Giới thiệu

StudyFlow là nền tảng quản lý học tập toàn diện, tích hợp:
- Quản lý môn học theo ngữ cảnh
- Hệ thống ghi chú thông minh với tìm kiếm nhanh
- Quản lý công việc và deadline
- Theo dõi tiến độ học tập trực quan

---

## Tính năng chính

### 1. Quản lý Môn học & Ghi chú
- **Không gian theo môn học:** Tạo danh mục riêng cho từng môn
- **Kho lưu trữ tài liệu:** Upload PDF, lưu link YouTube bài giảng
- **Ghi chú thông minh:** Ghi chép theo môn với tìm kiếm nhanh

### 2. Quản lý Nhiệm vụ (Task Management)
- **Chi tiết Task:** Priority, deadline, trạng thái
- **Thao tác linh hoạt:** Thêm/sửa/xoá, kéo-thả (drag-and-drop)
- **Bộ lọc & Sắp xếp:** Theo ngày, ưu tiên, môn học
- **Nhắc lịch tự động:** Thông báo khi sắp đến deadline

### 3. Thống kê & Báo cáo
- **Dashboard:** Biểu đồ thống kê tiến độ học tập
- **Xuất dữ liệu:** CSV/PDF
- **Phân loại độ khó:** Môn học được phân loại để ưu tiên xử lý

### 4. Trải nghiệm người dùng
- **Dark mode:** Hỗ trợ học tập ban đêm
- **Giao diện thân thiện:** Dễ sử dụng, trực quan
- **Tìm kiếm nhanh:** Tra cứu kiến thức tức thì

---

## Công nghệ sử dụng

| Thành phần       | Công nghệ                    |
|------------------|------------------------------|
| **Frontend**     | React                        |
| **Backend**      | FastAPI (Python)             |
| **Database**     | Cloud Firestore              |
| **Xác thực**     | Firebase Authentication      |
| **Hosting**      | Render/Vercel (dự kiến)      |

---

## Chức năng

### Cơ bản
- ✅ Đăng nhập / Đăng xuất (Firebase Auth)
- ✅ Quản lý môn học (CRUD)
- ✅ Ghi chú theo từng môn
- ✅ Deadline bài tập / lịch thi
- ✅ Đánh dấu hoàn thành
- ✅ Tìm kiếm nhanh

### Nâng cao
- Thống kê tiến độ học tập
- Upload PDF / link tài liệu
- Dark mode
- Phân loại độ khó môn học

---

## Hướng dẫn cài đặt

### Yêu cầu hệ thống
- **Python:** >= 3.8
- **Node.js:** >= 16.0.0
- **npm/yarn:** phiên bản mới nhất
- **Git:** để clone dự án
- **Tài khoản Firebase:** Để cấu hình Firestore và Authentication

### Bước 1: Thiết lập Firebase Project

1. Truy cập [Firebase Console](https://console.firebase.google.com/)
2. Tạo project mới hoặc chọn project có sẵn
3. Kích hoạt **Firebase Authentication**
   - Bật phương thức đăng nhập: Email/Password, Google, v.v.
4. Tạo **Cloud Firestore Database**
   - Chọn chế độ: Start in test mode (development) hoặc Production mode
   - Chọn vùng: `asia-southeast1` (Singapore) hoặc gần nhất
5. Tạo **Service Account** cho Backend:
   - Vào Project Settings → Service Accounts
   - Click "Generate new private key"
   - Lưu file JSON (sẽ dùng cho Backend)
6. Lấy Firebase Config cho Frontend:
   - Vào Project Settings → General
   - Scroll xuống "Your apps" → chọn Web app
   - Copy Firebase configuration object

### Bước 2: Cài đặt Backend

```bash
# Clone repository
git clone https://github.com/quanw12/StudyFlow
cd StudyFlow/Backend

# Tạo môi trường ảo (khuyến nghị)
python -m venv venv

# Kích hoạt môi trường ảo
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Cài đặt dependencies
pip install -r requirements.txt
```

**Tạo file `.env` trong thư mục `Backend/`:**

```env
# Firebase Service Account
FIREBASE_CREDENTIALS_PATH=./path/to/serviceAccountKey.json

# App Config
SECRET_KEY=your-secret-key-here
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

**Cài đặt Firebase Admin SDK:**

```bash
pip install firebase-admin
```

### Bước 3: Cài đặt Frontend

```bash
# Mở terminal mới
cd StudyFlow/Frontend

# Cài đặt dependencies
npm install
# hoặc
yarn install

# Cài đặt Firebase SDK
npm install firebase
# hoặc
yarn add firebase
```

**Tạo file `.env.local` trong thư mục `Frontend/`:**

```env
REACT_APP_API_URL=http://localhost:8000
REACT_APP_FIREBASE_API_KEY=your-api-key
REACT_APP_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
REACT_APP_FIREBASE_PROJECT_ID=your-project-id
REACT_APP_FIREBASE_STORAGE_BUCKET=your-project.appspot.com
REACT_APP_FIREBASE_MESSAGING_SENDER_ID=your-sender-id
REACT_APP_FIREBASE_APP_ID=your-app-id
```

**Tạo file `src/firebase/config.js`:**

```javascript
import { initializeApp } from 'firebase/app';
import { getAuth } from 'firebase/auth';
import { getFirestore } from 'firebase/firestore';

const firebaseConfig = {
  apiKey: process.env.REACT_APP_FIREBASE_API_KEY,
  authDomain: process.env.REACT_APP_FIREBASE_AUTH_DOMAIN,
  projectId: process.env.REACT_APP_FIREBASE_PROJECT_ID,
  storageBucket: process.env.REACT_APP_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: process.env.REACT_APP_FIREBASE_MESSAGING_SENDER_ID,
  appId: process.env.REACT_APP_FIREBASE_APP_ID
};

const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
export const db = getFirestore(app);
```

### Bước 4: Khởi động ứng dụng

**Terminal 1 - Backend:**
```bash
cd StudyFlow/Backend
# Kích hoạt venv nếu chưa
venv\Scripts\activate  # Windows
# source venv/bin/activate  # Linux/Mac

# Khởi động FastAPI server
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

**Terminal 2 - Frontend:**
```bash
cd StudyFlow/Frontend

# Khởi động React app
npm start
# hoặc
yarn start
```

Ứng dụng sẽ chạy tại:
- **Frontend:** http://localhost:3000
- **Backend API:** http://localhost:8000
- **API Documentation:** http://localhost:8000/docs

---

## Cấu trúc dự án

```
StudyFlow/
├── Backend/
│   ├── main.py                   # FastAPI entry point
│   ├── config/
│   │   ├── firebase.py           # Firebase Admin initialization
│   │   └── settings.py           # App settings
│   ├── models/                   # Pydantic models
│   ├── routes/                   # API endpoints
│   │   ├── auth.py               # Authentication routes
│   │   ├── subjects.py           # Subject management
│   │   ├── notes.py              # Notes management
│   │   └── tasks.py              # Tasks management
│   ├── services/
│   │   ├── auth_service.py       # Firebase Auth integration
│   │   └── firestore_service.py  # Firestore operations
│   ├── middleware/               # Auth middleware
│   ├── utils/                    # Helper functions
│   ├── requirements.txt          # Python dependencies
│   ├── .env                      # Environment variables (gitignore)
│   └── serviceAccountKey.json    # Firebase credentials (gitignore)
│
├── Frontend/
│   ├── public/                   # Static files
│   ├── src/
│   │   ├── components/           # React components
│   │   ├── pages/                # Page components
│   │   ├── firebase/
│   │   │   ├── config.js         # Firebase client config
│   │   │   └── auth.js           # Firebase Auth (client)
│   │   ├── services/
│   │   │   └── api.js            # Backend API calls
│   │   ├── hooks/                # Custom hooks
│   │   ├── context/              # Context providers
│   │   ├── utils/                # Helper functions
│   │   ├── styles/               # CSS/SCSS files
│   │   └── App.js                # Main App component
│   ├── .env.local                # Config (gitignore)
│   └── package.json              # Node dependencies
│
├── README.md                     # Tài liệu dự án
├── classDiagram.md               # Sơ đồ lớp
└── LICENSE                       # Giấy phép
```

---

## Kiến trúc & Luồng hoạt động

### Luồng Authentication
1. **Frontend:** User đăng nhập qua Firebase Auth (Client SDK)
2. **Frontend:** Lấy ID Token từ Firebase
3. **Frontend:** Gửi request kèm ID Token trong header đến Backend
4. **Backend:** Verify ID Token bằng Firebase Admin SDK
5. **Backend:** Trả về dữ liệu nếu token hợp lệ

## Firebase Services & Collections

### Firebase Authentication (Client-side)
Frontend sử dụng Firebase Auth:
- `createUserWithEmailAndPassword()` - Đăng ký
- `signInWithEmailAndPassword()` - Đăng nhập
- `signOut()` - Đăng xuất
- `onAuthStateChanged()` - Lắng nghe trạng thái
- `getIdToken()` - Lấy token gửi cho Backend

### Firestore Collections

#### Collection: `users`
```javascript
{
  uid: "user-id",
  email: "user@example.com",
  displayName: "Tên người dùng",
  createdAt: timestamp,
  settings: { theme: "dark", notifications: true }
}
```

#### Collection: `subjects`
```javascript
{
  id: "subject-id",
  userId: "user-id",
  name: "Cấu trúc dữ liệu và giải thuật",
  code: "CSC10004",
  credits: 4,
  difficulty: "hard", // easy, medium, hard
  color: "#FF6B6B",
  createdAt: timestamp,
  updatedAt: timestamp
}
```

#### Collection: `notes`
```javascript
{
  id: "note-id",
  userId: "user-id",
  subjectId: "subject-id",
  title: "Chương 1: Giới thiệu",
  content: "Nội dung ghi chú...",
  tags: ["introduction", "theory"],
  attachments: [{ type: "pdf", url: "...", name: "slide.pdf" }],
  createdAt: timestamp,
  updatedAt: timestamp
}
```

#### Collection: `tasks`
```javascript
{
  id: "task-id",
  userId: "user-id",
  subjectId: "subject-id",
  title: "Bài tập tuần 5",
  description: "Hoàn thành bài tập về cây nhị phân",
  priority: "high", // low, medium, high
  status: "todo", // todo, in-progress, done
  deadline: timestamp,
  completed: false,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

### Firestore Security Rules (Dự kiến)

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users collection
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    
    // Subjects collection
    match /subjects/{subjectId} {
      allow read, write: if request.auth != null && 
                            request.auth.uid == resource.data.userId;
    }
    
    // Notes collection
    match /notes/{noteId} {
      allow read, write: if request.auth != null && 
                            request.auth.uid == resource.data.userId;
    }
    
    // Tasks collection
    match /tasks/{taskId} {
      allow read, write: if request.auth != null && 
                            request.auth.uid == resource.data.userId;
    }
  }
}
```

---

## Screenshots

_Screenshots sẽ được cập nhật sau khi hoàn thành giao diện_

---

## API Endpoints

### Authentication
- `POST /api/auth/register` - Đăng ký (tạo user trong Firestore)
- `POST /api/auth/verify` - Verify Firebase token
- `GET /api/auth/me` - Lấy thông tin user (cần token)

### Subjects
- `GET /api/subjects` - Lấy danh sách môn học
- `POST /api/subjects` - Tạo môn học mới
- `GET /api/subjects/{id}` - Chi tiết môn học
- `PUT /api/subjects/{id}` - Cập nhật môn học
- `DELETE /api/subjects/{id}` - Xóa môn học

### Notes
- `GET /api/notes` - Lấy danh sách ghi chú
- `POST /api/notes` - Tạo ghi chú mới
- `GET /api/notes/{id}` - Chi tiết ghi chú
- `PUT /api/notes/{id}` - Cập nhật ghi chú
- `DELETE /api/notes/{id}` - Xóa ghi chú
- `GET /api/notes/search?q={query}` - Tìm kiếm

### Tasks
- `GET /api/tasks` - Lấy danh sách task
- `POST /api/tasks` - Tạo task mới
- `GET /api/tasks/{id}` - Chi tiết task
- `PUT /api/tasks/{id}` - Cập nhật task
- `DELETE /api/tasks/{id}` - Xóa task
- `PATCH /api/tasks/{id}/status` - Cập nhật trạng thái

---

## Testing

```bash
# Backend tests
cd Backend
pytest

# Frontend tests
cd Frontend
npm test
# hoặc
yarn test
```

---

## Đóng góp

Mọi đóng góp đều được hoan nghênh! Để đóng góp:

1. Fork dự án
2. Tạo branch mới (`git checkout -b feature/TenTinhNang`)
3. Commit thay đổi (`git commit -m 'Thêm tính năng XYZ'`)
4. Push lên branch (`git push origin feature/TenTinhNang`)
5. Tạo Pull Request

### Quy tắc code
- **Backend:** Tuân thủ PEP 8 cho Python code
- **Frontend:** Sử dụng ESLint cho JavaScript/React
- **Firebase:** Bảo mật Firestore Security Rules
- Viết tests cho các tính năng mới
- Cập nhật documentation khi cần
- Không commit `.env`, `serviceAccountKey.json`

---

## Roadmap

- [x] Thiết kế cơ sở dữ liệu Firestore
- [x] Setup project structure
- [x] Cấu hình Firebase project
- [ ] Xây dựng FastAPI Backend
  - [ ] Setup Firebase Admin SDK
  - [ ] Auth middleware với Firebase token
  - [ ] CRUD APIs cho Subjects, Notes, Tasks
- [ ] Xây dựng Frontend UI
  - [ ] Firebase Auth integration
  - [ ] API calls đến Backend
  - [ ] Protected routes
- [ ] Tìm kiếm nâng cao
- [ ] Responsive design
- [ ] Testing & Bug fixes
- [ ] Deploy Backend (Render) & Frontend (Vercel)

---

## License

Dự án này được phân phối dưới giấy phép MIT. Xem file [LICENSE](LICENSE) để biết thêm chi tiết.

---

## Tác giả

**Nguyễn Kiều Anh Quân**

- GitHub: [@quanw12](https://github.com/quanw12)
- Email: nguyenkieuanhquan12@gmail.com

---

## Acknowledgments

- Cảm ơn các thư viện mã nguồn mở được sử dụng trong dự án
- Cảm ơn cộng đồng developers đã hỗ trợ và đóng góp ý kiến

---

## Liên hệ & Hỗ trợ

Nếu bạn có câu hỏi hoặc gặp vấn đề, vui lòng:
- Tạo [Issue](https://github.com/quanw12/StudyFlow/issues) trên GitHub
- Gửi email đến: nguyenkieuanhquan12@gmail.com

---

<div align="center">
  
**⭐ Nếu dự án hữu ích, hãy cho một ngôi sao! ⭐**

</div>