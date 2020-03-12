+ 单链表的创建和插入元素等操作的源代码实现
  + poly结构存储非零项的系数和指数
  
````cpp
struct poly
{
	double coef;
	int expo;
	poly() {};
	poly(double _coef, int _expo) :coef(_coef), expo(_expo) {};
};
struct listnode {
	poly data;
	listnode* next;
	listnode() :next(NULL){};
	listnode(poly _data) :data(_data),next(NULL) {};//构造函数
};
listnode* CreateList(int n, poly* elem)
{
	listnode* head = new listnode, * temp = head;
	for (int i = 0; i < n; i++)
	{
		//temp->next=&listnode(elem[i]);注意这种写法错误
		temp->next = new listnode(elem[i]);
		temp = temp->next;
	}
	temp->next = NULL;
	return head;
}
int InsertList(listnode* L, int i, poly b)
{
	if (!L->next&&i>1)return false;
	if (!L->next && i == 1) { listnode* p = new listnode(b); p->next = NULL; L->next = p; return true; }
	listnode* temp = L->next;
	int index = 1;
	while (temp && index < i - 1)
	{
		temp = temp->next; index++;
	}
	//第i-1个元素为空
	if (!temp)return false;
	listnode* s = new listnode(b);//或者分配新空间，将s->data赋为b
	s->next = temp->next;
	temp->next = s; return true;
}
````
+ 多项式相加算法的源代码实现
````cpp
listnode* Addpolynomial(listnode* La, listnode* Lb)
{
	double coef1,coef2; int expo1,expo2;
	listnode* Lc = new listnode, * pa = La->next, * pb = Lb->next,*pc=Lc;
    //若第一个多项式为0
	if (!pa) {
		Lc = Lb; free(Lb); return Lc;
	}
    //若第二个多项式为0
	if (!pb) {
		Lc = La; free(La); return Lc;
	}
	while (pa && pb)
	{
		expo1 = pa->data.expo, expo2 = pb->data.expo; coef1 = pa->data.coef; coef2 = pb->data.coef;
		if (expo1 == expo2) //若两项的次数相等
        {
			coef1 +=coef2 ; 
			if (!coef1)
			{
				pa = pa->next; pb = pb->next;
			}
			else
			{
				pc->next = new listnode(poly(coef1, expo1));
				pc = pc->next; pa = pa->next; pb = pb->next;
			}
			
		}
		else if (expo1 < expo2)//若第一项的次数小于第二项
		{
			pc->next = new listnode(poly(coef1, expo1));
			pc = pc->next;
			pa = pa->next;
		}
		else//若第一项的次数大于第二项
		{
			pc->next = new listnode(poly(coef2, expo2));
			pc = pc->next; pb = pb->next;
		}
	}
	pc->next = pa ? pa : pb;
	free(La); free(Lb);
	return Lc;
}
````
+ 主函数源代码实现
````cpp
int main()
{
	int m,n,expo1,index=1;//m为第一个多项式的最高次数
	double coef1; 
	printf("input the degree of the first polynomial:\n");
	scanf("%d", &m);
	listnode* La = new listnode;
	printf("input the coefficient and the exponent according to the exponentially increasing order:\n");
	do
	{
		scanf("%lf%d", &coef1, &expo1);
		InsertList(La, index++, poly(coef1, expo1));
		
	} while (expo1 < m);


	index = 1;
	printf("input the degree of the second polynomial:\n");
	scanf("%d", &n);//n为第一个多项式的最高次数
	listnode* Lb = new listnode;
	printf("input the coefficient and the exponent according to the exponentially increasing order:\n");
	do
	{
		scanf("%lf%d", &coef1, &expo1);
		InsertList(Lb, index++, poly(coef1, expo1));
	} while (expo1 < n);

	listnode*Lc=Addpolynomial(La, Lb),*pc=Lc->next;
	if (!pc)printf("0");
	while (pc)
	{
		printf("(%lf,%d)", pc->data.coef, pc->data.expo);
		pc = pc->next;
	}

	return 0;
}
````
+ 结果演示
  + (1+x+x^2)+(-1-x-x^2) 
![triangle.txt结果演示5](C:\Users\Dell\Desktop\DataStructure_2020\Project\5.png "5.png")
  + (1+x^10000)+(-1+x^9999)
![triangle.txt结果演示6](C:\Users\Dell\Desktop\DataStructure_2020\Project\6.png "6.png")
  + (x+x^3+x^5)+(1+x^2+x^4)
![triangle.txt结果演示7](C:\Users\Dell\Desktop\DataStructure_2020\Project\7.png "7.png")
  + (0)+(1+x^100)
![triangle.txt结果演示8](C:\Users\Dell\Desktop\DataStructure_2020\Project\8.png "8.png")
  + (0)+(0)
![triangle.txt结果演示9](C:\Users\Dell\Desktop\DataStructure_2020\Project\9.png "9.png")