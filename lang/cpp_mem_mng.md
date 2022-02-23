# new和delete

new operator/delete operator就是new和delete**操作符**(C++ Primer中称为new表达式)，而operator new/operator delete是**函数**。 [详见[文档1](https://www.cnblogs.com/luxiaoxun/archive/2012/08/10/2631812.html)]

new 、operator new 和 placement new 区别  
1. new operator(或称new表达式)：不能被重载，其行为总是一致的。它先调用operator new分配内存，然后调用构造函数初始化那段内存。  
  new 操作符的执行过程：
    - 调用operator new分配内存 ；
    - 调用构造函数生成类对象；
    - 返回相应指针。
2. operator new：要实现不同的内存分配行为，应该重载operator new，而不是new。  
operator new就像operator + 一样，是可以重载的。如果类中没有重载operator new，那么调用的就是全局的::operator new来完成堆的分配。同理，operator new[]、operator delete、operator delete[]也是可以重载的。
    - 只分配所要求的空间，不调用相关对象的构造函数。当无法满足所要求分配的空间时，则  
        ->如果有new_handler，则调用new_handler，否则  
        ->如果没要求不抛出异常（以nothrow参数表达），则执行bad_alloc异常，否则  
        ->返回0  
    - 可以被重载
    - 重载时，返回类型必须声明为void*
    - 重载时，第一个参数类型必须为表达要求分配空间的大小（字节），类型为size_t
    - 重载时，可以带其它参数
3. placement new：只是operator new重载的一个版本。它并不分配内存，只是返回指向已经分配好的某段内存的一个指针。因此不能删除它，但需要调用对象的析构函数。  
如果你想在已经分配的内存中创建一个对象，使用new是行不通的。但placement new允许你在一个已经分配好的内存中（栈或者堆中）构造一个新的对象。原型中void* p实际上就是指向一个已经分配好的内存缓冲区的的首地址。[placement new使用场景](https://www.geeksforgeeks.org/placement-new-operator-cpp/)。

new operator(C++ Primer中称为new表达式)与delete operator的行为是不能够也不应该被改变，这是C++标准作出的承诺。而operator new与operator delete和C语言中的malloc与free对应，只负责分配及释放空间。但使用operator new分配的空间必须使用operator delete来释放，而不能使用free，因为它们对内存使用的登记方式不同。反过来亦是一样。

综上，**new表达式是分配内存+调用构造；operator new仅分配内存，不调用构造；placement new仅调用构造，不分配内存(使用传入的内存地址)**[C++ Primer 19.1.2节]。  

### 附1. [operator new](https://en.cppreference.com/w/cpp/memory/new/operator_new)公共库预定义的两种实现  

`void* operator new  ( std::size_t count ); (1)`  
申请内存失败时，函数抛出异常：
> In case of failure, the standard library implementation calls the function pointer returned by std::get_new_handler and repeats allocation attempts until new handler does not return or becomes a null pointer, at which time it throws std::bad_alloc.  

`void* operator new  ( std::size_t count, const std::nothrow_t& tag ); (5)`  
申请内存失败时，函数返回空指针，而不传播异常：  
> 5) Called by the non-throwing non-array new-expressions. The standard library implementation calls the version (1) and returns a null pointer on failure instead of propagating the exception.

### 附2. new操作中的异常处理
如上，new operator执行有3步，若第1步中的内存分配函数为不抛出异常，内存申请失败返回NULL时，不再继续执行第2步的调用构造函数，new operator立即返回，见[new expression](https://en.cppreference.com/w/cpp/language/new)：   
> If a non-throwing allocation function (e.g. the one selected by new(std::nothrow) T) returns a null pointer because of an allocation failure, then the new-expression returns immediately, it does not attempt to initialize an object or to call a deallocation function. 

### 附3. placement new实现

[new expression](https://en.cppreference.com/w/cpp/language/new)中的示例  
`::(optional) new (placement-params) ( type ) initializer(optional)`	(3)	  
`::(optional) new (placement-params) new-type initializer(optional)`	(4)	  

如`Foo* pfoo = ::new (buff)Foo;`实现调用类Foo的构造函数将创建的对象设置到buff内存中。[详见文档3]

## 参考
1. [C++中的new、operator new与placement new](https://www.cnblogs.com/luxiaoxun/archive/2012/08/10/2631812.html)
2. C++手册：[cppreference](https://en.cppreference.com/w/)
3. [Placement new的用法及用途](http://www.cppblog.com/kongque/archive/2010/02/20/108093.html)

# 智能指针
C++标准库memory头文件提供了两种智能指针类型来管理动态对象，区别在于管理底层指针的方式不同：   
- shared_ptr：允许多个指针指向同一个对象；内存资源共享。  
- unique_ptr：“独占”所指向的对象；  
- weak_ptr：伴随类，弱引用，指向shared_ptr所管理的对象。  

主流使用的是shared_ptr。[stackOverflow关于shared_ptr和unique_ptr的讨论](https://stackoverflow.com/questions/15648844/using-smart-pointers-for-class-members)。  

### shared_ptr
shared_ptr自动销毁锁管理的对象、自动释放相关联的内存。

