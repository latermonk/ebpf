


---
# Reference:    
Code:  
https://github.com/vincentmli/bpf-samples/blob/master/tcp_ack.c     

command:  
```
A quick demo of BPF XDP program to drop packet, sample code here:https://github.com/vincentmli/bpf-sam...
/*
* Sample XDP/tc program, sets the TCP PSH flag on every RATIO packet.
* compile it with:
*      clang -O2 -emit-llvm -c tcp_ack.c -o - |llc -march=bpf -filetype=obj -o tcp_ack.o
 * attach it to a device with XDP as:
 *      ip link set dev lo xdp object tcp_ack.o verbose
* attach it to a device with tc as:
*      tc qdisc add dev eth0 clsact
*      tc filter add dev eth0 egress matchall action bpf object-file tcp_ack.o
* replace the bpf with
*      tc filter replace dev eth0 egress matchall action bpf object-file tcp_ack.o
*/
```

```
clang -O2 -emit-llvm -c tcp_ack.c -o - |llc -march=bpf -filetype=obj -o tcp_ack.o
```

```
 ip link set dev lo xdp object tcp_ack.o verbose
```

command reference:       
https://github.com/xdp-project/xdp-tutorial/tree/master/basic01-xdp-pass   

