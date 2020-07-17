---
layout: post
title:  "leetcode的golang题解01-10"
date:   2020-07-17 22:10:00 +0800
tags:
  - leetcode
  - golang
categories:
  - LeetCode
  - GoLang
---

> 总算结束了考试与实训，试着再写写博客吧。最近了解了`golang`底层的`ReadFrom`和`WriteTo`实现，但不算太深，感觉写不了。那就做做题，写写题解，了解下`golang`的语法吧

### LeetCode-01
+ 题目
![LeetCode-01](https://blog.zhaxzhax.cn/pic/leetcode-golang-1.png)
+ 答案
```
    func twoSum(nums []int, target int) []int {
    result:= make(map[int]int)
    for index_num,num:= range nums{
        index_res,boolen:=result[num]
        if boolen{
            return []int{index_res,index_num} 
        }else{
            result[target-num]=index_num
        }
    }
    return []int{}
}
```
+ 思路
采用二层循环，实质上是进行了多余的计算。我们可以将`target`与`num`数组中的值作减法，将结果保存在`map`中。实质上，这种优化保存了每一次计算获取到的信息（`target`-`num`）。时间复杂度由二层循环的O(n^2)变为了O（n）。