# [LeetCode周赛176](<https://leetcode-cn.com/contest/weekly-contest-176>)

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



