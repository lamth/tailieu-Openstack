# Tìm hiểu về LDAP và các khái niệm liên quan.

## Giới thiệu

**LDAP**, hay **Lightweight Directory Access Protocol**, là một *giao thức* mở được sử dụng cho việc *lưu trữ và gọi lại dữ liệu* từ một *cấu trúc cây thư mục phân cấp*. Thông thường được dùng để lưu trữ thông tin về một tổ chức, các tài sản cũng như nhân viên của tổ chức. LDAP là một giải pháp linh hoạt để định xác định bất kỳ thực thể nào và tính chất của nó.

LDAP thường được triển khai như một phần của một hệ thống tương tác lớn hơn. Ví dụ như triển khai để xác thực tài khoản cho hệ thống Openstack.

## Dịch vụ thư mục (Directory service)

Dịch vụ thư mục là dịch vụ được sử dụng để lưu trữ, quản lý, và trình diễn dữ liệu theo dạng key-value.hư mục được tối ưu cho việc tra cứu, tìm kiếm, và đọc hơn là ghi, vì vậy chúng hoạt động tốt với dữ liệu được truy xuất hơn là dữ liệu thường xuyên thay đổi.

Dữ liệu được lưu trữ trong dịch vụ thư mục thường được mô tả một cách tự nhiên và được sử dụng để xác định những đặc tính của một thực thể. Ví dụ một đối tượng vật lý được biểu diễn trong dịch vụ thư mục là một sổ địa chỉ. Mỗi người được biểu diễn như một entry trong thư mục, với cặp key-value mô tả thông tin liên hệ, nơi kinh doanh,... Dịch vụ thư mục hữu ích trong nhiều kịch bản mà bạn muốn mô tả thông tin truy nhập.


## LDAP là gì?
LDAP, or lightweight directory access protocol là giao thức truyền thông định nghĩa các phương tức mà một dịch vụ thư mục có thể được truy xuất. LDAP định dạng cách dữ liệu ghi vào dịch vụ thư mục để nó có thể đại diện cho một người dùng.

LDAP là một giao thức hướng thông điệp. Client tạo ra một thông điệp LDAP chứa một yêu cầu và gửi nó đến server. Server xử lý yêu cầu đó và gửi trả kết quả lại cho client theo một chuỗi gồm một hoặc nhiều thông điệp LDAP.

## Các thành phần cơ bản của LDAP
### Attributes

Dữ liệu trong hệ thống  được lưu trong hệ thống LDAP được lưu trong thành phần mà được gọi là Attributes (thuộc tính). 





































Tài liệu tham khảo
https://www.digitalocean.com/community/tutorials/understanding-the-ldap-protocol-data-hierarchy-and-entry-components
https://ldap.com/basic-ldap-concepts/