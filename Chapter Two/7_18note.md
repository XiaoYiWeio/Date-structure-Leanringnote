#### 第二章 暴力求解

##### 2.2模拟

例题：

```c++
2.4，P10
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<iomanip>
using namespace std;
/*
ladder_shaped_diagram 梯形图
需要注意的是：头文件添加：#include<iomanip>，同时string 在初始化时可以直接赋值
右对齐为setiosflags(ios::right), 使用时通常要跟setw(),且填充字符用setfill()
*/


int ladder_shaped(int k)
{
	for (int i = 0; i < k; i++)
	{
		string s(k + 2 * i, '*');			//string 在初始化的时候：string str(length,'a') 填充length长的a
		cout << setiosflags(ios::right) << setw(k + 2 * (k - 1))<<setfill('&')<<s<<endl;
	}
	return 0;
}
int main()
{
	int h = 4;
	ladder_shaped(h);
	int k = h;
	return 0;
}

例题2.5 
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<iomanip>
using namespace std;
/*
首先确定有多少层筐，再确定每层筐的左上角与右下角的坐标，然后为对应的坐标赋值,层数默认最外层为0层，最内层为（n+1）/2 -1 层
左上角坐标确定为G[i][i] 右下角为[n-1-i][n-1-i]
每层的填充图案按照layer的奇偶确定，偶数为外筐花色，奇数为中心花色
*/


void display(char G[80][80],int n)
{
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
			cout << G[i][j];
		cout << endl<<endl;
	}
		
}

int main()
{
	int n;
	char c1, c2;								// c1:center ,c2:outer
	char G[80][80] = { 0 };
	while (cin >> n>>c1>>c2)
	{

		int layer = (n + 1) / 2;
		for (int i = 0; i < layer; i++)			//which layer
		{
			char ch = i % 2 == 0 ? c1 : c2;		//certain the char(color) 
			G[i][i] = ch;
			G[n - 1 - i][n - 1 - i] = ch;		// top left corner and bottom right corner
			int length = n - 2 * i;				// How many char on each layer
			for (int j = 1; j < length; j++)
			{
				G[i][i + j] = ch;
				G[i + j][i] = ch;
				G[n - 1 - i][n - 1 - i - j] = ch;
				G[n - 1 - i - j][n - 1 - i] = ch;
			}
		}
		// 去除四角：Remove four corners
		G[0][0] = ' ';
		G[0][n - 1] = ' ';
		G[n - 1][0] = ' ';
		G[n - 1][n-1] = ' ';
		display(G, n);
	}


	return 0;
}


```



无答案题

```c++
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<iomanip>
using namespace std;
/*
画布最大就是3000*3000；主要难点在于递归

要点1：getline函数；在读取完第一个int后要用getchar()将回车吃掉，不然影响getline读取。使用getline(cin,string) 不用cin.getline(temp,int)
		是为了避免cin后int值设置不足；
要点2：DFS
要点3：由于是对于的多组数据循环输出直到EOF，所以要保证在下组数据到来之前，所有数据被清空。例如G[][]
*/

char ori[6][6];
char G[3000][3000];

void recursion(int k, int x, int y, int n)
{
	if (k == 1)
	{
		for (int i = 0; i < n; i++)
			for (int j = 0; j < n; j++)
				G[i + x][j + y] = ori[i][j];
	}
	else
	{
		int sub_size = int(pow(n, k - 1));		//子图的size
		for (int i = 0; i < n; i++)
		{
			for (int j = 0; j < n; j++)
			{
				if (ori[i][j] == ' ')
					continue;
				recursion(k - 1, x + sub_size * i, y + sub_size * j, n);
			}
		}
	}
}

void clear(int n,int k)
{
	int num = int(pow(n, k));
	for (int i = 0; i < num; i++)
	{
		for (int j = 0; j < num; j++)
			G[i][j] = ' ';
	}
}

void display(int n, int k)
{
	int num = int(pow(n, k));
	for (int i = 0; i < num; i++)
	{
		for (int j = 0; j < num; j++)
			cout << G[i][j];
		cout << endl;
	}
}

int main()
{
	int n, k;
	while (cin >> n)
	{

		if (n == 0)
			return 0;
		string temp;
		getchar();
		for (int i = 0; i < n; i++)
		{
			getline(cin, temp);
			for (int j = 0; j < n; j++)
				ori[i][j] = temp[j];
		}
		cin >> k;
		clear(n, k);			//对G[][]进行打扫
		recursion(k, 0, 0, n);
		display(n, k);
	}
	return 0;
}
2.5 Hello World for U
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<iomanip>
using namespace std;
/*
可以首先确定n1,n3的值，只有（N+2）%3==0时，才可能n1=n2=n3，不然n1和n3都要小于n2
n1=n3,整个图像表示时，其实就是一个n1*n2的矩阵；
*/

void display(vector < vector<char>>g,int n1,int n2)
{
	for (int i = 0; i < n1; i++)
	{
		for (int j = 0; j < n2; j++)
			cout << g[i][j];
		cout << endl;
	}
}

int main()
{
	string str;
	while (cin >> str)
	{
		int n1, n2, n3,L;
		L = int(str.length());
		n1 = n3 = (L+2) / 3;
		n2 = (L + 2) - n1 - n3;
		vector <vector<char>>g;
		vector<char>temp(n2, ' ');
		for (int i = 0; i < n1; i++)
			g.push_back(temp);
		// 矩阵创建完毕：(n1,n2),下赋值
	
		// 按左中右顺序赋值
		int k = 0;
		for (int j = 0; j < n1; j++)
			g[j][0] = str[k++];
		for (int j = 0; j < n2 - 2; j++)
			g[n1 - 1][j + 1] = str[k++];
		for (int j = n3 - 1; j >= 0; j--)
			g[j][n2 - 1] = str[k++];
		display(g,n1,n2);
	}
	return 0;
}
```

