# OpenCL要点记录

## OpenCL C编程语言

### 地址空间限定符

OpenCL提供的不相交的命名地址空间有__global,__local,__constant和__private. 程序中函数参数或函数局部变量的地址空间名称是 __private.
