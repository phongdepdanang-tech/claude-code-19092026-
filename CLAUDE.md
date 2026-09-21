# CLAUDE.md — Northwind Auth Pages

## Mục đích của tài liệu này
Đây là quy chuẩn ghi nhớ cho các trang giao diện cơ bản (auth, form) trong dự án này. Nó tóm tắt lại những gì đã xây dựng ở `login.html` và `register.html`, đồng thời đặt ra **quy tắc thiết kế chung** để mọi trang web cơ bản tạo ra trong tương lai đều nhất quán.

---

## 1. Tổng quan các trang đã tạo

Hai trang xác thực (authentication) dùng chung thương hiệu **Northwind**:

| Trang | File | Vai trò |
|-------|------|---------|
| Đăng nhập | `login.html` | User đăng nhập bằng Email/Password hoặc tài khoản mạng xã hội |
| Đăng ký | `register.html` | User tạo tài khoản mới với đầy đủ thông tin cá nhân |

**Ngôn ngữ:** nội dung 100% tiếng Anh trên cả hai trang.

### 1.1 Trang đăng nhập — `login.html`
- **Yêu cầu:** trường Email + Password, nút "Sign in", checkbox "Remember me", link "Forgot password?", và các nút đăng nhập bằng Google / GitHub / Facebook (Lucide + Tailwind, responsive).
- **Hành động đã làm:** dựng form căn giữa màn hình theo theme dark; bỏ panel thương hiệu bên trái (yêu cầu cắt giảm); thêm hiệu ứng đổ bóng cam, glow nền, icon Lucide trong từng field; bổ sung validate email hợp lệ + mật khẩu ≥ 8 ký tự với thông báo lỗi màu `danger` có animation.
- **Kết quả:** form đăng nhập hoàn chỉnh, responsive PC/Tablet/Mobile, có toast demo cho các nút xã hội và submit giả lập.

### 1.2 Trang đăng ký — `register.html`
- **Yêu cầu:** Họ và tên (bắt buộc), Email, Mật khẩu, **Xác nhận mật khẩu (phải trùng)**, Giới tính (tùy chọn), Số điện thoại (tùy chọn, 10 chữ số), Địa chỉ (tùy chọn), **checkbox Đồng ý điều khoản (bắt buộc)**; link chuyển đổi qua lại với trang login.
- **Hành động đã làm:** xây dựng form bố cục 2 cột trên desktop (giới tính + sđt, password + confirm) xếp chồng trên mobile; validate tất cả trường bắt buộc và ràng buộc định dạng.
- **Kết quả:** form đăng ký đầy đủ, mọi ràng buộc nhập liệu đều có thông báo lỗi rõ ràng bên dưới field.

### 1.3 Liên kết chuyển đổi giữa hai trang
- `login.html` → "Don't have an account? **Create one**" → `register.html`
- `register.html` → "**Back to sign in**" (kèm icon `arrow-left`) → `login.html`

> **Lưu ý quan trọng:** file `register.html` từng bị ghi đè thành rỗng (Write nhiều lần thất bại). Nếu mở ra thấy trang trắng, cần **viết lại toàn bộ nội dung file**, dùng `login.html` làm khung tham chiếu cho theme.

---

## 2. QUY TẮC THIẾT KẾ CHUNG (bắt buộc áp dụng cho mọi trang cơ bản)

### 2.1 Công nghệ nền tảng (bắt buộc dùng chung)
- **Tailwind CSS** qua CDN: `<script src="https://cdn.tailwindcss.com"></script>`
- **Lucide Icons** qua CDN: `<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>` + `lucide.createIcons()`
- **Google Fonts:** Poppins (heading) + Inter (body)
- File nào dùng cũng phải khai báo đầy đủ **`tailwind.config`** và khối `<style>` gốc (giống hệt `login.html`) để theme được đồng nhất.

### 2.2 Theme màu sắc (GIỮ NGUYÊN — không đổi)
| Token | Màu | Công dụng |
|-------|-----|-----------|
| `base` | `#090A14` | Nền trang / page background |
| `panel` | `#0E1020` | Bề mặt card / surface |
| `field` | `#12142A` | Nền input |
| `line` | `#22243C` | Viền border |
| `brand` (DEFAULT) | `#DF6B33` | Màu chính / CTA |
| `brand.hover` | `#E77E4A` | Trạng thái hover CTA |
| `brand.soft` | `#F0A379` | Chữ nhấn, badge |
| `brand.deep` | `#A94A1D` | Glow đậm, gradient |
| `ink` | `#F4F5FA` | Văn bản chính |
| `muted` | `#8B90A8` | Văn bản phụ |
| `danger` | `#FF5D64` | Lỗi / ràng buộc nhập liệu |

### 2.3 Font chữ (bắt buộc dùng chung)
- `fontFamily.display` = **Poppins** — dùng cho các tiêu đề, trọng lượng 700–800.
- `fontFamily.sans` = **Inter** — dùng cho nội dung, trọng lượng 400–600.

### 2.4 Responsive (bắt buộc)
- Toàn bộ trang phải chạy tốt trên **PC / Tablet / Mobile**.
- Nền dùng `flex min-h-screen w-full overflow-hidden`.
- Nội dung form bọc trong `max-w-[26rem]` (login) / `max-w-[30rem]` (register) căn giữa.
- Bố cục nhiều cột dùng `grid` với breakpoint `sm:` — trên `sm` trở xuống tự xếp chồng.
- Luôn thêm glow nền cam 2 góc + lưới mờ với `pointer-events-none absolute -z-10`.

### 2.5 Lucide Icons (bắt buộc)
- Mỗi input quan trọng nên có icon Lucide ở bên trái (ví dụ: `mail`, `lock`, `user`, `phone`, `map-pin`, `shield-check`).
- Icon đổi màu thành `group-focus-within:text-brand` khi ô được focus.
- Các nút chuyển đổi dùng icon mũi tên (`arrow-left`, `arrow-right`).

### 2.6 Ràng buộc nhập liệu (bắt buộc cho trường quan trọng)
- Luôn đặt `novalidate` trên `<form>` và tự validate bằng JS.
- Trường bắt buộc đánh dấu bằng `<span class="text-danger">*</span>` cạnh label; trường tùy chọn ghi "(optional)".
- Mỗi field có thẻ `<p id="xxxError">` ẩn ngay bên dưới để hiện thông báo lỗi.
- **Helper chuẩn:**
  ```js
  const setFieldError = (inputId, errorId, invalid) => {
    const input = document.getElementById(inputId);
    const err   = document.getElementById(errorId);
    input.classList.toggle('border-danger/70', invalid);
    input.classList.toggle('focus:border-danger', invalid);
    input.classList.toggle('ring-4', invalid);
    input.classList.toggle('ring-danger/15', invalid);
    input.setAttribute('aria-invalid', String(invalid));
    err.classList.toggle('hidden', !invalid);
    err.classList.toggle('flex', invalid);
  };
  ```
- Xóa lỗi tự động khi user bắt đầu gõ (event `input` / `change`).
- **Quy tắc ràng buộc đang áp dụng:**
  - Email: `/^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/`
  - Mật khẩu: tối thiểu 8 ký tự
  - Xác nhận mật khẩu: phải bằng với mật khẩu đã nhập
  - Số điện thoại: 10 chữ số `/^\d{10}$/` (hoặc bỏ trống nếu tùy chọn)
  - Checkbox điều khoản: phải được chọn

### 2.7 Liên kết chuyển đổi trang (bắt buộc)
- Mọi trang cơ bản thuộc cùng luồng (ví dụ login ↔ register) **phải có liên kết qua lại**.
- Cách ghi: trang A có link dẫn đến trang B và trang B trỏ ngược về A.
- Sử dụng màu `text-brand`, hover `text-brand-soft`, có `focus-visible:underline` để dễ nhìn.

### 2.8 Hiệu ứng & tiện ích dùng chung
- `animate-rise` cho card khi load, `animate-field-error` cho thông báo lỗi.
- Trọng dụng `@media (prefers-reduced-motion: reduce)` để tắt animation cho người cần.
- Xử lý autofill của trình duyệt (tránh nền trắng nhòe trên nền tối).
- Có toast (`#toast`) cho các hành động demo.
- Focus trạng thái luôn hiển thị rõ (`focus-visible:ring`).

---

## 3. Ghi chú thực hiện
- Khi tạo trang mới: luôn **sao chép khung `tailwind.config` + `<style>` từ `login.html`** để giữ đúng theme, không tự ý thêm màu/font mới nếu chưa được yêu cầu.
- Khi thêm field mới, phải đảm bảo đủ bộ: label + dấu bắt buộc/tùy chọn + input + thẻ lỗi + logic validate trong JS.
- Submit hiện là demo (toast + setTimeout). Khi nối backend, thay đoạn `setTimeout` bằng `fetch()` tới endpoint thật.