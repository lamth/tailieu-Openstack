# Ghi chép quá trình tìm hiểu OpenStack



- Môi trường : Centos 7
- Phiên bản : Openstack Stein
- Hypervisor : KVM/QEMU
- Có sử dụng FirewallD, không sử dụng SeLinux.

## Mục Lục

## 1. Giới thiệu

- [Giới thiệu về Cloud Computing và Openstack](./docs/01.Overview/01.Introduce-to-Cloud-Computing.md)

- [Cài thử nghiệm Openstack sử dụng Packstack](./docs/01.Overview/02.Install_packstack_OpenstackStein.md)

- [Sử dụng Openstack dashboard](./docs/01.Overview/03.Use-Dashboard.md)

- [Chuẩn bị môi trường cài đặt Openstack Stein](./docs/01.Overview/04.Enviroment-setup.md)

### [2. Keystone](./docs)

- [Giới thiệu về  Openstack  Identity](./docs/02.Keystone/01.Introduct-Keystone.md)

- [ Cài đặt Keystone ](./docs/02.Keystone/02.Install-Keystone.md)

- [ Cấu hình Keystone](./docs/02.Keystone/03.Config-Keystone.md)

- [ Tìm hiểu Keystone Token](./docs/02.Keystone/04.Token-Keystone.md)

- [ Làm việc với Keystone sử dụng Openstack Client](./docs/02.Keystone/05.Keystone-cli.md)

- [ Làm việc với Keystone thông qua API sử dụng Curl](./docs/02.Keystone/06.Keystone-API-with-Curl.md)

### [3. Glance](./docs/03.Glance)

- [Giới thiệu về Openstack Image - Glance](./docs/03.Glance/01.Introduction-Glance.md)

- [Cài đặt Glance](./docs/03.Glance/02.Install-Glance.md)

- [ Tìm hiểu Metadata definition service trong Openstack image](./docs/03.Glance/03.Metadata-definition-concepts.md)

- [ Làm việc với Glance thông qua Openstack client và Glance API](./docs/03.Glance/04.Work-with-Glance.md)

- [Tìm hiểu Image Property(các thuộc tính của image)](docs/03.Glance/05.Image-Properties.md)

### [4. Placement](docs/04.Placement)

- [Giới thiệu về Placement](./docs/04.Placement/01.Introduction.md)

- [Cài đặt dịch vụ Placement](./docs/04.Placement/02.Install-Placement.md)


### [5. Nova](docs/05.Nova)

- [Giới thiệu về dịch vụ Openstack Compute - Nova](docs/05.Nova/01.Introduction.md)

- [Cài đặt Nova](docs/05.Nova/02.Installation.md)

- [Làm việc với Nova sử dụng Openstack client và Nova API](docs/05.Nova/03.Work-with-Nova-using-CLI&API.md)

- [Một số cấu hình bổ sung cho Nova](docs/05.Nova/04.Nova-config-file.md)

- [Sử dụng Metadata trong Nova](docs/05.Nova/05.Metadata.md)

- [Giao tiếp nội bộ của các thành phần trong Nova](docs/05.Nova/06.Nova-internal.md)

- [Migrate máy ảo trong Nova (chưa hoàn thành)](docs/05.Nova/07.Migrate-VM(Not-done-yet).md)

### [6. Neutron](docs/06.Neutron/)

- [Giới thiệu về Openstack Networking - Neutron và một số khái niệm liên quan](docs/06.Neutron/01.Introduction-neutron.md)

- [Cài đặt Openstack Neutron sử dụng LinuxBridge - mô hình Self-service](docs/06.Neutron/02.Installation.md)

- [Network namespace và kiến trúc các thành phần Neutron](docs/06.Neutron/03.Namespace-and-Networking-Architecture.md)

- [Tìm hiểu Address Scope](docs/06.Neutron/04.Address-Scopes.md)

- [Luồng đi của mạng trong Neutron sử dụng Linux Bridge](docs/06.Neutron/05.Linux-bridge-network-trafic-flow.md)

- [Cài đặt Openstack Neutron sử dụng Openvswitch - mô hình Self-service](docs/06.Neutron/06.Install-Neutron-SelfService-with-OpenvSwitch.md)

- [Luồng đi của mạng trong Neutron sử dụng Openvswitch](docs/06.Neutron/07.OVS-network-traffig-flow.md)