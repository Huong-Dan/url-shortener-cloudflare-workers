# URL Rút Gọn Miễn Phí Với Cloudflare Workers

## Các Bước Thực Hiện
- Sau khi đã tạo tài khoản Cloudflare, vào mục [Workers](https://dash.cloudflare.com/sign-up/workers).
- Bạn chọn cho mình một subdomain, chọn gói miễn phí.
- Sau đó, chọn Create a Service. <br />
[![](https://github.com/Huong-Dan/url-shortener-cloudflare-workers/blob/main/img1.png)](#)
- Đặt tên theo ý thích.
[![](https://github.com/Huong-Dan/url-shortener-cloudflare-workers/blob/main/img2.png)](#)
- Sau khi đã hoàn tất việc tạo một Worker (Service), bạn nhấn Quick edit ở trang quản lý Worker.
[![](https://github.com/Huong-Dan/url-shortener-cloudflare-workers/blob/main/img3.png)](#)
- Rồi dán vào đoạn mã dưới đây như [hình](https://github.com/Huong-Dan/url-shortener-cloudflare-workers/blob/main/img4.png).
```javascript
const redirects = new Map([
  ["url-rutgon", "https://google.com/url-chua-rut-gon"],
  ["url-rutgon2", "https://google.com/url-chua-rut-gon2"],
])

addEventListener('fetch', event => {
  event.respondWith(handleRedirect(event.request));
})

async function handleRedirect(request) {
  let pathname = new URL(request.url).pathname.replace("/", "");
  let location = redirects.get(pathname);
  return location 
    ? Response.redirect(location, 301) 
    : new Response("Not Found", {status: 404})
  }
}
```
- Sau đó, nhấn **Save and Deploy** và thưởng thức thành quả:)

## Credits
Nguồn tham khảo: [Lucjan Suski](https://lucjan.medium.com/free-url-shortener-with-cloudflare-workers-125eaf87b1ec)
