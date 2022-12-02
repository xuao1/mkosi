# mkosi
`mkosi` stands for *Make Operating System Image*, and is a tool for generating an OS tree or image that can be booted.

Here I will use `mkosi` to build Ubuntu 22.04 TLS

## Installation

Install `mkosi`:

```shell
sudo apt-get install mkosi
```

## Run

The following command will create a bootable image with the configuration file `mkosi.default` :

```shell
sudo mkosi qemu
```

`systemd-nspawn` can boot the resulting image:

```shell
systemd-nspawn -b -i image.raw
```

It can also be virtualized with `QEMU/KVM`:

```shell
qemu-system-x86_64 -m 512 -smp 2 -bios /usr/share/ovmf/OVMF.fd -drive format=raw,file=image.raw
```

## convert

To convert it to vmdk, so that we can run it on vmware or virtualbox:

```shell
qemu-img convert -pO vmdk image.raw dest.vmdk
```

[vmdk](https://baike.baidu.com/item/vmdk/3369989)

Remember using UEFI:

> 虚拟机-设置-选项-高级

## References

+ [mkosi — A Tool for Generating OS Images](http://0pointer.net/blog/mkosi-a-tool-for-generating-os-images.html) indroductory blog post by Lennart Poettering

- [Primary mkosi git repository on GitHub](https://github.com/systemd/mkosi/)
- [mkosi - ArchWiki (archlinux.org)](https://wiki.archlinux.org/title/Mkosi)
