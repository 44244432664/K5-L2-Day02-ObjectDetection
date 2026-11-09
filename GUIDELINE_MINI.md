# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Xe chủ yếu phục vụ việc di chuyển cá nhân hoặc gia đình, thường có 4–7 chỗ, đôi khi nhiều hơn, thân nhỏ nhất trong các loại xe | phần trên có hình thang cân, hoặc hình thang vuông, nếu hình thang vuông, phần thân xe vẫn có cửa sổ |
| `truck` | Xe thiết kế chủ yếu để vận chuyển hàng hóa, vật liệu hoặc thiết bị. Thường có cabin lái và khu vực chở hàng chuyên dụng, shape thường thấy là hình chữ nhật. | Khác với `van`, `truck` có 1 khoảng cách giữa phần đầu và thân/thùng xe |
| `bus` | Xe chủ yếu được thiết kế để vận chuyển nhiều hành khách, thường có nhiều hàng ghế và khoang hành khách chuyên dụng, thân dài | cả xe thường thấy có dạng hình chữ nhật, nhiều cửa sổ và chỗ ngồi (thường là vài chục) |
| `van` | Xe có hình thang vuông, thân dạng hộp, khoang xe cao và tương đối rộng, thường có thiết kế liền khối hoặc liền khoang. Có thể dùng để chở hàng hoặc chở một nhóm hành khách | khoang xe cao và tương đối rộng, thường có thiết kế liền khối hoặc liền khoang |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: hình chữ nhật nhỏ nhất bao quanh toàn bộ phần xe nhìn thấy được, bao gồm thân xe, bánh xe và các bộ phận gắn liền có thể nhận diện rõ (như gương chiếu hậu). Không lấy thêm bóng đổ, mặt đường hoặc vật thể xung quanh. Không cố tình mở rộng box cho đẹp hoặc cân đối.
- Vật thể bị che khuất: Nếu xe bị che bởi xe khác, cây, cột hoặc vật cản, chỉ vẽ box bao quanh các phần xe thực sự nhìn thấy được. Không suy đoán kích thước hay hình dạng phần bị che. Nếu nhiều phần nhìn thấy thuộc cùng một xe, vẫn chỉ tạo một box. Chỉ gán nhãn khi đủ đặc điểm để xác định lớp xe. Nếu ảnh có quá nhiều vật thể che khuất nhau, ưu tiên gắn nhãn các xe vẫn đủ xác định lớp, bỏ qua/ghi lại image ID, vị trí để hỏi giảng viên.
- Vật thể bị cắt bởi rìa ảnh: Chỉ vẽ box quanh phần xe nằm trong ảnh. Nếu xe kéo dài ra ngoài khung hình, đặt cạnh box trùng với rìa ảnh tương ứng. Không ước lượng phần xe nằm ngoài ảnh. Vẫn gán nhãn nếu phần còn lại đủ để xác định lớp (recommend từ 25% xe trở lên)
- Vật thể rất nhỏ/mơ hồ: Phóng to ảnh để kiểm tra trước khi quyết định. Nếu vẫn nhận diện chắc chắn được xe và phân biệt được một trong bốn lớp, tiếp tục gán nhãn. Nếu không đủ thông tin để xác định lớp, không đoán theo kích thước, màu sắc hoặc bối cảnh. Ghi lại image ID, vị trí và lý do chưa xác định để hỏi giảng viên. 

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_...` | | | |
| `drive_...` | | | |
| `drive_...` | | | |
