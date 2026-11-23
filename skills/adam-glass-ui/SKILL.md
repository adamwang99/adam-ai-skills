---
name: "adam-glass-ui"
description: "Áp phong cách kính pha lê sáng của Adam (Adam Glass) cho giao diện web/app: dùng khi bạn cần giao diện kính trong, liquid glass, hoặc muốn nút/thẻ/công tắc theo style đã chốt."
---

# Adam Glass — kính pha lê sáng

Phong cách kính sáng dùng trên các sản phẩm của Adam Uses AI (https://adamusesai.com). Dùng công thức dưới đây.

## Quy trình
1. Dựng/áp CSS theo công thức. Không dùng ảnh, không `backdrop-filter` hàng loạt, không SVG displacement.
2. **Luôn chụp ảnh thật** (Playwright) và đặt cạnh ảnh tham chiếu để so; khi có góp ý, cắt sát vùng đó phóng 3–5× để so trước khi sửa.
3. Sửa xong chụp lại, gửi ảnh so sánh, nói rõ còn khác chỗ nào.

## Mô hình ánh sáng (bắt buộc)
- Một đèn ở TRÊN-TRÁI. Bóng đổ lệch dưới-phải (`4px 10px 20px -10px` + `8px 22px 34px -22px`).
- Vùng hội tụ nằm trong bóng dưới-phải: đốm trắng, mép xa viền vàng→cam→xanh.
- Tán sắc chỉ ở cung dưới-phải của mép; cung trái ánh xanh–tím rất nhạt.

## Mép = ống kính (từ ngoài vào)
Đường tối 1px `rgba(35,48,70,.5)` → tia trắng 1.5px → ống rộng `--tube` (gradient nón: trắng ở trên, `rgba(100,118,146,.95)` ở đáy) có lõi sáng ở giữa → tia trắng trong + cạnh mảnh `rgba(70,90,120,.2)` → mặt phẳng xám nhạt hơi tối về đáy.
Ống ĐỀU bề rộng quanh khối; chỉ đậm nhạt xoay theo góc. `--tube`: 3px pill/nút nhỏ · 4px nút · 6px thẻ · 7px khối lớn.
Cài đặt: ống bằng `::after` (inset 1px, padding var(--tube), mask ring, `background: core, disp, bevel; background-blend-mode: normal, screen, normal`); các tia bằng inset box-shadow trên phần tử.

## Màu
Nền `#EDEFF2`; mặt kính `linear-gradient(180deg, rgba(255,255,255,.72), rgba(236,240,246,.80) 22%, rgba(232,236,243,.82))`; chữ `#2A2F38`/`#5B6371`.
Cam `#FFC4A2→#FF9560→#F86A2E→#E94D1C`; xanh `#9ACBFF→#4A92F4→#1D5CCF`; teal `rgba(110,218,195,.85)→rgba(52,186,158,.92)→rgba(30,160,132,.96)`.

## Thành phần
- Nút màu: vỏ kính + chất lỏng màu, vệt sáng nửa trên, ống cùng tông, vùng hội tụ mang màu.
- Ô tích: vỏ kính sáng bọc lõi teal đậm; bóng đổ màu teal trong, không xám.
- Công tắc: ống XÁM đựng chất lỏng teal (đậm đáy-trái, trong dần lên trên/sang phải). Núm = đĩa phẳng hơi LÕM (bóng mép trong trên-trái, sáng mép trong dưới-phải), vật liệu đặc → bóng đậm hắt lên chất lỏng và đổ ra nền; núm cách ống đều bốn phía.
- Ảnh bằng chứng chỉ đóng khung, không lọc màu.

## Không làm
Viền cầu vồng đều · bóng thẳng xuống · núm lồi · đổi bề rộng ống theo cạnh · tô màu lên chữ nhỏ.