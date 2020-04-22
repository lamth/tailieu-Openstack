# Làm việc với Keystone thông qua CLI

Có hai client được hỗ trợ là python-keystone client và python-openstackclient

## Thiết lập xác thực với mật khẩu thông qua CLI

- Để xác thực với keystone sử dụng mật khaaut và puthon-openstackclient, có hai lựa chọn: thứ nhất là thiết lập các flag cho các câu lệnh làm việc với keystone hoặc cách thứ hai là thiết lập các biến cho môi trường lưu thông tin xác thực.

- Các flag dùng cho xác thực:
  - **--os-username OS_USERNAME**: username của tài khoản

  - **--os-user-domain-name OS_USER_DOMAIN_NAME**: tên của domain cho tài khoản đó

  - **--os-password OS_PASSWORD**: mật khẩu cho tài khoản

  - **--os-project-name OS_PROJECT_NAME**: project của tài khoản

  - **--os-project-domain-name OS_PROJECT_DOMAIN_NAME**: domain của project

  - **--os-auth-url OS_AUTH_URL**: địa chỉ URL của server xác thực(keystone)

  - **--os-identity-api-version OS_IDENTITY_API_VERSION**: Phiên bản API của Keystone, thường là 3
  
- Hoặc thiết lập biến môi trường để không phải nhập lại các thông số trong mỗi lần chạy lệnh. Thay thông số và chạy các lệnh sau trước khi làm việc với các dịch vụ của openstack:
```
export OS_USERNAME=my_username
export OS_USER_DOMAIN_NAME=my_user_domain
export OS_PASSWORD=my_password
export OS_PROJECT_NAME=my_project
export OS_PROJECT_DOMAIN_NAME=my_project_domain
export OS_AUTH_URL=http://localhost:5000/v3
export OS_IDENTITY_API_VERSION=3
```

- Một cách khác để sử dụng biến môi trường là cho các lệnh export biến môi trường ở trên vào một file. Khi cần làm việc với Openstack, ta tiến hành source file đó.

- Sau khi thiết lập các thông tin xác thực, kiểm tra token được cấp:
```
lamth@Precision:~$ openstack token issue
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Field      | Value                                                                                                                                                                                   |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| expires    | 2020-04-18T03:44:53+0000                                                                                                                                                                |
| id         | gAAAAABemmmlAF_O31V3-ZnAVEEne39-mztnwsVtoIGPACc6-z5AE0bBb8_61ebVZ9D4GPWmg_U-y_W8hZBCBAicM6pcMkTe9s84_Sn7l3nX61CIrzEQCamFpjoxzDW1gWM-9brLSCAIYPmx_18L3aWIWE83jA1-J7x8S6mcS0n5fRfaGTxji7A |
| project_id | 8438aba4660e4e5e9ab029a4b2568159                                                                                                                                                        |
| user_id    | a4b7fe98e38a4af8bf9d6a344dbd0653                                                                                                                                                        |
+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```

- Để quản lý keystone, cần đăng nhập vào tài khoản có quyền admin


## Quản lý các user

- Khởi tạo một user:
```
lamth@Precision:~$ openstack user create --password-prompt --email tranhuulam199@gmail.com lamth
User Password:
Repeat User Password:
+---------------------+----------------------------------+
| Field               | Value                            |
+---------------------+----------------------------------+
| domain_id           | default                          |
| email               | tranhuulam199@gmail.com          |
| enabled             | True                             |
| id                  | 8f1d9c9b752c44aa95266b25980fb824 |
| name                | lamth                            |
| options             | {}                               |
| password_expires_at | None                             |
+---------------------+----------------------------------+
```

- Khởi tạo một project mới:
```
lamth@Precision:~$ openstack project create --domain default customer
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description |                                  |
| domain_id   | default                          |
| enabled     | True                             |
| id          | c75947145a0d42329757caf3b7fa13a5 |
| is_domain   | False                            |
| name        | customer                         |
| options     | {}                               |
| parent_id   | default                          |
| tags        | []                               |
+-------------+----------------------------------+
```

- Khởi tạo role:
```
lamth@Precision:~$ openstack role create compute-customer
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description | None                             |
| domain_id   | None                             |
| id          | 3512a490f4424ec98a400752a67fe5d1 |
| name        | compute-customer                 |
| options     | {}                               |
+-------------+----------------------------------+
```

- Gán role mới tạo cho user:
```
lamth@Precision:~$ openstack role add --project customer --user lamth compute-customer
lamth@Precision:~$ openstack role list --project customer --user lamth
Listing assignments using role list is deprecated. Use role assignment list --user <user-name> --project <project-name> --names instead.
+----------------------------------+------------------+----------+-------+
| ID                               | Name             | Project  | User  |
+----------------------------------+------------------+----------+-------+
| 3512a490f4424ec98a400752a67fe5d1 | compute-customer | customer | lamth |
+----------------------------------+------------------+----------+-------+
```

- Kiểm tra project:
```
lamth@Precision:~$ openstack project show customer
+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description |                                  |
| domain_id   | default                          |
| enabled     | True                             |
| id          | c75947145a0d42329757caf3b7fa13a5 |
| is_domain   | False                            |
| name        | customer                         |
| options     | {}                               |
| parent_id   | default                          |
| tags        | []                               |
+-------------+----------------------------------+
```

## Quản lý project
- Một group là một nhóm của không hoặc nhiều hơn các user, project sở hữu máy ảo. Một user có thể thuộc nhiều project nhưng ở phạm vi của project nào thì sẽ có quyền hạn theo role ở project đó.
- Liệt kê các project
```
openstack project list
```
- Tạo một project
```
openstack project create --description 'project mới của mình' --domain default new-project
```
- Cập nhật cấu hình cho project. Cấu hình một số thông số cho project như id, tên, mô tả, trạng thái enable.
	-	Tạm thời disable một project:
	```
	openstack project set PROJECT_ID --disable
	```
	- Enable một project đang disable:
	```
	openstack project set PROJECT_ID --enable
	```
	- Sửa tên của một project:
	```
	openstack project set PROJECT_ID --name project_B
	```
	- Xác nhận thay đổi:
	```
	openstack project show PROJECT_ID
	```
- Xóa một project:
```
openstack project delete PROJECT_ID
```


## Quản lý user.
- Liệt kê các user:
```
openstack user list -f json
```
- 
