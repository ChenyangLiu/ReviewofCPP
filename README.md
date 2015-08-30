# 程序设计复习

以下所有内容整理自孙甲松老师课件，代码均在GCC 4.9下编译通过。总结的内容比较简略，如有问题或补充，请联系[我](mailto:lcy_00000@163.com)，或者直接Pull request

## C语言部分
### 计算机中数的表示
原码：符号位在最高位，0表示正，1表示负，数值部分按一般的二级制形式表示

反码：对原码除符号位以外取反

补码：正数的补码与原码相同，负数的补码是在反码的最后一位上加1

偏移码：补码的符号位取反

---

浮点数表示方法：用尾数和阶码组合表示

### C语言中的数据类型

基本数据类型：整型，实型，字符型，void类型

### 文件

feof()函数会慢半拍

## CPP语言部分

### 函数重载
依据参数的类型与个数区分，静态绑定，编译时确定。

```cpp
double f(double x)
{
	return x;
}
int f(int x)
{
return x;
}
```
### 类

#### 静态成员

在所有类的实例中共用一个值（内存空间），适用于计数变量等。
需要注意在主程序外初始化
```cpp
class test
{
public:
	static int cnt;
}

int test::cnt = 0;
```

#### 友元
友元函数是能够访问类中的私有成员的非成员函数。友元函数从语法上看，它与普通函数一样，即在定义上和调用上与普通函数一样。
为什么需要友元？  我们已知道类具有封装和信息隐藏的特性。只有类的成员函数才能访问类的私有成员，程序中的其他函数是无法访问私有成员的。非成员函数可以访问类中的公有成员，但是如果将数据成员都定义为公有的，这又破坏了隐藏的特性。另外，应该看到在某些情况下，特别是在对某些成员函数多次调用时，由于参数传递，类型检查和安全性检查等都需要时间开销，而影响程序的运行效率。

firend关键字

#### 操作符重载

##### 双目运算符

重载为成员函数

```cpp
class test
{
public:
	test(double a) : a(a) {}
	test operator +(const test &right)
	{
		return test(sqrt(a * a + right.a * right.a));
	}
private:
	double a;
	
};
```

重载为友元函数

```cpp
class test
{
public:
	test(double a) : a(a) {}
	friend test operator +(const test &left, const test &right);
private:
	double a;
};

test operator +(const test &left, const test &right)
{
	return test(sqrt(left.a * left.a + right.a * right.a));
}
```

##### 单目运算符

重载为成员函数

```cpp
class test
{
public:
	void operator ++();	// 重载++a
	void operator ++(int); // 重载a++
private:
	double a;
};
```

重载为友元函数

```cpp
class test
{
public:
	friend void operator ++(test &t)	// 重载++a
	friend void operator ++(test &t, int) // 重载a++
private:
	double a;
};
```
##### 类型转换函数

```cpp
T operator T()
```
#### 类的继承与派生

```cpp
class derived : public base
```

#### 虚函数

基类与派生类拥有同名同参数的函数，采用动态束定，运行时通过虚函数表确定调用的函数。virtual关键字

#### 纯虚函数

存在于无法实例化的抽象类中

```cpp
virtual double fun()=0;
```

#### 虚基类

多继承时只继承自一个基类实例

```cpp
class derived : virtual public base
```

### 模板

```cpp
template<class T>
```
