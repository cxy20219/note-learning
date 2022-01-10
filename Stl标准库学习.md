## vector使用
### 1.vector存放内置数据
```c++
# include <iostream>
# include <vector>
# include <algorithm>
using namespace std;
//for_each()方法调用函数 
void vim(int n){
	cout<<n<<endl;
} 
void test01(){
	//创建vector容器
	vector<int> v;
	
	//向容器插入数据
	v.push_back(10);
	v.push_back(20);
	v.push_back(30);
	
	//通过迭代器访问容器
	vector<int>::iterator bg=v.begin(); //起始迭代器，指向容器第一个元素 
	vector<int>::iterator ed=v.end();   //结束迭代器，指向容器最后一个元素的下一个位置 
	
	//第一种遍历方式
	while(bg!=ed){
		cout<<*bg<<endl;
		bg++;
	} 
	
	//第二种遍历方式
	for(vector<int>::iterator bg2=v.begin();bg2!=v.end();bg2++){
		cout<<*bg2<<endl;
	}
	
	//第三种遍历方式 (使用algorithm里面的遍历方法)
	//需要自定义函数 
	for_each(v.begin(),v.end(),vim);	 
}
int main(){
	test01();
	return 0;
}
```
### 2.vector存放自定义数据
```c++
# include <iostream>
# include <vector>
using namespace std;
class Person{
public:
	Person(string name,int age){
		this->m_Name=name;
		this->m_Age=age;
	}
	string m_Name;
	int m_Age;
}; 
void test01(){
	vector<Person> v;
	Person p1("aa",10);
	Person p2("bb",20);
	Person p3("cc",30);
	
	//向容器中添加数据
	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	
	//遍历容器中的数据
	for(vector<Person>::iterator bg=v.begin();bg!=v.end();bg++){
		cout<<"姓名:"<<(*bg).m_Name<<"年龄:"<<(*bg).m_Age<<endl;
		cout<<"姓名:"<<bg->m_Name<<"年龄:"<<bg->m_Age<<endl;
	} 
}

//存放指针
void test02(){
	vector<Person*>v;

	Person p1("aa",10);
	Person p2("bb",20);
	Person p3("cc",30);
	
	//向容器中添加数据
	v.push_back(&p1);
	v.push_back(&p2);
	v.push_back(&p3);
	
	//遍历容器
	for(vector<Person *>::iterator bg=v.begin();v.begin()!=v.end();bg++){
		cout<<"姓名:"<<(*bg)->m_Name<<"年龄:"<<(*bg)->m_Age<<endl;
	} 
} 
int main(){
	test02();
	return 0;
}
```
### 3.容器的嵌套
```c++
# include <iostream>
# include <vector>
using namespace std;
void test01(){
	vector<vector<int> > v;
	
	//创建小容器
	vector<int>v1;
	vector<int>v2;
	vector<int>v3;
	
	//向容器中添加数据
	for(int i=0;i<4;i++){
		v1.push_back(i);
		v2.push_back(i+1);
		v3.push_back(i+2);
	} 
	
	//将小容器添加进大容器 
	v.push_back(v1);
	v.push_back(v2);
	v.push_back(v3);
	
	//通过大容器,访问所有数据
	for(vector<vector<int> >::iterator bg=v.begin();bg!=v.end();bg++){
		//*bg 是小容器 
		for(vector<int>::iterator bg2=(*bg).begin();bg2!=(*bg).end();bg2++){
			cout<<*bg2<<" ";
		}
		cout<<endl;
	} 
}
int main(){
	test01();
	return 0;
}
```
## string容器

### 1.构造函数
* string(); //创建一个空字符串
* string(const char* s); //使用字符串s初始化
* string(const string& str); //使用string对象初始化另一个对象
* string(int n,char c); //使用n个字符c初始化 
```c++
# include <iostream>
# include <string>
using namespace std;
void test01(){
	//默认构造
	string s1; 
	
	//字符串初始化 
	const char* str="hello world";
	string s2(str);   
	cout<<"s2="<<s2<<endl;
	
	//拷贝
	string s3(s2);
	cout<<"s3="<<s3<<endl;
	
	string s4(10,'a');
	cout<< "s4="<<s4; 
}
int main(){
	test01();
	return 0;
} 
```

### 2.赋值
```c++
void test02(){
	// char*类型字符串赋值 
	string str1;
	str1="hello world";
	cout<<"str1="<<str1<<endl;
	
	// 字符串赋值 
	string str2;
	str2 = str1;
	cout<<"str2="<<str2<<endl;
	
	// 单个字符赋值
	string str3;
	str3='a';
	cout<<"str3="<<str3<<endl;
	
	// assign赋值
	string str4;
	str4.assign("hello world c++");
	cout<<"str4="<<str4<<endl;
	
	// assign 把前n个字符赋值给当前字符串
	string str5;
	str5.assign("hello c++",5);
	cout<<"str5="<<str5<<endl; 
	
	// assign 把另一个字符串赋值给当前字符串 
	string str6;
	str6.assign(str5);
	cout<<"str6="<<str6<<endl;
	
	// assign 把n个字符赋值给当前字符产
	string str7;
	str7.assign(10,'w');
	cout<<"str7="<<str7<<endl; 
}
```

### 3.字符串的拼接
```c++
void test03(){
	// 重载+= 字符串操作 
	// 字符串拼接 
	string str1= "我";
	str1 +="爱c++";
	cout<<str1<<endl; 
	
	// 字符拼接 
	 str1+=";";
	 cout<<str1<<endl;
	 
	//  字符串相加
	string str2="我爱python;";
	str2+=str1;
	cout<<str2<<endl; 
	
	// append方式拼接
	// 拼接字符串
	string str3="I";
	str3.append("love");
	cout<<"str3="<<str3<<endl;
	
	// 把字符串前n个字符拼接到当前字符串
	str3.append("Java web",4);
	cout<<"str3="<<str3<<endl; 
	 
	//  拼接指定字符
	str3.append(str2,0,2);
	cout<<str3<<endl;
}
```
## set/multiset容器

简介：
* 所有元素被插入时会自动被排序
* 本质由关联式容器，底层由二叉树实现

区别：
* set不允许容器由重复的元素
* multiset允许容器有重复的元素

```c++

```
