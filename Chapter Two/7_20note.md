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

```

