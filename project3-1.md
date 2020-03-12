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
+ 判断对称性的算法源代码实现
````cpp
void isSymmetry(char* p, int len)
{
	s->data = new char[len+1];//分配空间要在函数内
	InitStack(s);

	for (int i = 0; i < len / 2; i++)
	{
		Push(s, p[i]);
	}
	int r = (len + 1) / 2;
	for (int j = r; j < len; j++)
	{
		if (p[j] != Top(s)) {
			printf("Not Symmetric"); free(s->data); return;
		}
		Pop(s);
	}
	free(s->data);//记得释放
	printf("Is Symmetric"); return;
}
````
+ 结果演示 输入：字符串、长度 输出：Is Symmetric / Not Symmetric

![1](C:\Users\Dell\Desktop\01.png "01.png")

![2](C:\Users\Dell\Desktop\02.png "02.png")



![4](C:\Users\Dell\Desktop\04.png "04.png")

![5](C:\Users\Dell\Desktop\05.png "05.png")
  
<br/>

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAfcAAAA2CAMAAADtaCCwAAAAAXNSR0IArs4c6QAAAKtQTFRFAAAAbKXBiUwAwYlMAABMicHBpWwq////wcHBAAAqKgAApcHBAEyJbCoAwaVsTInBKmylTAAAiUwqwcGlwcGJKkxsTGyIACpMwaWJiKWlACpsKmyJUImlpaaJpYlsTCsAwaWlKioApaXBjMGlbEwAakwqmqWxUExSd2wqiYlMLCoqKipMiYmlAExsiWxspYlMl2xMbIl7ACoqKkyJbGyTTGylbKWJKmxsiYmJ4TAvTQAABFlJREFUeNrtnOta4jAQhlMobNIDjVQECngGVtRVPOx6/1e2ObalJIo+gpTM96d5xiFg3iaZJNOiXyAXhUAgEAgEAh2yyOLkus72z/qApEYhbtTZvrEPWQaqcBJifHrmOni/1ai1fSOf7O0OdxT35PgMkdc0Bu6Hz/1pPm8p7pEknujbALgfMPcSaHWNXO/wjnEnXlOO/GHbxSh+zGKb865qq/6QBTpBTe1WHzN3v6W5Nx3k3mqyRuiFDdEQfyZnqO/xZvFraTf7WPu7Guexi9zF5Ea8tmirwZFoh4ae9Oplt/lY53fl7yT3eVBqqzbSF1JDu83Hxj0LB2xIGM6dHOcR6d1dYtwuYiEV79TPbvcxc0c8AhjEEXYxrhuFk+mF7iOltqqh3epj4y5FP97+O0DhbmlsLNqK1tBu8/mAe3J85CB3OVaW24rPiXoMrZPd5mPnToLScs5R7uRCNxIPi1Vj1Mpu87Fy98WGLXVzu46PjbfDy6b/G/lXsy5f//IWS2pot/lU1J+lU8WdjfDPTs7uCMmjyChky13/hh9Myv0uUkO7zWdFERZqyjuAx/MIBAKBQCAQCAQCgUAgEGgvhWV2CsYbZpWKXKbJ/PF7f4XvpbB/slOFKtlovdn9GxN27zFA5BV/MffYWKeoFrjvVku5P32/3uzZg8GdSuD0i9yNdYJ+QFOZXWjgTk3nk4lKbPn7tTNr2oQW3w9dyzSjde49Y9pZooxP1YH6wlzepE5R3xRQ7Ja7zDeR3DN+QCUIUHlstXZISYtkNB4MHh8RD+M0TnB7zC6jMOXHoUWZqT821Nlfvs06AWF+3Ieml0VOK/eXnwRtlbt4XkRwj9IuQs9hY7VrV8L50uEmFRlK9IFFet6ki5Lzx4DyO6Eo86RVFgiu1Unm81lnMZwSTyU55V+Whaw6Nx9h2TF30eE5d5WbpHNUEvOY3Jvh9FElrFxxz3Gsc91YpBBx7kVZZT2pO2SlTtpZsg+OupUbQoQbxHP9WcVdcOe9i3NXcBQqG3eRfjw4yqM8EaKLz+TcizLKruQEojp8mfvKHKL/oB50OIHpfvvceYdn3PPcU5V/lthj755e9bMLbbzHXd1LOr9xpb8HBu7UyeTWH+LOOvznuOv+y2YGuaKzc1exHAbu+8eddfj5Ztz1K0L0XECbcifmo/5exQvc94J7Fk7inMS78/s4XuGeTV4a73KvJDJ/yF37+2eAZvvc5aOhavBeief/VbqfoiUjec67FAuauOsbZLRWp5m7DgRGsF2/XcmgWobdNBU552ppFR3HKKueo0R4sOAJyHp9rTZerdzl+p2M22t1mrmzLyj7g7YlLDusHL97+X6dsBneF3F/ejLEpa2bkRrmWeDGQrhmhHF6WZR53WL/rVupMwuLLPZ8I6+tV4mwX7fvyl8FB3JH/rARQcd0T/0WhuN0EAgEAoFAoH2P1a/i3dVDFrcvD+vl7/oNP/Z/7e43b/S+/XI9/wFGjpzMM/lilgAAAABJRU5ErkJggg==">