
## A

## R

* [An introduction to parallel programming using Python's multiprocessing module](https://sebastianraschka.com/Articles/2014_multiprocessing.html)

Python的多进程模块

调度模型 

* Process
* Pool
    - Pool.apply
    - Pool.map （前面2个本质是一样的, 保证结果有序)
    - Pool.apply_async
    - Pool.map_async （获取结果立刻返回)

变量传递

* Queue (结果无序的，由进程执行的顺序决定, 可以通过自己传递order，在得到结果的时候排序) 适合生产消费者
* Pipes 
* Value, Array
* Manager

然后用了一个cpu密集型计算，来对比串型和多进程并行的效率，当进程个数和cpu cores一样的时候，效率最好。

* [Quick Tip: Speed up your Python data processing scripts with Process Pools](https://medium.com/@ageitgey/quick-tip-speed-up-your-python-data-processing-scripts-with-process-pools-cf275350163a)

使用py3中的 `concurrent.futures` 模块，实现并行处理图片缩略图的一个案例。


## Tips

* https://blog.csdn.net/orangleliu/article/details/82347384 Python日志解析入库批处理

## Share

* python pool 多进程怎么实现的?

共享内存，C variables and C arrays, 不是所有类型都可以共享的，共享内存只是把数据从master传递到slave 进程。

* multiprocessing and threading are same interface

