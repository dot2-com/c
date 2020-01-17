# 标准输出文件(stdout)，标准错误文件(stderr)，文件重定向(>)


### stdout 和 stderr

我们前面用 `printf` 函数可以输出我们想要显示的内容，默认会把内容输出到显示器。

在c语言中，我们可以把输出内容到显示器看作是写入内容到文件，系统规定 

0 表示标准输入文件 `stdin`（默认就是键盘），我们在后面讲文件操作的时候会讲到。

1 表示标准输出文件 `stdout`（默认就是显示器）

2 表示标准错误文件 `stderr`（默认也输出到显示器）


通过 `fprintf` 函数可以指定输出到哪个文件。

例如  `fprintf(stdout, "dot2.com");` 和 `printf("dot2.com");` 是等效的，因为前面说过 `printf` 默认就是输出到标准输出文件 `stdout`

同样也可以用 `fprintf(stderr, "dot2.com");` 或 `perror("dot2.com");` 输出内容到标准错误文件，默认会输出到显示器。

那么 `stdout` 和 `stderr` 都输出到显示器，有什么区别呢？

### 文件重定向

假设有如下代码：

```c
#include <stdio.h>

int main(void){
	fprintf(stdout, "点点学习网 dot2.com");
    fprintf(stderr, "百度 baidu.com");
    return 0;
}
```

`a>test.txt` 只能看到输出 `百度 baidu.com` ，`点点学习网 dot2.com` 被重定向到 `test.txt` 文件中。

`a 1>test.txt`  和上面的命令效果是一样的，`1` 表示 `stdout`，默认就是将标准输出文件的内容重定向到 `test.txt`

`a 2>test.txt`  只看得到输出 `点点学习网 dot2.com`，`百度 baidu.com` 被重定向到 `test.txt` 文件中。

`a 1>1.txt 2>2.txt` `stdout` 和 `stderr` 分别重定向到 `1.txt` 和 `2.txt`。

`a>test.txt 2>&1` `stdout` 和 `stderr` 都冲重定向到 `test.txt`

`>` 会覆盖原有文件的内容，`>>` 表示追加，在原有文件的基础上增加，不会覆盖原有内容。

