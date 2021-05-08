## 欧拉等幂和猜想

历经200余年的数学猜想，直到1966年，才由 Lander 和 Parkin 找到反例而被推翻。

> 欧拉等幂和猜想

> 对于每个大于2的整数n，任何n - 1个正整数的n次幂的和，都不是某正整数的n次幂。

1966年，莱昂·J·兰德（Leon J. Lander）和托马斯·R·帕金（Thomas R.Parkin）将数值限定为 250 ，在 CDC 6600 型号的计算机上进行了暴力破解。

### 任务

编写程序来搜索以下整数解决方案：

> a^5 + b^5 + c^5 + d^5 == e^5

其中 a ~ e 各不相等，且取值范围是(0， 250)。

### 相关知识

1. 费马小定理

> 假如 a 是一个整数，p 是一个质数，那么a^p - a 是 p 的倍数，可以表示为 a^p = a (mod p)

根据费马小定理，已知 x^2 = x (mod 2)，则 x^4 = x^2 (mod 2) = x (mod 2)，可推出 x^5 = x^2 (mod 2) = x (mod 2)。
已知 x^3 = x (mod 3)， 则 x^5 = x^3 (mod 3) = x (mod 3)。同理可知， x^5 = x (mod 5)。

2. 中国剩余定理

> 用现代数学的语言来说明，中国剩余定理给出了一元线性同余方程组有解的判定条件，并用构造法给出了在有解情况下解的具体形式。 

已知三个方程： x^5 = x (mod 2)， X^5 = x (mod 3)， x^5 = x (mod 5)。有 M = 30，M1 = 15，M2 = 10，M3 = 6。
根据 t1 * 15 = 1 (mod 2); t2 * 10 = 1 (mod 3); t3 * 6 = 1 (mod 5)，可解得 t1 = t2 = t3 = 1。
综上可得， x^5 = a1 * t1 * M1 + a2 * t2 * M2 + a3 * t3 * M3 = 31x = x (mod 30)。

### 解答

1. C 语言
```c
#include <stdio.h>

int main(void)
{
	int N = 250;
	long long pow5[N];
	for (int i = 0; i < N; i++)
		pow5[i] = i * i * i * i * i;
	for (int d = 4; d < N; d++) {
		for (int c = 3; c < d; c++) {
			for (int b = 2; b < c; b++) {
				for (int a = 1; a < b; a++) {
					long long sum = pow5[a] + pow5[b] + pow5[c] + pow5[d];
					for (int e = d + 1; e < N; e++) {
						if (sum == pow5[e])
							printf("%d %d %d %d %d\n", a, b, c, d, e);
					}
				}
			}
		}
	}
	return 0;
}
```

2. Python
```python3
```

3. Rust
```rust
```

4. Go 语言
```go
package main
 
import (
	"fmt"
	"log"
)
 
func main() {
	fmt.Println(eulerSum())
}
 
func eulerSum() (a, b, c, d, e int) {
	var pow5 [250]int
	for i := range pow5 {
		pow5[i] = i * i * i * i * i
	}
	for d = 4; d < len(pow5); d++ {
		for c = 3; c < d; c++ {
			for b = 2; b < c; b++ {
				for a = 1; a < b; a++ {
					sum := pow5[a] + pow5[b] + pow5[c] + pow5[d]
					for e = d + 1; e < len(pow5); e++ {
						if sum == pow5[e] {
							return
						}
					}
				}
			}
		}
	}
	log.Fatal("no solution")
	return
}
```


