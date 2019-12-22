# ARTS 打卡 
自愿加入左耳听风ARTS打卡活动，即每周至少做一道算法题（Algorithm），至少点评一篇英文文章（Review），
至少学习一个小技巧（Tips），写一篇分享（Share）。

笔者自己能最近在学习Go语言及Elasticsearch的东西，希望通过坚持ARTS打卡活动，可以提高自己在Go语言编程开发、设计模式、数据结构、网络协议、ES业务等多方面提高自己的专业技能。
## 打卡记录
### Week 1 (12.16 ~ 12.22)
#### Algorithm
No. 1122 相对数组的排序

题目中提到arr2中数据各不重复，且arr1中在arr2中出现的数字需要根据arr2的顺序排序，故可以先遍历arr2中的数据，当arr1中与当前数字不同时，指针后移，直到找到与当前数字，交换位置。
如此重复遍历即可；当arr2中数字遍历完后，再排序arr1中剩余的数字即可
```go
func relativeSortArray(arr1 []int, arr2 []int) []int {
	lastIdx := 0
	for i := 0; i < len(arr2); i++ {
		for j := lastIdx; j < len(arr1); j++ {
			if arr1[j] == arr2[i] {
				arr1[lastIdx], arr1[j] = arr1[j], arr1[lastIdx]
				lastIdx++
			}
		}
	}
	sort.Ints(arr1[lastIdx:])
	return arr1
}
```
#### Review
阅读了ES中相关性算法的几篇博客，根据这些博客的内容及自己的感悟写了一篇这方面的博客，详情请参考 Share 模块的博客分享。
#### Tips
最近在工作中遇到了关于时区的问题，汇总如下：

python中时间有多种形式：时间戳是指当前时间针对于1970年1月1号00：00：00为基准时间的时间偏移量，数据类型是int或float；格式化的时间，则包括‘年月日时分秒’的信息，GMT指的是格林威治时间，UTC指的是电子时间，UTC和GMT之间没有时差。北京所在的时区为 UTC+8时区，即东八区。
- time.time() 输出计算机本地当前时间的时间戳。
- time.gmtime() 输出格林威治时区的时间结构
- calendar.timegm(time_struct) 将传入的时间结构（**默认为UTC时间**)转化成当地的timestamp
- time.mktime() 默认传入为当地时间
- datetime.datetime().utcnow().timestamp() 输出UTC时间的时间戳
``` python
import time, datetime, calendar
>>> time.gmtime()
time.struct_time(tm_year=2019, tm_mon=12, tm_mday=2, tm_hour=7, tm_min=3, tm_sec=36, tm_wday=0, tm_yday=336, tm_isdst=0)

# 可以看出两种将时间结构转化成时间戳的方式，实际上是有差别的。time.mktime()并没有对其进行转化
>>> time.time() - calendar.timegm(time.gmtime())
0.2332170009613037
>>> time.time() - time.mktime(time.gmtime())
28800.772998809814
>>> datetime.datetime.utcnow().timestamp()
1575251293.053719
```
#### Share
[分享文章](https://blog.csdn.net/U5years/article/details/103656697)，欢迎指正。

