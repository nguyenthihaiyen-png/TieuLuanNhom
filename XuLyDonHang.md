```plantuml
@startuml

title BIỂU ĐỒ ACTIVITY DIAGRAM QUY TRÌNH XỬ LÝ ĐƠN HÀNG

skinparam backgroundColor white
skinparam shadowing false
skinparam roundcorner 12

skinparam activity {
    BackgroundColor #DCEBFA
    BorderColor #789AC8
    FontColor #26364A
    FontSize 12
}

skinparam activityDiamondBackgroundColor #FCE8C3
skinparam activityDiamondBorderColor #D49A45
skinparam ArrowColor #607D9B
skinparam activityStartColor #26364A
skinparam activityEndColor #26364A

|Khách hàng|
start
:Chọn sản phẩm;
:Chọn kích cỡ và topping;
:Nhập số lượng;
:Cung cấp thông tin đặt hàng;
:Chọn hình thức nhận hàng;
:Chọn phương thức thanh toán;

|Nhân viên thu ngân|
:Tiếp nhận yêu cầu đặt hàng;
:Tạo đơn hàng;
:Kiểm tra thông tin đơn hàng;

|Hệ thống|
while (THÔNG TIN ĐƠN HÀNG HỢP LỆ?) is (Không)
    :Thông báo thông tin không hợp lệ;
    |Khách hàng|
    :Chỉnh sửa thông tin đặt hàng;
    |Nhân viên thu ngân|
    :Kiểm tra lại thông tin;
    |Hệ thống|
endwhile (Có)

:Tính tổng tiền đơn hàng;
:Thực hiện thanh toán;
:Kiểm tra kết quả thanh toán;

while (THANH TOÁN CHƯA THÀNH CÔNG?) is (Có)
    :Thông báo thanh toán thất bại;
    |Khách hàng|
    :Thực hiện thanh toán lại;
    |Hệ thống|
    :Kiểm tra lại kết quả thanh toán;
endwhile (Không)

:Ghi nhận thanh toán;
:Kiểm tra nguyên liệu tồn kho;

while (NGUYÊN LIỆU KHÔNG ĐỦ SỐ LƯỢNG?) is (Có)
    :Thông báo thiếu nguyên liệu;
    |Thủ kho|
    :Tiếp nhận cảnh báo thiếu nguyên liệu;
    :Kiểm tra và bổ sung nguyên liệu;
    |Hệ thống|
    :Kiểm tra lại số lượng tồn kho;
endwhile (Không)

:Cập nhật trạng thái Đang pha chế;

|Nhân viên pha chế|
:Tiếp nhận đơn hàng;
:Chuẩn bị sản phẩm;

if (KHÁCH HÀNG CÓ YÊU CẦU HỦY ĐƠN?) then (Có)
    |Quản lý cửa hàng|
    :Tiếp nhận yêu cầu hủy đơn;
    :Xem xét yêu cầu hủy;

    if (QUẢN LÝ ĐỒNG Ý HỦY ĐƠN?) then (Có)
        |Hệ thống|
        :Cập nhật trạng thái Đã hủy;
        :Lưu lý do hủy đơn;
        stop
    else (Không)
        |Nhân viên pha chế|
        :Tiếp tục pha chế;
    endif
else (Không)
    :Tiếp tục pha chế;
endif

:Hoàn thành pha chế;

|Hệ thống|
:Cập nhật trạng thái Chờ nhận hàng;

if (HÌNH THỨC NHẬN HÀNG LÀ GÌ?) then (Tại cửa hàng)
    |Khách hàng|
    :Đến cửa hàng nhận sản phẩm;
else (Giao hàng)
    |Nhân viên giao hàng|
    :Tiếp nhận đơn được phân công;
    :Giao sản phẩm cho khách hàng;
    :Cập nhật kết quả giao hàng;
    :Cập nhật tình trạng thu tiền COD;
    |Khách hàng|
    :Nhận sản phẩm;
endif

|Hệ thống|
:Cập nhật trạng thái Hoàn thành;
:Lưu lịch sử đơn hàng;

stop
@enduml
https://github.com/nguyenthihaiyen-png/TieuLuanNhom/blob/0f84741934a26d4c6671dd2d9a51a9c177cb2c47/XuLyDonHang.jpg
