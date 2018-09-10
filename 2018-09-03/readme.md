
# A

# R


# T

面向对象设计中，为什么不要用 python 的 `__del__` 方法，原理和潜在隐患是什么？

`__del__` 是一个销毁器，垃圾回收的时候，清除对象内部资源会调用。不是在引用计数为0或者调用 del() 函数的时候。

多种不好的情况参看下面的链接 https://stackoverflow.com/questions/1481488/what-is-the-del-method-how-to-call-it

# S

### 使用 `logkit` 倒入数据到 `Elasticsearch`

[logkit](https://github.com/qiniu/logkit) 是七牛开发的一个日志收集工具，类似logstash，filebeat等工具，golang语言开发。

说说他的优点

* 提供web管理界面，可以通过UI来建立input，output工作流程
* golang开发，代码逻辑清晰，二次开发比较容易

主要的数据处理 pipline

```
input --> parser --> transformers --> output
```

这几个主要模块，都可以根据自己的需求拓展。

**parser**

我这里是文本类型的web日志，比默认的nginx日志复杂一些，只用grok表达式 + transformer 无法完成任务。然后花了2天自己写了一个 transformer, 感觉还不错，虽然逻辑比较简单，但是业务耦合性比较强，这样效率高一些。

grok表达式虽好，但是性能实在是不太好意思，所以在性能要求比较高的地方，尽量使用结构化的input数据，或者自定义解析方法。

**webui**

logkit的webui很方面，启动之后几乎不再需要操作 terminal 就可以完成整个操作，但是cli工具并不丰富，现有情况下必须借助webui才能完成操作，这一点也不是很友好，不适合批量操作等


测试了几个G的数据，插入速度大概在3～4k/qps, 还需要熟悉和进一步优化。


总的上手简单，基础功能也算丰富，自己定制也不困难。








