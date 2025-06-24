![](https://hits.sh/liufinback.github.io/2025-06-23 memccpy与memcpy的区别.md.svg)
1. memccpy语句在碰到`canRepair[k].type=10`就不能正常拷贝

``` cpp
struct SPC_BADPOINTINFO
{
	int  	x;         //坏点坐标x
	int  	y;         //坏点坐标y
	int  	type;      //坏点修补类型
	char 	reserve[4];
};
	
memccpy(&canRepair[k - 1], &canRepair[k], 1, sizeof(canRepair[0]));

canRepair[k].x = 455;
canRepair[k].y = 20;
canRepair[k].type = 9;
//此时拷贝的结果正常：
canRepair[k-1].x = 455;
canRepair[k-1].y = 20;
canRepair[k-1].type = 9;

canRepair[k].x = 455;
canRepair[k].y = 20;
canRepair[k].type = 10;
//此时拷贝的结果不正常：
canRepair[k-1].x = 455;
canRepair[k-1].y = 20;
canRepair[k-1].type = 9; //？？还是9
```

2. 用memcpy或者直接赋值结果都是正常的。

``` cpp
memcpy(&canRepair[k - 1], &canRepair[k], sizeof(canRepair[0]));
// 或者
canRepair[k-1].x = canRepair[k].x;
canRepair[k-1].y = canRepair[k].y;
canRepair[k-1].type = canRepair[k].type;
```

3. memccpy和memcpy有什么不同呢，为什么会有这个不同呢？
查到一个解释是`memccpy` 函数的原型是 `void *memccpy(void *dest, const void *src, int stop, size_t n)`。它用于复制内存，最多复制 `n` 个字节。在复制过程中，它会检查源内存区域中的每一个字节，如果遇到与 `stop` 参数指定的字符（它的值会被转换为无符号字符）相等的字节，就停止复制。它返回一个指向目标存储区中停止复制后的位置的指针（即下一个字节的位置），如果在复制完成前没有遇到这个停止字符，则返回 `NULL`

