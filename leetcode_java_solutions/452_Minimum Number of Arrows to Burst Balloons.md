### description  
在二维空间中有许多球形的气球。对于每个气球，提供的输入是水平方向上，气球直径的开始和结束坐标。由于它是水平的，所以y坐标并不重要，因此只要知道开始和结束的x坐标就足够了。开始坐标总是小于结束坐标。平面内最多存在104个气球。  
  
一支弓箭可以沿着x轴从不同点完全垂直地射出。在坐标x处射出一支箭，若有一个气球的直径的开始和结束坐标为 xstart，xend， 且满足  xstart ≤ x ≤ xend，则该气球会被引爆。可以射出的弓箭的数量没有限制。 弓箭一旦被射出之后，可以无限地前进。我们想找到使得所有气球全部被引爆，所需的弓箭的最小数量。  
  
Example:  
  
输入:  
[[10,16], [2,8], [1,6], [7,12]]  
  
输出:  
2  
  
解释:  
对于该样例，我们可以在x = 6（射爆[2,8],[1,6]两个气球）和 x = 11（射爆另外两个气球）。  
### solution  
```  
class Solution {  
    public int findMinArrowShots(int[][] points) {  
        Arrays.sort(points, new Comparator<int[]>() {  
            @Override  
            public int compare(int[] o1, int[] o2) {  
                return o1[1] - o2[1];  
            }  
        });  
        int count = 0;  
        int end = Integer.MIN_VALUE;    //容易出问题的地方，恰好输入是最小值  
        for(int[] interval: points) {  
            if(interval[0] > end || interval[0] == Integer.MIN_VALUE) { //第一次写的时候少了||后面的东西  
                count++;  
                end = interval[1];  
            }  
        }  
        return count;  
    }  
}  
```  
  
### 个人解读  
属于最优解问题：  
思路一：动态规划  
思路二：贪心算法  
  
可以与[435 Non-overlapping Intervals](435_Non-overlapping%20Intervals.md)关联起来  
然后问题：本题是否等于去求不重合的区间数量  
  
想当然会觉得没问题，因为把所有的不重合的挑出来以后(设为集合A)，那么剩余集合B里面的区间必然会有与A重合的，那么用飞镖射掉A的同时，就会顺带的把B里面的气球射掉  
然而问题来了，会不会出现这种情况：B1与A1重合，B2与A1重合，但是B1与B2不重合，所以射掉A1的时候，不能同时的把B1和B2射掉  
所以需要去证明：这种情况发生时候，B2或者B1必有另外一个A2，使得可以同时被飞镖射掉，并且同时不会引出新的"问题Bi  
  
以下去证明：  
  
证法一：  
//首先将Ai按照右节点从小到大排序，然后会因为右节点大小顺序不同，而产生相应的Bi（Bi为与An最接近的不被计算在内的区间）  
1)对于一个An来说，与他重叠的B需要满足一定的条件：  
  
+ a)Bi.end < An.end时 Bi.start < An-1.end < An.start  //在An前进行贪心计算，然而不满足条件而未算进去  
+ b)Bi.end = An.end时 Bi.start <= An.end   //在An前进行贪心计算时，Bi.start >= An-1.end；在An后进行贪心计算时，Bi.start <= An.end；所以Bi.start  <= An.end   
+ c)Bi.end > An.end && Bi.start < An.end < Bi.end  //在An后进行贪心计算， 不满足条件  
这一步很啰嗦，也很抽象，主要是为了说明一个结论：所有与An重合的，并且未被贪心算法收录的Bi，要么An.start在Bi的区间里，要么An.end在Bi的区间里  
不会出现Ai.start < Bi.start < Bi.end < Ai.end这种情况  
```  
下面这种情况不会出现  
   |-----------|        //Ai  
1--2--3--4--5--6--7  
|--|  |----|  |---|     //Bi  
```  
2)由1)可知，每一个An最多需有两个点需要处理(An.start 和 An.end)，由于A0.start(贪心算法排序后的第一个区间)前面不存在Bi，所以会猜测：对于所有贪心算法得到的不重复区间，只需要无脑射An.end，就会把所有气球射爆。  
3)如果全部射在An.end的话，所有的1)里面b)和c)的情形可以被包含到，而a)这种情况的气球会被An-1.end射掉  
证明完毕。  
  
综上可得：  
+ 该贪心算法合理；  
+ 得到的区间可以无脑选择右节点作为射击点  
  
延伸证法：  
不根据贪心算法，拿出来任意一组An的话，是否满足条件  
1)直接无脑选择所有An的右节点作为飞镖射击点  
2)如果存在射不到的Bi，那么这时候有 An-1.end < Bi.start < Bi.end < An.end  
3.1)如果An.end没有射中别的Bi，那么可以不在An.end上射击，在Bi上找一个合理的地方，如果找不到，则说明Bi应该被收录进An里面  
3.2)如果有射中别的Bi，另此时"别的Bi"记作C，那么C有两种情况，C与An+1接壤，  
//TODO   
  
tags:  
  - 数组  
  - 模型转换  
  - 贪心算法  
