# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Xe con dân dụng: sedan, hatchback, SUV, taxi, xe bán tải cabin nhỏ. Thân xe thấp, khoang hành khách rõ ràng. | Phân biệt với `van`: car có cửa sổ bên hông chia đều, không có thùng hộp kín; phân biệt với `truck`: không có thùng hàng tách rời |
| `truck` | Xe tải có thùng hàng riêng biệt hoặc xe đầu kéo. Cabin tách biệt với phần chở hàng; thùng hàng thường cao hơn hoặc là rơ-moóc. | Phân biệt với `van`: truck có thùng hàng mở hoặc tách rời, không phải thân hộp liền; phân biệt với `car`: to hơn và có cấu trúc cabin + thùng rõ ràng |
| `bus` | Xe buýt chở khách công cộng hoặc doanh nghiệp. Thân xe dài và cao, nhiều cửa sổ xếp đều theo hàng ngang liên tục. | Phân biệt với `van`: bus dài hơn rõ rệt, thường có 2 cửa lên/xuống; phân biệt với `truck`: không có thùng hàng, toàn bộ thân là khoang hành khách |
| `van` | Xe van hoặc minivan chở hàng/chở người. Thân hộp hình chữ nhật liền, ngắn hơn bus. Thường có cửa trượt bên hông. | Phân biệt với `bus`: van ngắn hơn nhiều, ít cửa sổ hơn; phân biệt với `car`: thân hộp vuông vức, không có đường cong khoang hành khách |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: vẽ cạnh box chạm rìa ngoài của phần thân xe nhìn thấy được, không bao gồm mặt đường, bóng xe, cây hay xe bên cạnh. Không để hở nhiều hơn ~2% kích thước vật thể.
- Vật thể bị che khuất: vẫn gán box quanh phần nhìn thấy nếu nhận biết được lớp; box chỉ bao phần thực sự thấy được, không ước đoán phần bị che.
- Vật thể bị cắt bởi rìa ảnh: box chạm đúng rìa ảnh tương ứng (x_min=0, x_max=1, y_min=0 hoặc y_max=1); không đoán phần nằm ngoài ảnh.
- Vật thể rất nhỏ/mơ hồ: nếu không thể xác định lớp chắc chắn do kích thước quá nhỏ hoặc bị che gần hết, không tự đoán và bỏ qua; nếu nghi ngờ ghi vào guideline.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_026` | Một xe thân hộp dài xuất hiện ở góc phải ảnh, kích thước lớn hơn van thông thường, dễ nhầm giữa `van` và `bus` | `bus` (class 2) | Thân xe dài rõ ràng, quan sát thấy nhiều cửa sổ xếp đều theo hàng ngang liên tục — đặc điểm của bus; nếu chỉ dài nhưng thiếu hàng cửa sổ liên tục thì mới là van |
| `drive_019` | Xe van bị che một phần lớn bởi xe buýt đứng ngay phía trước, chỉ nhìn thấy nửa thân sau và phần đuôi | `van` (class 3) | Phần nhìn thấy có hình dạng thân hộp đặc trưng của van, đủ để xác định lớp; vẽ box quanh phần thấy được, không ước đoán phần bị che |
| `drive_024` | Xe ở hàng xe phía xa (gần đỉnh ảnh) có kích thước box rất nhỏ, khó phân biệt `car` hay `van` | `van` (class 3) | Khi quan sát kỹ thấy mái xe bằng phẳng và thân hộp đặc trưng, không có đường cong khoang hành khách của car; gán `van` dù kích thước nhỏ vì hình dạng nhận biết được |
