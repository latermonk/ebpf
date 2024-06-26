# learning-ebpf




## start vm with limactl
```
limactl start learning-ebpf.yaml
limactl shell learning-ebpf
```


## You'll need to be root for most of the examples
```
sudo -s
```



## Book

## Code 
https://github.com/lizrice/learning-ebpf/  



---
Reference:
```
# This example requires Lima v0.8.0 or later
images:
- location: "https://cloud-images.ubuntu.com/releases/22.04/release/ubuntu-22.04-server-cloudimg-amd64.img"
  arch: "x86_64"
- location: "https://cloud-images.ubuntu.com/releases/22.04/release/ubuntu-22.04-server-cloudimg-arm64.img"
  arch: "aarch64"

cpus: 4
memory: "10GiB"

mounts:
- location: "~"
  writable: true
- location: "/tmp/lima"
  writable: true
provision:
- mode: system
  script: |
    apt-get update
    apt-get install -y apt-transport-https ca-certificates curl clang llvm jq
    apt-get install -y libelf-dev libpcap-dev libbfd-dev binutils-dev build-essential make 
    apt-get install -y linux-tools-common linux-tools-$(uname -r) 
    apt-get install -y bpfcc-tools
    apt-get install -y python3-pip
```