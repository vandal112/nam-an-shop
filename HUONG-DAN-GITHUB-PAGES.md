# Đưa giao diện lên GitHub Pages, database vẫn ở máy bạn

Mô hình này chạy như sau:

- GitHub Pages giữ giao diện tĩnh: `https://tenban.github.io/nam-an-shop-fullstack/`
- Máy bạn vẫn chạy backend Node.js và SQLite: `backend/data/shop.db`
- Một tunnel HTTPS nối từ Internet về máy bạn, ví dụ Cloudflare Tunnel.

## Lưu ý quan trọng

GitHub Pages không chạy được Node.js và không giữ được SQLite. Vì vậy GitHub chỉ làm địa chỉ cho giao diện. Muốn khách đặt hàng thật, máy bạn phải bật backend và tunnel.

Nếu dùng tunnel miễn phí dạng nhanh, địa chỉ backend có thể đổi mỗi lần mở. Khi đó bạn cần sửa `frontend/config.js` rồi đẩy lại GitHub. Muốn ổn định lâu dài thì cần một tunnel cố định hoặc tên miền riêng.

## Các bước chạy thử miễn phí

1. Tạo repository GitHub, ví dụ `nam-an-shop-fullstack`.
2. Upload/push thư mục `frontend` lên GitHub Pages.
3. Trên máy bạn, chạy `CHAY-BACKEND-CHO-GITHUB.bat`.
   - Khi được hỏi, nhập địa chỉ GitHub Pages, ví dụ:
     `https://tenban.github.io`
4. Mở terminal khác, chạy `CHAY-TUNNEL-CLOUDFLARE.bat`.
5. Copy link tunnel HTTPS mà Cloudflare hiện ra.
6. Sửa `frontend/config.js` trên GitHub thành:

```js
window.NAM_AN_API_BASE = 'https://link-tunnel-cua-ban.trycloudflare.com';
```

7. Chờ GitHub Pages cập nhật rồi mở lại web.

## Khi nào web hoạt động?

- GitHub Pages phải mở được.
- `CHAY-BACKEND-CHO-GITHUB.bat` phải đang chạy.
- Tunnel phải đang chạy.
- `frontend/config.js` trên GitHub phải trỏ đúng về link tunnel hiện tại.

## Khi tắt máy

Web GitHub vẫn mở được giao diện, nhưng sản phẩm, giỏ hàng, đăng nhập, đặt hàng và admin sẽ không dùng được vì database nằm trên máy bạn.
