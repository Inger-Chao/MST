```c++

#include<stdio.h>
#include<stdlib.h>
#include<graphics.h>
#include<conio.h>
#define M 20 /*最大顶点数*/
#define FINITY 5000/*5000代表无穷大*/
typedef char CityName[20];
typedef int distance;/*此处权值类型为两城市间距离*/
typedef struct {
	CityName name[M];/*顶点信息域*/
	distance edges[M][M];/*邻接矩阵*/
	int n, e;/*图中顶点总数与边数*/
}Mgraph;
typedef struct edgedata {
	int beg, en;//beg,en是边顶点序号
	int length;//边长
}edge;
typedef int dist[M][M];
typedef int path[M][M];
/*********************************************/
/*函数功能：创建一个默认为‘graph.txt'的图文件*/
/*函数参数：无                               */
/*函数返回值：无                             */
/*********************************************/
void creatFile() {
	char ch;
	Mgraph *g;
	g = (Mgraph*)malloc(sizeof(Mgraph));
	FILE *fp;
	fp = fopen("graph.txt", "w");
	if (fp == NULL) {
		printf("\t\t打开文件失败！");
		exit(0);
	}
	else
	{
		int i, j, k, w;
		printf("\n\n\n\n\n");
		printf("\t\t**********************请输入图的顶点数和边数：**********************\n");
		printf("\t\t\t\t\t\t");
		scanf("%d%d", &g->n, &g->e);
		fprintf(fp, "%d %d\n", g->n, g->e);
		printf("\t\t*************************请输入%2d个城市名称：***********************\n", g->n);
		for (i = 0; i < g->n; i++)
		{
			printf("\t\t\t\t\t\t");
			scanf("%s", &(g->name[i]));
			fprintf(fp, "%s ", &(g->name[i]));
			//		printf("%s的序号为%d\n", &(g->name[i]), i);
		}
		fprintf(fp, "\n");
		printf("\t\t********************请输入两城市序号及其间的距离：******************\n");
		for (k = 0; k < g->e; k++) {  /*读入网络中的边*/
			printf("\t\t\t\t\t\t");
			scanf("%d%d%d", &i, &j, &w);
			fprintf(fp, "%d %d %d\n", i, j, w);
		}
		fclose(fp);
		printf("\t\t********************************************************************\n\n");
		printf("\t\t               默认名为'graph.txt'的图文件已创建成功!               \n");
		printf("\t\t                                                                    \n");
		printf("\t\t                      输入任意键返回主菜单                          \n\n");
		printf("\t\t********************************************************************\n");
	}
}

/*************************************/
/*函数功能：读取一个图文件并         */
/*        建立该图的邻接矩阵存储结构 */
/*函数参数：邻接矩阵的指针变量g;     */
/*          存放图信息的文件名s;     */
/*          图的类型参数c            */
/*函数返回值：无                     */
/*************************************/
void read(Mgraph *g, char *s, int c) {
	int i, j, k, w;
	FILE *fp;
	fp = fopen(s, "r");
	if (fp) {
		fscanf(fp, "%d%d", &g->n, &g->e);//读入途中的顶点值
		for (i = 0; i < g->n; i++)//初始化邻接矩阵
		{
			fscanf(fp, "%s", &(g->name[i]));
		}
		for (i = 0; i < g->n; i++)
			for (j = 0; j < g->n; j++)
				if (i == j)
					g->edges[i][j] = 0;
				else
					g->edges[i][j] = FINITY;
		for (k = 0; k < g->e; k++) {
			fscanf(fp, "%d%d%d", &i, &j, &w);
			g->edges[i][j] = w;
			if (c == 0)
				g->edges[j][i] = w;
		}
		fclose(fp);
	}
	else g->n = 0;
}
void display(Mgraph *g, char *s) {
	int i, j, w;
	printf("\t\t********************************************************************\n\n");

	printf("\t\t**                    该城市图的邻接矩阵为                        **\n\n");
	for (i = 0; i<g->n; i++){
		printf("\t\t\t");
		for (j = 0; j < g->n; j++) {
			printf("  %6d", g->edges[i][j]);
			}
		printf("\n");
		}
	printf("\n\t\t********************************************************************\n");
	printf("\t\t**                    输入任意键返回主菜单                        **\n");
	printf("\t\t********************************************************************\n\n");
}
/*************************************/
/*函数功能：输出城市间的最短距离     */
/*函数参数：邻接矩阵的指针变量g;     */
/*          存放图信息的文件名s;     */
/*          图的类型参数c            */
/*函数返回值：无                     */
/*************************************/
void floyd(Mgraph g, path p, dist d) {
	int i, j, k;
	for (i = 0; i<g.n; i++)  /*初始化d*/
		for (j = 0; j < g.n; j++) {
			d[i][j] = g.edges[i][j];
			if (i != j && d[i][j] < FINITY)
				p[i][j] = i;
			else
				p[i][j] = -1;
		}
	for (k = 0; k < g.n; k++) /*递推求解每一对顶点间的最短距离*/
	{
		for (i = 0; i<g.n; i++)
			for (j = 0; j < g.n; j++)
				if (d[i][j] >(d[i][k] + d[k][j]))
				{
					d[i][j] = d[i][k] + d[k][j];
					p[i][j] = k;
				}
	}
	printf("\t\t/******************************************************************/\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                     所有城市间的距离为                         */\n");
	printf("\t\t/*                                                                */\n");
	for (i = 0; i<g.n; i++)
		for (j = 0; j<g.n; j++)
			if (i != j)
				printf("\t\t/*                      %s--->%s    %6dkm                  */\n", &(g.name[i]), &(g.name[j]), d[i][j]);
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                    输入任意键返回主菜单                        */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/******************************************************************/\n");

}
/*************************************/
/*函数功能：对边向量进行快速排序     */
/*函数参数：边向量edges			     */
/*          边向量左右下标left,right */
/*函数返回值：无                     */
/*************************************/
void QuickSort(edge edges[], int left, int right) {
	edge x;
	int i, j, flag = 1;
	if (left < right) {
		i = left;
		j = right;
		x = edges[i];
		while (i < j) {
			while (i < j&&x.length < edges[j].length)
				j--;
			if (i < j)
				edges[i++] = edges[j];
			while (i<j&&x.length>edges[i].length)
				i++;
			if (i < j)
				edges[j--] = edges[i];
		}
		edges[i] = x;
		QuickSort(edges, left, i - 1);
		QuickSort(edges, i + 1, right);
	}
}
/*************************************/
/*函数功能：从图g的邻接矩阵读取图的  */
/*			所有边信息				 */
/*函数参数：邻接矩阵g;				 */
/*          边向量edges				 */
/*函数返回值：无                     */
/*************************************/
void GetEdge(Mgraph g, edge edges[]) {
	int i, j, k = 0;
	for (i = 0; i < g.n; i++)
		for (j = 0; j<i; j++)
			if (g.edges[i][j] != 0 && g.edges[i][j] < FINITY) {
				edges[k].beg = i;
				edges[k].en = j;
				edges[k++].length = g.edges[i][j];
			}
}
/*************************************/
/*函数功能：kruskal求解最小生成树    */
/*函数参数：邻接矩阵g;               */
/*函数返回值：无                     */
/*************************************/
void kruskal(Mgraph g) {
	int i, j, k = 0, ltfl;
	int sum = 0;
	int cnvx[M];//记录连通分量
	edge edges[M*M];//存放图的所有边
	edge tree[M];//存放最小生成树的边信息
	GetEdge(g, edges);//读取所有边
	QuickSort(edges, 0, g.e - 1);//对边进行升序排列
	for (i = 0; i < g.n; i++)
		cnvx[i] = i;//令每一个点的连通分量为其顶点编号
	for (i = 0; i < g.n - 1; i++) //树中共有g.n-1条边
	{
		while (cnvx[edges[k].beg] == cnvx[edges[k].en])
			k++;//找到属于两个连通分量权最小的边
		tree[i] = edges[k];//将边k加入到生成树中
		ltfl = cnvx[edges[k].en];//记录选中边的中点的连通分量编号
		for (j = 0; j < g.n; j++) //两个连通分量合并为一个连通分量
			if (cnvx[j] == ltfl)
				cnvx[j] = cnvx[edges[k].beg];
		k++;
	}
	printf("\t\t/******************************************************************/\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                      该城市图的最小生成树为                    */\n");
	printf("\t\t/*                                                                */\n");
	for (j = 0; j < g.n - 1; j++)
		printf("\t\t/*                      %s------%s  %6dkm                  */\n", &(g.name[tree[j].beg]), &(g.name[tree[j].en]), tree[j].length);
	for (j = 0; j<g.n - 1; j++) {
		sum = sum + tree[j].length;
	}
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                     最小生成树的代价为：%5d                  */\n", sum);
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                      输入任意键返回主菜单                      */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/******************************************************************/\n");
}
/***********************************************/
/*函数功能：调用图形库画出一个本次演示的城市图 */
/*函数参数：void							   */
/*函数返回值：无						       */
/***********************************************/
void graph() {
	initgraph(823, 489);//定义画布
	void setbkcolor(COLORREF white);
	circle(115, 110, 23);
	outtextxy(100, 100, L"西宁");//画出西宁的顶点
	circle(125, 310, 23);
	outtextxy(110, 300, L"成都");//画出成都的顶点
	circle(305, 210, 23);
	outtextxy(290, 200, L"西安");//画出西安的顶点
	circle(495, 130, 23);
	outtextxy(480, 120, L"太原");//画出太原的顶点
	circle(515, 330, 23);
	outtextxy(500, 320, L"武汉");//画出武汉的顶点
	circle(735, 80, 25);
	outtextxy(720, 70, L"北京");//画出北京的顶点
	outtextxy(285, 100, L"1315km");
	line(138, 110, 473, 125);//西宁和太原的连线
	outtextxy(125, 200, L"1194km");
	line(117, 133, 123, 290);//西宁和成都的连线
	outtextxy(220, 155, L"863km");
	line(128, 127, 287, 197);//西宁和西安的连线
	outtextxy(215, 255, L"712.8km");
	line(143, 297, 283, 213);//成都到西安的连线
	outtextxy(295, 320, L"1146km");
	line(147, 313, 493, 327);//成都到武汉的连线
	outtextxy(365, 180, L"611km");
	line(323, 197, 473, 133);//西安到太原的连线
	outtextxy(375, 260, L"841km");
	line(327, 213, 497, 317);//西安到武汉的连线
	outtextxy(507, 210, L"937km");
	line(495, 153, 513, 307);//太原到武汉的连线
	outtextxy(595, 105, L"508km");
	line(517, 123, 710, 77);//太原到北京的连线
	outtextxy(630, 205, L"1180km");
	line(537, 327, 717, 97);//武汉到北京的连线
}
/*************************************/
/*函数功能：欢迎界面                 */
/*函数参数：void                     */
/*函数返回值：无                     */
/*************************************/
void welcome()
{
	printf("\n\n\n\n\n\n");
	printf("\t\t/******************************************************************/\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                  欢迎进入城市最小生成树系统                    */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                     输入任意键进入主菜单                       */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/******************************************************************/\n");
	while (getchar() == 0);
	system("CLS");
}
/*************************************/
/*函数功能：结束界面                 */
/*函数参数：void                     */
/*函数返回值：无                     */
/*************************************/
void goodbye()
{
	printf("\n\n\n\n\n\n");
	printf("\t\t/******************************************************************/\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                           感谢使用                             */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                            再见！                              */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/******************************************************************/\n");
	exit(0);
}
/*************************************/
/*函数功能：主菜单选择界面           */
/*函数参数：图的邻接矩阵g            */
/*函数返回值：无                     */
/*************************************/
void choose(Mgraph g) {
	int flag = 0;
	int choice;
	char filename[10];
	path p;
	dist d;
	system("CLS");
	printf("\n\n\n\n\n\n");
	printf("\t\t/******************************************************************/\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                   1.创建一个城市图文件                         */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                2.查看本次演示的城市图信息                      */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*         3.读取一个城市图文件并输出该城市图的邻接矩阵           */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*          4.读取一个城市图文件并输出城市间的最短距离            */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*             5.输出某城市图的最小生成树及其代价                 */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                      0.退出系统                                */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/*                  请输入选项[0/1/2/3/4]                         */\n");
	printf("\t\t/*                                                                */\n");
	printf("\t\t/******************************************************************/\n");
	scanf("%d", &choice);
	while (flag == 0) {
		if ((choice == 1) || (choice == 2) || (choice == 3) || (choice == 4) || (choice == 5)||(choice == 0))
		{
			flag = 1;
			system("CLS");
			switch (choice) {
			case 1:
				creatFile();
				Mgraph a;
				getchar();
				while (getchar() == 0);
				system("CLS");
				choose(a);
			case 2:
				graph();
				_getch();
				closegraph();
				system("CLS");
				choose(a);
			case 3:
				printf("\t\t********************************************************************\n");
				printf("\t\t\t\t\t请输入一个城市图的文件名：\n");
				printf("\t\t\t\t\t\t");
				scanf("%s", filename);
				read(&g, filename, 0);
				display(&g,filename);
				getchar();
				while (getchar() == 0);
				system("CLS");
				choose(a);
			case 4:
				printf("\t\t********************************************************************\n");
				printf("\t\t\t\t\t请输入一个城市图的文件名：\n");
				printf("\t\t\t\t\t\t");
				scanf("%s", filename);
				read(&g, filename, 0);
				floyd(g, p, d);
				getchar();
				while (getchar() == 0);
				system("CLS");
				choose(a);
			case 5:
				printf("\t\t********************************************************************\n");
				printf("\t\t\t\t\t请输入一个城市图的文件名：\n");
				printf("\t\t\t\t\t\t");
				scanf("%s", filename);
				read(&g, filename, 0);
				kruskal(g);
				getchar();
				while (getchar() == 0);
				system("CLS");
				choose(a);
			case 0:
				goodbye();
			}

		}
	}
}
/*************************************/
/*函数功能：主函数                   */
/*函数参数：void                     */
/*函数返回值：无                     */
/*************************************/
int main() {
	Mgraph g;
	welcome();
	while (1) {
		choose(g);
	}
	return 0;
}

```
