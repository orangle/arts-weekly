文件批处理
========

环境
* 64G 32核心 机械盘
* python2.7.5

文件的信息
```
$ tail www.geniatech.net
14.182.200.249 - - [23/Aug/2018:00:11:06 HKT] "GET http://www.geniatech.net/down-eng/upgrade/stvm8_5.0_MyGica_Dolby//update.xml HTTP/1.1" 404 0 0 319 "-" "Apache-HttpClient/UNAVAILABLE (java 1.4)" "-" "-" "HIT" "-" 1

$ ls -lsh www.geniatech.net
2.5G -rw-r--r-- 1 liuzz liuzz 2.5G 8月  24 16:01 www.geniatech.net

$ time wc -l www.geniatech.net
12762416 www.geniatech.net

real	0m0.579s
user	0m0.184s
sys	0m0.395s
```


#### 不解析，直接读取

```
# coding:utf-8
filename = "www.geniatech.net"
linenums = 0

with open(filename) as f:
    for line in f:
        linenums += 1

print linenums
```

testing
```
$ time python batch.py
12762416

real	0m2.606s
user	0m2.022s
sys	0m0.584s

$ time python batch.py
12762416

real	0m2.588s
user	0m2.040s
sys	0m0.548s
```

#### 不解析，多进程

```python
# coding:utf-8
import multiprocessing as mp

filename = "www.geniatech.net"
cores = 20

pool = mp.Pool(cores)
jobs = []

def work(line):
    pass

with open(filename) as f:
    for line in f:
        jobs.append(pool.apply_sync(work,(line,)))

for job in jobs:
    job.get()

pool.close()
```

上面的做法有问题，内存不断上升,会把整个文件加载到内存中，然后cpu也超过100%，几十秒无法完成，然后强制关闭了

```python
# coding:utf-8
import os
import multiprocessing as mp

filename = "www.geniatech.net"
cores = 5


def process_wrapper(chunkStart, chunkSize):
    num = 0
    with open(filename) as f:
        f.seek(chunkStart)
        lines = f.read(chunkSize).splitlines()
        for line in lines:
            num +=1
    return num

def chunkify(fname,size=1024*1024):
    fileEnd = os.path.getsize(fname)
    with open(fname,'r') as f:
        chunkEnd = f.tell()
        while True:
            chunkStart = chunkEnd
            f.seek(size,1)
            f.readline()
            chunkEnd = f.tell()
            yield chunkStart, chunkEnd - chunkStart
            if chunkEnd > fileEnd:
                break

pool = mp.Pool(cores)
jobs = []

for chunkStart, chunkSize in chunkify(filename):
    jobs.append(pool.apply_async(process_wrapper, (chunkStart,chunkSize)))

res = []
for job in jobs:
    res.append(job.get())

pool.close()
print sum(res)
```

上面的代码，还是没有完成sum的计算，但是多进程处理是可以的，并且在一定范围内，进程越多时间越短。
主要是通过生成器，每次取出文件的一段交给其他进程去处理，边处理边取出。


```
# 5个进程
$ time python batch.py
12762416

real	0m1.367s
user	0m4.004s
sys	0m2.653s

#15个进程
time python batch.py
12762416

real	0m0.672s
user	0m4.780s
sys	0m3.755s
```


