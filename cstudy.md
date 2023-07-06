---
title: C语言学习记录
date: 2023-03-05 21:07:33
tags:
---

```c
#include "stdio.h"
#define N 10
void Input(int b[N])
{//输入函数 
	int i;
	printf("请输入%d个整数：",N);
	for(i=0;i<N;i++)
	{
		scanf("%d",&b[i]);
	}
}
void BubbleSort(int b[N])
{//冒泡排序函数
	int i,j,t;
	for(i=1;i<N;i++)
	{ //外层循环控制趟数
		for(j=1;j<N-i+1;j++)
		{ //内层循环控制每趟的比较次数
			if(b[j-1]<b[j])
			{  
				t=b[j];
				b[j]=b[j-1];
				b[j-1]=t;
			} 
		} 
	}
}
void Print(int b[N])
{//输出函数 
	int i;
	for(i=0;i<N;i++)
	{
		if(i%10==0)
		printf("\n");
		printf("%6d",b[i]); 
	} 
	printf("\n");
}
int main()
{ 
	int a[N];
	Input(a);
	printf("排序前：");
	Print(a);
	BubbleSort (a);
	printf("排序后：");
	Print(a);
	return 0;
}
```

<https://www.tiktok.com/@extremeofficial>
<https://www.tiktok.com/@jiyayjt>
<https://www.tiktok.com/@bigznoexcuses>
<https://www.tiktok.com/@devonrodriguezart>
<https://www.tiktok.com/@chucanbang>
<https://www.tiktok.com/@navoiteam>
<https://www.tiktok.com/@therock>
<https://www.tiktok.com/@california_tonystark>
<https://www.tiktok.com/@sebastian_schieren>
<https://www.tiktok.com/@redbulltaiwan>
<https://www.tiktok.com/@redbull>
<https://www.tiktok.com/@tighteyex>
<https://www.tiktok.com/@olivernordin1>
<https://www.tiktok.com/@bdash_2>
<https://www.tiktok.com/@basketactions>
<https://www.tiktok.com/@tuvok12>
<https://www.tiktok.com/@kurtschneider>
<https://www.tiktok.com/@richardmbrowning>
<https://www.tiktok.com/@redbullfreerunning>
<https://www.tiktok.com/@mygwanglei>
<https://www.tiktok.com/@taylorswift>
<https://www.tiktok.com/@drifterjjlin>
<https://www.tiktok.com/@gemdzq>
<https://www.tiktok.com/@dino.serrao>
<https://www.tiktok.com/@fukada0318>

# 课本87页 课堂实践4-4 2023年3月14日  
```c
#include<stdio.h>
void week(int i)
{
	switch(i)
	{
	    case 1:printf("Monday");break;
	    case 2:printf("Tuesday");break;
	    case 3:printf("Wednesday");break;
	    case 4:printf("Thursday");break;
	    case 5:printf("Friday");break;
	    case 6:printf("Saturday");break;
	    case 7:printf("Sunday");break;
	    default:printf("输入错误！");
	}
}
int main()
{
	int i;
	printf("请输入1~7数字表示对应的星期几：");
	scanf("%d",&i);
	week(i);
	return 0;
}
```

# 计算三位数各数位和 课本57页 2023年3月6日  
```c
#include<stdio.h>
int sum(int n);
int main()
{
	int n;
	printf("请输入一个三位正整数：");
	scanf("%d",&n);
	printf("数%d的各位数字之和为：%d",n,sum(n)); //函数调用作为实参
	return 0;
}
int sum(int n)
{
	int ge,shi,bai;
	ge=n%10; //提取个位数
	shi=n/10%10; //提取十位数
	bai=n/100; //提取百位数
	return ge+shi+bai;
}
```

# 输入一个字符，输出ASCII比它大5的字符 正确答案 2023年3月6日
```c
#include<stdio.h>
char fun(char ch);
int main()
{
	char ch;
	ch=getchar();
	ch=fun(ch);
	putchar(ch);
	return 0;
}
char fun(char ch)
{
	return ch+5;
}
```

# 鸡兔同笼 正确答案 2023年3月6日  
```c
#include<stdio.h>
int fun_c(int h,int f);
int fun_r(int h,int cock);
int main()
{
	int f,h,cock,rabbit;
	printf("请输入总共的头数和脚数：");
	scanf("%d%d",&h,&f);
	cock=fun_c(h,f);
	rabbit=fun_r(h,cock);
	printf("鸡和兔子分别有%d,%d只。\n",cock,rabbit);
	return 0;
}
int fun_c(int h,int f) //计算鸡数
{
	int cock;
	cock=(4*h-f)/2; //设都是兔子，则所有的兔脚4*h减去现有的脚f，再除二，得鸡数
	return cock;
}
int fun_r(int h,int cock)
{
	return h-cock;
}
```

# 鸡兔同笼 2023年3月5日  
```c
#include <stdio.h>

int main() 
{
	int h, f;
	printf("请输入鸡兔共多少只：\f");
	scanf("%d", &h);
	printf("请输入鸡兔共多少只脚：\f");
	scanf("%d", &f);
	if ((f - 2 * h) >= 0 && (f - 2 * h) % 2 == 0 && (4 * h - f) >= 0 && (4 * h - f) % 2 == 0) 
	{
		printf("鸡有%d只，兔有%d只", (4 * h - f) / 2, (f - 2 * h) / 2);
	}
	else 
	{
		printf("您的输入有误！");
	}
	return 0;
}
```

# 时间计算 2023年3月5日  
```c
#include <stdio.h>
int time(int x,int y);
int main()
{
	int x,y,z;
	printf("开始时间： 流逝时间：");
	scanf("%d %d",&x,&y);
	z=((((y/60)*100)+x)+(y%60));
	printf("时间为：%d",z);
	return 0;
}
```

# 时间计算另一种 by Chen Decheng 2023年3月5日
```c
#include<stdio.h>
int fun(int t1,int t2);
int main()
{
    int t1,t2;
    printf("请输入开始时间和流逝时间：");
    scanf("%d%d",&t1,&t2);
    t1=fun(t1,t2);
	printf("流逝后的时间是：%d\n",t1);
	return 0; 
}
int fun(int t1,int t2)
{
	int h,m;
	h=t1/100;
	m=t1%100;
	t1=h*60+m+t2;
	h=t1/60;
	m=t1%60;
	t1=h*100+m;
	return t1;
}
```

# 输入一个字符，输出ASCII比它大5的字符 2023年3月5日  
```c
#include<stdio.h>
char fun(char ch);
int main()
{
	char ch=getchar();
	ch=fun(ch);
	putchar(ch);
	return 0;
}
char fun(char ch)
{
	return ch+5; 
}
```
