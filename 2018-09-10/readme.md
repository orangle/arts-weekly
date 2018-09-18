# A

# R



# T

Linux 文件夹下对文件大小，文件数目，以及文件行数的统计

当前下子目录大小
```
$ du -lsh ./*
```

文件数目
```
$ find ./ -type f|wc -l
```

文件行数
```
$ find ./ -type f  | xargs wc -l
```



# S 

Linux 文件变化的监控(filebeat， logstash文件夹的监控)

* 最简单的思路是通过定时扫描，记录所有文件的路径还有修改时间等信息
* 通过 inotify 调用来监控目录的变化，这种回调式的方式更好一些


