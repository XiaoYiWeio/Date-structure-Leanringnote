#### 第二章 暴力求解

##### 2.3其他模拟

例题：

```c++
例题2.9
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<cmath>
#include<iomanip>
using namespace std;
/*
利用vector<int>A,0表示有树，1表示无树。
*/



int main()
{
	int L, M;
	cin >> L >> M;
	vector<int>A(L+1);			//进入L+1个‘0’
	while (M != 0)
	{
		int a, b;
		cin >> a >> b;
		for (int i = a; i <= b; i++)
			A[i] = 1;
		M--;
	}
	int num = 0,i=0;
	while (i != A.size())		//判定了A[0]~A[size-1]	
	{
		if (A[i] == 0)
			num++;
		i++;
	}
	cout << num << endl;
	return 0;
}


例题2.10
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<cmath>
#include<iomanip>
using namespace std;
/*
判断两个字母是否属于同一个键位，str[i]-str[i-1]=keytab[str[i]-'a']-keytab[str[i-1]-'a'];
*/

int keytab[26] = {
	1,2,3,
	1,2,3,
	1,2,3,
	1,2,3,
	1,2,3,
	1,2,3,4,
	1,2,3,
	1,2,3,4
};


int main()
{
	string str;
	while (cin >> str)
	{
		int time = keytab[str[0]-'a'];
		for (int i = 1; i < int(str.length()); i++)
		{
			if (str[i] - str[i - 1] == keytab[str[i] - 'a'] - keytab[str[i - 1] - 'a'])
				time += 2;
			time += keytab[str[i] - 'a'];
		}
		cout << time<< endl;
	}
	return 0;
}

例题2.11
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<cmath>
#include<iomanip>
using namespace std;
/*

*/

int fun(int n)
{
	int count = 0;
	while (n != 1)
	{
		if (n % 2 == 0)
			n = n / 2;
		else
			n = (3 * n + 1) / 2;
		count++;
	}
	return count;
}

int main()
{
	int n;
	while (cin >> n)
	{
		if (n == 0)
			return 0;
		cout << fun(n) << endl;
	}
	return 0;
}
```

无答案题

```c++
Grading：
    
    
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<cmath>
#include<iomanip>
using namespace std;
/*
 
*/
 
 
 
int main()
{
    float p,t,g1,g2,g3,gj;
    while (cin >> p>>t>>g1>>g2>>g3>>gj)
    {
        if (abs(g1 - g2) <= t)
            cout << fixed << setprecision(1) << (g1 + g2) / 2 << endl;
        else if (abs(g1 - g3) <= t && abs(g2 - g3) <= t)
        {
            cout << fixed << setprecision(1) << max(max(g1, g2), g3) << endl;
        }
        else if (abs(g1 - g3) > t && abs(g2 - g3) > t)
            cout << fixed << setprecision(1) << gj << endl;
        else
        {
            float temp1 = abs(g1 - g3), temp2 = abs(g2 - g3);
            if (temp1 > temp2)
                cout << fixed << setprecision(1) << (g2 + g3) / 2 << endl;
            else
                cout << fixed << setprecision(1) << (g1 + g3) / 2 << endl;
        }
 
    }
    return 0;
}


路径打印：
    #include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<cmath>
#include<iomanip>
using namespace std;
 
//使用递归，递归参数记录的是级别数和当前所剩字符串内容
// 先排序，保证有序 然后考虑当i-1 和 i 的根目录一致的时候输出的问题
// 当i-1 和 i前面保持一致时，num记录current下标，k计算输出几个\t
 
 
void fun(string str, int n,int cur)
{
    if (cur >int( str.length() - 1))
        return;
    for (int i = 0; i < n; i++)
        cout << "  " ;
    while (str[cur]!='\\'&&cur<int(str.length()))
    {
        cout << str[cur++];
    }
    cout << endl;
    fun(str, n + 1, cur+1);
}
 
int main()
{
    int n;
     
    while (cin >>n)
    {
        if (n == 0)
            return 0;
        vector<string> str(n);
        for (int i = 0; i < n; i++)
            cin >> str[i];
        sort(str.begin(), str.end());
        for (int i = 0; i < n; i++)
        {
            int num = 0, index = 0, k = 0;
            if (i > 0)
            {
                while (str[i][num] == str[i - 1][num])
                {
                    num++;
                    while ((index = int(str[i].find('\\', index))) < num)
                    {
                        k++;
                        index++;
                    }
                }
            }
            fun(str[i], k, num);
        }
        cout << endl;
    }
    return 0;
}

坠落的蚂蚁：
    
法一：
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<cmath>
#include<iomanip>
using namespace std;

/*
要点是除了A之外的蚂蚁碰撞无所谓，只考虑有A参与的碰撞即可，注意考虑特殊点如dis=1
相向而行时是在x=0.5处相遇
*/




int main()
{
	int n;
	cin >> n;
	vector<int> t(4);		// 0 起始位置，1速度，2是否掉落(1表示已落)  3表示有多少个蚂蚁和自己在此刻碰头
	vector<vector<int>>ant;
	ant.resize(n, t);
	int a;
	for (int i = 0; i < n; i++)
	{
		cin >> ant[i][0] >> ant[i][1];
		if (ant[i][1] == 0)
			a = i;				//记录A蚂蚁
	}
	int time = 0;
	while (ant[a][2] != 1)
	{

		// 判断是否仅剩A且V_a=0
		if (ant[a][1] == 0)
		{
			int num = 0;
			for (int i = 0; i < n; i++)
			{
				if (ant[i][2] == 0)
					num++;
			}
			if (num == 1)			//仅有A蚂蚁 且 A蚂蚁静止  则不会掉落
			{
				cout << "Cannot fall!" << endl;
				return 0;
			}
		}


		// 判断是否有蚂蚁与A相碰
		vector<int>crash;
		for (int i = 0; i < n; i++)
		{
			if (i != a && ant[i][2] == 0 && ant[i][0] == ant[a][0])
				crash.push_back(i);
		}
		if (crash.size() == 1)
		{
			swap(ant[a][1], ant[crash[0]][1]);
		}
		else if (crash.size() == 2)
		{
			ant[a][1] *= -1;
			ant[crash[0]][1] *= -1;
			ant[crash[1]][1] *= -1;
		}


		//判断特殊情况（非整数点相遇）
		int pos=-1;
		for (int i = 0; i < n; i++)
		{
			if (i != a && ant[i][2] == 0 && ant[i][0] - ant[a][0] == 1)
			{
				if (ant[a][1] == 1 && ant[i][1] == -1)		//相向而行
				{
					pos = i;
				}
			}
			else if (i != a && ant[i][2] == 0 && ant[i][0] - ant[a][0] == -1)
			{
				if (ant[a][1] == -1 && ant[i][1] == 1)		//相向而行
				{
					pos = i;
				}
			}
		}

		if (pos == -1)
		{
			for (int i = 0; i < n; i++)				//move
			{
				if (ant[i][2] == 0)
				{
					ant[i][0] += ant[i][1];
					if (ant[i][0] == 0 || ant[i][0] == 100)
						ant[i][2] = 1;
				}
			}
		}
		else
		{
			swap(ant[a][1], ant[pos][1]);    //交换速度
			for (int m = 0; m < n; m++)
			{
				if (m != pos && m != a && ant[m][2] == 0)
				{
					ant[m][0] += ant[m][1];
					if (ant[m][0] == 0 || ant[m][0] == 100)
						ant[m][2] = 1;
				}
			}
		}
		time++;
			

		// 三只蚂蚁碰头只会在 -1 +1 0相遇时才会出现，只需要让+1 与-1交换速度即可。两只蚂蚁碰头时也是交换速度
		// 判断每只蚂蚁有多少只和其相遇
		//找出坐标最大那个 速度设为0， 另外两只不管
		//从头到尾只考虑A蚂蚁
	}
	cout << time << endl;
	return 0;
}

法二：


#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<cmath>
#include<iomanip>
using namespace std;

/*
当初试条件确定时，若N只向左运动，M只向右运动，那么每时每刻，均有n只蚂蚁在向左运动，同理有M只向右运动，
因此只看运动的方向，那么整列蚂蚁有三类，1列向左运动的且相对位置不变的蚂蚁和一列向右运动的相对位置不变的蚂蚁
以及一个速度为0的蚂蚁。
若有n只向左运动的，那么就说明初始状态下的前n只  必定从左侧掉下去，相应的 向右运动也如是
*/




int main()
{
	int n;
	cin >> n;
	vector<vector<int>>ant;
	ant.resize(n, vector<int>(2));
	int A;
	vector<int>left;
	vector<int>right;
	for (int i = 0; i < n; i++)
	{
		cin >> ant[i][0] >> ant[i][1];
	}
	sort(ant.begin(), ant.end());			//排序
	for (int i = 0; i < n; i++)
	{
		if (ant[i][1] == 0)
			A = i;
		else if (ant[i][1] == -1)
			left.push_back(i);				// 不设置size 不可以push_back
		else
			right.push_back(i);
	}

	if (A == left.size())
	{
		cout << "Cannot fall!";
		return 0;
	}
	else if (A < left.size())
	{
		cout << ant[left[A]][0];
		return 0;
	}
	else
	{
		// 从右边是第几个掉下去的：第n-A-1个
		cout <<100- ant[right[right.size()-1-(n-A-1)]][0];
		return 0;
	}
	return 0;
}




```

