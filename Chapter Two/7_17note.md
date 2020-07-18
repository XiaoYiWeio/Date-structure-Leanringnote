#### 第二章 暴力求解

例题：

```c++
//P7 反序数,注意一下对于n求反序数，循环中有三步：×10，取模相加，÷10
#include<iostream>
using namespace std;

//求反序数
int reverse(int n)
{
	int k=0;
	while (n != 0)
	{
		k *= 10;
		k += n%10;
		n /= 10;
	}
	return k;
}

int main()
{
	int  n = 1000;
	cout << "开始计算.....";
	while (n <= 9999)
	{
		if (9 * n == reverse(n))
			cout << n << endl;
		n++;
	}
	return 0;
}


#include<iostream>
#include<string>
using namespace std;

P8  例题2.3 对称平方数1
/*
C++ 11 后使用 to_string(int/double/float) 完成从数字到string的转换
int stoi (const string&  str, size_t* idx = 0, int base = 10);
stoi () 将字符串转换为整数，idx 如果不为零，则将idx设为str数字后第一个字符的位置

缺省使用时：
int i_dec = std::stoi(str); 10进制
int i_hex = std::stoi(str,16);	16进制
int i_bin = std::stoi(str,2); 2进制
int i_auto = std::stoi(str,0); //看默认是如何表示通通转为10进制，例如原本是0x7f,就转10进制
size_t是为了可移植性，通常将一些无符号的整形定义为size_t,比如说为了解决unsigned int 在不同平台上的占用空间不同，表示的位数不同的问题。

*/
bool symmetry(int n){
	int m = n * n;
	string s;
	s += to_string(m);
	for (int i = 0; i < int(s.length() / 2); i++)
	{
		if (s[i] != s[s.length() - i - 1])
			return false;
	}
	return true;
}

int main()
{
	
	for (int i = 0; i <= 256; i++)
	{
		if (symmetry(i))
			cout << i << endl;
	}
	return 0;
}




```



无答案题

```c++
习题 2.1 P10
#include<iostream>
#include<string>
using namespace std;


/*

*/
bool relation(int n)
{
	string s = to_string(n);
	for (int i = 0; i < int(s.length()); i++)
	{
		if (s[i] == '7')
			return true;
	}

	if (n % 7 == 0)
		return true;
	return false;
}
int main()
{
	int n, num = 0;
	cin >> n;
	for (int i = 0; i <= n; i++)
	{
		if (!relation(i))
			num += i * i;
	}
	cout << num;
	return 0;
}


习题2.2 
#include<iostream>
#include<string>
using namespace std;
/*
可以先规定个遍历的大概,x<=n/5,y<=n/3 这种
*/
 
int equation(int n)
{
    int x, y;
    double z;
    for (x = 0; x <= n / 5; x++)
        for(y=0;y<=n/3;y++)
            for (z = 0; z <= n * 3; z++)
            {
                 
                if (x + y + z == 100 && 5 * x + 3 * y + z / 3 <= n)
                    cout << "x=" << x << ",y=" << y << ",z=" << z<<endl;
            }
    return 0;
}
int main()
{
    int n;
    cin >> n;
    equation(n);
    return 0;
}

习题2.3 Old bill
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>
using namespace std;
/*
使用vector,然后判断符合条件就往里加，
最后利用algorithm 中max_element函数求最大值；
需要注意的是vector在初始化的时候，由于设计的是二维数组，所以应该先初始化设置好格式，vector 中嵌套vector ，并为其指定好格式resize
*/


int equation(int n,int x,int y,int z)
{
	int head, end;
	vector<vector<int>> a;
	vector<int> temp(3);
	a.resize(5, temp);

	for (head = 1; head <= 9; head++)
	{
		int temp = head * 10000;
		temp += x * 1000 + y*100 + z*10;
		for (end = 0; end < 10; end++)
		{
			//temp+=end   	//Total Price确定    这里出现问题，如果是temp+= end 那在内层循环里就会一直加temp,+1+2+3...+9
			if (temp % n == 0)		//整除则入容器
				a.push_back({ head,end,temp / n });
			temp++;
		}
	}
	// 总价为零的话就只输出一个 0
	if (a[a.size() - 1][2] == 0)
		cout << 0 << endl;
	else
	{
		/*//判断最大值,无需判断，因为head和end 都是自增的 所以肯定最后一个元素价格最高，只需要考虑没有解时输出为零即可
		int max=0;
		for (int i = 0; i < a.size(); i++)
		{
			if (a[i][2] > a[max][2])
				max = i;
		}
		*/
		cout <<a[a.size()-1][0]<< ' ' <<a[a.size() - 1][1]<< " " <<a[a.size() - 1][2]<< endl;
	}
	return 0;
}
int main()
{
	int n,x,y,z;
	cin >> n>>x>>y>>z;
	equation(n,x,y,z);
	return 0;
}
```

