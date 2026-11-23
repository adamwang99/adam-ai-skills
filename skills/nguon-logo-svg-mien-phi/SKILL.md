---
name: nguon-logo-svg-mien-phi
description: Lấy logo thương hiệu (Windows, Apple, Meta, Google, GitHub, Facebook, Zalo...) dạng SVG miễn phí, đúng giấy phép, để gắn lên nút tải, dải "dùng với", trang bán hàng. Dùng khi cần "logo chuẩn của hãng", "logo SVG đẹp", hoặc khi một trang cần biểu tượng hệ điều hành, nền tảng, mạng xã hội.
---

# Lấy logo SVG miễn phí cho web của bạn

Nguyên tắc: KHÔNG tự vẽ lại logo của hãng. Lấy tệp SVG có sẵn từ bộ miễn phí có giấy phép rõ, ghi nguồn cạnh tệp.

## Nguồn ưu tiên (theo thứ tự)

1. **SVG Logos của Gil Barbara**, giấy phép **CC0** (dùng tự do, không cần ghi công).
   - Trang: https://github.com/gilbarbara/logos · xem trước: https://svgporn.com
   - Lấy qua npm, không cần trình duyệt: gói `@iconify-json/logos`.
   - Có bản màu đầy đủ. Tên hay dùng: `microsoft-windows-icon`, `apple`, `macos`, `meta-icon`, `facebook`, `instagram-icon`, `messenger`, `google-icon`, `github-icon`, `telegram`, `whatsapp-icon`, `youtube-icon`, `tiktok-icon`, `chrome`.
2. **Simple Icons**, giấy phép **CC0**, logo MỘT MÀU (tô màu hãng bằng `fill`).
   - https://simpleicons.org · gói npm `simple-icons` hoặc `@iconify-json/simple-icons`.
   - Lưu ý: một số hãng đã yêu cầu gỡ khỏi bộ này (ví dụ các logo Microsoft). Không có thì quay về nguồn 1.
3. **Wikimedia Commons**: logo gốc của hãng, đọc kỹ dòng giấy phép trên trang tệp. Web đã dùng nguồn này cho logo Meta, Facebook, Instagram, Messenger (`public/images/ads-mcp/`).
4. **Trang tài nguyên thương hiệu chính thức** của hãng khi cần bản chuẩn nhất (Meta Brand Resources, Microsoft, Google). Làm theo điều khoản của hãng.

## Lấy một logo trong 1 phút (npm, chạy trong máy làm việc)

```bash
mkdir -p /tmp/logo && cd /tmp/logo
npm pack @iconify-json/logos --silent
tar -xzf iconify-json-logos-*.tgz
python3 - <<'PY'
import json
d = json.load(open("package/icons.json"))
W, H = d.get("width", 256), d.get("height", 256)
for ten, ra in [("microsoft-windows-icon", "windows.svg"), ("apple", "apple.svg")]:
    ic = d["icons"][ten]
    w, h = ic.get("width", W), ic.get("height", H)
    open(ra, "w").write(f'<svg xmlns="http://www.w3.org/2000/svg" viewBox="{ic.get("left",0)} {ic.get("top",0)} {w} {h}">{ic["body"]}</svg>')
    print(ra, w, h)
PY
```

Tìm tên logo: `python3 -c "import json;print([k for k in json.load(open('package/icons.json'))['icons'] if 'tu-khoa' in k])"`.

## Gắn vào web

- Đặt tệp trong `src/assets/<nhom>/` (Vite tự nhúng) hoặc `public/images/<nhom>/`.
- Kèm `README.md` cạnh tệp: tên logo, nguồn, phiên bản gói, giấy phép. Mẫu đang dùng: `src/assets/logo-he-dieu-hanh/README.md` (nút tải bộ cài Ads MCP).
- Dùng `<img alt="">` khi chữ bên cạnh đã ghi tên hãng; logo đứng một mình thì `alt` là tên hãng.
- Đặt logo trong ô nền sáng (`#f6f3ea`), cỡ 24 đến 30 px, đủ khoảng trống quanh logo. Không kéo méo, không đổi màu logo màu, không ghép chữ vào logo.
- Dải nhiều logo: để trên MỘT hàng (`flex-nowrap`, cuộn ngang khi hẹp). Không để logo rơi lẻ xuống dòng.

## Ghi chú pháp lý (nói rõ với chủ web khi cần)

- CC0 áp cho TỆP SVG. Logo vẫn là nhãn hiệu của hãng: chỉ dùng để chỉ đúng nền tảng (chạy trên Windows, quảng cáo trên Meta), không dùng như logo của mình, không ngụ ý hãng bảo trợ.
- Trang có logo Meta phải giữ dòng "không liên kết, không được Meta bảo trợ" (đã có `GhiChuThuongHieu`).
- Apple có điều khoản riêng về logo quả táo; nút tải bản Mac chấp nhận được vì chỉ báo hệ điều hành.


