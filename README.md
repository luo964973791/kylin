### 基于 x64 的处理器的Windows电脑安装aarch64版本麒麟v10系统

```javascript
./qemu-img create -f qcow2 D:\arm64\kylindisk.qcow2 40G
./qemu-system-aarch64.exe -m 4096 -cpu cortex-a72 -smp 8,sockets=4,cores=2 -M virt -bios D:\qemu\QEMU_EFI.fd -device VGA -device nec-usb-xhci -device usb-mouse -device usb-kbd -drive if=none,file=D:\arm64\kylindisk.qcow2,id=hd0 -device virtio-blk-device,drive=hd0 -drive if=none,file=D:\arm64\Kylin-Server-10-SP2-aarch64-Release-Build09-20210524.iso,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom  -net nic -net user,hostfwd=tcp::2222-:22
./qemu-system-aarch64.exe -m 4096 -cpu cortex-a72 -smp 8,sockets=4,cores=2 -M virt -bios D:\qemu\QEMU_EFI.fd -device VGA -device nec-usb-xhci -device usb-mouse -device usb-kbd -drive if=none,file=D:\arm64\kylindisk.qcow2,id=hd0 -device virtio-blk-device,drive=hd0 -drive if=none,file=,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom -net nic -net user,hostfwd=tcp::2222-:22
习惯： 用户： root   密码：Test!@123
```


###麒麟v10 SP2 版本安装docker-ce
```javascript
yum remove selinux-policy-ukmcs -y
curl -o /etc/yum.repos.d/CentOS-Base.repo https://repo.huaweicloud.com/repository/conf/CentOS-8-reg.repo

# 配置华为docker 镜像源
yum-config-manager --add-repo https://repo.huaweicloud.com/docker-ce/linux/centos/docker-ce.repo
sed -i 's+download.docker.com+repo.huaweicloud.com/docker-ce+' /etc/yum.repos.d/docker-ce.repo
echo "8" > /etc/yum/vars/centos_version
sed -i 's/$releasever/$centos_version/g' /etc/yum.repos.d/docker-ce.repo
sed -i 's/$releasever/$centos_version/g' /etc/yum.repos.d/CentOS-Base.repo
yum clean all
yum makecache
yum install docker-ce-3:19.03.15-3.el8 --downloadonly --downloaddir=/tmp/docker-ce/
```
