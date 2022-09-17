# C语言

.c - 源文件

.h - 头文件

```c
// 包含一个 stdio.h的文件 
// std-标准(standard)  i-库(input) o-输出(output)
#include <stdio.h>

// int 是整型的意思 
// main前面的int 表示main函数调用后返回一个整型值
int main() {   // 主函数-程序的入口-main函数只能有一个

	printf("hehe\n"); // 运行代码 在控制台输出hehe \n是打印后换行

	return 0;  // 返回 0
}
```

### 1.数据类型

```c
%c             字符
%d             有符号十进制整数
%f             浮点数(包括float和doulbe)
%e(%E)     	   浮点数指数输出[e-(E-)记数法]
%g(%G)     	   浮点数不显无意义的零"0"
%i             有符号十进制整数(与%d相同)
%u             无符号十进制整数
%o             八进制整数        		     0123
%x(%X)     	   十六进制整数0f(0F)          0x1234
%p             指针
%s             字符串

    
char ch = 'A';  // char -字符数据类型
// %c 是打印字符格式的数据(以字符的形式打印ch)
printf("%c\n", ch);

int age = 20; // int -整型数据类型
// %d 是打印整型十进制数据
printf("%d\n", age);

```

| 数据类型名 | 数据类型名(中) |
| ---------- | -------------- |
| char       | 字符数据类型   |
| short      | 短整型         |
| int        | 整型           |
| long       | 长整型         |
| long long  | 更长的整型     |
| float      | 单精度浮点数   |
| double     | 双精度浮点数0  |

| C声明         | 32位机器（X86） | 64位机器（X64） |
| ------------- | --------------- | --------------- |
| char          | 1               | 1               |
| short int     | 2               | 2               |
| int           | 4               | 4               |
| long int      | 4               | 8               |
| long long int | 8               | 8               |
| char *        | 4               | 8               |
| float         | 4               | 4               |
| double        | 8               | 8               |

```c
// 数据类型的大小  （以下单位为 字节   1字节=8个比特位）
int main() {
	// x32位
    printf("%d\n", sizeof(char)); // 1
	printf("%d\n", sizeof(short)); // 2
	printf("%d\n", sizeof(int)); // 4
	printf("%d\n", sizeof(long));// 4
	printf("%d\n", sizeof(long long)); // 8
	printf("%d\n", sizeof(float)); // 4
	printf("%d\n", sizeof(double)); // 8
	return 0;
}
```

### 2.变量

##### 1.变量与 局部/全局变量

```c
int num2 = 20; // 定义在大括号外的变量称 为 全局变量
// 当局部变量和全局变量的名字相同的时候，局部变量优先
int main() {
	// 常量变量
	// 变量： 类型 变量名 = 值

	// 向内存申请两个字节=16bit位 用来存放20
	short age = 20;
	float weight = 45.6f;

	int num1 = 10; // 定义在大括号中的变量 为 局部变量
	return 0;
}
```

##### 2.extern 声明外部变量(别的文件的全局变量)

```c
int main() {
	//extern 声明外部符号的（在别的文件）
	extern abc;
	//使用extern声明过的外部变量
	printf("hahaha = %d", abc); //hahaha = 2022

	//说明全局变量的作用域是整个工程
	return 0;
}
```

##### 3.变量相加

```c
int main() {
	// 计算2个数的和
	int num1 = 0;
	int num2 = 0;
	int sum = 0;
	//输入数据 - 使用 输入函数 scanf   (在控制台内输入两个数字后 计算数字是多少)
	//%d%d 意思是要放入两个整数
	scanf_s("%d%d", &num1, &num2); // &取地址符号()

	sum = num1 + num2;

	printf("num = %d\n", sum);
	return 0;
}
```

### 3.常量

##### 1.常量分类

- 字面常量
- const 修饰的常变量
- #define定义的标识符常量
- 枚举常量

```c
//3.#define定义的标识符常量
#define Max 10

//4.枚举常量(一一列举)
enum Sex {
	MALE, //男  默认为0
	FEMALE, //女  默认为1
	SECRET //保密  默认为2
};
int main() {
	//1.字面常量 （字面上理解的常量）
	3; // 字面常量
	100; // 字面常量
	3.14; // 字面常量

	//2.const 修饰的常变量（是变量但是又有常属性，在变量无法使用的场景也无法使用）
	const int num = 10; // 在变量前加上const 变成常变量
	// num = 15; 修改则报错

	//3.#define定义的标识符常量
	int arr[Max] = { 0 }; // 在常量无法使用的场景也能使用(数组长度参数)

	//4.枚举常量(一一列举) 定义的值有默认值为下标值
	//使用在外面定义的枚举常量
	enum Sex s = MALE;
	//但是s还是一个变量 只是MALE（外面定义的枚举常量）为常量而已
	//s = 0

	return 0;
}
```

##### 2.const 修饰指针变量

```c
int main() {
	int m = 10;
	int n = 100;

	int* p = &m;  // 储存了&m的地址
	//可以的操作：
	*p = 0; //修改值
	p = &n; //修改地址

	int const* p = &m;  // 使用const 修饰了*p
	//可以的操作：
	p = &n;
	//不可以的操作：
	*p = 0;

	int const* const p = &m; // 使用const修饰了 *p 与 p
	//不可以的操作：
	p = &n;
	*p = 0;
}
```











### 4.生命周期

- 变量的生命周期指的是变量的创建到变量的销毁之间的一个时间段
  - 1.**局部变量**的生命周期：进入作用域生命周期开始，出作用域生命周期结束
  - 2.**全局变量**的生命周期：整个程序的生命周期



### 5.字符串

- 由双引号引起的一串字符 就是字符串

```c
#include <string.h>
int main() {
	// "abc" 实际上在最后面有一个隐藏的'\0' 所以长度为3
	char arr1[] = "abc"; //将字符串储存在字符中

	//字符串的结束标语 是'\0' 如果没有自己加上，是不会停止的，长度或打印出来的数据则不正确
	char arr2[] = { 'a','b','c',0 };
	//%s 意思是打印字符串
	//printf("%s\n", arr1);
	printf("%s\n", arr2);

	printf("%d\n", strlen(arr1));
	printf("%d\n", strlen(arr2));

	return 0;
}
```

### 6.分支

#####  1.if语句

- 语句结构：

  - ```c
    // 单分支
    if(表达式){
        语句;
    }
       
    // 双分支
    if(表达式){
        语句1;
    }else {
        语句2;
    }
        
    
    // 多分支
    if(表达式1){
        语句1;
    }else if(表达式2){
        语句2;
    }else{
        语句3
    }
    ```


##### 2.switch语句

- 语句结构：

  - ```c
    switch(整型表达式){
          // 语句项
           case 整型常量表达式;
            	语句;
            	break; // 达成条件 运行代码块后 break跳出switch语句
           case xxx;
            	语句;
            	break;
            ...
           	default:
    			语句
    		break;
    }
    ```

- 例子：

  - ```c
    int main() {
    	int day = 3;
    
    	switch (day)
    	{
    	case 1:
    		printf("星期一\n");
    		break;
    
    	case 2:
    		printf("星期二\n");
    		break;
    
    	case 3:
    		printf("星期三\n");
    		break;
    
    	case 4:
    		printf("星期四\n");
    		break;
    
    	case 5:
    		printf("星期五\n");
    		break;
    
    	case 6:
    		printf("星期六\n");
    		break;
    
    	case 7:
    		printf("星期天\n");
    		break;
    
    	default:
    		printf("我不到啊\n");
    		break;
    	};
    	return 0;
    }
    ```





### 7.函数

```c
// 自定义函数
Add(int x, int y) {
	//处理数据
	int z = x + y;
	//返回参数
	return z;
}

int main() {
	int num = 100;
	int num2 = 500;
	int sum = 0;
	//调用函数
	sum = Add(num, num2);

	printf("%d\n", sum);
	return 0;
}
```

##### 1.函数是什么

- 是一个大型程序中的某部分代码，由一个或多个语句块组成。它负责完成某项特定任务，而且相较于其他代码，具备相对的独立性。
- 一般会有输入参数并有返回值，提供对过程的封装和细节的隐藏。这些代码通常被集成为软件库。

- C语言中 函数的分类分为： **库函数**  与  **自定义函数**



##### 2.库函数

- 就是C语言提供的 包含大多基本操作的函数，供程序员使用。
- 大概分类有：数学函数、字符函数、字符串函数、输入输出函数、动态分配函数、随机函数...

- 使用库函数，必须包含 #include对应的头文件

- 常用的库函数查找网站：https://zhuanlan.zhihu.com/p/451192455

##### 3.自定义函数

- 自定义函数和库函数一样，有函数名，返回值类型和函数参数。
- 但是不一样的是这些都是我们自己来设计，这给程序员一个很大的发挥空间。

- 函数的组成：

  - ```c
    type fnName(para1,*){
        // 语句项
    }
    //type = 返回类型
    //fnName = 函数名
    //para1 = 函数参数
    ```

- 例子：写一个函数 找出两个数的较大值

  - ```c
    int getMax(int a, int b) {
    	int num = a > b ? a : b; // 判断哪个值大
    	return num; // 返回
    }
    
    int main() {
    	int a = 10;
    	int b = 20;
    	// getMax() 函数的使用
    	printf("%d\n", getMax(a, b));   //打印20
    
    	return 0;
    }
    ```

- 例子：交换两个变量的值

  - ```c
    void swap(int* pa, int* pb) {
    	int tmp = 0;
    	//根据指针地址交换数据
    	tmp = *pa;
    	*pa = *pb;
    	*pb = tmp;
    }
    
    int main() {
    	int a = 10;
    	int b = 20;
    
    	int* pa = &a; // 获取地址
    	int* pb = &b; // 获取地址
    	swap(pa, pb); // 使用函数 并传递地址
    
    	printf("a=%d  b=%d\n", a, b); // a=20 b=10
    
    	return 0;
    }
    ```

    



##### 4.函数参数

参数分为**实际参数(实参)** 与 **形式参数(形参)**

- 实际参数(实参)
  - 真实的传给函数的参数，叫实参。
  - 实参可以是：常量、变量、表达式、函数等等。
  - 无论实参是何种类型，在进行函数调用的时候，它们都必须有确定的值，以便把这些值传送给形参。



- 形式参数(形参)
  - 形式参数是指函数名后括号中的变量。
  - 因为形式参数只有函数被调用的过程中才实例化，所以叫形式参数。
  - 形式参数当函数调用完后，就自动销毁，因此形式参数只有在函数中才有效。

- 例子：

  - ```c
    int add(int a, int b) {
    	//函数调用后，在函数内使用的是   形参
    	int tmp = 0;
    	//根据指针地址交换数据
    	tmp = a + b;
    	//在函数内 形参的修改 不会影响实参
    	return tmp;
    }
    
    int main() {
    	int a = 10;
    	int b = 20;
    	//调用函数时 传入的参数就是    实参
    	int addNum = add(a, b);
    
    	printf("%d\n", addNum);
    
    	return 0;
    }
    ```

    



##### 5.函数调用

- 传值调用

  - 函数的形参和实参分别占有不同内存块，对形参的修改不会影响实参。

  - 例子：

    - ```c
      int getMax(int a, int b) {
      	int num = a > b ? a : b; // 判断哪个值大
      	return num; // 返回
      }
      
      int main() {
      	int a = 10;
      	int b = 20;
      	// getMax() 函数的使用
      	printf("%d\n", getMax(a, b));   //打印20
      
      	return 0;
      }
      ```





- 传址调用

  - 传址调用是把函数外部创建**变量的内存地址**传递给函数参数的一种调用函数的方式。
  - 这种传参方式可以让函数和函数外边的变量建立起真正的联系，也就是函数内部就可以直接操纵函数外部的变量。

  - 例子：

    - ```c
      void swap(int* pa, int* pb) {
      	int tmp = 0;
      	//根据指针地址交换数据
      	tmp = *pa;
      	*pa = *pb;
      	*pb = tmp;
      }
      
      int main() {
      	int a = 10;
      	int b = 20;
      
      	int* pa = &a; // 获取地址
      	int* pb = &b; // 获取地址
      	swap(pa, pb); // 使用函数 并传递地址
      
      	printf("a=%d  b=%d\n", a, b); // a=20 b=10
      
      	return 0;
      }
      ```

      

##### 6.函数的嵌套调用和链式访问

- 函数嵌套调用：

- 函数和函数之间可以有机组合。

- 函数嵌套调用例子：

  - ```c
    int a() {
    	printf("hahaha\n");
    }
    int b() {
    	int i = 0;
    	while (i <= 5)
    	{
    		a(); // 调用函数a
    		i++;
    	}
    }
    int main() {
    	b();
    	return 0;
    }
    ```

- 链式访问：

- 把一个函数的返回值 当成另一个函数的参数

  - ```c
    int main() {
    	int len = 0;
    	//非链式访问
    	len = strlen("abc");
    	printf("%d\n", len);
    
    	//把函数的返回值 放进一个函数的参数内 就是链式访问
    	printf("%d\n", strlen("abc"));
    
        printf("%d", printf("%d", printf("%d", 43););); // 打印出4321 
        // 因为printf返回值是打印的字符数
    	return 0;
    }
    ```

    





##### 7.函数的声明和定义

函数声明：

- 告诉编辑器有一个函数叫什么，参数是什么，返回类型是什么。但是具体是不是存在，无关紧要。
- 函数的声明一般出现在函数的使用之前，要满足先声明后使用。
- 函数的声明一般要放在头文件(.h)中的。



函数定义：

- 函数的定义是指函数的具体实现，交代函数的功能实现。



模块化例子：

```c
// add.c源文件  用来定义函数
add(int x, int y) {
	return x + y;
}
// add.h头文件  用来声明函数
#ifndef __ADD_H__ // 如果没有定义过(第一次引入)，为真 执行下面的代码
#define __ADD_H__ // 定义头文件
// 函数声明
add(int x,int y);

#endif

// test.c源文件 主文件 来调用、使用函数
#include "add.h"

int main() {
	int num1 = 5;
	int num2 = 10;

	printf("%d\n", add(num1, num2)); // 15

	return 0;
}
```





##### 8.函数递归

- 程序**调用自身**的编程技巧称为递归。
- 一个过程或函数再其定义或说明中有直接或间接的调用自身的一种方法，它通常把一个大型负责的问题层层转化为一个与原问题相似的规模较小的问题来求解，递归策略只需要少量的代码就可以解析过程所需要的的多次重复计算，大大减少代码量。
- 递归主要思考方式在于：大事化小



- 递归的两个必要条件：
  - 存在限制条件，当满足这个限制条件的时候，递归便不再继续。
  - 每次递归调用之后越来越接近这个限制条件。



- 递归的缺点：
  - 执行次数过多 则会出现栈溢出
  - 会出现栈溢出的需求 使用别的方法如循环



- 简答递归例子：

  - ```c
    int main() {
    	printf("haha\n");
    	main(); // 调用自身 不停执行main函数 一直打印haha
    	return 0;
    }
    ```

  - 递归无限重复时，会报错：《栈溢出》。  因为没有限制条件。



- 例子：接收一个整型数，按照顺序打印它的每一位，如：1234 输出 1 2 3 4

  - ```c
    void fnD(int num) {
    	if (num > 9) { // 如果传来的值大于9 则最少为10位数
    		fnD(num / 10); // 再给函数传递/10的值 进行递归
    	};
    	printf("%d\n", num % 10); // 打印  值的%10
    }
    
    int main() {
    	fnD(1234);  // 传递参数
    
    	return 0;
    }
    ```

- 例子：编写函数，不用临时变量获取数组长度。

  - ```c
    // 正常使用临时变量获取数组长度
    int fnD(char* str) {
    	// 计算字符串的长度
    	int lens = 0;
    	// 判断
    	while (*str != '\0') {
    		//当前这个字符 是不是字符串的结束语\0 如果不是则传递下一位字符
    		str++; // 指针+1 代表数组中当前字符的下一个字符
    		lens++; // 记录长度
    		//fnD(str);
    	}
    
    	return lens;
    }
    int main() {
    	char arr[] = { "abb" };
    	int len = printf("%d\n", fnD(arr));
    	// 传递数组 传递的不是整个数组 而是第一个元素的地址
    
    	return 0;
    }
    ```

  - ```c
    // 不使用临时变量获取数组长度
    
    int fnD(char* str) {
    	// 判断当前这个字符 是不是字符串的结束语\0 如果不是则传递下一位字符
    	if (*str != '\0') {
    		// 传递的是 str+1 是值的下一位
    		// 比如：第一次为bit *str=a   传递的第二次str+1后 *str为b
    		return 1 + fnD(str + 1);
    		// 思路：
    		// 第一次： 1+fnD('bc')
    		// 第二次： 1+1+fnD('b')
    		// 第三次： 1+1+1+fnD('\0')
    		//最后返回：1+1+1+0
    	}
    	else { // 如果是'\0' 则返回0
    		return 0;
    	}
    }
    
    int main() {
    	char arr[] = { "abc" };
    	// 传递数组 传递的不是整个数组 而是第一个元素的地址
    	printf("%d\n", fnD(arr)); // 3
    
    	return 0;
    }
    ```

- 递归与迭代例子：

  - ```c
    // 求n的乘阶（不考虑溢出）
    
    // 循环的方式
    int fnD(int num) {
    	int ret = 1;
    	for (int i = 1; i <= num; i++){
    		ret *= i;
    	}
    	return ret;
    }
    int main() {
    	char num = 5;
    	//求num的阶乘
    	printf("%d\n", fnD(num)); // 3
    	return 0;
    }
    
    // 递归的方式
    int fnD(int num) {
    	if (num <= 1) {
    		return 1;
    	}
    	else {
    		return num * fnD(num - 1);
    		// 相当于：
    		// 5 * fnD(5-1)=4 * fnD(4-1)=3 * fnD(3-1)=2 * fnD(2-1)=1*1
    	}
    }
    int main() {
    	char num = 5;
    	//求num的阶乘
    	printf("%d\n", fnD(num)); // 120
    	return 0;
    }
    
    ```

- 描述第n个斐波那契数（1 1 2 3 5 8 13....前两个数的和等于第三个数）

  - ```c
    // 递归并不适合斐波那契数的计算 会触发大量的计算 算第50时就会很慢很慢
    int fnD(int num) {
    	if (num <= 2) {
    		return 1;
    	}
    	else {
    		return fnD(num - 1) + fnD(num - 2);
    		// 相当于 fnD(6-1) + fnD(6-2)   往后推断
    		//   6
    		//  4 5
    		// 2 3 4
    	}
    }
    int main() {
    	char num = 6;
    	//求num个菲波那切数
    	printf("%d\n", fnD(num));
    	return 0;
    }
    ```

  - ```c
    // 有些算法不适合使用递归 ，所以需要迭代写法。
    int fnD(int num) {
    	int a = 1;
    	int b = 1;
    	int c = 1;
    
    	while (num > 2)
    	{
    		c = a + b;
    		// 第一次：c = 1+1
    		// 第二次：c = 1+2
    		// 第三次: c = 2+3
    		// 第四次: c = 3+5
    		a = b;
    		// 第一次：a = 1
    		// 第二次：a = 2
    		// 第三次: a = 3
    		// 第四次: a = 5
    		b = c;
    		// 第一次：b = 2
    		// 第二次：b = 3
    		// 第三次: b = 5
    		// 第四次: b = 8
    
    		// 1 1 2 3 5   执行了四次 6 -4 = 2  条件为num>2 才继续执行 而C的结果为8 正确
    		num--;
    	}
    	return c;
    }
    
    int main() {
    	char num = 6;
    	//求num个菲波那切数
    	printf("%d\n", fnD(num));
    	return 0;
    }
    ```

    





### 8.数组

- 数组定义：

```c
int main() {
    // 定义一个长度为10，类型为int的数组
	int arr[10] = { 0,1,2,3,4,5,6,7,8,9 };
    
    // 遍历数组
	int i = 0;
	while (i < 10)
	{
		printf("%d\n", arr[i]);
		i++;
	};

	return 0;
}
```



##### 1.一维数组的创建和初始化

- 数组的创建

  -  数组是一组相同类型元素的集合。数组的创建方式：

  - ```c
    int main() {
    	//type_t arr_name [const_n]
    	//类型	   名字    存放个数(只能放常量不能放变量)
    
    	//创建一个数组 - 存放整型 - 放10个
    	int arr[10] = {1,2,3};  // 不完全初始化（剩下的元素默认初始化为0）
    
    	//创建一个数组 - 存放字符 - 放5个
    	char arr2[5] = {"a","b"}; // 不完全初始化(剩下的元素默认初始化为0)
        char arr3[5] = "ab"; //ab后还有一个\0
        char arr4[] = "abcdef"; //没有存放个数 根据字符数计算数量 6+1(\0) =7
        
       	printf("%d\n", sizeof(arr4)); // 7 sizeof计算arr4所占空间大小 7个元素(包括\0)
    	printf("%d\n", strlen(arr4)); // 6 strlen求字符串的长度6个元素 遇到\0停止 不计算\0
    
        //1.strlen 和 sizeof没有关联
    	//2.strlen 是库函数 - 是求 字符串长度的 只能针对字符串求长度
    	//3.sizeof 是操作符 - 计算变量、数组、类型的大小（单位是字节）
    
        
            
        int a = 5;
        int arr2[a]; //报错 存放个数只能放常量 不能放变量
    	return 0;
    }
    ```

- sizeof、strlen例子：

  - ```c
    int main() {
    	char arr1[] = "abc";
    	char arr2[] = { 'a','b','c' };
    
    	printf("%d\n", sizeof(arr1)); // 4   a b c \0  没有括号的字符串最后有\0
    	printf("%d\n", sizeof(arr2)); // 3   a b c  放括号时 没有\0
    	printf("%d\n", strlen(arr1)); // 3   a b c \0  求\0之前的字符长度
    	printf("%d\n", strlen(arr2)); // 随机值 a b c  求\0之前的字符长度 而带括号没有\0只能往后找到\0为止 所以是随机值
    
    	return 0;
    }
    ```



##### 2.一维数组的使用

- [] 下标引用操作符，它就是访问数组的操作符。

  - ```c
    int main() {
    	//数组不完全初始化
    	int arr[10] = { 0 };
    	//计算数组的元素个数
    	int sz = sizeof(arr) / sizeof(arr[0]);
    	//对数组内容赋值 数组是使用下表来访问的，下标从0开始
    	for (int i = 0; i < sz; i++)
    	{
    		arr[i] = i;
    	}
    	//输出数组内容
    	for (int i = 0; i < sz; i++)
    	{
    		printf("%d\n", arr[i]); // 0 1 2 3 4 5 6 7 8 9
    	}
    	return 0;
    }
    ```

- 数组是使用下标来访问的，下标是从0开始。

- 数组的大小可以通过计算得到：

  - ```c
    int arr[10];
    int sz = sizeof(arr)/sizeof(arr[0]) // 因为单位为字节 所以1个字符为4字节 再40/4=10  能得到字符数
    ```

    

##### 3.一维数组在内存中的存储

- 一维数组在内存中是连续存放的

```c
int main() {
	int arr[] = { 1,2,3,4,5,6,7,8,9,10 };

	int sz = sizeof(arr) / sizeof(arr[0]);

	for (int i = 0; i < sz; i++)
	{
		printf("&arr[%d]=%p\n", i, &arr[i]);
		//& arr[0] = 0000005EA6D4F688
		//& arr[1] = 0000005EA6D4F68C
		//& arr[2] = 0000005EA6D4F690
		//& arr[3] = 0000005EA6D4F694
		//& arr[4] = 0000005EA6D4F698
		//& arr[5] = 0000005EA6D4F69C
		//& arr[6] = 0000005EA6D4F6A0
		//& arr[7] = 0000005EA6D4F6A4
		//& arr[8] = 0000005EA6D4F6A8
		//& arr[9] = 0000005EA6D4F6AC

		//  一维数组在内存中是连续存放的
	}

	return 0;
}
```



##### 4.二维数组的创建和初始化

```c
int main() {
    // 3行4列的二维数组  省略中间括号会自动根据行数列数分配
    int arr[3][4] = { 1,2,3,4,5 };
    // 第一行1 2 3 4
    // 第二行5 0 0 0
    // 第三行0 0 0 0
   
	int arr[3][4] = { {1,2,3},{4,5} };
	// 第一行1 2 3 0
	// 第二行4 5 0 0
	// 第三行0 0 0 0

	//int arr[][] = { 1,2,3,4,5,6,7,8 }; // 这样会报错 (arr缺少下标)
	int arr2[][4] = { {1,2,3,4},{5,6,7,8} }; // 行可以省略 列不可以省略

	return 0;
}
```



##### 5.二维数组的使用

- 根据下标访问二维数组

  - ```c
    int main() {
    	int arr[3][4] = { {1,2,3},{4,5} };
    
    	for (int i = 0; i < 3; i++)
    	{
    		for (int j = 0; j < 4; j++) {
    			printf("%d ", arr[i][j]);
    		}
    		printf("\n");
    	}
    	// 第一行1 2 3 0
    	// 第二行4 5 0 0
    	// 第三行0 0 0 0
    
    	return 0;
    }
    ```

    



##### 6.二维数组在内存中的存储

- 二维数组的储存也是连续储存的

```c
int main() {
	int arr[3][4] = { {1,2,3},{4,5} };

	for (int i = 0; i < 3; i++)
	{
		for (int j = 0; j < 4; j++) {
			printf("&arr[%d][%d]= %p\n", i, j, &arr[i][j]);
		}
	}
	/*
	二维数组的储存也是连续储存的
	& arr[0][0] = 00000035CAEFF508
	& arr[0][1] = 00000035CAEFF50C
	& arr[0][2] = 00000035CAEFF510
	& arr[0][3] = 00000035CAEFF514
	& arr[1][0] = 00000035CAEFF518
	& arr[1][1] = 00000035CAEFF51C
	& arr[1][2] = 00000035CAEFF520
	& arr[1][3] = 00000035CAEFF524
	& arr[2][0] = 00000035CAEFF528
	& arr[2][1] = 00000035CAEFF52C
	& arr[2][2] = 00000035CAEFF530
	& arr[2][3] = 00000035CAEFF534
	*/
	return 0;
}
```



##### 7.数组作为函数参数

- 冒泡排序函数

```c
// 传递来的数组 接收可以通过int* arr 或 int arr[] 接收
fnD(int* arr, int sz) {
	//决定轮数
	for (int i = 0; i < sz - 1; i++) {
		//假设这一趟要排序的数据 已经有序
		int flag = 1;
		//决定每轮的次数
		for (int j = 0; j < sz - 1 - i; j++) {
			if (arr[j + 1] < arr[j]) {
				int max = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = max;
				//如果数组进行了排序操作 则说明本轮排序不完全有序
				flag = 0;
			}
		}
		//本轮排序结束后 如果数组已经有序 则不进行下次排序
		if (flag == 1) {
			break;
		}
	}

	for (int i = 0; i < sz; i++) {
		printf("%d ", arr[i]);
	}
}

int main() {
	int arr[] = { 9,8,7,1,4,5,3,2,6,0 };
	//对arr进行排序
	int sz = sizeof(arr) / sizeof(arr[0]);
	//arr是数组 我们传递过去的arr参数 实际上是arr首元素的地址
	fnD(arr, sz);

	return 0;
}
```

- 数组名是什么？

  - 数组名其实就是数组的首元素地址；

  - ```c
    int main() {
    	int arr[] = { 9,8,7,1,4,5,3,2,6,0 };
    
    	//得到首元素的地址
    	printf("%p\n", arr);  // 00000952C39FAC8
    	printf("%p\n", &arr[0]); // 00000952C39FAC8
    	//进行解引用 得到数组第一个值
    	printf("%d\n", *arr); // 9
    
    	return 0;
    }
    ```

  - 数组名在有两种例外的情况下不是首元素地址

  - ```c
    int main() {
    	int arr[] = { 9,8,7,1,4,5,3,2,6,0 };
    
    	// 1.sizeof内部单独放一个数组名的时候 此时此刻的数组名表示整个数组
    	// sizeof(数组名)计算的是整个数组的大小 单位是字节
    	int sz = sizeof(arr) / sizeof(arr[0]);
    
    	//2.&（取地址）数组名 的时候代表整个数组。
    	//&数组名，取出的是整个数组的地址。
    	printf("%p\n", &arr); // 000000D79318F6B8
    
    	return 0;
    }
    ```

    







##### 8.数组的应用实例1：三子棋



###### 1.创建文件

- ```c
  // test.c
  //测试游戏逻辑
  
  // 菜单
  void menu() {}
  // 游戏
  void game() {}
  // 菜单处理函数
  void open() {}
  // 主函数
  int main() {
  	return 0;
  }
  
  // game.h
  // 关于游戏相关的函数、符号声明，头文件包含。
  
  // game.c
  //三子棋游戏相关函数实现
  #define _CRT_SECURE_NO_WARNINGS 1;
  #include <stdio.h>
  
  
  ```

###### 2.打开菜单

```c
// test.c
#include "game.h"

// 打印出选择菜单
void menu() {
	printf("***********************************\n");
	printf("**********    1.play    ***********\n");
	printf("**********    0.exit    ***********\n");
	printf("***********************************\n");
}

void game() {}

void open() {
	int input = 0;
	do {
		//打开菜单
		menu();
		printf("请选择！");
		//获取用户选择的数字
		scanf("%d", &input);
		//根据输入数字选择
		switch (input) {
		case 1:
			printf("三子棋！\n");
			break;
		case 0:
			printf("退出游戏！\n");
			break;
		default:
			printf("输入错误！请重新选择！\n");
			break;
		}
	} while (input);
}

int main() {
	open();

	return 0;
}
```

###### 3.构建棋盘生成相关函数

```c
// game.h============================================================
// 关于游戏相关的函数、符号声明，头文件包含。
#define _CRT_SECURE_NO_WARNINGS 1;

#include <stdio.h>

// 符号的定义
#define ROW 3
#define COL 3

// 函数的声明

//初始化棋盘
void InitBoard(char board[ROW][COL], int row, int col);
//打印棋盘
void displayBoard(char board[ROW][COL], int row, int col);

// game.c============================================================
//三子棋游戏相关函数实现
#include "game.h"

//初始化棋盘数据
void InitBoard(char board[ROW][COL], int row, int col) {
	//遍历二维数组 把所有数组所有数设为空格
	for (int i = 0; i < row; i++) {
		for (int j = 0; j < col; j++) {
			board[i][j] = ' ';
		}
	}
}

//打印棋盘
void displayBoard(char board[ROW][COL], int row, int col) {
	// 打印几行
	for (int i = 0; i < row; i++) {
		{ // -----------打印数据-------------
			//打印几列
			for (int j = 0; j < col; j++) {
				//打印数据
				printf(" %c ", board[i][j]);
				if (j < col - 1) { //最后一行不打印
					printf("|");
				}
				// 每次打印一个数据 为 n | n | n | n
			}
			printf("\n");
		}

		{ // -----------打印分割线-------------
			//打印上下分割线 如果行数是最后一行 则不打印
			if (i < row - 1) {
				//循环列数
				for (int i = 0; i < col; i++)
				{
					//每有一列 则打印一个上下分割线
					printf("---");
					//如果是最后一列 则不打印
					if (i < col - 1) {
						printf("|");
					}
				}
				printf("\n");
			}
		}
	}
}


```

###### 4.玩家与电脑下棋逻辑

```c
// game.c
//玩家下棋
void playMove(char board[ROW][COL], int row, int col) {
	printf("玩家回合 \n");
	int x = " ";
	int y = " ";
	while (1) {
		printf("请输入坐标 =>");
		scanf("%d %d", &x, &y);

		//判断坐标是否合理

		if (x >= 1 && y >= 1 && x <= row && y <= col) {
			//判断对应坐标位置是否已落子
			if (board[x - 1][y - 1] == ' ') {
				board[x - 1][y - 1] = '*';
				break;
			}
			else {
				//如果已经落子 则提示重新输入
				printf("输入坐标已落子 请重新输入\n");
			}
		}
		else {
			//如果不合法 则提示重新开始 不结束循环
			printf("输入坐标不合法 请重新输入\n");
		}
	}
}

//电脑下棋
void computerMove(char board[ROW][COL], int row, int col) {
	printf("电脑回合 \n");
	while (1) {
		//获取随机数
		// rand() % row=3  会得到随机的0-2
		int x = rand() % row;
		int y = rand() % col;

		//判断随机出来的坐标是否已经落子
		if (board[x][y] == ' ') {
			board[x][y] = '#';
			break;
		}
		//如果已经落子 则循环重新获取
	}
}
```

```c
// test.c
void game() {
	//储存数据 二维数组
	char board[ROW][COL];
	//初始化棋盘 （空格）
	InitBoard(board, ROW, COL);
	//打印棋盘
	displayBoard(board, ROW, COL);
	//游戏输赢状态
	char flag = 0;
	while (1) { // 死循环 直到出赢家
		//玩家先动
		playMove(board, ROW, COL);
		//打印棋盘
		displayBoard(board, ROW, COL);


		//电脑后动
		computerMove(board, ROW, COL);
		//打印棋盘
		displayBoard(board, ROW, COL);

	}
}
```

###### 5.判断输赢逻辑

```c
//game.c
//判断棋盘是否已经满了
char isFull(char board[ROW][COL], int row, int col) {
	for (int i = 0; i < row; i++) {
		for (int j = 0; j < col; j++) {
			if (board[i][j] == ' ') {
				return 'N';
			};
		}
	}
	//循环完成后 并没有输出N 则代表棋盘已满 输出G
	return 'G';
}

//输出 "*" 表示玩家胜利
//输出 "#" 表示电脑胜利
//输出 "G" 表示平局
//输出 "N" 表示继续
//判断谁赢
char isWin(char board[ROW][COL], int row, int col) {
	for (int i = 0; i < row; i++) {
		//横向三子链接
		if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][1] != ' ') {
			//输出胜利方符号
			return board[i][1];
		}
	}

	for (int i = 0; i < row; i++) {
		//竖向三子链接
		if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[1][i] != ' ') {
			//输出胜利方符号
			return board[1][i];
		}
	}

	//斜向三子链接
	if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[1][1] != ' ') {
		//输出胜利方符号
		return board[1][1];
	}
	else if (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[1][1] != ' ') {
		//输出胜利方符号
		return board[1][1];
	}

	//判断棋盘是否已经输入满了 如果输入满了 则代表平局
	return (isFull(board, row, col));
}
```

```c
// test.c
void game() {
	//储存数据 二维数组
	char board[ROW][COL];
	//初始化棋盘 （空格）
	InitBoard(board, ROW, COL);
	//打印棋盘
	displayBoard(board, ROW, COL);
	//游戏输赢状态
	char flag = 0;
	while (1) { // 死循环 直到出赢家
		//玩家先动
		playMove(board, ROW, COL);
		//打印棋盘
		displayBoard(board, ROW, COL);
		//判断输赢
		flag = isWin(board, ROW, COL);
		if (flag != 'N') break;

		//电脑后动
		computerMove(board, ROW, COL);
		//打印棋盘
		displayBoard(board, ROW, COL);
		//判断输赢
		flag = isWin(board, ROW, COL);
		if (flag != 'N') break;
	}
	if (flag == '*') {
		printf("玩家胜利\n");
	}
	else if (flag == '#') {
		printf("电脑胜利\n");
	}
	else if (flag == 'G') {
		printf("平局！\n");
	}
}
```



##### 9.数组的应用实例2：扫雷

```c
test.c - 扫雷游戏的测试

game.c - 游戏的逻辑函数实现

game.h - 游戏的逻辑函数声明
#define  _CRT_SECURE_NO_WARNINGS

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

//难度列表
#define EASY_COUNT 10
//游戏难度
#define GAME_DIFFICULTY EASY_COUNT

//棋盘大小
#define ROW 9
#define COL 9
#define ROWS ROW+2
#define COLS COL+2
```

###### 1.打印菜单

```c
// test.c
dispalyMenu() {
	printf("**********************************\n");
	printf("**********  1.扫雷游戏  **********\n");
	printf("**********  0.退出菜单  **********\n");
	printf("**********************************\n");
}
main() {
	//设置随机数
	srand((unsigned int)time(NULL));
	int input = ' ';
	do {
		//打印菜单
		dispalyMenu();
		//用户输入数字
		scanf("%d", &input);
		//判断用户选择项
		switch (input) {
		case 0:
			printf("退出游戏-w-\n");
			break;

		case 1:
			//开始游戏
			game();
			break;
		default:
			printf("输入错误 请重新选择！\n");
			break;
		}
	} while (input);

	return 0;
}
```

###### 2.初始化棋盘

```c
//test.c
game() {
	int mine[ROWS][COLS]; // 存放布置炸弹的棋盘
	int show[ROWS][COLS]; // 存放排查炸弹的棋盘

	//初始化棋盘
	initBoard(mine, ROWS, COLS, '0');
	initBoard(show, ROWS, COLS, '*');
}

//game.h
//初始化棋盘
void initBoard(int board[ROWS][COLS], int rows, int cols, char set);

// game.c
//初始化棋盘
void initBoard(int board[ROWS][COLS], int rows, int cols, char set) {
	for (int i = 0; i < rows; i++) {
		for (int j = 0; j < cols; j++) {
			board[i][j] = set;
		}
	}
}
```

###### 3.打印棋盘

```c
// test.c
game() {
	int mine[ROWS][COLS]; // 存放布置炸弹的棋盘
	int show[ROWS][COLS]; // 存放排查炸弹的棋盘

	//初始化棋盘
	initBoard(mine, ROWS, COLS, '0');
	initBoard(show, ROWS, COLS, '*');
	//打印棋盘
	//displayBoard(mine, ROW, COL);
	displayBoard(show, ROW, COL);
}

// game.h
//打印棋盘
void displayBoard(int board[ROWS][COLS], int row, int col);


//game.c
//打印棋盘
void displayBoard(int board[ROWS][COLS], int row, int col) {
	printf("---------------------------------------\n"); // 打印分割线
	for (int i = 0; i <= col; i++) { // 打印标尺数
		printf("%d ", i);
	}
	printf("\n");
	//打印棋盘数据
	for (int i = 1; i <= row; i++) {
		printf("%d ", i);// 打印标尺数
		for (int j = 1; j <= col; j++) {
			printf("%c ", board[i][j]);
		}
		printf("\n");
	}
	printf("---------------------------------------\n"); // 打印分割线
}
```

###### 4.布置地雷

```c
// test.c
game() {
	int mine[ROWS][COLS]; // 存放布置炸弹的棋盘
	int show[ROWS][COLS]; // 存放排查炸弹的棋盘

	//初始化棋盘
	initBoard(mine, ROWS, COLS, '0');
	initBoard(show, ROWS, COLS, '*');
	//打印棋盘
	//displayBoard(mine, ROW, COL);
	displayBoard(show, ROW, COL);

	//布置地雷
	setMine(mine, ROW, COL);
}

// game.h
//布置地雷
void setMine(int mine[ROWS][ROWS], int row, int col);

// game.c
//布置地雷
void setMine(int mine[ROWS][COLS], int row, int col) {
	int count = GAME_DIFFICULTY;

	while (count) {
		int x = rand() % row + 1;
		int y = rand() % col + 1;
		if (mine[x][y] == '0') {
			mine[x][y] = '1';

			count--;
		}
	}
}
```

###### 5.排查地雷

```c
// test.c
game() {
	int mine[ROWS][COLS]; // 存放布置炸弹的棋盘
	int show[ROWS][COLS]; // 存放排查炸弹的棋盘

	//初始化棋盘
	initBoard(mine, ROWS, COLS, '0');
	initBoard(show, ROWS, COLS, '*');
	//打印棋盘
	displayBoard(show, ROW, COL);

	//布置地雷
	setMine(mine, ROW, COL);

	//玩家排查地雷
	finMine(mine, show, ROW, COL);
}

//game.h

//排查地雷
void finMine(int mine[ROWS][COLS], int show[ROWS][COLS], int row, int col);

// game.c

//查询坐标的旁边有几个地雷
static int findMineCount(int mine[ROWS][COLS], int x, int y) {
	int count = 0;
	for (int i = x - 1; i <= x + 1; i++) {
		for (int j = y - 1; j <= y + 1; j++) {
			if (mine[i][j] == '1') {
				count++;
			}
		}
	}

	return count;
}

//排查地雷
void finMine(int mine[ROWS][COLS], int show[ROWS][COLS], int row, int col) {
	int x = 0;
	int y = 0;
	int flag = (row * col) - GAME_DIFFICULTY;

	while (flag) {
		printf("请输入要排查的坐标=>");
		scanf("%d %d", &x, &y);
		//判断坐标合法性
		if (x >= 1 && x <= row && y >= 1 && y <= col) {
			if (mine[x][y] == '0') {
				int mineCount = findMineCount(mine, show, row, col, x, y);
				show[x][y] = mineCount + '0';
				flag--;
				displayBoard(show, ROW, COL);
			}
			else {
				printf("BOMM！ 您死了！游戏结束！");
				break;
			}
		}
		else {
			printf("坐标不合法 请重新输入！");
		}
	}
	printf("恭喜您赢了！=w= ！\n");
}
```



### 9.循环语句

##### 1.while循环

- 语法结构：

  - ```c
    while(表达式){
    	循环语句;
    }
    ```

- 例子：

  - ```c
    int main() {
    	//打印1 - 10
    	int i = 1;
    	while (i <= 10)
    	{
    		printf("%d\n", i);
    		i++;
    	};
    	return 0;
    }
    ```

- break

  - ```c
    int main() {
    	//打印1 - 10
    	int i = 1;
    	while (i <= 10)
    	{
    		if (i == 5) { break; } // break 结束循环
    		printf("%d\n", i); // 打印出1-4
    		i++;
    	};
    	return 0;
    }
    ```

- continue

  - ```c
    int main() {
    	//打印1 - 10
    	int i = 1;
    	while (i <= 10)
    	{
    		i = i + 1;
    		if (i == 5) { continue; } // continue 结束本轮循环 开始下一轮循环
    
    		printf("%d\n", i); // 打印出23467891011
    	};
    	return 0;
    }
    ```




##### 2.for循环

- 语法结构：

  - ```c
    for(表达式1;表达式2;表达式3){
    	循环语句;
    }
    ```

- 例子：

  - ```c
    	//打印1 - 10
    	for (int i = 1; i <= 10; i++) {
    		if (i == 5) {
    			continue;
    		}
    		printf("%d", i); // 1 2 3 4 6 7 8 9 10
    	}
    
    	return 0;
    }
    ```

##### 3.do... while()循环

- 语法结构

  - ```c
    do{
        循环语句;
    }
    while(表达式);
    ```

- 例子

  - ```c
    int main() {
    	//打印1 - 10
    	int i = 1;
    	do
    	{
    		printf("%d\n", i); // 1 2 3 4 5 6 7 8 9 10
    		i++;
    	} while (i <= 10);
    
    	return 0;
    }
    ```

- 打印出 1-5的乘阶

  - ```c
    int main() {
    	int sum = 0;
    	int ret = 1;
    	// 打印1!+!2+ ...5!
    	for (int i = 1; i <= 5; i++)
    	{
    		ret = 1;
    
    		for (int j = 1; j <= i; j++)
    		{
    			ret *= j;
    			//printf("%d\n", ret);
    		}
    
    		sum += ret;
    	}
    	printf("%d\n", sum);
    	return 0;
    }
    ```

##### 4.二分法 查找有序数组中某个值

```c
int main() {
	int arr[] = { 1,2,3,4,5,6,7,8,9,10 };
	int k = 7; // 要查找的值
	// sizeof(arr[0]) 一个数的长度为4  一共是40 所以是40/4 = 10
	int size = sizeof(arr) / sizeof(arr[0]) - 1;
	int left = 0; // 左下标
	int right = size - 1; // 右下标

	while (left <= right)
	{
		int mind = (left + right) / 2;
		printf("%d\n", mind); // 打印中间值
		if (k < arr[mind]) { // 所需的值是否小于 数组的中间值
			right = mind - 1; // 如果小于 则right 边界为中间值-1
		}
		else if (k > arr[mind]) { // 如果所需的值大于 数组的中间值
			left = mind + 1; // 如果大于 则left 边界为中间值+1
		}
		else { // 如果都不符合 中间值刚好是k
			printf("下标为%d\n", mind);
			break; // 找到后结束循环
		}

		//但是 如果 left大于right 则表示
		if (left > right) {
			printf("找不到！！");
			break;
		}
	}

	return 0;
}
```

##### 5.多个字符从两端移动- 向中间汇聚

- welcome to biy!!!!!!   
- welc#########!!!!

```c
#include <stdio.h>
#include <string.h>
#include <windows.h>
#include <stdlib.h>

int main() {
	char arr1[] = "welcome to bit!!!!!!";
	char arr2[] = "####################";

	int left = 0;
	//int right = sizeof(arr) / sizeof(arr[0]) - 2; // 字符串数组最后还有一个 \0 还占一个位置 所以多-1
	int right = strlen(arr1) - 1; // strlen查找的字符串数组长度 不会包括\0 所以-1就行

	printf("%d\n", right);

	while (left <= right)
	{
		arr2[left] = arr1[left];
		arr2[right] = arr1[right];

		Sleep(500);
		system("cls");
		left++;
		right--;
	}
	printf("%s\n", arr2);

	return 0;
}
```

##### 6.编辑代码实现用户登陆情景，密码错误情况只有三次机会。

```c
int main() {
	int password = 123456;
	int chance = 3;
	int inputPassword;

	while (chance > 0)
	{
		printf("请输入密码！\n");
		scanf_s("%d\d", &inputPassword);
		printf("输入完成：%d\n", inputPassword);
		if (password == inputPassword) {
			printf("密码正确！登录成功\n");
			break;
		}
		else {
			system("cls");
			printf("密码错误！\n");
			chance--;
			if (chance == 0) {
				printf("输入密码机会已用完！请等待60分钟后重试\n");
			}
		}
	}

	return 0;
}
```







































### 10.操作符

#### 1.算数操作符

- 除了%操作符之外，其他的几个操作可以作用与整数和浮点数。
- 对于/操作符，如果两个操作数都为整数，执行整数除法。而只要有浮点数执行的就是浮点数除法。
- %操作符的两个操作数必须为整数。返回的是整除之后的余数。



- \+  (加)
- \-   (减)
- \*  (乘)
- /（除） 

  - ```c
    int main() {
    	// 整数除法
    	int a = 3 / 5; // 0.6
    	printf("%d\n", a); // 0
    	int b = 6 / 5; // 1.2
    	printf("%d\n", b); // 1
    
    	// 小数除法
    	//想得到小数 需要除以的数之间至少有一个小数
    	float c = 3 / 5.0; // 0.6
    	printf("%f\n", c); // 0.60000
    	float d = 6 / 5.0; // 1.2
    	printf("%f\n", d); // 1.20000
    }
    ```
    
    

- %（取余）

  - ```c
    int main() {
    	//算的是 7/3得到的余数 得1
    	int a = 7 % 3; // 1
    	printf("%d\n", a);
        // %操作符的两个操作数必须为整数。返回的是整除之后的余数。
    
    	int a = 7 % 3.0; // 报错 取余不能有非整数或浮点数
    	printf("%d\n", a);
    }
    ```
    
    


#### 2.位移操作符

- \>>
- <<

  - ```c
    int main() {
        // >> << 不会影响原数据
    	//  << 左移操作符 （左边丢弃，右边补0）
    	int a = 2;
    	// 把a的二进制位向左移动一位
    	printf("%d\n", a << 1); // 4
    	// 0010 为2   向左一位0100 为4
    
    	//  >> 右移操作符  
        // 分别为算数右移 和 逻辑右移
        // 当前为逻辑右移 = 左边丢弃，右边补0
    	int b = 2;
    	// 把a的二进制位向右移动一位 
    	printf("%d\n", b >> 1); // 1
    	// 0010 为2   向右一位0001 为1
        
        //  >> 右移操作符
    	//算数右移 = 右边丢弃，左边补原符号位
    	int c = -1;
    	printf("%d\n", c >> 1); // -
        // 原码：1000000000000000000000000000000001
        // 反码：1111111111111111111111111111111110
        // 补码：1111111111111111111111111111111111
        
        // 所以 1111111111111111111111111111111111 删掉右边的1 左边再补一个1 所以还是得到-1
    }
    ```
    
  - 对于移位算数符，不要移动负数位，这个是标准未定义的。(会报错)


#### 3.(2进制)位操作符

- 他们的操作数 必须是整数

- & 按位与   （与）有0则0

  - ```c
    	int a = 3;
    	int b = 5;
    	// & - 按(2进制)位与
    	int c = a & b;
    	printf("%d", c); // 1
    	// 000000000000000000000000000000011  // 3
    	// 000000000000000000000000000000101  // 5
    	// 只有上下都是1才能得1
    	// 得到
    	// 000000000000000000000000000000001  // 1
    
    ```

- | 按位或 （或）有1则1

  - ```c
    int main() {
    	int a = 3;
    	int b = 5;
    	// | - 按(2进制)位或
    	int c = a | b;
    	printf("%d", c); //
    	// 000000000000000000000000000000011  // 3
    	// 000000000000000000000000000000101  // 5
    	// 两个之间有一个1 就为1
    	// 得到 7
    	// 000000000000000000000000000000111  // 7
    
    	return 0;
    }
    ```

- ^ 按位异或    （非）有1则0

  - ```c
    int main() {
    	int a = 3;
    	int b = 5;
    	// ^ - 按(2进制)位异或
    	int c = a ^ b;
    	printf("%d", c); // 6
    	// 000000000000000000000000000000011  // 3
    	// 000000000000000000000000000000101  // 5
    	// 相同为0，相异为1
    	// 得到
    	// 000000000000000000000000000000110  // 6
    }
    ```
    
    

#### 4.赋值操作符

- =
- +=
- -=
- *=
- /=
- &=
- ^=
- \>>=
- <<=

#### 5.单目操作符（只有一个操作数）

- ！ 逻辑反操作（真变假 假变真）
- \- （负值）
- \+（正值）

#### sizeof

- sizeof（操作数的类型长度 或 计算操作数（数组也行）的所占空间的大小【以字节为单位】）

  - ```c
    // sizeof
    int main() {
    	int a = 10;
    
    	printf("%d\n", sizeof(a)); // 计算a所占空间的大小，单位是字节
    	printf("%d\n", sizeof(int)); // 计算int类型长度，单位是字节
    
    	//sizeof是一个操作符 而不是函数
    
    	int arr[10] = { 0 };
    	printf("%d\n", sizeof(arr)); //得40 计算arr数组所占空间的大小，单位是字节
    	printf("%d\n", sizeof(int[10])); //得40 计算int [10]arr数组的类型长度，单位是字节
        
        
        
        short s = 5;
    	int i = 10;
    	printf("%d\n", sizeof(s = a + 2)); // 2
    	//因为short是短整型 字节长度为2  也不会因为=int类型的数字会内存会发生改变
    	printf("%d\n", s); // 5  不是12的原因是 sizeof内不会真正发生运算
    }
    ```
    
    

- ~ 对一个数的二进制按位取反 （按【二进制】位取反） 

  - ```c
    int main() {
    	int a = -1;
    	// 在内存中存储他的二进制数列的补码
    	// 00000000000000000000000000000001 - 源码
    	// 11111111111111111111111111111110 - 反码
    	// 11111111111111111111111111111111 - 补码 = 反码+1
    
    	// ~ 按位取反
    	int b = ~a;
    	// 11111111111111111111111111111111 - 补码
    	// 00000000000000000000000000000000 - 取反后
    	printf("%d\n", b);  // 0
    	printf("%d\n", a);  // -1  a不变
    }
    ```
    
    

- -- 前置、后值--

- ++ 前置、后置++

- &（取地址操作符）

- \* 间接访问操作符(解引用操作符)

  - ```c
    int main() {
    	int a = 10;
    
    	// & - 取地址操作符
    	printf("%p\n", &a);  // 0000005C7B30F6C4
    
    	int* pa = &a; // pa是用来存放地址的 - pa就是一个 《指针变量》
    
    	// 可以通过 pa查找到a
    	// * 解引用操作符 或 间接访问操作符
    	// *pa 根据里面存的地址 找到a的对象
    	*pa = 20; // 就等于把a的值改为20
    	printf("%d\n", a);  //20
    }
    ```
    
    

- （类型）   强制类型转换

  - ```c
    int main() {
    	// (类型) 强制转换类型
    	// int类型存放小数会警告 强制类型转换后不会警告 但是会丢失小数的精度
    	int a = (int)3.14;
    }
    ```
    
    


#### 6.关系操作符

- \>
- \>=
- <
- <=
- !=
- ==

#### 7.逻辑操作符

- && 逻辑与 （都是真才是真）
- || 逻辑或  （一个真就是真）

#### 8.条件操作符

- 三目（三元）操作符
- exp1 ? exp2 : exp3

#### 9.逗号表达式

- exp1,exp2,exp3,...expN

  - ```c
    int main() {
    	int a = 3;
    	int b = 5;
    	int c = 0;
    	//逗号表达式要从左到右依次计算，但是整个表达式的结果是最后一个表达式的结果
    	int d = (c = 5, a = c + 3, b = a - 4, c += 5);
    	printf("a=%d b=%d c=%d d=%d", a, b, c, d); // a=8 b=4 c=10 d=10
    }
    ```
    
  


#### 10.下标引用、函数调用和结构成员

- [] 下标引用操作符

  - 操作数：一个数组名+一个索引值
  - ```c
    
    int main() {
    	int arr[10] = { 1,2,3,4,5,6,7 };
    	//查找arr数组的第五个元素
    	printf("%d\n", arr[4]);
    }
    ```

    

- () 函数调用操作符

  - ```c
    //函数
    fn(int arr[10]) {
    	printf("%d\n", arr[4]);
    }
    
    int main() {
    	int arr[10] = { 1,2,3,4,5,6,7 };
    	// 函数名(参数) 函数调用操作符  
    	fn(arr);
    }
    ```

    

- . 结构成员操作符

  - ```c
    //结构体： 类似js对象
    //定义一个自定义类型
    struct Book {
    	// 结构体成员(变量)
    	char name[20];
    	char id[20];
    	int price;
    };
    
    int main() {
    	struct Book b = { "C--","C123456789",55 };
    
    	// 打印 .结构成员操作符   结构体变量名.成员名
    	printf("书名=%s\n", b.name);
    	printf("id=%s\n", b.id);
    	printf("价格=%d\n", b.price);
    }
    ```

    

- -> 结构成员操作符

  - ```c
    //结构体： 类似js对象
    //定义一个自定义类型
    struct Book {
    	// 结构体成员(变量)
    	char name[20];
    	char id[20];
    	int price;
    };
    
    int main() {
    	struct Book b = { "C--","C123456789",55 };
    	//*说明pb是指针  struct Book说明pb的b是这个类型
    	struct Book* pb = &b;
        // 结构体指针->成员名
    	// -> pb指向的对象的name    
    	printf("书名=%s\n", pb->name); // 书名=C--
    	printf("id=%s\n", pb->id);
    	printf("价格=%d\n", pb->price);
    
    	return 0;
    }
    ```

    


#### 11.原码 反码 补码

整数的二进制表示形式有三种：

- 原码
  - 直接根据数值写出的二进制序列就是原码
- 反码
  - 原码的符号位不变，其他位按取反就是反码
- 补码
  - 反码+1，就是补码

![image-20220826152613163](.\img\源码反码补码.png)



#### 12.表达式求值

- 表达式求值的顺序一部分是由操作符的优先级和结合性决定的。
- 同样，有些表达式的操作在求值的过程中可能需要转换为其他类型。



##### 1.隐式类型转换(整型提升)

- C的整型算术运算总是至少以确实整型类型的精度来进行的。

- 为了获得这个精度，表达式中的字符和短整型操作数在使用之前被转换为普通整型，这种转换称为**整型提升**。

  - ```c
    char a,b,c
    ...
    a = b + c 
    ```

  - b和c的值被提升为普通整型，然后再执行加法运算。

  - 加法运算完成后，结果将被**截断**（例如：4个字节的数据要放入1个字节的数据的时候，只保留最低的1个字节内容，其他3个字节扔掉），然后再储存于a中。

- ![image-20220912160705553](.\img\整型提升.png)

- 例子：整型提升的过程

  - ```c
    int main() {
    	// 计算的时候 a和b都是char类型 都没有达到一个int的大小
    	// 所以就会发生整型提升：
    
    	char a = 3;
    	//00000000 00000000 0000000 000000011
    	//因为char只能存8个比特位
    	//所以只储存了 00000011 - a
    	char b = 127;
    	//01111111 - b
    	char c = a + b;
    	// 整型提升是按照变量的数据类型的符号位来提升的
    	//00000011 - a 第一个数0 被看为符号位 所以整型提升后得到
    	//00000000 00000000 00000000 00000011
    	//01111111 - b 第一个数0 被看为符号位 所以整型提升后得到
    	//00000000 00000000 00000000 01111111
    
    	// a和b相加得到：
    	// 00000000 00000000 00000000 10000010 
        // 加完后需要放在c里面 可c的类型为char 只能放8个比特位
    	// 所以 c = 10000010
    	// 因为打印时候 需要使用%d 就是整型类型打印 所以需要进行整型提升
    	// 10000010  高号位为1 所以整型提示后得到：
    	// 11111111 11111111 11111111 10000010  在内存的时候 存的是补码
    	// 而打印出来需要打印出来 源码
    	// 补码求源码 要 -1取反  所以得到
    	// 11111111 11111111 11111111 10000010 - 补码
    	// 11111111 11111111 11111111 10000001 - 反码 （补码-1）
    	// 10000000 00000000 00000000 01111110 - 源码  (反码取反)  符号位(第一位)不变
    	// %d意味着有符号数 所以要打印源码   打印出来就是 -126
    	printf("%d\n", c);  // -126
    	printf("%c\n", c);  // ?  因为已经转换成了整型类型 所以无法以字符类型打印
    	return 0;
    }
    ```

- 例子：

  - ```c
    int main() {
    	char c = 1;
    	printf("%u\n", sizeof(c)); //1
    	printf("%u\n", sizeof(+c)); //4   发生了整型提升 所以为四个字节的数
    	printf("%u\n", sizeof(-c)); //4
    }
    ```




##### 2.算数转换

- 如果某个操作符的各个操作符属于不同的类型，那么除非其中一个操作数转换为另一个操作数的类型，否则操作就无法进行。下面的层次体系称为**寻常算数转换**

```c
long double
double
float
unsigned long int 
long int
unsigned int 
int 
```

```c
int main() {
	int a = 4;
	float b = 4.5f;

	a + b;  // 向精度更高的进行转换  a转换为float

	return 0;
}
```

##### 3.操作符的属性

- 复杂表达式的求值有三个影响的因素。
  - 1.操作符的优先级 
  - 2.操作符的结合性 
  - 3.是否控制求值顺序

```c
int main() {
	int a = 4;
	int b = 5;
	int c = a + b * 7;// 优先级决定计算顺序 （*的优先级比+更高）
	int c = a + b + 7;// 优先级不起作用，则结合性决定顺序
	return 0;
}
```



### 11.常见关键字

C语言内置的关键字，不能定义为变量名等冲突。

![image-20220826152740112](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220826152740112.png)

#### 1.关键字 typedef （类型重定义）

```c
int main() {
	//无符号int类型
	unsigned int num = 20;

	//可以使用typedef重命名 为自定义类型 u_int使用
	typedef unsigned int u_int;

	u_int num1 = 200;  // u_int等与 unsigned int
	return 0;
}
```

#### 2.关键字 static 

- static 修饰局部变量

```c
void test() {
	//在函数内的变量 变量会在函数结束后销毁
	//如果添加了 static 后 函数结束后不会被销毁 被保留累加过的数
    //相当于局部变量的生命周期变长了
	static int a = 1;
	a++;
	// 没加static 的时候 打印出 2 2 2 2 2
	//加了static后 打印 2 3 4 5 6
	printf("%d\n", a);
}
int main() {
	int i = 0;
	while (i < 5)
	{
		test();
		i++;
	}
	return 0;
}
```

- static 修饰全局变量
  - 使用extern（声明外部符号）从另一个源文件中获取变量，如果另一个源文件中的变量使用了static，则无法获取。
  - 因为static改变了变量的作用域 让静态的全局变量只能在自己所在的源文件内部使用

```c
// test1文件
int main() {
	extern int abc;
	printf("abc = %d\n", abc); //在test2文件的abc变量没有使用static时 打印出 abc = 2022
    
    printf("abc = %d\n", abc); //在test2文件的abc变量使用了static时，则报错

	return 0;
}

// test2文件
static int abc = 2022;
```

- static 修饰函数

```c
// test1文件
//使用extern 声明外部函数
extern int Add(int, int);

int main() {
	int a = 10;
	int b = 20;
	// 使用外部函数
	int sum = Add(a, b);
	// 如果在test2的函数 没有使用static进行修饰 则可以使用 打印30
    // 如果在test2的函数 使用了static进行修饰 则报错
	printf("%d\n", sum);
	return 0;
}

//test2文件
// 使用static修饰函数 改变了函数的链接属性（正常的函数拥有外部链接属性，如果被static修饰，则会变成内部链接属性 则无法在外部使用这个函数）
static int Add(int x, int y) {
	int z = 0;
	z = x + y;

	return z;
}
```



### 12.#define 定义常量和宏

```c
#define Max 100; // 使用#define 定义标识符常量

#define MAX(X,Y) X>Y?X:Y;// 使用#define 定义宏-带参数（类似函数）

int main() {
	int a = 10;
	int b = 20;

	int max = MAX(a, b);
	printf("%d\n", max); // 打印出20

	return 0;
}
```





### 13.结构体(对象)

#### 1.结构体初识

- 结构体是一些值的集合，这些值称为成员变量。结构的每个成员可以使不同类型的变量。
- 结构的成员可以是变量、数组、指针，甚至是其他结构体。

```c
struct A
{
	char name;
    int age;
}

//创建一个结构体类型 (类似js的对象)
struct Book
{
	char name[20]; // 结构成员
	short price;
    struct A arr;  //结构成员也可以是其他结构体
},s1,s2;  // s1 和 s2 也是结构体变量 不过是全局变量
int main() {
	//使用结构体 创建一个该类型的结构体变量
	struct Book b1 = { "C语言XXX",50,{'梁非凡',18} };
	printf("书名：%s\n", b1.name);
	printf("价格：%d\n", b1.price);
    
	//修改结构体中的数据
	b1.price = 250;
	printf("修改后的价格：%d\n", b1.price);

	return 0;
}
```

#### 2.访问结构体

- 结构体使用指针变量储存 并 使用指针变量打印数据
- 结构体成员的访问使用 **.** 或 **->**

```c
//创建一个结构体类型 (类似js的对象)
struct Book
{
	char name[20];
	short price;
};

int main() {
	//使用结构体 创建一个该类型的结构体变量
	struct Book b1 = { "C语言XXX",50 };
	//获取b1的指针位置 用pb指针变量储存
	struct Book* pb = &b1;
	printf("指针变量：%p\n", pb);

	//.操作符 引用于   结构体变量.成员
	//->操作符 引用于 结构体变量->成员

	//利用pb指针变量打印出 b1的书名和价格
	printf("书名：%s 价格：%d\n", (*pb).name, (*pb).price); // 书名:C语言XXX 价格:50
	//简化上行的(*pb).name  pb->name
	printf("书名：%s 价格：%d\n", pb->name, pb->price); // 书名:C语言XXX 价格:50

	return 0;
}
```

#### 3.结构体传参

- 传递参数使用指针传递效率更高
  - 因为函数传参时，参数是需要压栈的，如果传递一个结构体对象的时候，结构体过大，参数压栈的系统开销更大，会导致性能下降。

```c
struct B {
	char name[10];
	int age;
	char sex[5];
};
//创建一个结构体类型 (类似js的对象)
struct Stu
{
	struct B sd;
	char major[20];
	short total;
};

print1(struct Stu n) {
	printf("%s %d %s %s %d", n.sd.name, n.sd.age, n.sd.sex, n.major, n.total);
}
// 接收结构体变量的地址
print2(struct Stu* n) {
	printf("%s %d %s %s %d", n->sd.name, n->sd.age, n->sd.sex, n->major, n->total);
}

int main() {
	//使用结构体 创建一个该类型的结构体变量
	struct Stu b1 = { {"梁非凡",18,"男"},"游戏工程师",150 };
	//写一个函数打印b1的内容
	print1(b1); 
	//传递结构体变量的地址
	print2(&b1);  // 使用指针传递效率更高
	return 0;
}
```









### 14.指针

#### 1.指针是什么？

- 指针是编程语言中的一个对象，利用地址，它的值直接指向存在电脑存储器中另一个地方的值。由于通过地址能找到所需的变量单元，可以说，地址指向该变量单元。因此，将地址形象化的称为“指针”。意思是通过它能找到以它为地址的内存单元。

```c
int main() {
   
1.	int a = 10; // 向内存申请4个字节
	// &a   &为取地址操作符
	// %p是以地址形式打印
	printf("%p\n", &a); // 拿到a存在内存的4个字节中第1个字节的地址  获得00000026C9DCF794 为16进制数

	//有一种变量是用来存放地址的 - (数据类型)* 指针变量
2.	int* p = &a;
	printf("%p\n", p); //和上面打印的一样

	//* 解引用操作符
	//对p进行解引用操作 - 找到他所指向的对象a
	printf("%d\n", *p); // 10
3.	*p = 20; // 把通过*p找到的a的值 改为20
	printf("%d\n", a); // 20

	return 0;
}
```

- 指针大小在32位平台是4个字节，64位平台是8个字节

```c
int main() {
	int a = "w";
	int* pc = &a;
	
	printf("%d\n", sizeof(pc)); //指针大小 在x64平台上能存64个二进制位 为8个字节
	printf("%d",sizeof(char))//1 字节 char的大小
    printf("%d",sizeof(char*))// 32位输出4  64位输出8
	return 0;
}
```

#### 2.指针类型的意义

- **1.指针类型决定了：指针解引用的权限有多大**

  - ```c
    int a = 0x11223344;  // 在内存中 四个字节储存了 44 33 22 11
    	//使用char*类型储存a的指针地址
    char* pc = &a;
    	// int*解引用能访问4个字节  char*解引用只能访问1个字节
    	// 所以被修改后a的内存为  00 33 22 11
    *pc = 0;
    ```

- **2.指针类型决定了：指针走一步能走多远(步长)**

  - ```c
    int arr[10] = { 1,2,3,4 };
    	//储存的是第一个元素的地址
    int* p = arr;
    char* pc = arr;
    
    printf("%p\n", p); // FFBD8
    printf("%p\n", p + 1); // FFBDC   +1相当于跳过一个整型 4字节
    printf("------------\n");
    printf("%p\n", pc); // FFBD8
    printf("%p\n", pc + 1); // FFBD9  +1相当于跳过一个字符 1字节
    
    // arr 内存的数据为：01 00 00 00 02 00 00 00 03 00 00 00 04 00 00 00 00...
    // 其中 01为一个字节 
    // p+1 = 从01 跳4个字节 到02
    // pc+1 = 从01 跳一个字节 到01的后一个字节 00
    
    ```

#### 3.野指针

- 概念：野指针就是指针指向的**位置是不可知**的（随机、不正确、没有明确限制）

```c
// 情况1： 指针变量不初始化会导致野指针
int main() {
	// p就是一个野指针
	int* p; // p是一个局部的指针变量，局部变量不初始化的话，默认是随机值
	*p = 20; // 非法访问内存
}

// 情况2： 越界访问会导致野指针
int main() {
	int arr[10] = { 0 };

	int* p = arr;
	// 0 -> 10 会循环11次 最后一次的p会越界访问
	// 访问非本数组的字节会非法访问内存  就是一个野指针
	for (int i = 0; i <= 10; i++)
	{
		*p = i;
		p++;
	};
}
// 情况3： 指针指向的空间释放

```

- **如何规避野指针**：

  - 1.指针初始化

    - ```c
      // 当前不知道指针应该初始化为什么的时候 初始化为NULL
      int* p = NULL;
      ```

  - 2.小心指针越界

  - 3.指针指向空间释放及时置空(NULL)

  - 4.指针使用之前检查有效性

    - ```c
      int* p = NULL;
      if(p!=NULL) {
          *p = 10;
      };
      ```

#### 4.指针运算

- 指针 + - 整数
- 指针 - 指针
- 指针的关系运算
  - 允许**指向元素的指针**与**指针数组最后一个元素后面**的那个内存位置指针比较
  - 但是不允许与指针第一个元素之前的那个内存位置的指针进行比较




###### 1.指针+-整数

```c
int main() {
	float values[5];
	float* vp;
	// 地址是由低到高
	//				      指针比较大小（关系运算）
	for (vp = &values[0]; vp < &values[5];) {
		// *vp++  指针+整数
		*vp++ = 0;
	}
    
}
```

###### 2.指针 - 指针

```c
int main() {
	int arr[10] = { 1,2,3,4,5,6,7,8,9,10 };
	char c[5];
	// 指针减去指针 得到的是 两个指针之间的元素个数
	printf("%d\n", &arr[9] - &arr[0]); // 9
    // 指针和指针相减的前提是 两个指针都来同一块空间
    printf("%d\n", &arr[9] - &c[0]); // ?
}
```

###### 3.指针的关系运算

```c
int main() {
	int arr[10] = { 1,2,3,4,5,6,7,8,9,10 };
	int* p = arr;
	// + 9就是跳过9个数  为10
	int* pend = arr + 9;
	//     以关系运算判断指针是不是到最后了
	while (p <= pend)
	{
		printf("%d\n", *p);
		//p往后走一个数
		p++;
	}
}
```





#### 5.指针和数组

- 数组名就是数组首元素的地址：

```c
int main() {
	int arr[10] = { 1,2,3,4,5,6,7,8,9,10 };
	// 数组名就是数组首元素的地址
	printf("%p\n", arr);  // 000000903891FA58
	// 首元素的地址
	printf("%p\n", &arr[0]); // 000000903891FA58
}


int main() {
	int arr[10] = { 0 };
	int* p = arr;
	for (int i = 0; i < 3; i++) {
		printf("%p === %p\n", &arr[i], p + i);
		//  000000C50CAFF9B8 == = 000000C50CAFF9B8
		//	000000C50CAFF9BC == = 000000C50CAFF9BC
		//	000000C50CAFF9C0 == = 000000C50CAFF9C0
		//如果要赋值 使用解引用操作符*
		*(p + i) = i;
		printf("%d\n", arr[i]); // 0 1 2
	}
}
```



##### 1.二级指针 

```c
int main() {
	int a = 10;
	//pa是指针变量 一级指针
	int* p = &a;
	//ppa就是一个二级指针变量
	int** ppa = &p;  //&p 获取p在内存中的起始地址

    // **ppa 先通过*ppa 找到p 然后对p进行解引用操作：*p 最后得到的是a
	//*p == a
	//*ppa == p
	//**ppa == a
}
```

##### 2.指针数组

- 什么是指针数组

```c
int main() {
	int arr[10]; // 整型数组 - 存放整型的数组

	char ar[5]; // 字符数组 - 存放字符的数组

	int* cd[10]; // 整型指针数组 - 存放整型指针的数组
}
```











### 15.模拟实现字符串相关函数



#### 1.模拟实现strcpy

##### - 基本使用：

```c
int main() {
	char arr1[20] = "xxxxxxxxxxxxxx";
	char arr2[] = "hello";

	//模拟实现 strcpy(目标空间的起始地址,源空间的起始地址)
	strcpy(arr1, arr2);

	printf("%s\n", arr1); // hello
}
```

##### - 基本实现：

```c
//模拟实现 strcpy(目标空间的起始地址,源空间的起始地址)
void my_strcpy(char* dest, char* src) {
	// *src 不等于\0时循环就不会结束 \0的ASCE码为0
	while (*src) {
		*dest = *src;
		dest++;
		src++;
	}
	//因为循环到 \0时结束了循环 没有把\0放在目标数组里 所以需要最后时候放入\0
	*dest = *src;
}

int main() {
	char arr1[20] = "xxxxxxxxxxxxxx";
	char arr2[] = "hello";

	my_strcpy(arr1, arr2);
	printf("%s\n", arr1); // hello
}
```

##### - 优化：拷贝逻辑优化

```c
void my_strcpy(char* dest, char* src) {
	while (*dest++ = *src++);  // 优化
    // 因为*dest++ = *src++是一个赋值表达式  而的返回值是赋过去值
    // 赋值的最后是\0  ASCE码为0 所以停止循环
    // 同时兼顾了停止循环 与 拷贝
    
    // *dest++ = *src++
    // 相当于  a = 1  b= 2  c = a = b +2 
    // c = a(a = b +2) 相当于c = a的值  返回的最后是c的值
    // 所以  *dest++ = *src++ 返回的是*dest的被赋值后的值 
}

int main() {
	char arr1[20] = "xxxxxxxxxxxxxx";
	char arr2[] = "hello";

	my_strcpy(arr1, arr2);
	printf("%s\n", arr1); // hello
}
```

##### - 优化：断言判断参数是否无效

```c
#include <assert.h>
void my_strcpy(char* dest, char* src) {
	//assert(条件)  断言  条件符合时发出错误
	assert(dest != NULL); // 如果符合条件 则报错！
	while (*dest++ = *src++);
}

int main() {
	char arr1[20] = "xxxxxxxxxxxxxx";
	char arr2[] = "hello";
	my_strcpy(arr1, arr2);
	printf("%s\n", arr1); // hello
}
```

##### -优化：const限制源空间不会被改变

```c
//模拟实现 strcpy(目标空间的起始地址,源空间的起始地址)
// 使用const 可以防止通过指针方式改变它的值
void my_strcpy(char* dest, const char* src) {
	assert(dest != NULL);
	while (*src++ = *dest++); // 如果放反了 被const修饰的src指针会报错 无法赋值
}

int main() {
	char arr1[20] = "xxxxxxxxxxxxxx";
	char arr2[] = "hello";

	my_strcpy(arr1, arr2);
	printf("%s\n", arr1); // hello
}
```













