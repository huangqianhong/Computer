# [小q想撸串](<https://ac.nowcoder.com/acm/contest/696/A>)

### 题目描述 

​    小Q挺喜欢撸串的，没错，字符串！

​    你给小Q送上了n个字符串

​    对于一个字符串s，如果在小Q撸掉(删除)任意个字符之后，"NowCoder"是其子串，则这个字符串s是可撸的。小Q最近切题切到手软，想撸串散散心。如果你给他呈现的字符串是可撸的，他会很开心，否则他会很桑心。

### 输入描述:

```
一个整数n，表示字符串的数量 

接下来每行一个字符串s_isi，表示小Q看到的第i个字符串
```

### 输出描述:

```
输出有n行，如果小Q开心他会说QAK，否则他会说QIE
```

示例1

## 输入

复制

```
2
NowCoder
NoowCoder
```

## 输出

复制

```
QAK
QAK
```

## 说明

```
第一个字符串不需要撸掉任何字符
第二个字符串撸掉第二个或者第三个都可以
```

示例2

## 输入

复制

```
5
Nowcoder
nowcoder
NowCoder
NowoowCoder
NOI2019NowCoder
```

## 输出

复制

```
QIE
QIE
QAK
QAK
QAK
```

## 备注:

```java
对于50\%50%的数据，满足n=1 , 1\leq |S_i|\leq 10n=1,1≤∣Si∣≤10
对于100\%100%的数据，满足n\leq 10^5 , 1\leq|s_i|\leq 100n≤105,1≤∣si∣≤100
```

### 大仙的个人想法

关于题目的我:把问题想复杂了，我真的太难了qaq~~我是一个没有读懂中文体面的蒟蒻，理值气也壮.jpg~~；

首先我们他只要求我们存在newcoder这个几个字符，并且是按照顺序来的就okk了。

上代码：

```java


import java.util.Scanner;

public class Main {
    static String [] arr;
    static boolean[] vis;
    static String finalStr = "NowCoder";
    static boolean flag = true;
    public static boolean panduan(String s){
        int index =0;
        for(int i =0;i<s.length();i++){
            if(finalStr.charAt(index)==s.charAt(i)){
                index++;
            }
        }
        return index==finalStr.length();
    }
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int n = cin.nextInt();
        arr = new String[n];
       for(int i =0;i<n;i++){
           String str = cin.next();
           if(panduan(str)){
               System.out.println("QAK");
           }else {
               System.out.println("QIE");
           }
       }
        cin.close();
    }
}

```

# [小L的序列]()

### 大仙的个人看法

 这题主要用的是进制的转换，这几题的难度都不是特别大，接下来要对进制转换和判断需要多家联系，自己还是特别菜

```


import java.util.Scanner;

public class Main {
    static int n;
    static int[] arr;
//    static int[] res;
    public static boolean panduan(int k){
        int res1 = 0;
        int res0 = 0;
//
        while(k!=0){
            if(k%2==0)
                res0++;
            else
                res1++;
            k/=2;
        }
//        System.out.println(res);

        return res1>res0;
    }
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        n = cin.nextInt();
//        arr = new int[n];
        int sum = 0;
        for(int i =0;i<n;i++){
         int    a = cin.nextInt();
            if(panduan(a)){
                sum++;
            }else {
                sum--;
            }

        }
        System.out.println(sum);
        cin.close();
    }
}

```

