#  drop icmp demo

## Prepare

```shell
sudo apt update
sudo apt install clang llvm git vim wget -y
```


```shell
git clone --recurse-submodules https://github.com/libbpf/bpftool.git
cd src
make
sudo make install
```

golang:
```shell
wget https://go.dev/dl/go1.22.1.linux-arm64.tar.gz
```


```shell
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.22.1.linux-amd64.tar.gz
```

```shell
export PATH=$PATH:/usr/local/go/bin
```

```shell
 go version
```



## Install bpftool
```shell
git clone --recurse-submodules https://github.com/libbpf/bpftool.git
cd src
make
sudo make install
```

如果報錯：
asm/types.h' file not found

```shell
apt install linux-headers-`uname -r`
```

根据实际情况做链接
```shell
sudo ln -s /usr/include/x86_64-linux-gnu/asm /usr/include/asm
```


## 写程序1
libbpf目录下 ./ksp/bpf/ 放文件 dicmp_kern.c & Makefile 


编译:
```shell
clang -S \
    -g \
    -target bpf \
    -I../../libbpf/src\
    -Wall \
    -Werror \
    -O2 -emit-llvm -c -o dicmp_kern.ll dicmp_kern.c
```


```shell
llc -march=bpf -filetype=obj -O2 -o dicmp_kern.o dicmp_kern.ll
```

## 写程序2
libbpf目录下 usp下放 go程序

编译：
```shell
go mod init dicmp
go mod tidy
CGO_ENABLED=0 go build . 
sudo ./dicmp_usp
```



## 测试丢包

```shell
go mod init dicmp
go mod tidy
CGO_ENABLED=0 go build . 
sudo ./dicmp
```






---
https://admida0ui.tech/2023/08/11/ebpf/     
https://github.com/adamlahbib/pingkiller     
https://stackoverflow.com/questions/77454504/asm-types-h-error-during-compilation-of-ebpf-code      


