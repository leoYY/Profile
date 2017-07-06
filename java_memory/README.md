# Java heap memory profile or trace

由于Java Heap内存由JVM单独管理，无法通过linux下的trace或profile工具对系统调用进行排查。而且由于Java的GC机制，hprof文件并不能方便的追查导致GC的原因，
待GC的很多对象都已经unreachable。

## 相关工具

| Name | desc |
|-----| ------:|
|jmap|jdk自带工具，支持dump hprof文件，使用其他解析工具进行查看解析|
|ecplise MAT| 分析hprof文件工具|
|btrace|类似dtrace，systemtap等trace工具|
|allocation-instrumenter|实现与btrace类似， 专注于trace memory allocation事件|

## 其他工具
| Name | desc |
| ----| ---:|
|javap| 可以直接用来查看.class文件的类似汇编的命令|

## 相关工具使用情况对比
***
以上工具可以分为两部分，  
**jmap，eclipse MAT**结合使用， 根据hprof分析内存使用情况，  
优点：可以对alive对象进行reference的分析，以及各种占比，shallow heap和retained heap统计，live对象的内存以及对应地址，且MAT支持一种语言进行排序，条件查询；  
缺点：对于可以被GC但未GC的unreachable对象无法分析上下文，对于分析哪些对象导致GC原因不太方便。 
***
**btrace，allocation-instrumenter**都是trace类型，主要是实现是通过asm进行codegen，
并改写当前程序的bytecode，  
优点：可以统计所有申请内存调用的数据，  
缺点：TODO（目前排查频繁minor GC问题，比较需要trace类型的工具，感觉可以满足profile类工具的需求）；

_通过查看new xxx[]的.class文件的命令，会存在专门的NEWARRAY命令，相关asm codegen也是通过匹配类似命令的方式实现_
