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
