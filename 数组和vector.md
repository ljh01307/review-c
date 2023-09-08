# 数组和vector
### 例题：
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/832a4959-9eea-4d9f-b159-2be0a03453ae)
解答：
```c++
int main() {
	int n;
	cin >> n;
	int a[100];
	for (int i = 0; i < n; i++) {
		cin >> a[i];
	}
	int max[100];
	max[0] = a[0];
	int result = 0;
//思路如图
	for (int i = 1; i < n; i++) {
		if (max[i - 1] < 0)max[i] = a[i];
		else max[i] = a[i] + max[i - 1];
		if (max[i] > result)result = max[i];
	}
	cout << result << endl;
	return 0;
}
```
------------
### 数组排序
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/a7ddae0f-c342-4dbc-994c-bccc71275a3d)

------------
#### 查找函数
int* find(num,num+n,x)    查不到返回后面的地址(num+n)

### 二分查找
```c++
int bSearch(int* a, int n, int x) {
	int up = n - 1, low = 0;
	int mid = (up + low) / 2;
	while (low <= up) {
		if (x < mid)up = mid - 1;
		else if (x > mid)low = mid + 1;
		else return mid;
	}
	return -1;
}
```
指针版
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/445dea70-ecd7-49e9-946f-f840202e6153)

-----------------
upper_bound()// 返回最后一个 <=x 的元素的下一个地址值或者 a (所有元素都大于 x)
lower_bound()// 返回第一个 >=x 的元素的地址值，或者a+n (所有元素都小于x )  **if(lower_bounder!=a+n)证明已经查找到了**
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/62f95f02-296c-490f-a1c7-db6d4f91cfed)

---------
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/24f59e89-f5ef-41c3-aa60-3af1f5b3821c)
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/030d6395-b850-41bf-9ce5-0670d76f7838)
> 不要忘记要先排序好

-------------

### 动态分配实现动态数组
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/45db45dc-b346-453d-abea-68cd110a4240)

--------------

### memset&memcpy
```c++
int main() {
	int n = 10;
	int* p = new int[n];
	memset(p, -1, n * sizeof(int));
	for (int i = 0; i < n; i++) {
		cout << *(p + i) << endl;
	}
	cout << "-----------" << endl;
	int* q = new int[n];
	memcpy(q, p, 5 * sizeof(int));
		for (int i = 0; i < n; i++) {
			cout << *(q + i) << endl;
		}
	return 0;
}
```
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/51a4e29e-a55b-4155-b7b0-64212bc8a6c7)

-----------------

### array(和静态数组对应)
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/78812a49-6b0e-44d4-b6ac-90ba5c21b3bb)

----------

## vector(和动态数组对应)
```c++
class CVector {
	int cap;
	int sz;
	int* buf;
public:
	CVector() { cap = 4; sz = 0; buf = new int[4]; }
	CVector(unsigned n, int val = 0);
	CVector(const CVector& a);
	void print();
	void push_back(int val);
	void remove_pos(int pos);
	void remove_val(int val);
	int find(int val);
	int IsSortedVector();
	~CVector() {
		delete[] buf;
		buf = 0;
	}
};
CVector::CVector(unsigned n, int val) {
	buf = new int[n];
	cap = sz = n;
	for (int i = 0; i < sz; i++)
		buf[i] = val;
}
CVector::CVector(const CVector& a) {
	cap = sz = a.sz;
	buf = new int[cap];
	memcpy(buf, a.buf, sz * sizeof(int));
}
void CVector::print() {
	for (int i = 0; i < sz; i++) {
		cout << buf[i] << " ";
	}
	cout << endl;
	cout << cap << " " << sz << " \n";
	
}
void CVector::push_back(int val) {
	if (sz == cap) {
		cap += 4;
		int* newBuf = new int[cap];
		memcpy(newBuf, buf, sz * sizeof(int));
		delete[] buf;
		buf = newBuf;
		buf[sz++] = val;
	}
	else {
		buf[sz++] = val;
	}
}
int CVector::find(int val) {
	if (sz == 0)return -1;
	int pos = 0;
	for (int i = 0; i < sz; i++) {
		if (buf[i] == val)return i;
	}
}
void CVector::remove_pos(int pos) {
	if (sz == 0 || pos < 0 || pos >= sz)return;
	for (int i = pos; i < sz; i++)buf[i] = buf[i + 1];
	sz--;
}
void CVector::remove_val(int val) {
	if (sz == 0)return;
	int pos = this->find(val);
	remove_pos(pos);
	sz--;
}
int CVector::IsSortedVector() {
	if (sz == 0)return 0;
	for (int i = 1; i < sz; i++) {
		if (buf[i] < buf[i - 1]) {
			return 0;
		}
	}
	return 1;
}
```
验证：
![image](https://github.com/ljh01307/review-cPlusPlus/assets/112680236/cc324986-66f3-4653-8b46-c82a73c78eb6)


