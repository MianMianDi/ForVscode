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


<img src="data:image/jpg;base64,iVBORw0KGgoAAAANSUhEUgAAAL4AAAAwCAMAAACYEDAHAAAAAXNSR0IArs4c6QAAAIRQTFRFAAAAAEyJiUwApcHBAAAqbKXBKgAAwcHBKCgowYlMACpsTAAAwcGJAABMicHBwaVsTInBpWwqbCoAKmylTCoAwcGlTImlj6XBACpMpYlsKkxMnolMYF1apWxMr6WJKkyJV2yliVwqACoqKmyJibOJKipse6WlMkZYwaWlTImJiaVspaVsVmnG8QAAAbZJREFUaN7tmMt2gyAQhgERIkbjrWqbe5umt/d/v4LgQaMu2kU6nMJG5fyLjzkz/4ygN+T0WrmNv/PR/2P8l4Dzx8ruZdFUN9IcG/nBgOBnW4bacB33W5hP8Uea+lAhkW4YCHwREPlM0p45Saf4I02pTpHAwN9JNAVFwx4n24cz+FaTpLnaolCS56ka4uOITvGHGvxQwDNOnR4ytpd4Dn+gyWyVgDHO1ybXLzVBS/haQ2UBHwNAzqO8hu81TZmjBfxeI/FP0oZEAKR0u/VcdxktvhhajL7W0FAbE+YEUtdVKU2vBVrGNxrj/tZpQeCraAqZ03rNu4vS9PjLh7y3cTJtK6Z4Z8EGmkwfDQp+eZvLM2BDjRGa7gUAn6CRnc/iW40ZF2B0rxVKmogherJG0k7HmZEGK89sQQRf5T6tZcUeKuvvct0eYKRpr5y/n/3visf3+B7f43v8++OXsklFulsRF6OPedf+xaVwMnnMhCbOjua+nh0/Ykfxu8ldbJ11HjXGl4Wz+CIgySdzFp+Gm2OOnMWX3rmOHcaHcWfza3wYlx4e3+N7/J/hq5nZxWnZ/215/P+L/w1cPRUsHSiPJgAAAABJRU5ErkJggg==" />

  
<br/>
<img src="data:image/jpg;base64,iVBORw0KGgoAAAANSUhEUgAAAQsAAAA1CAMAAABhjD4JAAAAAXNSR0IArs4c6QAAAKVQTFRFAAAAAAAqKCgoicHBTInBpWwqAABMwcHBKgAAwaVsAEyJKiosbCoDbKXBiUwATAAApcHBACpsTExMwcGlwYlMwcGJKmylfUwqACpMTCoAwaWJpauUpaVswaWlicGlpYlspYlMWWyJKzdLiaXBpaXBKmyJe4mlKkxsiaWJiWw2iYmJKkyJTExsV3+lTGylpcGlbEwAACoqbIlsiaWlAExsTEY8bKWJeJD6sQAAAppJREFUaN7tm9t6ojAQgJM1HKRFQS1FbVetVWut3e7x/R9tk0wCCNhVu3uxk5mLQnHgMz+TyRwi+8RIrBALYkEsTmHBv4X66HcCEE9dXDwGwf1t211WX8pOKs1CLCzS53XQhdGkyWwg5eWpL/8RkzFjm8Sr31LRZ2wvldJON0TC4uvgxQ4mmsNhq/7c9PX58Lp2S0WfZUrJx8NCmYAZzEqPm/9SFDK45nd6zbusvt/RVsNDho+Fedle8cr/wKJpNMhY+NpbSN8xUhejNvu3+gJ44WWRGW8ZJXIRyZ/G7CgLHt/0dwmmdaTGwv9s7f6HHGa7VyxZ7OehtCCMvpNVJ0V0F+brdhgFi2CkNYMeShY8HpkwYqp8wS55x1+oOQL+dYSSRZqYdyxgfK3vvMai4IeMhR07j3vVEOLIOgJrKlYWomDhHRzb4wtQbuX1/7OQ7rB3MN70y/V7cac+QRJyaRb5cnjbYMHjbntuVtWPlGvNcZiFYhFBmm6m/H74ZrEsZHwxaebsB/r592N5PdVyiAWxIBbEglgQC2JBcpVB5DScQ1S9WeKJnc5mAYkVX0GdIpuMGX8NPJdZSAoqDzGJmEBV3j6fhU6/TcKJpGb3QRao6pcXs4BWx4PuAGSo2h5n+87XSekikJTsLmKh1tQKCttJdXaObMraf3TnJorSX6S2mJe6ioINin0DptfhrFXIhaMo6EOA5TCKco7wWLGAxiFLt07PEd0sN1svWOZ0rJUvlVkIvXVtsHY0HxEmZ5+NdaMIxNW4k4RYNOUnISC7aF1TScguiMVlc6Tc5/kxOek5/OphMW+e/63vcNr3UXahN51Mn99qH4miMyDgFyWq6nNBcF4+B3ax3G+b6d9q+mg3wxyci3/QnTj2zN9bTSUqZpqB0AAAAABJRU5ErkJggg==" />


[//]: <![16](https://raw.githubusercontent.com/MianMianDi/ForVscode/master/MarkdownImages21.jpg "21.jpg")>


