#### 第三章 排序与查找

##### 3.1 排序

例题：

```c++
例题3.1
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

/*

*/


bool cmp(int a, int b)
{
	return a > b;
}

int main()
{
	int n;
	cin >> n;
	vector<int>A;
	for (int i = 0; i < n; i++)
	{
		int temp;
		cin >> temp;
		A.push_back(temp);
	}
	sort(A.begin(), A.end(),cmp);
	for (int i = 0; i < n; i++)
		cout << A[i] << " ";
	return 0;
}

例题3.2
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

/*
黄金法则，cmp函数编写时，返回值为true的时候，比较符号前的数就会排在比较符号后的数的后面
即：return a***b  ，那么这个 表达式为true时就代表a被执行了
*/

const int MAX_NUM = 100;
struct Stu
{
	int score;
	int sno;
}stu[MAX_NUM];

bool cmp(Stu a, Stu b)
{
	if (a.score == b.score)
		return a.sno < b.sno;
	else
		return a.score < b.score;
}

int main()
{
	int n;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> stu[i].sno >> stu[i].score;
	}
	sort(stu,stu+n,cmp);
	for (int i = 0; i < n; i++)
		cout << stu[i].sno << " " << stu[i].score << endl;
	return 0;
}
例题3.3
#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
using namespace std;
 
/*
 
*/
 
const int MAX_NUM = 1000;
struct Stu
{
    int no;
    int score;
    string sname;
 
};
 
bool cmp1(Stu a, Stu b)         //升序
{
    if (a.score == b.score)
        return a.no < b.no;
    else
        return a.score < b.score;
}
     
bool cmp2(Stu a, Stu b)         //降序
{
    if (a.score == b.score)
        return a.no < b.no;
    else
        return a.score > b.score;
}
 
int main()
{
    int n,flag;
    Stu stu[MAX_NUM];
    while (cin >> n >> flag)
    {
        for (int i = 0; i < n; i++)
        {
            stu[i].no = i;
            cin >> stu[i].sname >> stu[i].score;
        }
        if (flag == 1)
            sort(stu, stu + n, cmp1);
        else
            sort(stu, stu + n, cmp2);
 
        for (int i = 0; i < n; i++)
            cout << stu[i].sname << " " << stu[i].score << endl;
    }
    return 0;
}
```

无答案题

```c++
习题3.1
#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
using namespace std;

/*
直接sort就行了
*/


int main()
{
	int n;
	while (cin >> n)
	{
		vector<int> A;
		for (int i = 0; i < n; i++)
		{
			int temp;
			cin >> temp;
			A.push_back(temp);
		}
		sort(A.begin(), A.end());
		cout << A[n - 1] << endl;
		if (n == 1 || A[0] == A[n - 1])
		{
			cout <<-1;
		}
		else
		{
			for (int i = 0; i < n-1; i++)
				cout << A[i] << " ";
		}
		cout << endl;
	}

	return 0;
}
习题3.2
#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
using namespace std;

/*
输入的时候就对奇偶分开存储，然后分别排序
*/

bool cmp(int a,int b)		//降序排列
{
	return a > b;
}

int main()
{
	int n;
	while (cin >> n)
	{
		vector<int> A,B;
		if (n % 2 == 1)
			A.push_back(n);
		else
			B.push_back(n);

		for (int i = 0; i < 9; i++)
		{
			int temp;
			cin >> temp;
			if (temp % 2 == 1)
				A.push_back(temp);
			else
				B.push_back(temp);
		}
		
		sort(A.begin(), A.end(),cmp);
		sort(B.begin(), B.end());

		for (int i = 0; i<int(A.size()); i++)
			cout << A[i] << " ";
		for (int i = 0; i<int(B.size()); i++)
			cout << B[i] << " ";
		cout << endl;
	}

	return 0;
}
习题3.3
#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
using namespace std;

/*
输入的时候就对奇偶分开存储，然后分别排序
*/

const int MAX_NUM = 100;
struct rat
{
	int weight;
	string color;
}R[MAX_NUM];

bool cmp(rat a,rat b)		//降序排列
{
	return a.weight > b.weight;
}

int main()
{
	int n;
	while (cin >> n)
	{
		vector<rat> A;
		for (int i = 0; i <n; i++)
		{
			rat temp;
			cin >> temp.weight>>temp.color;
			A.push_back(temp);
		}	
		sort(A.begin(), A.end(),cmp);

		for (int i = 0; i<int(A.size()); i++)
			cout << A[i].color <<endl;
	}

	return 0;
}   

习题3.4：

#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
#include<limits.h>
using namespace std;

/*
对国家建立结构体,输入完毕后按照不同的方式排序，排序后更新rank 值，最后输出
*/

const int MAX_NUM = 100;

struct country
{
	int cno;
	int pop;
	double ans[4];			// golden,medal, golden/pop,medal/pop
	int rank=INT_MAX;		// 使用时需要加头文件：#include<limits.h>
	int rank_way=INT_MAX;
};

int k;
bool cmp1(country a, country b)		//金牌总数 < 奖牌总数 < 金牌人口比例 < 奖牌人口比例 
{
	return a.ans[k] > b.ans[k];
}
int main()
{
	int n,m;
	while (cin >> n>>m)
	{
		vector<country>C;
		vector<int>M;
		for (int i = 0; i < n; i++)
		{
			country temp;
			cin >> temp.ans[0] >> temp.ans[1] >> temp.pop;
			temp.cno = i;
			temp.ans[2] = (double)temp.ans[0] / temp.pop;
			temp.ans[3] = (double)temp.ans[1] / temp.pop;
			C.push_back(temp);
		}				
		
		for (int i = 0; i < m; i++)
		{
			int temp;
			cin >> temp;
			M.push_back(temp);
		}
		//输入完毕，开始排序
		
		// 四种方式排序
		for (int i = 0; i < 4; i++)
		{
			k = i;										//表示排序方式
			sort(C.begin(), C.end(), cmp1);				//排序完毕
			for (int j = 0; j < n; j++)					//对每个国家的rank更新 
			{
				if (j >= 1&&C[j].ans[k] == C[j - 1].ans[k] )
				{
					int x = j - 1;
					while (x>=0&&C[j].ans[k] == C[x].ans[k])
						x--;									// 当发现ans值相同时要一直往前回溯，找到最初的下标 才是真正的排名
					x++;
					if (C[j].rank > x)
					{
						C[j].rank = x;
						C[j].rank_way = k;
					}
				}
				else if (C[j].rank > j)
				{
					C[j].rank = j;
					C[j].rank_way = k;
				}
			}
		}
		// 输出结果


		for (int i = 0; i < m; i++)
		{
			for (int j = 0; j < n; j++)
			{
				if (C[j].cno == M[i])
				{
					cout << C[j].rank+1 << ":" << C[j].rank_way+1 << endl;
					break;
				}
			}
		}
	}

	return 0;
}
```

