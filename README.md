# 🎂 Sinh nhật Duy Linh — Photo Sharing App

Ứng dụng chia sẻ ảnh real-time tại đêm tiệc. Khách chụp ảnh từ điện thoại → xuất hiện ngay trên màn hình chiếu.

## Cấu trúc

```
index.html          → duylinh.netlify.app/       (trang khách)
admin/index.html    → duylinh.netlify.app/admin  (màn hình chiếu)
```

---

## Bước 1 — Tạo Firebase project

1. Vào https://console.firebase.google.com → **Add project**
2. Đặt tên (ví dụ: `duylinh-birthday`) → tắt Google Analytics → **Create project**
3. Vào **Build → Firestore Database** → **Create database** → chọn **Start in test mode** → chọn region `asia-southeast1` → **Enable**
4. Vào **Build → Storage** → **Get started** → **Start in test mode** → **Done**
5. Vào **Project settings** (icon ⚙️) → **General** → cuộn xuống → **Add app** → chọn **Web** (`</>`)
6. Đặt tên app → **Register app** → copy đoạn `firebaseConfig`

---

## Bước 2 — Điền config vào code

Mở **cả hai file** sau và thay phần `firebaseConfig`:

- `index.html` (dòng ~140)
- `admin/index.html` (dòng ~110)

```js
const firebaseConfig = {
  apiKey:            "AIza...",        // ← thay bằng giá trị thật
  authDomain:        "duylinh-birthday.firebaseapp.com",
  projectId:         "duylinh-birthday",
  storageBucket:     "duylinh-birthday.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123:web:abc",
};
```

---

## Bước 3 — Deploy lên Netlify

### Cách 1: Kéo thả (nhanh nhất)
1. Vào https://app.netlify.com → **Add new site → Deploy manually**
2. Kéo thả **toàn bộ thư mục** `duylinh-birthday/` vào ô drop
3. Netlify tự deploy trong ~30 giây
4. Vào **Site configuration → Change site name** → đặt thành `duylinh`
5. Site sẽ có URL: `https://duylinh.netlify.app`

### Cách 2: Netlify CLI
```bash
npm i -g netlify-cli
netlify deploy --dir . --prod
```

---

## Bước 4 — Kiểm tra trước tiệc

1. Mở `https://duylinh.netlify.app/admin` trên máy tính/TV → đây là màn hình chiếu
2. Dùng điện thoại quét QR code trên màn hình → vào `https://duylinh.netlify.app`
3. Nhập tên → chụp ảnh → chia sẻ → ảnh xuất hiện ngay trên màn hình ✅

---

## Lưu ý quan trọng

- **Firestore rules**: Để ở chế độ test mode trong 30 ngày là đủ cho tiệc sinh nhật
- **Storage rules**: Tương tự, test mode là được
- **Ảnh được nén** xuống tối đa 1920px trước khi upload để nhanh hơn
- **Xóa project Firebase** sau tiệc để tránh phát sinh chi phí (free tier rất rộng rãi)

---

## Tuỳ chỉnh

| Thứ cần đổi | Vị trí |
|---|---|
| Tên "Duy Linh" | Tìm và thay trong cả 2 file HTML |
| Màu chủ đạo | CSS variable `--gold: #c9a74a` |
| Số thumbnail hiển thị | `limit(20)` và `slice(1, 6)` trong admin/index.html |
