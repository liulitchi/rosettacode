## 巴贝奇的问题

查尔斯·巴贝奇（Charles Babbage），英国数学家。为了研制分析机，花费了大量时间和金钱。并相信他的分析机可解决各种数学问题，他举了一个例子：

> 一个数平方后，最末六位为 26 9696 ，那这个数的最小值为多少？

> > —— 巴贝奇，致鲍登勋爵的信，1837年

他估计答案可能是 9 9736 ，平方为 99 4726 9696； 不过他也不能确定。

### 任务

运用你熟悉的编程语言，验证巴贝奇的猜测。


### 解答

- 1. C 语言

```c
#include <stdio.h>
#include <limits.h>

int main(void) {
	int current = 518; 	// 设 current 为要求的整数，已知 269696 的平方根为 519，
                      // 我们先从 518 开始
	int square;         // 设 square 为 current 的平方数
 
	// 为 square 求十万的模，然后验证
	while (((square = current * current) % 1000000 != 269696) && (square < INT_MAX)) {
		current += 2;
	}
 
	if (square > INT_MAX)
	    printf("已超出最大值。");
	else		   
	    printf("所求值为 %d 。\n", current);
  
	return 0;
}
```
