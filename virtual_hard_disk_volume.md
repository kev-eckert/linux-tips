# Virtual HardDisk volume

## Create virtual disk

Create with fixed size of 130 Mo
```bash
dd if=/dev/zero of=vdisk.img bs=1M count=130
```

Create filesystem
```bash
mkfs.ext4 vdisk.img
```

Mount virtual disk
```bash
mount vdisk.img /mnt/
```

## Extend virtual disk

You want to enlarge it, so first add some zeros to the image using `dd`, That added 400M to the image
```bash
dd if=/dev/zero bs=1M count=400 >> vdisk.img
```

Extend filesystem
```bash
resize2fs vdisk.img
```
