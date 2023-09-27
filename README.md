# qemu-static

The purpose of this project is to build a highly compatible QEMU binary package
for linux to use with Zig testing.

Zig needs a very recent QEMU version, sometimes unreleased commit-revs, and
sometimes with custom patches. For this reason, distro-based QEMU packages are
unsuitable.

The overall strategy is to use Alpine Linux to host a QEMU build and link
statically to all possible libraries.

It is a non-goal to build QEMU with all features enabled.
It is a non-goal to build older versions of QEMU.

## build docker image
```
docker build --tag qemu .
```

## run container, save ID, copy artifact(s)
```
mkdir artifact
docker run -it --cidfile=qemu.cid qemu true
docker cp "$(cat qemu.cid):work/artifact/." artifact/.
```

## review final artifact(s)
```
ls -al artifact/
```

## cleanup container, ID-file, and image
```
docker container rm $(cat qemu.cid)
rm qemu.cid
docker image rm qemu
```

## really, really cleanup docker
```
docker system prune --force
```
