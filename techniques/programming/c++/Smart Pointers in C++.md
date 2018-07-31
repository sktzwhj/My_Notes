#Smart Pointers in C++

C\++的优点和缺点几乎都是由指针和内存管理带来的， 让用户去管理指针本身就是一件很痛苦的事，且容易犯错，新的C++标准借鉴了和boost库类似的智能指针来解决这个问题。

简单来说，在一个局部作用域中new一个对象，那么出了作用域之后，指针自然就失效了，但是问题在于指针指向的空间可能没有被释放，从而导致内存泄露问题。

换言之，这里要注意析构函数被调用的时机。对于在栈上声明的类的对象，在出作用域的时候其析构函数会被自动调用。但是如果是在堆上new出来的，其析构函数就不会被自动调用，而需要显式地delete才能析构。

以下就几种常见的智能指针做下总结，

##unique_ptr
C++的RAII特性可以被利用在生命周期结束时释放资源，因而可以被用来实现一个简单的
class Unique {
public:
   Unique(int n) {
       std::cout << "Unique" << std::endl;
       ptr = new int[n];
   }
   ~Unique() {
       std::cout << "~Unique" << std::endl;
       delete []ptr;
   }
   // other func
private:
   int *ptr;
};



##shared_ptr
shared_ptr要解决的问题就是多个指针共享一个对象，简单来想可以通过引用计数的方法，最后一个拥有该对象的指针负责对资源的释放。具体来说就是所有指向同一个对象的shared_ptr共享了一个counter，shared_ptr对象在析构时，如果counter == 0，　则delete相应对象。

但是shared_ptr在遇到循环引用问题时会出问题。具体来说，

using namespace std;
class myClass {
public:
    smart_ptr<myClass> parent;
    smart_ptr<myClass> child;
    string name;
    myClass(string name):name(name){cout<<"Create "<<name<<endl;};
    ~myClass(){cout<<"Delete "<<name<<endl;}
};

int main() {
    smart_ptr<myClass> p1(new myClass("a"));
    smart_ptr<myClass> p2(new myClass("bb"));
    p1->child=p2;
    p2->parent=p1;
}

假如我们有如上程序，当离开main函数作用域时，p1和p2指向的对象counter均为1，因此就无法析构了。
为了解决这个问题，则引入了weak_ptr。　

##weak_ptr
weak_ptr解决循环引用的方法就是，weak_ptr不拥有其指向的对象。
将一个weak_ptr指向一个对象的时候，并不会使得counter+1。
但是weak_ptr并不完美，因为其并不拥有对象，因此你不能用weak_ptr来访问对象成员。
但是可以用weak_ptr来构造shared_ptr，因此weak_ptr其实更是一个桥梁。　

NOTES
在使用shared_ptr时，有一些需要注意的地方。
比如说，你不能用一个raw pointer来创建两个shared_ptr。
另外，执行

shared_ptr<std::string> ptr{new string("hello")};
这个语句其实需要两次new操作，一个是用来new string，另一个则是shared_ptr内部用来new 控制块(主要是counter)的。一个高效的方法是

auto ptr = std::make_shared<std::string>("hello")

这个语句会把两次new优化成new一块连续的空间从而提高




