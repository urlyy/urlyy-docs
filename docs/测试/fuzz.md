# 介绍
fuzz(模糊测试)是一种运行时软件测试技术，简单来说就是通过生成大量的输入数据，通过多次的运行，试图触发程序的漏洞。

虽然是力大砖飞，但也要有效率，现代计算机的算力和电力不是给我们浪费的。因此会基于某些指标(如代码覆盖率)进行输入数据的引导性生成。输入数据的生成一直是fuzz的研究重难点。

# Sanitizer
对于c和cpp，由于过度信任程序员，一些本应报的错却没有报。如下面的例子。
```c
#include <stdlib.h>

int main() {
    // 分配内存但不释放，造成内存泄漏
    int *ptr = (int*)malloc(sizeof(int));
    *ptr = 42;
    // 访问已释放的内存
    free(ptr);
    *ptr = 100;  // 这里会触发 use-after-free 错误
    return 0;
}
```
使用如下命令运行
```shell
gcc main.c -o main
./main
```
然而，加上AddressSanitizer，就可以在运行时发现这个错误。
```shell
gcc -fsanitize=address main.c -o main
./main
```

然而，Sanitizer本质上是通过编译期插桩实现的，会较大地影响程序运行的时空性能，所以也不能在生产环境滥用。

Sanitizer有很多种类和用法，资料可参考:
- [github.com/google/sanitizers/wiki](https://github.com/google/sanitizers/wiki)

# AFL
对于只拿来用的测试人员来说，直接使用[afl++](https://github.com/AFLplusplus/AFLplusplus)会更合适。



# libFuzzer
[LibFuzzer](https://llvm.org/docs/LibFuzzer.html)