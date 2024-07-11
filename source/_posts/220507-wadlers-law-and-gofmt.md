title: 沃德勒定律 (Wadler's Law) 和 gofmt
date: 2022-05-07 09:50:40
categories:
- Thoughts
tags: golang
---

早上在听Changelog的Podcast，[Go Tooling](https://changelog.com/gotime/90)这期，讲到最开始大家一般都没有对`gofmt`里规定的格式做到百分百的接受，但是最后会发现它的好处。我就想起来了昨天看到的[沃德勒定律 (Wadler's Law)](https://github.com/nusr/hacker-laws-zh#%E6%B2%83%E5%BE%B7%E5%8B%92%E5%AE%9A%E5%BE%8B-wadlers-law)，大意是人们在设计语言的时候会在不是那么重要的事情上花更多的时间，而在重要的事情上反而会花费比较少的时间。`gofmt`在这方面的贡献就是减少了在代码风格上可能引发的争议，而是解放人们可以在更重要的事情上花时间。