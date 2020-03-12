+ 栈的源代码实现（顺序存储）
````cpp
#ifndef STACK_H_
#define STACK_H_
#define maxsize 10010

template<typename T>
struct stacknode
{
	int top;
	T* data;
};
template<typename T>
void InitStack(stacknode<T>* s)
{
	s->top = 0;
}
template<typename T>
void Push(stacknode<T>* s, T x)
{
	if (s->top == maxsize)printf("Stack Overflow");
	else s->data[s->top++] = x;
}
template<typename T>
T Pop(stacknode<T>* s)
{
	if (s->top == 0)printf("Stack Empty");
	else return s->data[--s->top];    
}
template<typename T>
T Top(stacknode<T>* s)
{
	if (s->top == 0)printf("Stack Empty");
	else return s->data[s->top - 1];
}
#endif
````
+ 进制转换的源代码实现（注：只处理11至36进制，添加字母表示）
````cpp
//输入n为十进制，转换为m进制
stacknode<int>* s = new stacknode<int>;
char hashtable[26] = { 'A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z' };
void conversion(int n, int m)
{
	
	s->data = new int[maxsize];
	InitStack(s); int r;
	while (n != 0)
	{
		r = n % m;
		if (m>=11&&m<=36&&r > 9)r = hashtable[r - 10];
		Push(s, r);
		n /= m;
	}
	while (s->top != 0)
	{
		if(Top(s)>=65)
			printf("%c", Top(s));
		else printf("%d", Top(s));
		Pop(s);
	}
}
````
+ 结果演示 输入：十进制数n、m进制 输出：n转换成m进制后的数
  


![2](C:\Users\Dell\Desktop\13.png "13.png")

![3](C:\Users\Dell\Desktop\14.png "14.png")

![4](C:\Users\Dell\Desktop\15.png "15.png")

![5](‪C:\Users\Dell\Desktop\22.jpg "22.jpg")

![6](‪‪C:\Users\Dell\Desktop\21.jpg "21.jpg")


