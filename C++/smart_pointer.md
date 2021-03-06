# 智能指针
参考：https://blog.csdn.net/K346K346/article/details/81478223

- unique_ptr
- shared_ptr
- auto_ptr（淘汰）
- wear_ptr

## 1、简介

程序用堆来存储动态分配的对象即那些在程序运行时分配的对象，当动态对象不再使用时，我们的代码必须显式的销毁它们。

在C++中，动态内存的管理是用一对运算符完成的：new和delete，new:在动态内存中为对象分配一块空间并返回一个指向该对象的指针，delete：指向一个动态独享的指针，销毁对象，并释放与之关联的内存。

动态内存管理经常会出现两种问题：一种是忘记释放内存，会造成内存泄漏；一种是尚有指针引用内存的情况下就释放了它，就会产生引用非法内存的指针。

为了更加容易（更加安全）的使用动态内存，引入了智能指针的概念。智能指针的行为类似常规指针，重要的区别是它负责自动释放所指向的对象。标准库提供的两种智能指针的区别在于管理底层指针的方法不同，shared_ptr允许多个指针指向同一个对象，unique_ptr则“独占”所指向的对象。标准库还定义了一种名为weak_ptr的伴随类，它是一种弱引用，指向shared_ptr所管理的对象，这三种智能指针都定义在memory头文件中。

## 2、unique_ptr和auto_ptr

### auto_ptr淘汰原因
使用 shared_ptr 时运行正常，因为 shared_ptr 采用引用计数，pwin 和 films[2] 都指向同一块内存，在释放空间时因为事先要判断引用计数值的大小因此不会出现多次删除一个对象的错误。

使用 unique_ptr 时编译出错，与 auto_ptr 一样，unique_ptr 也采用所有权模型，但在使用 unique_ptr 时，程序不会等到运行阶段崩溃，而在编译期因下述代码行出现错误

使用 auto_ptr 运行下发现程序崩溃了，原因在上面注释已经说的很清楚，films[2] 已经是空指针了，下面输出访问空指针当然会崩溃了。

指导你发现潜在的内存错误。这就是为何要摒弃 auto_ptr 的原因，一句话总结就是：避免因潜在的内存问题导致程序崩溃。

### unique_ptr安全性
从上面可见，unique_ptr 比 auto_ptr 更加安全，因为 auto_ptr 有拷贝语义，拷贝后原对象变得无效，再次访问原对象时会导致程序崩溃；unique_ptr 则禁止了拷贝语义，但提供了移动语义，即可以使用 std::move() 进行控制权限的转移，如下代码所示：

```
unique_ptr<string> upt(new string("lvlv"));
unique_ptr<string> upt1(upt);	//编译出错，已禁止拷贝
unique_ptr<string> upt1=upt;	//编译出错，已禁止拷贝
unique_ptr<string> upt1=std::move(upt);  //控制权限转移

auto_ptr<string> apt(new string("lvlv"));
auto_ptr<string> apt1(apt);	//编译通过
auto_ptr<string> apt1=apt;	//编译通过
```

unique_ptr 不仅安全，而且灵活。如果 unique_ptr 是个临时右值，编译器允许拷贝语义。

## 3、shared_ptr
shared_ptr最初实现于Boost库中，后由 C++11 引入到 C++ STL。shared_ptr 利用引用计数的方式实现了对所管理的对象的所有权的分享，即允许多个 shared_ptr 共同管理同一个对象。像 shared_ptr 这种智能指针，《Effective C++》称之为“引用计数型智能指针”（reference-counting smart pointer，RCSP）。

因此编译时需要使用c++11后面的版本
unique_ptr编译错误(unique_ptr compile error)： g++ g++ -std=c++14 -Wall -Wextra -pedantic ptr.cpp -g

这个智能指针面试常考设计一个源代码。

### 基础类
```
class Point {
private:
    int x, y;
public:
    Point(int xVal = 0, int yVal = 0) :x(xVal), y(yVal) {}
    int getX() const { return x; }
    int getY() const { return y; }
    void setX(int xVal) { x = xVal; }
    void setY(int yVal) { y = yVal; }
};
```

### 辅助类
```
class RefPtr {
private:
    friend class SmartPtr;      
    RefPtr(Point *ptr):p(ptr),count(1){}
    ~RefPtr(){delete p;}
    
    int count;   
    Point *p;                                                      
};
```

### shared_ptr类
````
class SmartPtr {
public:
	//构造函数
	SmartPtr() { rp = nullptr; }
	SmartPtr(Point *ptr):rp(new RefPtr(ptr)) {}
	SmartPtr(const SmartPtr &sp):rp(sp.rp) { 
		++rp->count;
		cout << "in copy constructor" <<endl;
	}
	
	//重载赋值运算符
	SmartPtr& operator=(const SmartPtr& rhs) {
		++rhs.rp->count;
		if (rp != nullptr && --rp->count == 0) {
			delete rp;
		}
		rp = rhs.rp;
		cout << "in assignment operator" << endl;
		return *this;
	}
	
	//重载->操作符
	Point* operator->() {
		return rp->p;
	}
	
	//重载*操作符
	Point& operator*() {
		return *(rp->p);
	}

	~SmartPtr() {
		if (--rp->count == 0) delete rp;
		else cout << "还有" << rp->count << "个指针指向基础对象" << endl;
	}

private:
	RefPtr* rp;
};
````

### 测试
```int main()
{
    //定义一个基础对象类指针
    Point *pa = new Point(10, 20);

    // 定义三个智能指针类对象，对象都指向基础类对象 pa
    // 使用花括号控制三个智能指针的生命周期，观察计数的变化
    {
        SmartPtr sptr1(pa);// 此时计数 count=1
        cout << "sptr1:" << sptr1->getX() << "," << sptr1->getY() <<endl;
        {
            SmartPtr sptr2(sptr1); // 调用拷贝构造函数，此时计数为 count=2
            cout<< "sptr2:" << sptr2->getX() << "," << sptr2->getY() <<endl;
            {
            	SmartPtr sptr3;
                SmartPtr sptr3=sptr1; // 调用赋值操作符，此时计数为 conut=3
                cout<<"sptr3:"<<(*sptr3).getX()<<","<<(*sptr3).getY()<<endl;
            }
            //此时count=2
        }
        //此时count=1；
    }
    //此时count=0；对象 pa 被 delete 掉
    cout << pa->getX() << endl;
    return 0;
}
```

## 4、weak_ptr
weak_ptr 被设计为与 shared_ptr 共同工作，可以从一个 shared_ptr 或者另一个 weak_ptr 对象构造而来。weak_ptr 是为了配合 shared_ptr 而引入的一种智能指针，它更像是 shared_ptr 的一个助手而不是智能指针，因为它不具有普通指针的行为，没有重载 operator* 和 operator-> ，因此取名为 weak，表明其是功能较弱的智能指针。它的最大作用在于协助 shared_ptr 工作，可获得资源的观测权，像旁观者那样观测资源的使用情况。观察者意味着 weak_ptr 只对 shared_ptr 进行引用，而不改变其引用计数，当被观察的 shared_ptr 失效后，相应的 weak_ptr 也相应失效。


其实 weak_ptr 可用于打破循环引用。引用计数是一种便利的内存管理机制，但它有一个很大的缺点，那就是不能管理循环引用的对象。

在 Man 类内部会引用一个 Woman，Woman 类内部也引用一个 Man。当一个 man 和一个 woman 是夫妻的时候，他们直接就存在了相互引用问题。man 内部有个用于管理wife生命期的 shared_ptr 变量，也就是说 wife 必定是在 husband 去世之后才能去世。同样的，woman 内部也有一个管理 husband 生命期的 shared_ptr 变量，也就是说 husband 必须在 wife 去世之后才能去世。这就是循环引用存在的问题：husband 的生命期由 wife 的生命期决定，wife 的生命期由 husband 的生命期决定，最后两人都死不掉，违反了自然规律，导致了内存泄漏。
weak_ptr 对象引用资源时不会增加引用计数，但是它能够通过 lock() 方法来判断它所管理的资源是否被释放。做法就是上面的代码注释的地方取消注释，取消 Woman 类或者 Man 类的任意一个即可，也可同时取消注释，全部换成弱引用 weak_ptr。



下面给出几个使用指南。
（1）如果程序要使用多个指向同一个对象的指针，应选择 shared_ptr。这样的情况包括：
（a）将指针作为参数或者函数的返回值进行传递的话，应该使用 shared_ptr；
（b）两个对象都包含指向第三个对象的指针，此时应该使用 shared_ptr 来管理第三个对象；
（c）STL 容器包含指针。很多 STL 算法都支持复制和赋值操作，这些操作可用于 shared_ptr，但不能用于 unique_ptr（编译器发出 warning）和 auto_ptr（行为不确定）。如果你的编译器没有提供 shared_ptr，可使用 Boost 库提供的 shared_ptr。

（2）如果程序不需要多个指向同一个对象的指针，则可使用 unique_ptr。如果函数使用 new 分配内存，并返还指向该内存的指针，将其返回类型声明为 unique_ptr 是不错的选择。这样，所有权转让给接受返回值的 unique_ptr，而该智能指针将负责调用 delete。可将 unique_ptr 存储到 STL 容器中，只要对容器元素不使用拷贝操作的算法即可（如 sort()）。例如，可在程序中使用类似于下面的代码段。

（3）虽然说在满足 unique_ptr 要求的条件时，使用 auto_ptr 也可以完成对内存资源的管理，但是因为 auto_ ptr 不够安全，不提倡使用，即任何情况下都不应该使用 auto_ptr。

（4）为了解决 shared_ptr 的循环引用问题，我们可以祭出 weak_ptr。

（5）在局部作用域（例如函数内部或类内部），且不需要将指针作为参数或返回值进行传递的情况下，如果对性能要求严格，使用 scoped_ptr 的开销较 shared_ptr 会小一些。

















