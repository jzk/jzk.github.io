title: Java Exception的log里没有stack trace
date: 2021-04-08 13:59:37
tags:
---

今天听说一个生产环境上的bug。在服务器的Log里有NullPointException，但是没有stack trace，也就没有行号，完全无从下手解决问题。

Log 长这样

```
ERROR xxx.xxx.xxx.Class: java.lang.NullPointerException
java.lang.NullPointerException: null
```


我先是试图在最近release涉及到这个class的PR里找，但是改动太多了，有点像大海捞针。

而且看代码里，在用Apache common logs  和log4j，都是大刀阔斧得catch 所有的exception 用下面的代码打log，理论上应该会有stack trace才对。

```java
   try{
       //...
   } catch (final Exception e) {
		logger.error(e, e);
   }
```

后来在Google上搜 [log java.lang.NullPointerException no stack trace](
https://www.google.com/search?q=log+java.lang.NullPointerException+no+stack+trace&rlz=1C5GCEM_enUS921US921&sxsrf=ALeKk02BZcvxwTNorHJ3UVv2iye8q0DIEg%3A1617912633654&ei=OWNvYLqPJ8j5-gSfvKHIAw&oq=log+java.lang.NullPointerException+no+stack+trace&gs_lcp=Cgdnd3Mtd2l6EAM6CQgAELADEAgQHjoECCMQJzoECAAQHjoFCCEQoAE6BwghEAoQoAFQu4oCWO-pAmDjqgJoBnAAeACAAe0BiAHBEJIBBjE2LjQuMZgBAKABAaoBB2d3cy13aXrIAQHAAQE&sclient=gws-wiz&ved=0ahUKEwj6j7meuu_vAhXIvJ4KHR9eCDkQ4dUDCA0&uact=5)

找到[这个答案](https://stackoverflow.com/a/3010106/703308)，解释了这个现象。

> You are probably using the HotSpot JVM, it has a optimization is that when an exception (typically a NullPointerException) occurs for the first time, the full stack trace is printed and the JVM remembers the stack trace (or maybe just the location of the code). When that exception occurs often enough, the stack trace is not printed anymore, both to achieve better performance and not to flood the log with identical stack traces.

☆ 大意就是JVM有一个默认的优化，如果一个Exception发生次数太多，就会在之后的log里不再打印stack trace。

所以我开始在Datadog里往前翻log，翻到了最先的一条，果然找到了一条记录是有StackTrace的。 翻了一下记录发现，大约5-10次后就不再打stack trace了。。。

感觉JVM设计还是有点粗糙，在决定做这种优化的时候应该给个提示，而不是只是打出null完事。