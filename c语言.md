### **1.a--与--a**

a--是先赋值再减1

--a是先减1再赋值

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221122214324300.png" alt="image-20221122214324300" style="zoom:50%;" />

其中（--x==y++）相当于：

```c
m=--x//此时m=9，x=9
n=y++//此时n=9，y=10
m==x//此逻辑式成立

```

注意：++，--**不能用在常值上**

### 2.注意赋值和逻辑比较

![image-20221123195526970](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221123195526970.png)

它执行的是：

1.将0，1分别赋值给i,x；

2.将10赋值给i，并且x>0；（此条件始终成立，故语句能始终执行下去）

![image-20221123202951608](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221123202951608.png)

### 3.c语言次方

```c
#include<math.h>
double pow(double x,double y)
```

即x的y次方

e.x.

```c
#include <stdio.h>
#include <math.h>
int main()
{
    printf("%f",pow(2,3));
    return 0;
}
```

结果为8；

### 4.static的用法

static int 不管在函数内还是函数外，都作为一个全局变量可以保存它被修改以后的值。

而 int 则没有这一功能，只有作为全局变量时能保存修改。放在函数内部时，每次调用都用的是一个新的数。

![image-20221124190628183](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221124190628183.png)

因为k的类型为static，故第二次进入该函数的时候，k的值仍为第一次改变的-1，而不是0；

### 5.递归函数

简单说就是函数套函数

e.x.

![image-20221124190906188](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221124190906188.png)

```c
#include <stdio.h>

int eat(int day, int num) {
	if (day == 1) {
		return num;
	}
	eat(day - 1, (num + 1) * 2);//此处就是递归
}

int main() {
	int num;
	num = eat(10, 1);
	printf("%d", num);
	return 0;
}
```



### 6.约瑟夫问题

![image-20221124194152582](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221124194152582.png)

```c
#include <stdio.h>

int main() {
	int n, i, num, loop;
	num = 0;
	int a[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
	scanf("%d", &n);
	for (i = 0; i < 10; i++) {
		num = (num + n - 1) % (10 - i);//此处关键
		printf("%d ", a[num]);
		for (loop = num; loop < 10 - (i + 1); loop++) {
			a[loop] = a[loop + 1];//出一个，后面的全往前移一个
		}
	}
	return 0;
}
```

### 7.小写字母和大写字母的转换

在ascii码中，小写字母在大写字母后边，小写字母比大写字母大32；

e.x:

我们想讲c转化为C，只需执行c-32即可

### 8.c语言字符转数字

对于数字字符m：m-'0';

对于小写字母字符m：m-'a';

对于大写字母字符m：m-'A';

### 9.不同进制输出

```c
#include <stdio.h>

int main()
{
	int i = 31;

	printf("i = %d\n", i);  // %d表示以十进制输出整型数据
	printf("i = %o\n", i);  // %o表示以八进制输出整型数据，注意这里是小写字母o
	printf("i = %x\n", i);  // %x表示以十六进制输出整型数据，如果数字中包含字母时，字母为小写
	printf("i = %X\n", i);  // %X表示以十六进制输出整型数据，如果数字中包含字母时，字母为大写
	printf("i = %#x\n", i); // %o表示以十六进制输出整型数据，输出结果中带有0x
	printf("i = %#X\n", i); // %o表示以十六进制输出整型数据，输出结果中带有0X

	return 0;
}

```

### 10.c语言进制转换

任意进制转10进制

```c
#include <stdio.h>
int main(){
	int x,p;   //x输入数字  p该数的进制数  
	scanf("%d",&x);
	scanf("%d",&p);
	int y=0,product=1;
	while(x!=0){
		y=y+(x%10)*product;
		x=x/10;
		product=product*p;
	}
	printf("%d",y);
	return 0;
} 
```

（二）十进制转任意进制
**注意：这里只能用do...while（原因：如果输入的是0，那么我们希望a[0]=0**

```c
#include <stdio.h>
int main(){
	int x,p; //x为十进制数，p为目标进制大小 
	scanf("%d",&x);
	scanf("%d",&p);
	int a[100]; //存放余数 
	int count=0;
	do{
		a[count++]=x%p;
		x=x/p;
	}while(x!=0);//当商不为0时进行循环 
	
	for(int i=count-1;i>=0;i--){
		printf("%d",a[i]);
	}
} 
```



### 11.矩阵输出空格问题

如果遇到一下输出格式

![image-20221125190211692](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221125190211692.png)

可以在输入数组时采用

```
scanf("%5d",a[x][y]);
```

在输入是格式为%5d，即可让输出数字占五个字符

### **12..选择排序**

```c
#define N 8
#include <stdio.h>
int main()
{      double a[N],t; 
       int i,j,k;
       printf("input  %d  number:\n",N);
       for(i=0;i<N;i++)    // 输入N个待排序的数
            scanf("%lf",&a[i]);      
       for(i=0;i<N–1;i++) {	  // N个数共需进行N-1趟排序
             k=i;// 本趟参加排序的N-i个数的第一个数下标为i，k是要找的最小元素的下标
             for(j=i+1;j<N;j++) 
                   if(a[j]<a[k]) k=j;     // a[j]比a[k]小，则将j赋给k
             t=a[k];     // 将找到的最小元素交换到本趟排序数的最前面
             a[k]=a[i]; 
             a[i]=t; 
        }  
        for(i=0;i<N;i++) 
           printf("%.2f  ",a[i]);    // 结果保留2位数
       printf("\n");
       return 0;
} 


```

从数组第一个开始，和每一个比，把每次比的最小的放到最前面

### **13.常用的数学模型**

![image-20221125222031306](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221125222031306.png)

### 14.关于%

%两边都必须是整数

### 15.逻辑表达式

![image-20221125225446107](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221125225446107.png)

PS：除了赋值式（以及！）是从右到左，其他都是从左到右

注意:**0为假非0为真！！0为假非0为真！！0为假非0为真！！**

![image-20221125225937198](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221125225937198.png)

![image-20221125225919293](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221125225919293.png)

#### 例题：

![image-20230205134436236](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230205134436236.png)

**答案：C**

**别忘了赋值语句！！！**，考就考赋值语句

### 16.没有定义返回值类型的函数

C语言中没有定义返回值类型的函数默认返回值类型为**int**

### 17.指针初始化和定义的一些易错点

#### 17.1.对于数组名

将指针变量名(实质是一个地址)与数组名(做右值时表示数组首元素首地址)绑定，直接看下面代码：

```c
//指针定义并初始化
char str[] = "hello"; 
char *p = str;   //对于数组，指针定义并初始化时不需要&
 
//先定义后初始化
char str[] = "hello";
char *p;
p = str;  //注意别写&str
//原因：因为&str做右值时表示整个数组的首地址
```

#### 17.2.对于普通变量

```c
//指针定义并初始化
char a = 65; 
char *p = &a;   //对于普通变量，指针定义并初始化时需要&
 
//先定义后初始化
char a = 65; 
char *p;
p = &a;  
```

#### 17.3.关于scanf（）与字符串

当定义了char *a以及char str[]时

可以

```c
char str[10];
scanf("%s",str);
```

**但是绝对不能**

```c
char *a;
scanf("%s",a);
```

a没有空间去存储%s的内容，除非先执行a=（char*）malloc（sizeof（xx））；

#### 17.4.总结

总结：给指针变量p赋值时，无论是定义时初始化p，还是先定义p后初始化，有如下规律：

用数组名给指针变量赋值时，不需要在数组名str前加取地址符&  ，因为str已经表示数组首元素首地址

用普通变量名给指针赋值时，需要在普通变量名a前加取地址符&，因为&a表示与变量名a绑定的内存空间的首地址

### 17.5关于字符指针的问题

因为类似char*p=“string”；

p指向的是**常量区**，常量区只需读不许修改

所以类似strcpy，strcat这种string函数是不可以对于字符指针使用的（strcmp这种可以）

### 18.关于char str[10]; str="string";的问题

1.必须明白char str[10]；是定义了一个含有十个元素的数组，而且这十个元素在内存中是以连续的存储单元存放的。其中str是该数组的数组名字，而且str还是该数组的首地址，也就是十个元素中的第一个元素的地址，但务必注意**str是一个指针常量**，**它是不能被赋值的也不能进行自增自减的！**

2、您指出char str[10]；str="string"；是错误的，因为前面已经指出**str只是一个地址，不是变量是不能被赋值的**。

3、char *s；是定义的一个指针变量，它指向一个字符型数据，它是可以被赋值的。指针变量和普通变量是一个道理的，不同的只是指针变量存放的是地址，而普通变量存放的是数值或字符等。*s代表的是指针所指向的数据，您用\*s="string"；是错误的，因为\*s和其他变量一样只能存放一个一个字符，而"string"中包含7个字符分别为s,t,r,i,n,g,\0；切勿把*s="string"与s="string"混同，后者是可以的，因为s是一个指针s**="string"是把该字符串的首地址赋值给了s而不是把string的每个地址都给了s**，前面已经指出字符串"string" 是存放在连续的存储单元的，所以可以通过s的递增来实现对每个元素的访问。

4、一维数组的初始化应该是如果元素为整数可用char str[10]=｛5，4，3，2，1｝；如果是字符则用char str[10]="string"；

【一】char s[5]="string";（数组s仅有5个存储空间是不能存放7个元素的）
等价于char *s;*s="string";（*s仅能代表一个元素，是不能赋值给它整个数组的）
【二】char s[5]="string";（错误同上 ）

![image-20230205133159736](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230205133159736.png)

**答案：B**

### 19.转义符与字符串长度

![image-20230205133713197](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230205133713197.png)

**答案：A**

x，y，两个

\n为转义符换行，一个

\102为转义符求八进制102对应ascii码，一个

\\\为转义符单斜杠，一个

\一个

### **20.printf中“%6.2f”的用法**

![image-20230205134921191](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230205134921191.png)

最终结果是（空格）49.50

PS：%6.2f意思是输出数据为6位且小数点后保留2位，并且**小数点占一位**

### 21.字符串+1

字符串＋1相当于左移一位

比如“ccc”+1

printf后会输出“cc”

### 22.” “与‘ ’的区别

” “是**字符串**，字符串内可不含字符，如“ ”表示空串；

单引号括起来的是**字符**，有且必须只有一个字符。

例如：“A”是字符串常量，包括‘A’及‘\0’两个字符，而‘A’是字符常量，只有一个字符。 

### 22.递归函数与函数嵌套

递归函数必须满足的两个条件：

1.存在***\*限制条件\****，当满足这个限制条件时，递归便不再继续。

2.每次[递归调用](https://so.csdn.net/so/search?q=递归调用&spm=1001.2101.3001.7020)之后**越来越接近**这个限制条件。

函数嵌套：

如果函数1调用了函数2，函数2再调用了函数3，便形成了函数的嵌套调用。

e.g.函数调用func（func（func（x）））不一定由限制条件，故不能说是递归调用，而是函数嵌套

### 23.结构体数组的print

![image-20230210125611974](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230210125611974.png)

因为.的优先级比*高，所以他实际上执行的是\*（（data+1）.a），肯定错误

正确的是

![image-20230210125829995](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230210125829995.png)

### 24.浮点型输出整形的相关问题

题目为：printf（“%f”，50\30）;的输出结果为？

自己尝试后发现为0.00000。

后来发现只要输出类型为浮点型，输入类型为整形，（输入输出类型不一样）那么他的结果就一直为0.

这是因为**浮点数和整数在printf时访问数据的寄存器是不一样的，属于未定义行为**

### 25.C语言中的4舍5入问题

1.只需要将输出结果+0.5强制类型转换为int即可、

e.g (int)(a+0.5)

2.调用round（）函数

### 26.进制转换

#### 1.任意进制转十进制

```c
#include <stdio.h>
int main(){
	int x,p;   //x输入数字  p该数的进制数  
	scanf("%d",&x);
	scanf("%d",&p);
	int y=0,product=1;
	while(x!=0){
		y=y+(x%10)*product;
		x=x/10;
		product=product*p;
	}
	printf("%d",y);
	return 0;
} 
```

#### 2.十进制转任意进制

```c
#include <stdio.h>
int main(){
	int x,p; //x为十进制数，p为目标进制大小 
	scanf("%d",&x);
	scanf("%d",&p);
	int a[100]; //存放余数 
	int count=0;
	do{
		a[count++]=x%p;
		x=x/p;
	}while(x!=0);//当商不为0时进行循环 
	
	for(int i=count-1;i>=0;i--){
		printf("%d",a[i]);
	}
} 
```

#### 3.二进制转16进制

```c
#include <stdio.h>
#include <math.h>
int main(){
	//输入2进制数 
	int x;
	scanf("%d",&x); 
	
	//确定：16进制数组大小size与2进制数组大小size*4.
	int X=x;
	int size=0; 
	while(true){
		if(X%10000!=0){ //采取看4位二进制的方法 
			size++;
			X=X/10000;
		}else{
			break;
		} 
	}
	char tt[size];   //16进制数数组 
	int t[size*4]; //2进制数数组 
      //存入 
	int sum=0;
	int count=0;
	for(int i=0;i<sizeof(t)/sizeof(int);i++){
		t[i]=x%10;
		x=x/10;
		sum=sum+t[i]*pow(2,count);
		count++;
		if(count%4==0){
			if(sum>=10){
				tt[--size]=65+(sum-10);  //字符'A'的ascii码为65 
			}else{
				tt[--size]='0'+sum;    
			}
			count=0;
			sum=0;
		}	
	}
	for(int i=0;i<sizeof(tt);i++){
		printf("%c",tt[i]);
	}
	return 0;
} 
```

### 27.将数字字符串转化为整数

只需-‘0’

e.g.

int d; 

d="123"-'0';

### 28.标识符的定义

![image-20230215171517399](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230215171517399.png)

### 29.区分行指针和指针数组

#### 1.行指针

§1．定义行指针变量

•类型标识符 (*变量名)[常量表达式]；

例如：

```c
int (*p)[4],(*q)[3]; 

​      int a[4][3],x[5][4];

​       p=x；   // 使p指向数组x的第1行

​       q=a+1;  // 使q指向数组a的第2行
```

•要注意的是p、q虽然都是行指针变量，但类型不同。

§2．用行指针引用数组元素

例如：

```c
int a[3][4],(*p)[4]; p=a;
```

   p指向数组a的第1行，可以用行指针变量p表示数组元素a\[i][j]的三种形式：p\[i][j]、*(*(p＋i)＋j) 和*(p[i]＋j)。

•要注意：p的值可修改，如p=p+1,后 指针p与a不再指向同一行。

#### 2.指针数组

§1.指针数组定义

•类型标识符 *数组名[数组长度]；

•例如，

```c
int *p[10]；
```

–即定义了数组p是指针数组。

–数组p的每个元素是指针类型，存储int型变量的地址。 

### 30.条件语句赋值顺序问题

```c
#include <stdio.h>

int main() {
	int a = 2, b = 3, i = 10;
	for (i = 0; i < b; i++) {
		a++;
	}
	if ( a || (b = 4)) {
		a = 10;
	}
	printf("%d,%d", a, b);
	return 0;
}

```

此语句最终结果a=10，b=3

因为if后是或（||），所以b=4这个赋值语句没有机会执行，但是如果if后是且（&&）,则最终结果为a=10；b=4.

### 31.二级指针不能直接指二维数组

