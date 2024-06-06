# LXC Installation

```bash
sudo apt install -y lxd
# sudo snap install lxd
```

## Usage

```bash
lxd init
```

Images

```bash
lxc remote list
```

```bash
lxc image info ubuntu:lts
```

```bash
lxc image list ubuntu:version
lxc image list centos:version
```

Launch container

```bash
lxc launch images:centos/8 vm
```

Container Info

```bash
lxc info vm
```

Shell login

```bash
lxc exec vm -- bash
lxc shell vm
```
