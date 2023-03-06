---
description: Redirect() vs RedirectPermanent() in ASP.NET
---

# Redirect() vs RedirectPermanent() in ASP.NET

Sự khác biệt cơ bản giữa hai loại này là `RedirectPermanent`gửi cho trình duyệt `HTTP 301`mã trạng thái (Đã di chuyển vĩnh viễn) trong khi `Redirect`sẽ gửi `HTTP 302`mã trạng thái.

Sử dụng `RedirectPermanent`nếu tài nguyên đã được di chuyển vĩnh viễn và sẽ không còn truy cập được ở vị trí trước đó. Hầu hết các trình duyệt sẽ lưu trữ phản hồi này và tự động thực hiện chuyển hướng mà không yêu cầu lại tài nguyên ban đầu.

Sử dụng `Redirect`nếu tài nguyên có thể có sẵn ở cùng một vị trí (URL) trong tương lai.

**Ví dụ**

Giả sử bạn có người dùng trong hệ thống của mình. Bạn cũng có một tùy chọn để xóa người dùng hiện có. Trang web của bạn có một tài nguyên `/user/{userid}`hiển thị thông tin chi tiết của một người dùng nhất định. Nếu người dùng đã bị xóa, bạn phải chuyển hướng đến `/user/does-not-exist`trang. Trong trường hợp này:

Nếu người dùng sẽ **không bao giờ** được khôi phục lại, bạn nên sử dụng `RedirectPermanent`để trình duyệt có thể truy cập trực tiếp `/user/does-not-exist`vào các yêu cầu tiếp theo ngay cả khi URL trỏ đến `/user/{userid}`.

Nếu người dùng có thể được khôi phục trong tương lai, bạn nên sử dụng tệp `Redirect`.
