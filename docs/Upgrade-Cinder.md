mikata to rocky
Cinder

# Nâng cấp database Openstack Cinder từ Mikata lên Rocky.

## Môi trường
OS : Centos 7
Cinder : 8.1.1 (Openstack Mitaka)
Database: mariadb

## Cài đặt Cinder 8.1.1

Cấu hình repo cho openstack mitaka.

```
yum install -y https://buildlogs.centos.org/centos/7/cloud/x86_64/openstack-mitaka/centos-release-openstack-mitaka-1-4.el7.noarch.rpm

sed -i  's#http://mirror.centos.org#http://buildlogs.centos.org#g' /etc/yum.repos.d/CentOS-OpenStack-mitaka.repo
sed -i  's#gpgcheck=1#gpgcheck=0#g' /etc/yum.repos.d/CentOS-OpenStack-mitaka.repo
```