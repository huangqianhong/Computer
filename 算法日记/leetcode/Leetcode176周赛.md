# [LeetCode周赛176](<https://leetcode-cn.com/contest/weekly-contest-176>)

[TOC]



### [A统计有限矩阵的负数](<https://leetcode-cn.com/problems/count-negative-numbers-in-a-sorted-matrix/>)

给你一个 m * n 的矩阵 grid，矩阵中的元素无论是按行还是按列，都以非递增顺序排列。 

请你统计并返回 grid 中 负数 的数目。

 ##### 样例

示例 1：

输入：grid = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]]
输出：8
解释：矩阵中共有 8 个负数。
示例 2：

输入：grid = [[3,2],[1,0]]
输出：0
示例 3：

输入：grid = [[1,-1],[-1,-1]]
输出：3
示例 4：

输入：grid = [[-1]]
输出：1

##### 解析

直接就暴力枚举，然后获取到值

##### 代码

```


public class Main {
    public static int countNegatives(int[][] grid) {
        int res = 0;
        for(int i =0;i<grid.length;i++){
            for(int j =0;j<grid[i].length;j++){
                if(grid[i][j] < 0){
                    res++;
                }
            }
        }
        return res;
    }
    public static void main(String[] args) {
//        int[][] arr ={{4,3,2,-1},{3,2,1,-1},{1,1,-1,-2},{-1,-1,-2,-3}};
        int[][] arr ={{3,2},{1,0}};
        System.out.println(countNegatives(arr));

    }
}

```

### [B:最后k个数的乘积](<https://leetcode-cn.com/problems/product-of-the-last-k-numbers/>)

请你实现一个「数字乘积类」ProductOfNumbers，要求支持下述两种方法：

1. add(int num)

将数字 num 添加到当前数字列表的最后面。
2. getProduct(int k)

返回当前数字列表中，最后 k 个数字的乘积。
你可以假设当前列表中始终 至少 包含 k 个数字。
题目数据保证：任何时候，任一连续数字序列的乘积都在 32-bit 整数范围内，不会溢出。

##### 样例

```
输入：
["ProductOfNumbers","add","add","add","add","add","getProduct","getProduct","getProduct","add","getProduct"]
[[],[3],[0],[2],[5],[4],[2],[3],[4],[8],[2]]

输出：
[null,null,null,null,null,null,20,40,0,null,32]

解释：
ProductOfNumbers productOfNumbers = new ProductOfNumbers();
productOfNumbers.add(3);        // [3]
productOfNumbers.add(0);        // [3,0]
productOfNumbers.add(2);        // [3,0,2]
productOfNumbers.add(5);        // [3,0,2,5]
productOfNumbers.add(4);        // [3,0,2,5,4]
productOfNumbers.getProduct(2); // 返回 20 。最后 2 个数字的乘积是 5 * 4 = 20
productOfNumbers.getProduct(3); // 返回 40 。最后 3 个数字的乘积是 2 * 5 * 4 = 40
productOfNumbers.getProduct(4); // 返回  0 。最后 4 个数字的乘积是 0 * 2 * 5 * 4 = 0
productOfNumbers.add(8);        // [3,0,2,5,4,8]
productOfNumbers.getProduct(2); // 返回 32 。最后 2 个数字的乘积是 4 * 8 = 32 


```



##### 解析

> 这个题型我也是第一次见，所以记下来玩玩，写出框架然后让自己填空，有点意思哈,思想很简单，暴力枚举就可以过了

##### 代码：

```java
class ProductOfNumbers {
    private List<Integer> arrList = new ArrayList<Integer>();

    public ProductOfNumbers() {
        
    }
    
    public void add(int num) {
        arrList.add(num);
    }
    
    public int getProduct(int k) {
        int res = 1;
        int m = arrList.size();
        for(int i =1;i<=k;i++){
            res = res * arrList.get(m-i);
        }
        return res;
    }
}
```



### [C:最多可以参加的会议节目](<https://leetcode-cn.com/problems/maximum-number-of-events-that-can-be-attended/>)

##### 题目描述

给你一个数组 events，其中 events[i] = [startDayi, endDayi] ，表示会议 i 开始于 startDayi ，结束于 endDayi 。

你可以在满足 startDayi <= d <= endDayi 中的任意一天 d 参加会议 i 。注意，一天只能参加一个会议。

请你返回你可以参加的 最大 会议数目

##### 样例一

```
输入：events = [[1,2],[2,3],[3,4]]
输出：3
解释：你可以参加所有的三个会议。
安排会议的一种方案如上图。
第 1 天参加第一个会议。
第 2 天参加第二个会议。
第 3 天参加第三个会议。
```

##### 样例二

```
输入：events= [[1,2],[2,3],[3,4],[1,2]]
输出：4
```

##### 解析

这道题运用的是贪心的手法，

> 1、将这个二维数组按照最先结束的时间来进行升序排列
>
> ​		为什么按照最先结束的时间来呢，其实有三种方案选择，第一个就是最先开始的时间升序排列，第二个就是会议时间持续的长短（可能时间很晚，但是持续的时间非常短），第三个就是最先结束的时间。其实最先结束的时间就是第一种方案和第二种方案的总和。

> 2、先选择的就选掉了，后面没有的就只能算自己的福分不够了

##### 代码

```java


import java.util.Arrays;
import java.util.Comparator;
import java.util.HashSet;
import java.util.Set;

public class Main {


    public static int maxEvents(int[][] events) {
        Set<Integer> hashSet = new HashSet<Integer>();
        //数据不可重复，底层是由hashMap哈希表结构存储。
        //排序：就是将所有时间按照最后结束的时间来排序（ASC）,
        //如果最后结束的时间是相同的话，就按照最先开始的的升序排列就行了，sort默认是升序
        Arrays.sort(events, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                return o1[1] - o2[1];
            }
        });
        
        for (int[] event:events){
            int a = event[0];   //开始的天数
            int b = event[1];   //结束的天数
            for(int i = a;i<=b;i++){
                //从开始到结束，我要选择一个最早的开会时间，早点开完早点结束
                if(!hashSet.contains(i)){
                    hashSet.add(i);
                    break;
                }
            }
        }
        return hashSet.size();
    }
    public static void main(String[] args) {
        int[][] arr = {{1,4},{4,4},{2,2},{3,4},{1,1}};
        System.out.println(maxEvents(arr));

    }
}

```

### D题太难了，做不来，而且还看不懂，算了算了。



