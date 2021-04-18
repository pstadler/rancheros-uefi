# UEFI bootable RancherOS image

This repository exists for my own convenience. Issues may or may not be answered.

Related: [RancherOS on FreeNAS 11.3](https://blog.hugopoi.net/2020/03/01/install-rancheros-on-freenas-11-3/)

```sh
# /mnt/efipart/EFI/BOOT/grub.cfg
set timeout=1
menuentry "Rancher from GPT" {
    search --no-floppy --set=root --label RANCHER_STATE
    linux    /boot/vmlinuz-4.14.138-rancher printk.devkmsg=on rancher.state.dev=LABEL=RANCHER_STATE rancher.state.wait panic=10 console=tty0 console=ttyS0 rancher.autologin=ttyS0
    initrd    /boot/initrd-v1.5.6
}
```
