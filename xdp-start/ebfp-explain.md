# ebpf start 

```
#!/usr/bin/python3  
from bcc import BPF

program = r"""
int hello(void *ctx) {
    bpf_trace_printk("Hello World!");
    return 0;
}
"""

b = BPF(text=program)
syscall = b.get_syscall_fnname("execve")
b.attach_kprobe(event=syscall, fn_name="hello")

b.trace_print()
```



---
# explain

**Line 1:** `#!/usr/bin/python3`
这是一条 shebang 指令，用于指定当前脚本的解释器是 Python 3。运行时，操作系统会自动检测到这个指令，并使用 Python 3 作为解释器来执行脚本。

**Line 2-3:** `from bcc import BPF`
这两个语句将 `BCC` 模块中的 `BPF` 变量导入当前脚本。`BCC` 是一个基于 eBPF 的系统调用跟踪工具，`BPF` 是其中的一个核心组件。

**Line 4-6:**
```python
program = r"""
int hello(void *ctx) {
    bpf_trace_printk("Hello World!");
    return 0;
}
"""
```
这是一条字符串，包含了一个 C 语言风格的函数定义。该函数名为 `hello`，它将被用来捕捉某个系统调用（在本例中是 `execve` 呼叫）的事件。

**Line 7:** `b = BPF(text=program)`
使用 `BPF` 对象来创建一个新的 BPF 程序，并传入前一个字符串作为该程序的定义。这个过程称为“编译” BPF 程序。

**Line 8:** `syscall = b.get_syscall_fnname("execve")`
从 BPF 程序中获取名为 `execve` 的系统调用函数的名称。在 Linux 中，系统调用是一个特殊的函数，可以通过该函数来访问操作系统的底层功能。

**Line 9:** `b.attach_kprobe(event=syscall, fn_name="hello")`
将前一个函数（`hello`）与前一个系统调用（`execve`）关联起来。这个过程称为“附加” kprobe。kprobe 是一种 Linux kernel 中的调试机制，用于捕捉系统调用事件。

**Line 10:** `b.trace_print()`
启动 BPF 程序，并开始追踪系统调用事件。在每个系统调用事件中，BPF 程序将执行相关函数（在本例中是 `hello`）并输出结果。

总的来说，这个程序使用 BCC 庫来创建一个 BPF 程序，该程序捕捉了 `execve` 系统调用的事件，并将这些事件转换为字符串输出。
