# UEFI bootable RancherOS image

This repository exists for my own convenience. Issues may or may not be answered.

Related: [RancherOS on FreeNAS 11.3](https://blog.hugopoi.net/2020/03/01/install-rancheros-on-freenas-11-3/)

```sh
# /mnt/efipart/EFI/BOOT/grub.cfg
set timeout=1
menuentry "Rancher from GPT" {
    search --no-floppy --set=root --label RANCHER_STATE
    linux    /boot/vmlinuz-4.14.138-rancher printk.devkmsg=on rancher.state.dev=LABEL=RANCHER_STATE rancher.state.wait panic=10 console=tty0 console=ttyS0 rancher.autologin=ttyS0
    initrd    /boot/initrd-v1.5.8
}
```

## Change kernel boot parameters

Because we're using UEFI, `ros config syslinux` won't work for editing kernel boot parameters. Use this instead:

```sh
$ sudo system-docker run --rm --privileged -it -v /:/host alpine /bin/sh
# inside the alpine container:
$ mkdir -p /mnt/boot; mount /host/dev/vda1 /mnt/boot
$ vi /mnt/boot/EFI/BOOT/grub.cfg
$ umount /host/dev/vda1
# exit the container and reboot rancheros
```
