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



























