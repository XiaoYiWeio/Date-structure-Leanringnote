#### 第三章 排序与查找

##### 3.2 查找

例题：

```c++
例题3.4
#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
#include<limits.h>
using namespace std;
 
/*
vector.find  但是find不属于vector的内容 而是属于algorithm提供的函数，使用时注意头文件  但是都在std里
vector.begin() 迭代器指到这里时 指示的是A【0】，而vector.end()指示的是A[N-1]之后的元素，访问会越界
find之后返回值是迭代器，想要输出具体下标需要用distance函数找和A.begin之间的距离
distance(it1,it2)返回两个迭代器之间的距离
*/
 
 
int main()
{
    int n;
    while (cin >> n)
    {
        vector<int>A;
        int k;
        for (int i = 0; i < n; i++)
        {
            int temp;
            cin >> temp;
            A.push_back(temp);
        }
        cin >> k;
        vector<int>::iterator it = find(A.begin(), A.end(), k);
        if (it == A.end())
            cout << "-1" << endl;
        else
        {
            int pos = distance(A.begin(), it);
            cout << pos << endl;
        }
    }
    return 0;
}

例题3.5
#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
#include<limits.h>
using namespace std;
 
/*
vector.find  但是find不属于vector的内容 而是属于algorithm提供的函数，使用时注意头文件  但是都在std里
vector.begin() 迭代器指到这里时 指示的是A【0】，而vector.end()指示的是A[N-1]之后的元素，访问会越界
find之后返回值是迭代器，想要输出具体下标需要用distance函数找和A.begin之间的距离
distance(it1,it2)返回两个迭代器之间的距离
*/
 
 
int main()
{
    int n,m;
    while (cin >> n)
    {
        vector<int>A;
        for (int i = 0; i < n; i++)
        {
            int temp;
            cin >> temp;
            A.push_back(temp);
        }
        cin >> m;
        for (int i = 0; i < m; i++)
        {
            int temp;
            cin >> temp;
            vector<int>::iterator it = find(A.begin(), A.end(), temp);
            if (it == A.end())
                cout << "NO\n";
            else
                cout << "YES\n";
        }
 
    }
    return 0;
}



```

无答案题

```c++
习题3.5
#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
#include<limits.h>
using namespace std;
 
/*
vector.find  但是find不属于vector的内容 而是属于algorithm提供的函数，使用时注意头文件  但是都在std里
vector.begin() 迭代器指到这里时 指示的是A【0】，而vector.end()指示的是A[N-1]之后的元素，访问会越界
find之后返回值是迭代器，想要输出具体下标需要用distance函数找和A.begin之间的距离
distance(it1,it2)返回两个迭代器之间的距离
*/
 
struct num
{
    int x;
    int y;
};
 
 
bool cmp(num a, num b)
{
    if (a.x != b.x)
        return a.x < b.x;
    else
        return a.y < b.y;
}
int main()
{
    int n;
    while (cin >> n)
    {
        vector<num>A;
        for (int i = 0; i < n; i++)
        {
            num temp;
            cin >> temp.x>>temp.y;
            A.push_back(temp);
        }
        sort(A.begin(), A.end(), cmp);
        cout << A[0].x << " " << A[0].y << endl;
    }
    return 0;
}


#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
#include<limits.h>
using namespace std;
 
/*
先完成对数组的输入，然后挨个判断，输出下标即可(首尾分开分析)
*/
 
 
 习题3.6
int main()
{
    int n;
    while (cin >> n)
    {
        vector<int>A;
        for (int i = 0; i < n; i++)
        {
            int temp;
            cin >> temp;
            A.push_back(temp);
        }
 
        //head && end,不考虑size=1的情况
        if (A[0] != A[1])
            cout << 0 <<" ";
        for (int i = 1; i < n-1; i++)
        {
            if (A[i] > A[i + 1] && A[i] > A[i - 1])
                cout << i << " ";
            else if (A[i] < A[i + 1] && A[i] < A[i - 1])
                cout << i << " ";
        }
        if (A[n - 1] != A[n - 2])
            cout << n - 1 << " ";
        cout << endl;
 
    }
    return 0;
}


#include<iostream>
#include<vector>
#include<algorithm>
#include<string>
#include<limits.h>
using namespace std;
 
/*
先完成对数组的输入，然后用find函数+distan函数 即可
使用双层循环，同时需要设置一个数组来记录已经被输出过的字符
*/
 
 
习题3.7
int main()
{
    string A,visit="";
    while (cin >> A)
    {
        string::iterator it = A.begin(),temp,temp2;
        for (; it != A.end()-1; it++)                   //temp 记得find(it+1,end) 不然肯定会查到it自己
        {
            temp = find(it+1, A.end(), *it);
            temp2 = find(visit.begin(), visit.end(), *it);
            if (temp != A.end()&&temp2==visit.end())    //这里visit表示的记录过的字符，所以应该是判断当visit中不存在的话就进行循环即==visit.end()
            {
                cout << *it << ":" << distance(A.begin(),it);
                for (; temp != A.end(); temp++)
                {
                    if (*temp == *it)
                        cout << "," << *it << ":" << distance(A.begin(), temp);
                }
                cout << endl;
                visit += *it;
            }
        }
    }
    return 0;
}
```

