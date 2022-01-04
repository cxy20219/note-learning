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