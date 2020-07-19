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

### LeetCode-02
+ 题目
![LeetCode-02](https://blog.zhaxzhax.cn/pic/leetcode-golang-2.png)
+ 答案
```
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    dummy := new(ListNode)
    curr := dummy
    carry := 0
    for(l1!=nil||l2!=nil||carry>0){
        curr.Next=new(ListNode)
        curr=curr.Next
        if(l1!=nil){
            carry+=l1.Val
            l1=l1.Next
        }
        if(l2!=nil){
            carry+=l2.Val
            l2=l2.Next
        }
        curr.Val=carry%10;
        carry=carry/10
    }
    return dummy.Next
}
```
+ 思路
这题其实就是进位，以及链表的操作。这题我是借鉴的题解，因为我写的代码太过于复杂，以至于我没有调试出来。注意golang的`new`和`make`。

### LeetCode-03
+ 题目
![LeetCode-03](https://blog.zhaxzhax.cn/pic/leetcode-golang-3.png)
+ 答案
```
func lengthOfLongestSubstring(s string) int {
    map_char:=make(map[byte]int)
    length:=0
    length_var:=0
    length_str:=len(s)
    for v,_:=range s{
        for j:=v;j<length_str;j++{
        _,e:=map_char[s[j]]
        if e{
            if length_var>length{
                length=length_var
            }
            map_char=make(map[byte]int)
            length_var=0
            break;
        }else{
            length_var++
            map_char[s[j]]=1
            if j==length_str-1{
                 if length_var>length{
                length=length_var
            }
            }
        }
     }
    }
    return length

}
```
+ 思路
此题我的代码效率极低，应该是进行了重复的计算。在算法执行过程中，出现了子串长度的比较。如果采用双指针法，就能保证找到的下一个子串长度一定大于现在的最大不重复子串长度，就会少了很多多余计算。我会再试一试。