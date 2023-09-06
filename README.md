## 复习and拓展：函数设计
### 传值
#### 最大公约数
```c++
unsigned gcd(unsigned int a, unsigned int b;) {
		unsigned int r;
		while (r = a % b) {
			a = b;
			b = r;
		}
		return r;
```
#### 判断素数
```c++
bool isPrime(int a){
		if (a < 2)return false;
		for (int i = 2; i * i <= a; ++i) {
			if (a % i == 0)return false;
		}
		return ture;
	}
```
----------
### 传指针
#### 用特定指针表示未查到
```c++
#define N 100;
int main() {
	int a[N];
	//.....
	while (cin >> x) {
		int* p = a;
		for (; p < a + N; ++p) {
			if (*p == x)break;
		}
		if(p==a+N)//....
		else //....
	}
}
```
#### 指针传递数组
```c++
	double ave(double* a, int n) {
		double sum = 0;
		for (int i = 0; i < n; i++) {
			sum += *(a + i);
		}
		return sum / n;
	}
```
#### STL的部分函数（传递首地址和尾地址）
```c++
reverse(a,a+n);
sort(a,a+n);
```
-------
### 传引用
```c++
//普通引用初始化的时候需要*左值*
		int& rInt = 5; //error
	//只有 const 类型的引用才能直接赋*常量*
		const int& rInt = 5; //ok
	//const引用不能修改附属实体的值
		int val = 6;
		const int& rInt = val;
		val++;//ok
		rInt++;//error
```
