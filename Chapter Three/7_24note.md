#### 第四章 字符串

##### 4.1 字符串

string的长度:``string.length()`` 和 ``string.size()`` 二者功能相同
string元素的访问：

+ 可以直接用下标访问从0-size()-1 
+ 也可以使用迭代器：

```c++
for(string::iterator it = str.begin(),it!=str.end(),it++)
    printf("%c",*it);
```

string中的元素操作：

``insert()``在任意位置插入string元素，传入参数是``int/迭代器``

```c++
str.insert(str.size(),"end wordld");
```

``erase()``在任意位置擦除元素

```
erase(pos,n) 从第pos开始删除n个字符，erase(0,1)就是删除第一个字符
erase(it)  删除it迭代器所在的字符（单个字符）
erase(first,last) 删除从first到last之间的字符，这里first与last使用的是迭代器
```

``clear()``清空整个字符串

```c++
str.clear(); 		//这步之后str为空
```

string整体上可以当作数字进行处理，string直接相加，表示对接；

```c++
str1 += "hello"
```

string支持的比较运算符有：<, >, <=, >= 判断两个字符串是否相等用== or !=，比较时的规则是字典序进行大小比较。例如：

```c++
string str1 = "abc";
string str2 = "abcd";
string str3 = "bc";

那么有：
   	str1 <str2<str3
    拥有相同字符序列的字符串，长度更长的为大
```

string 常用函数有：

+ str.find() 用于在字符串中查找特定字符/子串，找到即返回下标(使用int类型接收）否则返回string::npos,这个函数比较简单用于寻找字符串里第一次出现的字符可以使用，如果需要遍历以及多次查询操作的话还是使用std自带的find函数，std::find(A.begin(),A.end(),*it); it表示迭代器。查到即返回迭代器，查不到返回A.end()；
+ str.substr(3,5) 返回子串，为string类型，返回3-5的子串