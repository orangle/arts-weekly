

* [Inside the Python GIL](https://www.dabeaz.com/python/GIL.pdf) , [Understanding the Python GIL](https://www.dabeaz.com/python/UnderstandingGIL.pdf) 估计是讲解GIL内部机制最用心的两个sides.
* [Grok the GIL: Write Fast and Thread-Safe Python](https://emptysqua.re/blog/grok-the-gil-fast-thread-safe-python/)

编译语言的优化会在机器码的级别优化, 充分发挥机器性能，而Python的优化是在解释器的优化上，也就是说程序的速度首先受到解释器的速度限制。

> The GIL protects access to things like the current thread state and heap allocated object for garbage collection



