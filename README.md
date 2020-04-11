# qemu-static

The purpose of this project is to build a highly compatible QEMU binary package
for linux. The overall strategy is to use Alpine Linux and link statically to
all possible libraries.

## build docker image
```
docker build --tag qemu-static:5.0.0-rc1 .
```

## run container, save ID, copy artifact(s)
```
docker run -it --cidfile=qemu.cid qemu-static:5.0.0-rc1 true
docker cp "$(cat qemu.cid):work/artifact" artifact
```

## review final artifact(s)
```
ls -al artifact/
total 28100
drwxr-xr-x 2 nobody users     4096 Apr 11 07:42 .
drwxr-xr-x 6 nobody users     4096 Apr 11 08:02 ..
-rw-r--r-- 1 nobody users 28762792 Apr 11 07:43 qemu-linux-x86_64-5.0.0-rc1.tar.xz
```
