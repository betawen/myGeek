# Project0

### Points:修改Makefile

`make depend`；

`make`；

出现问题`u_char`,去掉makefile中的`Werror`;

出现问题`undefined`,增加编译选项`-fno-stack-protector`，详情见`project0/build/makefile`;

`make clean`;

`make`;

`vi bochsrc`,详情见`project0/build/bochsrc`;

`bochs -f bochsrc`.
