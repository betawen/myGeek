# bochs安装和nasm安装

### bochs

靠谱网站下载`bochs-2.6.tar.gz`

`cd bochs-2.6`

`./configure`

`make`

`sudo make install`

`bximage`,`fd.[hd]`之间选择`fd`,命名时输入你想要的名字，其他默认即可（命名默认a）

### nasm

`sudo apt-get install nasm`,若后续步骤无问题，则按此执行，若有问题，则参考`bochs`的安装过程

`nasm -v`版本检查

### bochs简单引导/测试

`dd if=boot.bin of=a.img bs=512 count=1 conv=notrunc`，`boot.bin`来源？

`vi boot.asm`,内容如下：

​	 `org 07c00h		;告诉编译器程序加载到7c00处`

​ 	`mov ax,cs`

​ 	`mov ds,ax`

​ 	`mov es,ax`

​ 	`call DispStr		;调用显示字符串例程`

​	 `jmp $`

`DispStr:`

​ 	`mov ax,BootMessage`

​	 `mov bp,ax		;ES:BP=串地址`

​ 	`mov cx,16			;CX=串长度`

​ 	`mov ax,01301h		;AH=13,AL=01h`

​	 `mov bx,000ch		;页号为0（BH=0）黑底红字（BL=0Ch,高亮）`

​	 `mov dl,0`

​ 	`int 10h		;10h号中断`

​ 	`ret`

`BootMessage:		db="Hello OS world!"`

​ 	`times 510-(\$-$$)	db 0	;填充剩下的空间，使生成的二进制代码恰好为512字节`

​	 `dw 0xaa55		;结束标志`



`nasm boot.asm -o boot.bin`

继而执行`dd`……命令，出现提示三行

配置`bochsrc`，内容参照`project0/build/bochsrc`,注意目录名称和软盘名称的正确性。

