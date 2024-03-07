# JVM 常用参数总结
> 本文主要是 [JavaGuide-最重要的JVM参数总结](https://javaguide.cn/java/jvm/jvm-parameters-intro.html) 的阅读实践和记录

## 一、堆内存相关

### 1.1 显示指定堆内存

堆是 Java 虚拟机所管理的内存中最大的一块；根据应用程序需求初始化堆内存也是与性能相关的最常见的实践之一。可以通过以下的 JVM 参数指定堆的大小范围：

``` sh
-Xms<heap size>[unit]
-Xmx<heap size>[unit]
```

* heap size：表示指定的大小
* unit: 表示大小单位，可用单位有 “g”(GB)， “m”(MB), "k"(KB)

### 1.2 显示指定新生代内存

根据 [Oracle 官方文档](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/gctuning/sizing.html)，在堆总可用内存配置完成之后，影响垃圾回收性能的第二大影响因素是为 `Young Generation` 在堆内存所占的比例。默认情况下，YG 的最小大小为 1310 *MB*，最大大小为 *无限制*。 可通过以下方式指定新生代内存的大小：

**1.通过`-XX:NewSize`和`-XX:MaxNewSize`指定**

```sh
-XX:NewSize=<young size>[unit]
-XX:MaxNewSize=<young size>[unit]
```

**2.通过`-Xmn<young size>[unit]`指定**

​	如，为新生代分配 256m 的内存（NewSize 与 MaxNewSize 设为一致），参数写为：

```sh
-Xmn256m
```



除此之外，还可以通过**`-XX:NewRatio=<int>`** 来设置**老年代与新生代**内存的比值, 比如下面的参数就是设置老年代与新生代内存的比值为 1。也就是说老年代和新生代所占比值为 1：1，新生代占整个堆栈的 1/2。
```sh
-XX:NewRatio=1
```

!!! GC调优策略中很重要的一条经验总结
    将新对象预留在新生代，由于 Full GC 的成本远高于 Minor GC，因此尽可能将对象分配在新生代是明智的做法，实际项目中根据 GC 日志分析新生代空间大小分配是否合理，适当通过“-Xmn”命令调节新生代大小，最大限度降低新对象直接进入老年代的情况。



**3.元空间相关参数**

```sh
-XX:MetaspaceSize=N # 触发 Full GC 的阈值大小
-XX:MaxMetaspaceSize=N #设置 Metaspace 的最大大小
```





## 参考

[1][JVM堆空间大小的设置（-Xms和-Xmx）和查看](JVM堆空间大小的设置（-Xms和-Xmx）和查看)
