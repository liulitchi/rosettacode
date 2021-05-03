## 巴贝奇问题 [原文](https://rosettacode.org/wiki/Babbage_problem)

查尔斯·巴贝奇（Charles Babbage），英国数学家。为了研制分析机，几乎投入了毕生的的时间和精力。他期望分析机可以解决各类数学难题，如下面一个例子：

> 一个整数平方后，最后六位是26 9696，那这个数的最小值是多少？

>	—— 巴贝奇，1837年，写给鲍登勋爵的信。

他估计答案可能是9 9736 ，平方为99 4726 9696； 不过他也不太确定。

### 任务

使用你熟悉的编程语言，来验证巴贝奇的猜测。

### 解答

1. C 语言

```c
#include <stdio.h>
#include <limits.h>

// 根据题意，很明显该整数的个位数是4或6，
// 已知269696的平方根是519，我们从524开始，验证各个偶数 

int main(void) {
	int current = 524;     // 设 current 为所求的整数                              
	int square;            // 设 square 为 current 的平方数
 
	// 为 square 取百万的模，然后验证
	while (((square = current * current) % 1000000 != 269696) && (square < INT_MAX)) {
		current += 2; 
	}
 
	if (square > INT_MAX)
	    printf("已超出最大值。");
	else		   
	    printf("所求值为 %d。\n", current);
  
	return 0;
}
```
