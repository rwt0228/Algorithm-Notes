### description    
  Given a group of two strings, you need to find the longest uncommon subsequence of this group of two strings. The longest uncommon subsequence is defined as the longest subsequence of one of these strings and this subsequence should not be any subsequence of the other strings.  
    
  A subsequence is a sequence that can be derived from one sequence by deleting some characters without changing the order of the remaining elements. Trivially, any string is a subsequence of itself and an empty string is a subsequence of any string.  
    
  The input will be two strings, and the output needs to be the length of the longest uncommon subsequence. If the longest uncommon subsequence doesn't exist, return -1.  
    
  Example 1:  
  Input: "aba", "cdc"  
  Output: 3  
  Explanation: The longest uncommon subsequence is "aba" (or "cdc"),   
  because "aba" is a subsequence of "aba",   
  but not a subsequence of any other strings in the group of two strings.   
  Note:  
    
  Both strings' lengths will not exceed 100.  
  Only letters from a ~ z will appear in input strings.  
    
  给定两个字符串，你需要从这两个字符串中找出最长的特殊序列。最长特殊序列定义如下：该序列为某字符串独有的最长子序列（即不能是其他字符串的子序列）。  
    
  子序列可以通过删去字符串中的某些字符实现，但不能改变剩余字符的相对顺序。空序列为所有字符串的子序列，任何字符串为其自身的子序列。  
    
  输入为两个字符串，输出最长特殊序列的长度。如果不存在，则返回 -1。  
    
### solution    
```    
  class Solution {  
     public int findLUSlength(String a, String b) {  
         if (a.equals(b))  
              return -1;  
          return Math.max(a.length(), b.length());  
      }  
    
  }  
```    
    
### 个人解读    
    
  以下是错误思路  
  ```  
    相当于先求最长公共子序列，然后用最长的长度去减该长度。  
    需要用到二维动态规划吗？？  
    用吧，然后就是套模板即可。（需要对模板好好复习下）    
  ```  
    
  反思：为什么自己脑子没有转过弯来。。。。。  
    
    
    
tags:    
  -  数学  
  -  反思  
