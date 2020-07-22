# Tìm hiểu về Openstack Dashboard - Horizon.

## Tổng quan về Horizon.
Horizon là triển khai chuẩn của Openstack Dashboard, cung cấp một giao điện nền tảng web cho người dùng để sử dụng các dịch vụ Openstack bao gồm Nova, Swift, Keystone,...

## Cài đặt Horizon.

Dịch vụ cần thiết duy nhất để cài đặt Horizon là Keystone. Horizon có thể kết hợp với các dịch vụ khác như Image service, Compute, và Networking. Cũng có thể sử dụng Openstack Dashboard trong môi trường với các dịch vụ stand-alone như Object storage.



### Cài đặt và cấu hình các thành phần.
Cài đặt gói:
```
yum install openstack-dashboard -y
```
Chỉnh sửa file cấu hình `/etc/openstack-dashboard/local_settings` theo các  bước sau:
- Sửa Cấu hình dashboard sử dụng các dịch vụ openstack trên controller host:
```
OPENSTACK_HOST = "192.168.30.171"
```
- Cấu hình các host có thể truy cập dashboard, ở đây cấu hình cho tất cả các host đều có thể truy cập dashboard:
```
ALLOWED_HOSTS = ['*']
```
- Cấu hình memcached, tìm và sửa cấu hình.
```
SESSION_ENGINE = 'django.contrib.sessions.backends.cache'

CACHES = {
    'default': {
         'BACKEND': 'django.core.cache.backends.memcached.MemcachedCache',
         'LOCATION': '192.168.30.171:11211',
    }
}
```

- Enable the Identity API version 3:
```
OPENSTACK_KEYSTONE_URL = "http://%s:5000/v3" % OPENSTACK_HOST
```
- Enable support for domains:
```
OPENSTACK_KEYSTONE_MULTIDOMAIN_SUPPORT = True
```
- Configure API versions:
```
OPENSTACK_API_VERSIONS = {
    "identity": 3,
    "image": 2,
    "volume": 3,
}
```

- Cấu hình `Default` làm domain mặc định cho người dùng mà tạo ra trên dashboard:
``` 
OPENSTACK_KEYSTONE_DEFAULT_DOMAIN = "Default"
```
- Cấu hình role mặc định cho user mà được tạo trên dashboard:
```
OPENSTACK_KEYSTONE_DEFAULT_ROLE = "user"
```
- Nếu sử dụng tùy chọn mạng 1(chỉ có provider network) thì cần tát các giao diện hỗ trợ cho các dịch vụ mạng layer3:
```
OPENSTACK_NEUTRON_NETWORK = {
    ...
    'enable_router': False,
    'enable_quotas': False,
    'enable_distributed_router': False,
    'enable_ha_router': False,
    'enable_lb': False,
    'enable_firewall': False,
    'enable_vpn': False,
    'enable_fip_topology_check': False,
}
```
- Cấu hình time zone:
```
TIME_ZONE = "Asia/Ho_Chi_Minh"
```
- Cấu hình webroot
```
WEBROOT = "/dashboard/"
```
- Lưu file.

- Thêm dòng sau vào file **/etc/httpd/conf.d/openstack-dashboard.conf** nếu chưa có:
```
WSGIApplicationGroup %{GLOBAL}
```

## Hoàn tất quá trình cài đặt
- Khởi động lại web server và dịch vụ lưu trữ phiên:
```
systemctl restart httpd.service memcached.service
```
- Cấu hình firewalld:
```
firewall-cmd --add-port=80 --permanent
firewall-cmd --reload
```


## Tài liệu nguồn:
- https://docs.openstack.org/horizon/latest/install/install-rdo.html

