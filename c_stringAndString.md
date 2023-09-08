# 复习与拓展：c串和string
## c字符串
```c++
//字符串结束标志  \0
// C 语言规定:以  \0  作为字符串结束标志
//代表 ASCII 码为  0  的字符，表示一个"空字符"只起一个标志作用)
	char s[30] = "apple\0banana";
	cout << s << endl;//apple
	cout << s + 6 << endl;//banana
```
----------
### 常见字符串输入
```c++
char str[31];
cin >> str;
cout << str << endl;
cin.getline(str, 31);
cout << str;
```
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/597c9836-1c41-4db3-a135-9d05e40b9832)
### 一些操作函数与单个字符串输出
- 检查字母、数字字符函数 isalnum  if ( isalnum (ch) ) putchar(ch)；
- 检查字母函数 isalpha
- 检查数字字符函数 isdigit
- 检查大写字母函数 isupper
- 检查小写字母函数 islower  if(islower(s[i])) ++cnt；
- 小写字母转换为大写字母函数 toupper  ch = toupper(ch)；
- 大写字母转换为小写字母函数 tolower  ch = tolower(ch);
  
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/59039f18-32a5-482f-99e8-70e4cb5c2d14)
#### 例：把小数化成分数
思路：
1. 用char[]来存储小数char[0]='0';char[1]='.';
2. 约分,用gcd()函数
3. 输出
```c++
#include<iostream>
#include<cstring>
#include<algorithm>
#include<cmath>
using namespace std;
int gcd(int a, int b) {
	int r;
	while (r = a % b) {
		a = b;
		b = r;
	}
	return b;
}
int main() {
	char a[20];
	int x = 0;
	int y = 1;
	cin >> a;
	for (int n = 2; n < strlen(a); n++) {
		x = x * 10 + (a[n]-'0');//记得要减去一个‘0’
		y *= 10;
	}
	int m = gcd(x, y);
	cout << x << " " << y << " " << m << endl;
	cout << x / m << "/" << y / m << endl;
	return 0;
}
```
----------
### 常用的字符串运算函数
1. 计算长度：int strlen(s) 不计'\0'的长度
2. 拷贝:char* strcpy(char* str1, char* str2)
     - char* str**n**cpy(char* str1, char* str2,**size_t n**)功能类似，但最多拷贝n个字符，不够的用'\0'填充
```c++
//拷贝字符串 strcpy
//原型char* strcpy(char* str1, char* str2)
//其中:参数 str1、str2 为字符串中某个字符的地址
	char str1[31], str2[31];
	strcpy(str1, "Apple is sweet");
	strcpy(str2, str1);
//函数功能:将"字符串"完整地复制到"字符数组"中，字符数组中原有内容被覆盖。(连同结束标志一复制)
	return 0;
```
3. 字符串比较函数：int strcmp(char* str1,char* str2)
     - char* str**n**cmp(char* str1, char* str2,**size_t n**)功能类似，但最多比较n个字符，碰到不相等则提前返回   
  返回值：
      - 1比2大：-1 (<0)
      - 1比2小：1 (>0)
      - 1,2相同：0
5. 连接字符串：char* strcat(char* str1,char* str2)
   将地址str2后面的全部字符接到地址str1串的后面
6. 取子串
 ```c++
char* strstr(const char* str1, const char* str2);
//其中 : 参数 str1、str2 为字符串中某个字符的地址
char a[18] = "strayaabirds";
char b[10] = "aa";
char* p = strstr(a, b);
cout << p << endl;//aabirds
p = strstr(a, "cab");
cout << p << endl;//无输出
```
6. size_t一种用来记录大小的数据类型，和(unsigned)long int类似
例题：剪花布条：找子串
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/9617b9a5-81d4-436c-a92a-d997753e5a07)
```c++
int main() {
	char s1[1001], s2[1000], s[1000];
	while (cin >> s1) {
		int n = 0;
		if (s1[0] == '#')break;
		cin >> s2;
		int len = strlen(s2);
		for (int i = 0; i <= strlen(s1) - len;i++) {
			strcpy_s(s, s1 + i);
			s[len] = '\0';
			if (strcmp(s, s2)==0) {
				i += len-1;
				++n;
			}
		}
		cout << n << endl;
	}
	return 0;
}
```
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/f6ced048-e3f0-4a86-ab38-7de959a7bd72)

---------
## string
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/d8f4fcab-9b67-436e-9152-e97086f75680)
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/11722e66-90fd-4977-b239-46e4a2975110)
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/9cfde872-5ea2-4314-808e-d285cfc80006)
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/15961e7d-7d35-4973-a52a-e0075c0e22a5)
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/93bbbecf-0733-4fab-997c-1816c8aeb07f)
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/c0506580-79bf-4056-ae51-4de4f73b6ec3)            

------
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/0b801f50-20cd-461f-8c3d-63fea5cf8553)
```c++
string s = "hello000000";
	cout << s[s.find_last_not_of('0')] << endl;//输出‘o’
```
 -------
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/87353507-fd9f-4700-a9e3-80161b7759f3)
再创一个string，当上下加起来大于10的时候把s[i]=1,最后进一格加上这个string

> 2023.9.8😸




