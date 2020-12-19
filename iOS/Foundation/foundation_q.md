# 2019-04-08

问题：访问__weak 修饰符的变量必须访问注册到pool中的对象？

解释：__weak 不持有对象，访问该对象时可能对象已被废弃，放入pool中保证在pool销毁前对象一直存在。

求证：查看weak实现的源代码，看是否有pool的存在。

# 2019-04-28

问题：NSTimer类循环引用问题，具体代码见博客isa-swizzling。dealloc方法是对象的方法，类循环引用怎么解释？

解释：类可以理解为静态的，会一直存在，所以不释放没有关系，关键是timer不在使用调用`invalidate`，这样对应的selector就不会执行了。o

# 2020-12-19

问题：Apple 文档上写不要在init和dealloc方法中使用setter/getter，但是没有写具体的理由。

解释：其中提到的一个原因是会触发KVO通知。还有就是当自己重写了setter或者子类复写了setter，此时setter内部会进行一些操作，这个时候对象其实还没有完全初始化。

[Apple Doc](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmPractical.html)
[stackoverflow discussion](https://stackoverflow.com/questions/10505274/don-t-use-accessor-methods-in-initializer-methods-and-dealloc?noredirect=1&lq=1)
