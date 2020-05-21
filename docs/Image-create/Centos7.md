
## 1. Công cụ sử dụng

- Quản lý, khởi tạo máy ảo : virt-manager
- KVM-Host : Centos 7 

## 2. Tải image ISO

- Iso sử dụng: Centos 7.9.2003

```
wget http://mirrors.vhost.vn/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-2003.iso -O /var/lib/libvirt/images/CentOS-7-x86_64-Minimal-2003.iso
```

- Tài liệu : https://docs.openstack.org/image-guide/


## 3. Chuẩn bị máy ảo
- Tạo máy ảo mới từ ISO:

![](http://i.imgur.com/uLnOyNO.png)

- Chọn ISO centos 7.9-2003 vừa tải về

![](http://i.imgur.com/7Dd15Et.png)

- Chọn cấu hình Cpu và Ram

![](http://i.imgur.com/oT6fWq6.png)

- Cấu hình ổ cứng:

![](http://i.imgur.com/87qol09.png)

- Xem lại thông tin và Finish để tạo máy ảo:

![](http://i.imgur.com/d3iDTP0.png)

## 4. Cấu hình hệ điều hành

- Lựa chọn ngôn ngữ

![](https://i.imgur.com/uMQn40R.png)

- Cấu hình các thông số cơ bản cho máy ảo

![](https://i.imgur.com/Q4AzhWR.png)

- Lựa chọn Timezone

![](https://i.imgur.com/Wc4cErl.png)

- Cấu hình partion cho máy ảo

![](https://i.imgur.com/62DKoOR.png)

- Lựa chọn  "Standard partion" và khởi tạo các mount point

![](https://i.imgur.com/UhQ6Wz9.png)

- Thêm mount point "/" với 100% disk space

![](https://i.imgur.com/pQXjxeA.png)

- Lựa chọn Filesystem Ext4 và Update seting

![](https://i.imgur.com/VcpemP2.png)

- Done và thực hiện format disk

![](https://i.imgur.com/BRncG3C.png)'


- Enable network card

![](https://i.imgur.com/KWKH7Jq.png)

- Bắt đầu quá trình cài đặt

![](https://i.imgur.com/uTW2mwB.png)

- Set password cho root

![](https://i.imgur.com/fmfb6Wg.png)

- Done cài đặt, Reboot

![](https://i.imgur.com/WDBNvBx.png)

## 5. Cài đặt trên máy ảo

- Update package:
```
yum update -y
```
- Cài đặt QEMU agent
```
yum install -y qemu-guest-agent
systemctl enable qemu-guest-agent.service
systemctl start qemu-guest-agent.service
```

- Tắt tắt firewalld
```
systemctl disable firewalld
systemctl stop firewalld
```

- Tắt SELINUX:
```
sed -i "s/SELINUX=.*/SELINUX=disabled/g" /etc/selinux/config
setenforce 0
```

- Cài dịch vụ acpid để hypervisor có thể bật và tắt máy ảo:
```
yum install -y acpid
systemctl enable acpid
```
- Cài cloud-init để máy ảo có thể tương tác với metadata service, nhận một số thông tin như ssh-key:
```
yum install -y cloud-init
```

- Sau khi cài đặt cloud-init, thực hiện chỉnh sửa một số cấu hình để cloud-init có thể cấu hình tài khoản root và cho phép đăng nhập bằng password:
```
sed -i 's/disable_root: 1/disable_root: 0/g' /etc/cloud/cloud.cfg  
sed -i 's/ssh_pwauth:   0/ssh_pwauth:   1/g' /etc/cloud/cloud.cfg
sed -i 's/name: centos/name: root/g' /etc/cloud/cloud.cfg
```
- Tiếp theo cài đặt cloud-utils-growpart để cho phép chỉnh kích thước phân vùng:
```
yum install cloud-utils-growpart -y
```

- Để máy ảo có thể truy cập được địa chỉ của metadata service thì cần disable zeroconf route bằng lệnh sau:
```
echo "NOZEROCONF=yes" >> /etc/sysconfig/network
```
- Để nhận được hostnamne từ cloud-init, xoá file hostname
```
rm -f /etc/hostname
```
- tắt postfix:
```
systemctl stop postfix
systemctl disable postfix
```
- Tắt IPv6 net-module
```
echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.conf
echo "net.ipv6.conf.default.disable_ipv6 = 1" >> /etc/sysctl.conf
sysctl -p
```

- Xoá cấu hình net-card mặc định (nếu có)
```
rm -rf /etc/sysconfig/network-scripts/ifcfg-eth0
```
- Tắt NetworkManager
```
systemctl stop NetworkManager
systemctl disable NetworkManager
```

- Cấu hình để có thể console được:
    - Ở file
    -  cấu hình /etc/default/grub và cấu hình sửa giá trị trong GRUB_CMDLINE_LINUX : xóa `rhgb quiet` và thêm `console=tty0 console=ttyS0,115200n8` 
    ```
    GRUB_CMDLINE_LINUX="crashkernel=auto console=tty0 console=ttyS0,115200n8"
    ```
    - Lưu lại thay đổi bằng lệnh sau:
    ```
    grub2-mkconfig -o /boot/grub2/grub.cfg
    ```

- Xóa cloud-init info
  ```
  rm -rf /var/lib/cloud/*
  ```

- Xoá log
```
yum clean all
rm -f /var/log/wtmp /var/log/btmp
rm /root/.bash_history; history -c 
```

- Shutdown máy ảo
```
poweroff
```
## 6. Trên KVM host

- Clean MAC Addr
```
yum instal libguestfs-tools-c
yum install /usr/bin/virt-sysprep
virt-sysprep -d centos7.0
```

hoặc nếu trên Ubuntu:
```
apt instal -y libguestfs-tools
virt-sysprep -d centos7.0
virtsh undefine centos7.0
```


-  Compress image
```
virt-sparsify --compress /var/lib/libvirt/images/centos7.0.qcow2 CentOS7-64bit-2019.img

```


- Copy image 
```
scp CentOS7-64bit-2019.img root@controller1:/root/

```

- Trên Controller khởi tạo image
```
glance image-create --name CentOS7-64bit-2019 \
--disk-format qcow2 \
--min-disk 5 \
--container-format bare \
--file /root/CentOS7-64bit-2019.img \
--visibility=public \
--property hw_qemu_guest_agent=yes \
--property hw_disk_bus=scsi \
--property hw_scsi_model=virtio-scsi --progress
```

```
openstack server create Cent7-cli\
  --image CentOS7-64bit-2019 \
  --network provider1 \
  --flavor 1 --user-data passwd-cloud
```
