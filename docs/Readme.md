# Tìm hiểu OpenStack

![](https://i.imgur.com/IZgCQ9y.png)

- Môi trường : Centos 7
- Phiên bản : Openstack Stein
- Hypervisor : KVM/QEMU
- Có sử dụng FirewallD, không sử dụng SeLinux.

## Mục Lục

## 1. Giới thiệu  

- [Giới thiệu về Cloud Computing và Openstack](./01.Overview/01.Introduce-to-Cloud-Computing.md)

- [Cài thử nghiệm Openstack sử dụng Packstack](./01.Overview/02.Install_packstack_OpenstackStein.md)

- [Sử dụng Openstack dashboard](./01.Overview/03.Use-Dashboard.md)

- [Chuẩn bị môi trường cài đặt Openstack Stein](./01.Overview/04.Enviroment-setup.md)

### 2. Openstack Identity - Keystone

- [Giới thiệu về  Openstack  Identity](./02.Keystone/01.Introduct-Keystone.md)

- [ Cài đặt Keystone ](./02.Keystone/02.Install-Keystone.md)

- [ Cấu hình Keystone](./02.Keystone/03.Config-Keystone.md)

- [ Tìm hiểu Keystone Token](./02.Keystone/04.Token-Keystone.md)

- [ Làm việc với Keystone sử dụng Openstack Client](./02.Keystone/05.Keystone-cli.md)

- [ Làm việc với Keystone thông qua API sử dụng Curl](./02.Keystone/06.Keystone-API-with-Curl.md)

### 3. Openstack Image - Glance

- [Giới thiệu về Openstack Image - Glance](./03.Glance/01.Introduction-Glance.md)

- [Cài đặt Glance](./03.Glance/02.Install-Glance.md)

- [ Tìm hiểu Metadata definition service trong Openstack image](./03.Glance/03.Metadata-definition-concepts.md)

- [ Làm việc với Glance thông qua Openstack client và Glance API](./03.Glance/04.Work-with-Glance.md)

- [Tìm hiểu Image Property(các thuộc tính của image)](docs/03.Glance/05.Image-Properties.md)

### 4. Placement

- [Giới thiệu về Placement](./04.Placement/01.Introduction.md)

- [Cài đặt dịch vụ Placement](./04.Placement/02.Install-Placement.md)


### 5. Openstack Compute - Nova

- [Giới thiệu về dịch vụ Openstack Compute - Nova](docs/05.Nova/01.Introduction.md)

- [Cài đặt Nova](docs/05.Nova/02.Installation.md)

- [Làm việc với Nova sử dụng Openstack client và Nova API](docs/05.Nova/03.Work-with-Nova-using-CLI&API.md)

- [Một số cấu hình bổ sung cho Nova](docs/05.Nova/04.Nova-config-file.md)

- [Sử dụng Metadata trong Nova](docs/05.Nova/05.Metadata.md)

- [Giao tiếp nội bộ của các thành phần trong Nova](docs/05.Nova/06.Nova-internal.md)

- [Migrate máy ảo trong Nova (chưa hoàn thành)](docs/05.Nova/07.Migrate-VM(Not-done-yet).md)

### 6. Openstack Networking - Neutron

- [Giới thiệu về Openstack Networking - Neutron và một số khái niệm liên quan](/06.Neutron/01.Introduction-neutron.md)

- [Cài đặt Openstack Neutron sử dụng LinuxBridge - mô hình Self-service](/06.Neutron/02.Installation.md)

- [Network namespace và kiến trúc các thành phần Neutron](/06.Neutron/03.Namespace-and-Networking-Architecture.md)

- [Tìm hiểu Address Scope](docs/06.Neutron/04.Address-Scopes.md)

- [Luồng đi của mạng trong Neutron sử dụng Linux Bridge](/06.Neutron/05.Linux-bridge-network-trafic-flow.md)

- [Cài đặt Openstack Neutron sử dụng Openvswitch - mô hình Self-service](/06.Neutron/06.Install-Neutron-SelfService-with-OpenvSwitch.md)

- [Luồng đi của mạng trong Neutron sử dụng Openvswitch](./06.Neutron/07.OVS-network-traffig-flow.md)

### 7. Openstack Block Storage - Cinder

- [Tìm hiểu tổng quan về dịch vụ Openstack Block Storage](./07.Cinder/01.Introduction.md)
- [Cài đặt Cinder-sử dụng storage backend LVM](./07.Cinder/02.Installation.md)
- [Kiến trúc và luồng hoạt động giữa các thành phần của Cinder](./07.Cinder/03.Cinder-Architecture.md)
- [Một số câu lệnh làm việc với Cinder](./07.Cinder/04.Work-with-Cinder-using-CLI.md)
- [Cấu hình mutilple backend cho Cinder](./07.Cinder/05.Config-multiple-backend.md)
- [Tìm hiểu cơ chế Filter và weghter trong Cinder để scheduler](./07.Cinder/06.Scheduler-Filter-Multiple-backend.md)
