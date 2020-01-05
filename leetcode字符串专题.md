题外话：大仙还是个菜鸡啊，啥都不会，菜的一批，希望各位大佬多多提携，本蒟蒻在这里先膜各位大佬为敬。

# 1、[Leetcode13 罗马数字转整数 简单](<https://leetcode-cn.com/problems/roman-to-integer/>)

题解：一开始我就想直接遍历~~本人只会遍历\大哭.jpg~~，每一次遍历将其中的一个字符存起来（数组）也可以用hashmap存储，然后到时候在进行遍历，但是没有考虑特殊情况，所以我就凉凉

这六种特殊情况不是一锤子买卖的，而是每一次遇到“I”,"X","C"这三个字符，都要去判断其后面的字符是否存在特殊情况。其他的就最简单的枚举，最后要注意边界~~踩过坑~~

```java
public class Main {
    public static void main(String[] args){
        Scanner cin = new Scanner(System.in);
        String str = cin.next();
        System.out.println(romanToInt(str));
    }
    //其中的一个小难点:就是把里面的特殊化给去掉
    public static int romanToInt(String s) {
        int sum = 0;

        int arr[] = new int [7];
        for(int i =0;i<s.length();i++){
            switch (s.charAt(i)){
                case 'I':
                    if(i+1<s.length() && s.charAt(i+1)=='V'){		//小老弟，别越界哈
                        sum += 4;
                        i++;
                        break;
                    }
                    if(i+1<s.length() &&s.charAt(i+1)=='X'){
                        sum += 9;
                        i++;
                        break;
                    }
                    arr[0]++;									//选中了就放进数组里面去，和hashmap同样的道理
                    break;
                case 'V':
                    arr[1]++;
                    break;
                case 'X':
                    if(i+1<s.length() &&s.charAt(i+1)=='L'){
                        sum += 40;
                        i++;
                        break;
                    }
                    if(i+1<s.length() &&s.charAt(i+1)=='C'){
                        sum += 90;
                        i++;
                        break;
                    }
                    arr[2]++;
                    break;
                case 'L':
                    arr[3]++;
                    break;
                case 'C':
                    if(i+1<s.length() &&s.charAt(i+1)=='D'){
                        sum += 400;
                        i++;
                        break;
                    }
                    if(i+1<s.length() &&s.charAt(i+1)=='M'){
                        sum += 900;
                        i++;
                        break;
                    }
                    arr[4]++;
                    break;
                case 'D':
                    arr[5]++;
                    break;
                case 'M':
                    arr[6]++;
                    break;
            }
        }

        int k = 1;
        boolean f = true;
        for(int i =0;i<7;i++){
            sum = sum + k*arr[i];
//            if(f){
//                k = k*5;
//            }else{
//                k = k*2;
//            }
             k = f?(k*5):(k*2);
            f = !f;
        }



            return sum;
    }

}
```



2、[LeetCode20:有效的括号](<https://leetcode-cn.com/problems/valid-parentheses/>)

题解：我一开始的思路是计数器的方式，但是这样是不行的，因为这样不合法（例如：{ ( [ ) ] }）

这样无法让括号合法,最后自己看题解去了，然后发现是栈这东西，而且还利用了hashmap来存储数据。

```java
public class Main {
    //首先用一个数组来表示是否被使用过
    //hashMap的几个方法需要了解一下
    //stack中的数据是如何解决的
    public static  void main(String[] args){
        Scanner cin = new Scanner(System.in);
        String str = cin.next();
        System.out.println(isValid(str));
    }
    public static boolean isValid(String s) {
        HashMap<Character,Character> map = new HashMap<>();
        map.put(')','(');
        map.put(']','[');
        map.put('}','{');

        Stack<Character>  stack = new Stack<>();
        for(char c:s.toCharArray()){
            //判断是否包含hashmap里面的key里面的value，
            //即（【{
            //
            if(!map.containsKey(c)){
                stack.add(c);       //默认添加valUe

            }else{
                //你包含了{【（,但是你的栈里面却什么都没有，铁定凉凉
                if(stack.size() == 0){
                    return false;
                }
                char h  = stack.pop();
                if(h!= map.get(c)){
                    return false;
                }

            }
        }
        return stack.empty()?true:false;

    }
}

```

题解明天来补/xk，睡觉睡觉，刚不动了。。。。。