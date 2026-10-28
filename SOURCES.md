# Nguồn và giới hạn của thư viện giải pháp

Đối chiếu trực tuyến ngày 27/10/2026. Nội dung web được tải trực tiếp bằng HTTPS; PDF DOE đã được chuyển sang văn bản và đọc các phần liên quan. Ứng dụng lưu quy tắc trong `app.js`, không gọi API nghiên cứu khi xem báo cáo.

| Nguồn thực sự đã đọc | Ngày/năm nguồn | Nội dung sử dụng và phạm vi |
| --- | --- | --- |
| [W3C WAI: Disclosure Card](https://www.w3.org/WAI/ARIA/apg/patterns/disclosure/examples/disclosure-card/) | Trang hướng dẫn đang truy cập; không gán năm xuất bản chưa xác minh | Article có heading; button điều khiển vùng chi tiết bằng aria-expanded/aria-controls; không bọc toàn bộ thẻ vào button; bỏ qua click vào input/link/label hoặc khi chọn văn bản. Đây là mẫu minh họa, cần kiểm thử thực tế, không phải chứng nhận accessibility. |
| [Nielsen Norman Group: Progressive Disclosure](https://www.nngroup.com/articles/progressive-disclosure/) | Jakob Nielsen, 03/12/2006 | Tóm tắt trước, chi tiết và thông số chuyên sâu chỉ mở khi yêu cầu. Nguyên tắc UX, không phải nguồn năng lượng. |
| [DOE: Energy Saver Guide](https://www.energy.gov/sites/default/files/2022-08/energy-saver-guide-2022.pdf) | 2022 | Tr. in 2–3 (PDF 6–7): khảo sát trước can thiệp, người có chuyên môn, đánh giá sau. Tr. 12 và 17–18 (PDF 16, 21–22): nhu cầu làm mát, nhiệt độ phù hợp tiện nghi, lọc và quạt. Tr. 31 (PDF 35): cửa/gioăng, nguồn nhiệt, khoảng hở theo hướng dẫn tủ lạnh. Tr. 34–35 (PDF 38–39): quản lý nguồn máy tính/điện tử và điện chờ. Tr. 35–37 (PDF 39–41): chiếu sáng, đối chiếu lumen, sự tương thích điều khiển. |
| [Bộ Công Thương: ra mắt cẩm nang tiết kiệm điện 2025](https://moit.gov.vn/tin-tuc/su-dung-nang-luong-tiet-kiem-va-hieu-qua/bo-cong-thuong-ra-mat-bo-cam-nang-tiet-kiem-dien-nam-2025.html) | 14/04/2025 (metadata xuất bản) | Xác nhận có cẩm nang gia đình và văn phòng/công nghiệp/tòa nhà thuộc Chương trình quốc gia 2019–2030, nêu phạm vi thiết bị Việt Nam. Đây là bài giới thiệu, không dùng để gán thông số kỹ thuật hoặc mức giảm cho từng máy. |
| [EVN: biểu giá theo QĐ 1279/QĐ-BCT](https://www.evn.com.vn/d/vi-VN/news/Bieu-gia-ban-le-dien-theo-Quyet-dinh-so-1279QD-BCTngay-0952025-cua-Bo-Cong-Thuong-60-28-502668) | 09/05/2025 | Đã đọc trang, có phân biệt nhóm khách hàng và sinh hoạt. Không suy ra đây là biểu giá mới nhất tại ngày nghiên cứu; không nhập các con số từ ảnh bảng giá, không đổi cấu hình người dùng. |

## Cách chuyển nguồn thành quy tắc

`CarbonModel.solutionRules` lưu mục đích, điều kiện, bước thực hiện, nhóm chi phí, độ khó, an toàn, nguồn và trang. `solutionCatalog` ghép quy tắc với thiết bị, tạo hướng dẫn và các kịch bản riêng cho giảm giờ, thay công suất, điện chờ. Thẻ có đủ thông số sẽ hiển thị ngay mức giảm do engine hiện có tính. Thẻ chưa đủ dữ liệu chỉ hỏi trường liên quan; giá mua/lắp là tùy chọn, chỉ cần cho đầu tư và hoàn vốn. Thư viện không tự cấp W, giá, % giảm hoặc giờ giảm cho các phương án.

Các công thức định lượng là mô hình kỹ thuật của ứng dụng: ΔE từ thay đổi công suất/giờ/điện chờ, có tải và số lượng. Đây là giả định kịch bản do người dùng nhập, không phải số tiết kiệm do tài liệu DOE bảo đảm. Điều chỉnh nhiệt độ, sleep, vệ sinh, gioăng và thông gió chỉ là thực hành định tính khi chưa có số đo riêng.

Giá điện tiếp tục dùng **đơn giá do người dùng cấu hình**, không phải tính hóa đơn bậc thang hoặc theo giờ cho mọi khách hàng. Tiền tiết kiệm và hoàn vốn chỉ là ước tính theo đơn giá đó; không tự gọi là tiền hóa đơn giảm chính xác. Không dùng giá mua máy, trợ cấp, thuế, biểu giá hoặc tỷ lệ tiết kiệm tại Mỹ cho Việt Nam. Hệ số CO₂e không được tự thay đổi.

Phân loại `deviceGroup` là taxonomy phục vụ báo cáo, ưu tiên tên nhận diện được (đặc biệt tủ lạnh, máy bơm, TV); không ghi đè `type` trong dữ liệu đã lưu. Biểu đồ tháng dùng điện năng mô hình × ngày dùng từng dòng, khác với tổng công suất cơ bản nếu có số đo/tải/điện chờ.

## Nguồn không truy cập/xác minh được

- Các trang DOE riêng lẻ về air-conditioning, refrigerators-and-freezers, computers-home-office-equipment-and-electronics, lighting-choices-save-you-money, fans-cooling trả HTTP 404. Dùng PDF chính thức đã đọc thay thế.
- Hai trang cẩm nang toàn văn do bài Bộ Công Thương liên kết (`t42589`, `t42590` trên tietkiemnangluong.com.vn) trả HTTP 403. Chưa đọc toàn văn, không trích khuyến nghị kỹ thuật từ các tài liệu đó.
- URL Epson thử truy cập hướng dẫn tắt máy chiếu trả HTTP 403. Không xác minh model hoặc thời gian làm nguội; quy tắc chỉ yêu cầu tra hướng dẫn model và áp dụng nguyên tắc quản lý nguồn điện tử nói chung.
- URL DOE thử truy cập `maintain_pumping_systems.pdf` trả HTTP 404. Chưa có nguồn hướng dẫn bơm gia đình cụ thể. Với bơm chỉ hỗ trợ khảo sát nhu cầu/kWh và nhờ chuyên môn theo nguyên tắc khảo sát chung, không tự mô phỏng giảm giờ bơm hoặc suy diễn lợi ích bảo dưỡng.

Không có số liệu giá thị trường thiết bị đã xác minh. Chi phí nhân công/vật tư/dịch vụ được ghi chưa biết hoặc cần báo giá; “không cần mua mới” không có nghĩa tổng chi phí thực hiện bằng 0.
