# qemu-static

The purpose of this project is to build a highly compatible QEMU binary package
for linux. The overall strategy is to use Alpine Linux and link statically to
all possible libraries.

## build docker image
```
docker build --tag qemu .
```

## run container, save ID, copy artifact(s)
```
docker run -it --cidfile=qemu.cid qemu true
docker cp "$(cat qemu.cid):work/artifact" artifact
```

## review final artifact(s)
```
ls -al artifact/
```
