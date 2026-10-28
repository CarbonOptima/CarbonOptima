# CarbonOptima: cơ sở khoa học và thuyết trình

## Phạm vi của dự án

CarbonOptima ước tính **phát thải gián tiếp do điện lưới trong giai đoạn sử dụng thiết bị**. Không phải tổng dấu chân carbon của cả trường hoặc phân tích vòng đời. Độ chính xác phụ thuộc dữ liệu đo, lịch sử dụng và hệ số phát thải. Phiên bản này không tuyên bố đạt một độ chính xác phần trăm cụ thể.

## Những yếu tố ảnh hưởng

| Yếu tố | Tác động | Lựa chọn cho đề tài cấp trường |
|---|---|---|
| Điện năng thực đo (kWh) | Tích lũy tiêu thụ thực theo thời gian, bao gồm tải và chu kỳ hoạt động | Ưu tiên nhất; nhập kWh của **cả dòng thiết bị** trong một ngày hoạt động đại diện |
| Công suất điện thực so với định mức | Thiết bị thường không chạy ở định mức suốt thời gian bật | Dùng tỷ lệ tải trung bình, đo hoặc ghi rõ là giả định |
| Thời gian và số ngày hoạt động | Lịch học, cuối tuần, nghỉ hè làm thay đổi tổng năm | Nhập giờ/ngày và ngày/năm; phân tích riêng nhóm có lịch khác nhau |
| Chế độ chờ | Máy tính, máy chiếu vẫn dùng điện khi không làm việc | Nhập W chờ và giờ chờ; giờ bật + chờ ≤ 24 |
| Hệ số phát thải lưới điện | Cơ cấu nguồn điện và năm công bố làm thay đổi phát thải/kWh | Cho chỉnh hệ số và ghi nguồn, năm; chưa áp dụng hệ số theo giờ |
| Số người và nhu cầu sử dụng | Ảnh hưởng thời gian và chế độ hoạt động | Đối chiếu cùng mức phục vụ; không gán hệ số tăng tùy ý |
| Hiệu suất, tuổi thiết bị, bảo dưỡng | Có thể thay đổi điện năng để cung cấp cùng dịch vụ | Phản ánh qua kWh đo hoặc công suất/tải; không nhân thêm một lần nữa |
| Rò rỉ môi chất lạnh | Phát thải trực tiếp, tùy khối lượng rò rỉ và GWP của môi chất | Ngoài phạm vi hiện tại; cần hồ sơ bảo trì và loại môi chất |
| Nhiên liệu, vận chuyển, sản xuất/thải bỏ | Những nguồn phát thải ngoài điện vận hành | Đề cập giới hạn, không trộn với kết quả điện |
| Điện mặt trời và nguồn tự dùng | Làm thay đổi lượng điện mua từ lưới | Chưa mô hình hóa; muốn tính cần tách kWh lưới với nguồn khác |

**Không nhân thêm cos φ** vào công suất tác dụng W hoặc công tơ kWh. Nếu nhãn chỉ ghi VA hay A, cần xác định công suất tác dụng đúng cách. Công suất lạnh BTU/h, HP và điện đầu vào W không thể dùng thay nhau. Không tự nhân thêm tổn thất truyền tải vào hệ số đã chọn nếu chưa xác định ranh giới kiểm kê.

## Công thức đã triển khai

Khi chưa có số đo:

`E_ngày = N × (P_điện × f_tải × t_bật + P_chờ × t_chờ) / 1000`

N là số thiết bị; P đơn vị W; t đơn vị giờ; E đơn vị kWh. Chia 1000 để đổi Wh sang kWh. Tải là tỷ số công suất điện trung bình trong cửa sổ hoạt động trên công suất định mức, bao gồm chu kỳ chạy/nghỉ. Không nhân thêm “hệ số chu kỳ” nếu tải đã phản ánh yếu tố này.

Khi có số đo: `E_ngày = kWh đo của cả dòng / số ngày đo đại diện` (người nhập thực hiện phép chia trước). Số đo phải bao gồm điện chờ nếu cần tính điện chờ. Hệ thống không cộng lại điện chờ hoặc nhân số lượng lên số đo này.

`CO₂e_ngày = E_ngày × EF`; `CO₂e_năm = CO₂e_ngày × số ngày hoạt động`.

Bản gốc từng dùng 0,6235 kg CO₂e/kWh **chưa được xác minh nguồn/năm**; phiên bản hiện tại để trống hệ số cho người dùng cấu hình; không khẳng định đây là hệ số hiện hành của Việt Nam. Trước khi trình bày kết quả chính thức, tìm thông báo hệ số phát thải lưới của cơ quan có thẩm quyền, lưu bản công bố, kiểm tra năm và phạm vi khí (CO₂ hay CO₂e), cập nhật trường nguồn. Nếu nguồn chỉ công bố CO₂, ghi rõ giới hạn, không diễn giải thành đầy đủ mọi khí nhà kính. 1 tấn/MWh có cùng trị số với 1 kg/kWh.

Ví dụ minh họa với EF = 0,6235: 8 đèn × 40 W × 6 giờ × tải 100% = 1,92 kWh/ngày, tương ứng 1,19712 kg/ngày. Giảm 1 giờ bật dư giúp giảm 0,32 kWh/ngày (0,19952 kg/ngày), nếu thực sự có thể cắt mà vẫn bảo đảm độ sáng. 200 ngày/năm và giá giả định 3.000 ₫/kWh cho tiết kiệm 192.000 ₫/năm.

## Giải pháp có căn cứ

Gợi ý thực hành luôn xuất hiện theo loại thiết bị, kể cả khi người dùng chỉ nhập thông tin cơ bản. Chi phí 0 đồng mua thêm chỉ áp dụng cho thay đổi cách dùng thiết bị hiện có, chưa tính thời gian thực hiện. Bảo dưỡng/thay mới cần báo giá; không suy diễn mức tiết kiệm từ lời khuyên. Phương án định lượng chỉ được tạo khi có số giờ có thể giảm, điện chờ hoặc thông số thay thế phù hợp. Thiếu hệ số phát thải vẫn hiển thị kWh và giải pháp; CO₂ giữ trạng thái chưa cấu hình.

- Giảm giờ: dùng chính số giờ bật dư đã khảo sát, không lấy tỷ lệ giảm cố định.
- Điện chờ: dùng W chờ × giờ chờ. Chưa có báo giá công tắc thì không hiển thị hoàn vốn giả.
- Thay thiết bị: so sánh W cũ và W mới ở cùng tải, thời gian và mức dịch vụ. Đèn phải đủ quang thông/độ rọi; điều hòa phải đủ công suất lạnh. Không chỉ chọn thiết bị ít W hơn.
- Chi phí thay = số lượng × chi phí mỗi thiết bị do người dùng nhập (nên gồm lắp đặt). Hoàn vốn đơn giản = chi phí / tiền điện giảm trong năm; chưa gồm lãi suất, bảo trì, giá điện tương lai và carbon chế tạo.
- Ưu tiên hành động không cần đầu tư, sau đó theo kWh có thể giảm. Nhãn “khuyên dùng” là quy tắc xếp hạng này, không phải tối ưu toàn cục.
- Phương án độc lập, **không cộng chồng** giờ giảm và thay thế trên cùng dòng. Muốn kết hợp phải tính lại trạng thái sau từng thay đổi.
- Với kWh đo tổng, cần đo riêng các chế độ trước khi định lượng từng biện pháp; công cụ không suy diễn từ nhãn W. Thiết bị duy trì nguồn được loại khỏi gợi ý cắt điện. Người dùng cần đánh dấu các trường hợp đặc biệt mà tên thiết bị không nhận diện được.

## Thực nghiệm phù hợp cấp trường

1. Chọn một lớp và một phòng máy; kiểm kê thiết bị, công suất điện, lịch học, số người, điều kiện phòng.
2. Đo tối thiểu một tuần học trước can thiệp bằng công tơ nhánh hoặc thiết bị đo phù hợp. Đo có giám sát; không để học sinh tự đấu nối điện.
3. Chọn một thay đổi, chẳng hạn tắt đèn lúc phòng trống. Phân công người ghi giờ bật/tắt, số kWh đầu/cuối và mức tiện nghi. So sánh các ngày có lịch học tương đương; nếu có thể dùng thêm một phòng đối chứng.
4. Đo một tuần sau; báo cáo từng ngày và trung bình. Ngày nghỉ hoặc số người thay đổi phải ghi chú. Với điều hòa, đối chiếu điều kiện vận hành tương đương để hạn chế nhiễu.
5. So sánh kWh dự tính và đo; sai lệch tương đối = |ước tính − đo| / đo × 100%, chỉ tính khi số đo > 0. Ghi độ chính xác thiết bị đo, số ngày và khoảng dao động. Không gọi khoảng nhạy cảm là khoảng tin cậy thống kê.
6. Trình bày kWh trước, sau, chênh lệch; rồi mới quy đổi CO₂e và tiền. Báo cáo cả trường hợp không tiết kiệm được. Không nhân lên cả trường nếu mẫu chưa đại diện.

Bố cục thuyết trình: vấn đề → phạm vi → dữ liệu và công thức → demo → thực nghiệm → kết quả và giới hạn. Điểm mạnh là mô hình giải thích được và kiểm chứng được, không phải thêm càng nhiều hệ số càng chính xác.

## Tài liệu phương pháp để đối chiếu

- [GHG Protocol Scope 2 Guidance](https://ghgprotocol.org/scope-2-guidance): kiểm kê phát thải liên quan điện mua; tham khảo cách xác định ranh giới và hệ số.
- [IPCC 2006 Guidelines — Volume 2 Energy](https://www.ipcc-nggip.iges.or.jp/public/2006gl/vol2.html): nguyên tắc dữ liệu hoạt động × hệ số phát thải.

Các tài liệu trên là nguồn phương pháp; không được dùng để gán nguồn cho giá trị EF chưa xác minh trong bản gốc.

## Phiên bản quản lý theo tháng

Form dùng N × W × giờ/ngày × ngày/tháng / 1000. Với 2 × 1200 × 1 × 30, kết quả là 72 kWh/tháng. Thẻ và tổng danh sách dùng công thức này. Số đo/tải/điện chờ được giữ dưới dạng mô hình bổ sung, hiển thị riêng khi có thay đổi và dùng trong báo cáo chi tiết; không cộng hai kết quả. Ưu tiên Cao/Trung bình/Thấp chỉ ảnh hưởng lựa chọn giải pháp, không thay đổi kWh. Mỗi dòng có số ngày/tháng riêng. Tổng năm là kịch bản 12 tháng lặp lại lịch tháng mẫu, cần sửa theo thực tế khi báo cáo. Hệ số phát thải và giá điện chưa cấu hình không được coi là 0 hoặc thay bằng số minh họa.

## So sánh giải pháp trong 7 ngày

Báo cáo yêu cầu người dùng chọn lịch Hằng ngày, thứ Hai–thứ Sáu hoặc Tùy chỉnh; mặc định chưa xác nhận lịch. Các ngày được chọn lặp lại giờ dùng/ngày của các dòng có số ngày/tháng khác 0; chưa tự suy ra lịch từng thiết bị từ tổng ngày/tháng. Ngày bỏ chọn đặt nhóm không thiết yếu về 0, nhưng vẫn giữ kWh/ngày đã khai báo của thiết bị critical hoặc ưu tiên high trong cả hai trạng thái; không đề xuất cắt nguồn nhóm này. Lịch duy trì nhóm thiết yếu này là giả định cần đối chiếu thực tế. Mỗi lần so sánh một phương án để tránh cộng trùng. Biểu đồ cột kép bắt đầu từ 0; thiếu hệ số dùng kWh và giữ CO₂e ở trạng thái chưa cấu hình.

Phương án đủ dữ liệu có điện năng giảm tính từ thông số nhập; tiền và carbon chỉ tính khi có cấu hình. Phương án thiếu dữ liệu cho nhập thông số còn thiếu trong tab báo cáo, chỉ lưu bản mô phỏng trong sessionStorage của tab, không ghi đè danh sách thiết bị gốc. Giải pháp định tính là khuyến nghị kiểm tra/vận hành, không gán phần trăm hoặc kWh giảm. Tủ lạnh và máy bơm không nhận gợi ý giảm giờ tự động. Hoàn vốn vẫn dùng lịch tháng mẫu × 12, khác với lịch tuần được chọn; cần kiểm chứng bằng số đo trước/sau tương đương.

## Thư viện quyết định có nguồn

Báo cáo hiện dùng `solutionCatalog` và `solutionRules` trong app.js để tạo thẻ mở rộng có nguồn, điều kiện và trường mô phỏng riêng. Xem SOURCES.md để phân biệt tài liệu đã đọc, phạm vi áp dụng và URL không truy cập được. Khuyến nghị không tự sinh tỷ lệ giảm. Các nhãn hiển thị là Có thể tính toán / Cần thêm thông tin / Hướng dẫn tiết kiệm. Giá điện giữ đơn giá cấu hình; không tự suy ra hóa đơn bậc thang.
