# C语言

## 一.基础

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
//%d - 打印整型
//%c - 打印字符
//%f - 打印浮点数字（小数）
//%p - 以地址的形式打印
//%x - 打印16进制数字...

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
| double     | 双精度浮点数   |

```c
// 数据类型的大小  （以下单位为 字节   1字节=8个比特位）
int main() {
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

### 6.选择语句

##### 1.if语句

```c
int main() {
	int input = NULL;
	printf("加入比特\n");
	printf("你要好好学习吗？(1/0):");
	// 控制台中输入input的值
	scanf_s("%d", &input);
	//判断input是否等于1
	if (input == 1)
		printf("好offer");
	//如果不等于1 再判断input是否等于0
	else if (input == 0)
		printf("卖红薯");

	return 0;
}
```

### 7.循环

##### 1.while循环

```c
int main() {
	int line = 0;
	printf("加入比特 \n");

	//条件
	while (line < 20)
	{
		//代码块
		line++;
		printf("%d敲代码！\n", line);
	}
	return 0;
}
```

##### 2.for循环



##### 3.do...while循环





### 8.函数

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

    









































### 9.数组

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





##### 8.数组的应用实例1：三子棋





##### 9.数组的应用实例2：扫雷











### 10.操作符

##### 1.算数操作符

- \+  (加)
- \-   (减)
- \*  (乘)
- /（除） 
- %（取余）

##### 2.位移操作符

- \>>
- <<

##### 3.(2进制)位操作符

- & 按位与   （与）有0则0
- ^ 按位或    （或）有1则1
- | 按位异或 （非）有1则0

##### 4.赋值操作符

- =
- +=
- -=
- *=
- /=
- &=
- ^=
- \>>=
- <<=

##### 5.单目操作符（只有一个操作数）

- ！（真变假 假变真）
- \- （负值）
- \+（正值）
- &（取地址）
- sizeof（操作数的类型长度【以字节为单位】）
- ~ 对一个数的二进制按位取反 （按【二进制】位取反） 
- -- 前置、后值--
- ++ 前置、后置++
- \* 间接访问操作符(解引用操作符)
- （类型）   强制类型转换

##### 6.关系操作符

- \>
- \>=
- <
- <=
- !=
- ==

##### 7.逻辑操作符

- && 逻辑与 （都是真才是真）
- || 逻辑或  （一个真就是真）

##### 8.条件操作符

- exp1 ? exp2 : exp3

##### 9.逗号表达式

- exp1,exp2,exp3,...expN

##### 10.下标引用、函数调用和结构成员

- []
- ()
- .
- ->

##### 11.原码 反码 补码

![image-20220826152613163](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220826152613163.png)

### 11.常见关键字

C语言内置的关键字，不能定义为变量名等冲突。

![image-20220826152740112](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220826152740112.png)

##### 1.关键字 typedef （类型重定义）

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

##### 2.关键字 static 

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





### 13.指针

```c
int main() {
   
1.	int a = 10; // 向内存申请4个字节
	// &a   &为取地址操作符
	// %p是以地址形式打印
	printf("%p\n", &a); // 获取a存在内存的地址  获得00000026C9DCF794 为16进制数

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

	return 0;
}
```

### 14.结构体(对象)

- 类似js的对象 

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
	//打印
	printf("书名：%s\n", b1.name);
	printf("价格：%d\n", b1.price);
	//修改结构体中的数据
	b1.price = 250;
	printf("修改后的价格：%d\n", b1.price);

	return 0;
}
```

- 结构体使用指针变量储存 并 使用指针变量打印数据

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



### 15.分支

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

### 16.循环语句

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









