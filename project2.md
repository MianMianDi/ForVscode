+ 单链表的创建和插入元素等操作的源代码实现
````cpp
struct listnode {
	Point3D data;
	listnode* next;
	listnode() :next(NULL){};
	listnode(Point3D _data) :data(_data),next(NULL) {};//构造函数
};
listnode* CreateList(int n, Point3D* elem)
{
	listnode* head=new listnode,*temp=head;
	for (int i = 0; i < n; i++)
	{
		//temp->next=&listnode(elem[i]);注意这种写法错误
		temp->next = new listnode(elem[i]);
		temp = temp->next;
	}
	temp->next = NULL;
	return head;
}
int InsertList(listnode* L, int i, Point3D b)
{
	if (!L->next&& i>1)return false;
	if (!L->next && i == 1) { listnode* p = new listnode(b); p->next = NULL; L->next = p; return true; }
	listnode* temp = L->next; 
	int index = 1;
	while (temp && index < i-1)
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
+ 三等分多边形各边的源代码实现
  + num参数为需加细总次数，TrisectPolygon函数返回num次细分后多边形结点链表的头节点
  + SubdivideNode函数处理以a为起始点，以b为终点所形成的边，返回该边需要添加的三个点的坐标向量数组
````cpp
Point3D* SubdivideNode(Point3D a, Point3D b)//平面图形三等分
{
	Point3D* P=new Point3D;
	
	P[0].x = (2 * a.x + b.x) / 3;
	P[0].y = (2 * a.y + b.y) / 3;
	
	P[1].x = (a.x + b.x) / 2 - sqrt(3) * (b.y - a.y) / 6;
	P[1].y= (a.y + b.y) / 2 + sqrt(3) * (b.x - a.x) / 6;
	
	P[2].x = (2 * b.x + a.x) / 3;
	P[2].y = (2 * b.y + a.y) / 3;

	for (int i = 0; i < 3; i++)
	{
		P[i].z = 0;
	}
	return P;
}
listnode* TrisectPolygon(char filename[],int num)
{
	FILE* fp;
	int n,cls,step=0;//step记录加密次数,n记录当前有的节点总数
	if (!(fp = fopen(filename, "r"))) exit(1);
	fscanf(fp, "%d", &n);
	Point3D* e = new Point3D[n];//分配一个Point数组的空间
	for (int i = 0; i < n; i++)
	{
		fscanf(fp, "%lf%lf%lf", &e[i].x, &e[i].y, &e[i].z);
		printf("(%f,%f,%f)\n", e[i].x, e[i].y, e[i].z);
	}
	
	listnode* L = CreateList(n, e);//创建多边形节点构成的链表
	free(e);
	//printf("n=%d\n", GetListLength(L));
								   
	for (; step < num; step++)//加细过程
	{
		int index = 2;//当前插入位置 
		listnode* pa = L->next, * pb = pa->next;
		for (int i = 1; i <= n - 1; i++)//加细第i条边
		{
			
			Point3D* p = SubdivideNode(pa->data, pb->data);
            //p存储该边需要添加的三个节点的坐标向量
			for (int j = 0; j < 3; j++)
			{
				InsertList(L, index++, p[j]);
                //在第index个元素处插入
			}
			index++; pa = pb; pb = pb->next; //处理下一条边
		}
		n += 3 * (n - 1);//每细分一次，总节点个数增加3*(n-1) 
        //printf("n=%d\n", GetListLength(L));
	}

	fscanf(fp, "%d", &cls);
	fclose(fp);
	return L;
}
````

+ 绘制并显示多边形的源代码实现
````cpp
void BoundingcomputationForListPolygon(listnode* L)
{
	
	Point3D box_center; //the center of bounding box
	Real	rad;		//the radiance of bounding box

	if (!L->next) {
		SetVec3D(&box_center, 0.0, 0.0, 0.0);
		rad = 1.0;
		return;
	}
	listnode* p = L->next;
	Real xmin, xmax, ymin, ymax;
	xmin = 10000.0;
	ymin = 10000.0;
	xmax = -10000.0;
	ymax = -10000.0;
	while(p) {
		if (p->data.x < xmin) xmin = p->data.x;
		if (p->data.x > xmax) xmax = p->data.x;
		if (p->data.y < ymin) ymin = p->data.y;
		if (p->data.y > ymax) ymax = p->data.y;
		p = p->next;
	}
	Real xb, yb;
	xb = (xmin + xmax) / 2.0;
	yb = (ymin + ymax) / 2.0;
	SetVec3D(&box_center, xb, yb, 0.0);

	xb = (xmax - xmin) / 2.0;
	yb = (ymax - ymin) / 2.0;
	rad = xb > yb ? xb : yb;
	rad = rad * 1.2;
	p = L->next;//p重置为第一个元素节点
	Real cx, cy, cz;
	while(p) {
		cx = (p->data.x - box_center.x) / rad;
		cy = (p->data.y - box_center.y) / rad;
		cz = 0.0;
		SetVec3D(&p->data, cx, cy, cz);
		p = p->next;
	}
}
void ListPolygonDisp(listnode* L)
{
	float cx, cy, cz;
	//glLineWidth(4.0);
	glBegin(GL_LINE_STRIP);
	listnode* p = L->next;
	while(p) {
		cx = (float)(p->data.x);
		cy = (float)(p->data.y);
		cz = (float)(p->data.z);
		glVertex3f(cx, cy, cz);
		p = p->next;
	}
	
	glEnd();
	glFlush();
}
void DisplayTrisectPolygon(listnode* L)
{
	if (!L->next)return;
	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
	glColor3f(0.0, 0.0, 1.0);
	ListPolygonDisp(L);
	
}
````
+ 结果演示(加密次数分别为0，1，2，3，4)
![polynomial结果演示0](C:\Users\Dell\Desktop\DataStructure_2020\Project\0.png "0.png")
![polynomial结果演示1](C:\Users\Dell\Desktop\DataStructure_2020\Project\1.png "1.png")
![polynomial结果演示2](C:\Users\Dell\Desktop\DataStructure_2020\Project\2.png "2.png")
![polynomial结果演示3](C:\Users\Dell\Desktop\DataStructure_2020\Project\3.png "3.png")
![polynomial结果演示4](C:\Users\Dell\Desktop\DataStructure_2020\Project\4.png "4.png")
