#  README

##  start a vm
```
vagrant init ubuntu/impish64 // 21.10

22.04  ubuntu/jammy64

vagrant init ubuntu/jammy64 // 22.04
```

## install lib
```
apt-get install -y make clang llvm libelf-dev libbpf-dev bpfcc-tools libbpf
```

## start the first 
```
cat /sys/kernel/debug/tracing/trace_pipe
```
