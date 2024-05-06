### 基于 x64 的处理器的Windows电脑安装aarch64版本麒麟v10系统

```javascript
./qemu-img create -f qcow2 D:\arm64\kylindisk.qcow2 40G
./qemu-system-aarch64.exe -m 4096 -cpu cortex-a72 -smp 8,sockets=4,cores=2 -M virt -bios D:\qemu\QEMU_EFI.fd -device VGA -device nec-usb-xhci -device usb-mouse -device usb-kbd -drive if=none,file=D:\arm64\kylindisk.qcow2,id=hd0 -device virtio-blk-device,drive=hd0 -drive if=none,file=D:\arm64\Kylin-Server-10-SP2-aarch64-Release-Build09-20210524.iso,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom  -net nic -net user,hostfwd=tcp::2222-:22
./qemu-system-aarch64.exe -m 4096 -cpu cortex-a72 -smp 8,sockets=4,cores=2 -M virt -bios D:\qemu\QEMU_EFI.fd -device VGA -device nec-usb-xhci -device usb-mouse -device usb-kbd -drive if=none,file=D:\arm64\kylindisk.qcow2,id=hd0 -device virtio-blk-device,drive=hd0 -drive if=none,file=,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom -net nic -net user,hostfwd=tcp::2222-:22
习惯： 用户： root   密码：Test!@123
```


###麒麟v10 SP2 Kernel: 4.19.90-24.4.v2101.ky10.x86_64版本安装docker-ce
```javascript
cat << EOF > /etc/yum.repos.d/EPKL.repo
[EPKL]
name = Kylin Linux Advanced Server 10 - Os
baseurl = http://update.cs2c.com.cn/NS/V10/V10SP3/EPKL/$basearch/
gpgcheck = 1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-kylin
enabled = 1
EOF



yum clean all
yum makecache
yum install docker-ce docker-ce-cli --downloadonly --downloaddir=/tmp/docker-ce/
```
