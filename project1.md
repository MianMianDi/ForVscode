+ 计算多边形面积的算法：

````cpp
    Point3D crossProduct(Point3D o,Point3D a, Point3D b)
    {
        Point3D c;
        c.x = (a.y-o.y) * (b.z-o.z) - (a.z-o.z) * (b.y-o.y);
        c.y = (a.z-o.z) * (b.x-o.x) - (a.x-o.x) * (b.z-o.z);
        c.z = (a.x-o.x) * (b.y-o.y) - (a.y-o.y) * (b.x-o.x);
        return c;
    }
    Point3D total = {0,0,0};//叉乘的累加
        for (i = 0; i < n - 1; i++)
        {
            //求P[0]与P[i]构成的向量和P[0]与P[i+1]构成的向量的叉乘
            C[i] = crossProduct(P[0],P[i], P[i + 1]);
            //printf("%f,%f,%f\n", C[i].x, C[i].y, C[i].z);
            total.x += C[i].x; total.y += C[i].y; total.z += C[i].z;
        }
    //求面积
	area = sqrt(total.x * total.x + total.y * total.y + total.z * total.z)/2;
	printf("area=%f\n", area);
````

+ 算法复杂度：一轮循环，每次都进行常数次乘法和加法运算，i=0,1,...,n-2。故时间复杂度为O(n)
  
+ 求多边形中距离最远点并连接显示的算法：

````cpp
double distance(Point3D a, Point3D b) {
	return sqrt((b.x - a.x) * (b.x - a.x) + (b.y - a.y) * (b.y - a.y) + (b.z - a.z) * (b.z - a.z));
}
for (i = 0; i < n-1; i++)
	{
		for (int j = i + 1; j < n; j++)
		{
			if (distance(P[i], P[j]) > maxDistance)
			{
				maxDistance = distance(P[i], P[j]);
				index1 = i; index2 = j;
			}
		}
	}
	printf("maxDistance=%f\n", maxDistance);
````    

````cpp
void DisplayPolygon3D(Polygon3D *plyg)
{
	if (plyg->num_pnt<=0)	return;

	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
	glColor3f(0.0, 0.0, 1.0);
	polygondisp(plyg->num_pnt, plyg->Point, plyg->closed);

	glColor3f(1.0, 0.0, 0.0);
	pointsdisp(plyg->num_pnt, plyg->Point);

	glColor3f(0.0, 0.0, 0.0);
	My_pointsdisp(1, plyg->Point + index1);
	My_pointsdisp(1, plyg->Point + index2);
	Pl[0] = *(plyg->Point + index1);
	Pl[1] = *(plyg->Point + index2);
	My_linedisp(2, Pl);
}
````
+ 算法复杂度：两轮循环，i=0,1,...,n-2,j=i+1,...,n-1。 故时间复杂度为(n-1)+(n-2)+...+1=O(n^2)
+ 求解结果
+ shoe.txt结果演示
    
    
![shoe.txt结果演示1](C:\Users\Dell\Desktop\DataStructure_2020\Project\shoe.png "shoe.png")

![shoe.txt结果演示2](C:\Users\Dell\Desktop\DataStructure_2020\Project\shoe1.png "shoe1.png" )
  
+ ellipse.txt结果演示

![ellipse.txt结果演示1](C:\Users\Dell\Desktop\DataStructure_2020\Project\ellipse.png "ellipse.png")

![ellipse.txt结果演示2](C:\Users\Dell\Desktop\DataStructure_2020\Project\ellipse1.png "ellipse1.png")