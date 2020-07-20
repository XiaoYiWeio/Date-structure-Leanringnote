#### 第二章 暴力求解

##### 2.2日期问题

例题：

```c++
例题2.6 P16

#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<iomanip>
using namespace std;
/*

*/

int fun(int y, int m, int d)
{
	int a[12] = { 31,28,31,30,31,30,31,31,30,31,30,31 };
	int num = 0;
	for (int i = 0; i < m - 1; i++)
		num += a[i];
	num += d;
	if (((y % 4 == 0 && y % 100 != 0) || y % 400 == 0)&&m>2)
		num++;
	return num;
}

int main()
{

	int y, m, d;
	while (cin >> y >> m >> d)
	{
		cout<<fun(y, m, d)<<endl;
	}
	return 0;
}


例题2.7
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<iomanip>
using namespace std;
/*

*/


void date(int y, int n)
{
	int m=n/31, d,num=0;
	int a[12] = { 31,28,31,30,31,30,31,31,30,31,30,31 };	
	if (((y % 4 == 0 && y % 100 != 0) || y % 400 == 0))
		a[1]++;
	for (int i = 0; i < m; i++)
	{
		num += a[i];
	}
	d = n - num;
	while (d >= a[m])
	{
		d -= a[m];
		m++;	
	}
	if (d == 0)
	{
		m--;
		d = a[m];
	}
	cout << y << " ";
	cout << setw(2) << setfill('0') << m + 1 << " ";
	cout<<setw(2)<<setfill('0')<< d << endl;
}

int main()
{

	int y, n;
	while (cin >> y >> n)
	{
		date(y, n);
		cout << endl;
	}
	return 0;
}



例题2.8

#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<iomanip>
using namespace std;
/*
重点在于利用2.7于2.6，同时考虑到当增加超过365/366时需要Y++,temp-=yearsday;
*/

int date_to_num(int y, int m, int d)
{
	int a[12] = { 31,28,31,30,31,30,31,31,30,31,30,31 };
	int num = 0;
	for (int i = 0; i < m - 1; i++)
		num += a[i];
	num += d;
	if (((y % 4 == 0 && y % 100 != 0) || y % 400 == 0) && m > 2)
		num++;
	return num;
}

void num_to_date(int y, int n)
{
	int m = n / 31, d, num = 0;
	int a[12] = { 31,28,31,30,31,30,31,31,30,31,30,31 };
	if (((y % 4 == 0 && y % 100 != 0) || y % 400 == 0))
		a[1]++;
	for (int i = 0; i < m; i++)
	{
		num += a[i];
	}
	d = n - num;
	while (d >= a[m])
	{
		d -= a[m];
		m++;
	}
	if (d == 0)
	{
		m--;
		d = a[m];
	}
	cout << y << " ";
	cout << setw(2) << setfill('0') << m + 1 << " ";
	cout << setw(2) << setfill('0') << d << endl;
}

int totalday(int y)
{
	return ((y % 4 == 0 && y % 100 != 0) || y % 400 == 0)?366:365;
}

int main()
{

	int y, m, d,add,temp;
	while (cin >> y >> m >> d>>add)
	{
		temp=date_to_num(y, m, d);
		temp += add;
		int year_days = totalday(y);
		if (temp > year_days)
		{
			y++;
			temp -= year_days;
		}
		num_to_date(y, temp);
	}
	return 0;
}
```



无答案题

```c++
2.6
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<cmath>
#include<iomanip>
using namespace std;
/*
计算距离0年0月0日的总天数，再相减.输出绝对值
*/
int totalday(int y)
{
    return ((y % 4 == 0 && y % 100 != 0) || y % 400 == 0) ? 366 : 365;
}
 
int date_to_num(int y, int m, int d)
{
    int a[12] = { 31,28,31,30,31,30,31,31,30,31,30,31 };
    int num = 0;
    for (int i = 0; i < m - 1; i++)
        num += a[i];
    num += d;
    if (((y % 4 == 0 && y % 100 != 0) || y % 400 == 0) && m > 2)
        num++;
    for (int i = 1; i <= y-1; i++)
    {
        num += totalday(i);
    }
    return num;
}
 
 
 
 
int main()
{
    int s1, s2;
    while (cin >> s1 >> s2)
    {
        int y1 = s1 / 10000, y2 = s2 / 10000;
        int m1 = (s1 / 100) % 100, m2 = (s2 / 100) % 100;
        int d1 = s1 % 100, d2 = s2 % 100;
        cout<<1+abs(date_to_num(y1, m1, d1) - date_to_num(y2, m2, d2))<<endl;
    }
    return 0;
}    
2.7
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<cmath>
#include<iomanip>
using namespace std;
/*
计算距离1年1月1日的总天数，mod 7 即可；mod 7 =0 则为星期一
*/
int totalday(int y)
{
    return ((y % 4 == 0 && y % 100 != 0) || y % 400 == 0) ? 366 : 365;
}
 
int date_to_num(int y, int m, int d)
{
    int a[12] = { 31,28,31,30,31,30,31,31,30,31,30,31 };
    int num = 0;
    for (int i = 0; i < m - 1; i++)
        num += a[i];
    num += d;
    if (((y % 4 == 0 && y % 100 != 0) || y % 400 == 0) && m > 2)
        num++;
    for (int i = 1; i <= y-1; i++)
    {
        num += totalday(i);
    }
    return num;
}
 
 
 
 
int main()
{
    int d,mon,y;
    string m;
    string month[12] = { "January","February","March","April","May","June","July","August","September","October","November","December" };
    string weekday[7] = { "Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday" };
    while (cin >> d >> m>>y)
    {
        for (int i = 0; i < 12; i++)
            if (m == month[i])
            {
                mon = i+1;
                break;
            }
        int temp = date_to_num(y, mon, d) - date_to_num(1, 1, 1);
        temp %= 7;
        cout << weekday[temp]<<endl;
    }
    return 0;
}   
2.8
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
#include<cmath>
#include<iomanip>
using namespace std;
/*
计算距离0年0月0日的总天数，再相减.输出绝对值
*/
int totalday(int y)
{
    return ((y % 4 == 0 && y % 100 != 0) || y % 400 == 0) ? 366 : 365;
}
 
int date_to_num(int y, int m, int d)
{
    int a[12] = { 31,28,31,30,31,30,31,31,30,31,30,31 };
    int num = 0;
    for (int i = 0; i < m - 1; i++)
        num += a[i];
    num += d;
    if (((y % 4 == 0 && y % 100 != 0) || y % 400 == 0) && m > 2)
        num++;
    for (int i = 1; i <= y-1; i++)
    {
        num += totalday(i);
    }
    return num;
}
 
 
 
 
int main()
{
    int s1, s2;
    while (cin >> s1 >> s2)
    {
        int y1 = s1 / 10000, y2 = s2 / 10000;
        int m1 = (s1 / 100) % 100, m2 = (s2 / 100) % 100;
        int d1 = s1 % 100, d2 = s2 % 100;
        cout<<1+abs(date_to_num(y1, m1, d1) - date_to_num(y2, m2, d2))<<endl;
    }
    return 0;
}

    
```

