#  # ebpf start



overview

ebpf









---

## install lib
```
apt-get install -y make clang llvm libelf-dev libbpf-dev bpfcc-tools libbpf
```

## start the first 
```
cat /sys/kernel/debug/tracing/trace_pipe
```

Reference:     

https://github.com/feiskyer/ebpf-apps      
