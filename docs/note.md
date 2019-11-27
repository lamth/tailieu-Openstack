# Một số ghi chú bổ xung.


## Cách cài các phiên bản openstack cũ.
Vì các phiên bản Openstack cũ (EOL) sẽ bị xóa khỏi mirror.

Cài repo khác cho centos, ví dụ:
```

yum install -y https://buildlogs.centos.org/centos/7/cloud/x86_64/openstack-mitaka/centos-release-openstack-mitaka-1-4.el7.noarch.rpm

sed -i  's#http://mirror.centos.org#http://buildlogs.centos.org#g' /etc/yum.repos.d/CentOS-OpenStack-mitaka.repo
sed -i  's#gpgcheck=1#gpgcheck=0#g' /etc/yum.repos.d/CentOS-OpenStack-mitaka.repo
```

