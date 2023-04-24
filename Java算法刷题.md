# 剑指Offer简单版

## DAY3

### 替换空格

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

示例 1：

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

注意点：

Java中string是不可变类型 ，需要使用StringBuilder，获取原字符串需要使用 toCharArary()函数

```java
class Solution {
    public String replaceSpace(String s) {
        StringBuilder res=new StringBuilder();
        for(Character c:s.toCharArray()){
            if(c==' '){
                res.append("%20");
            }
            else{
                res.append(c);
            }
        }
        return res.toString();
        }
        
    
}
```



### 左旋转字符串

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

示例 1：

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

示例 2：

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```



```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        StringBuilder res=new StringBuilder();
        StringBuilder temp=new StringBuilder();
        int count=0;
        for(Character c:s.toCharArray()){
            if(count!=n){
                count++;
                temp.append(c);
            }
            else{
                res.append(c);
            }
        }
        res.append(temp.toString());
        return res.toString();

    }
}
```

## DAY4

### 数组中重复的数字

找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：

```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```



使用Set

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> dic = new HashSet<>();
        for(int num : nums) {
            if(dic.contains(num)) return num;
            dic.add(num);
        }
        return -1;
    }
}
```



## DAY5

### 第一次只出现一次的字符

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

示例 1:

```
输入：s = "abaccdeff"
输出：'b'
```

示例 2:

```
输入：s = "" 
输出：' '
```

tips:HashMap和LinkedHahMap

```java
class Solution {
    public char firstUniqChar(String s) {
        Map<Character,Boolean> dic=new LinkedHashMap<>();
        char[] sc=s.toCharArray();
        for(char c: sc){
            dic.put(c,!dic.containsKey(c));
        }
        for(Map.Entry<Character,Boolean> d: dic.entrySet()){
            if(d.getValue()) return d.getKey();
        }
        return ' ';
    }
}
```

Entry是Map的元素对象，Map由Entry组合而成，表示一个键值对，Map集合通过entrySet()方法转换成的这个set集合，set集合中元素的类型是Map.Entry<K,V>，Map.Entry和String一样，都是一种类型的名字，只不过Map.entry是静态内部类，是Map中的

















# 春招备战热身

## DAY3 

### 用栈实现队列

请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（push、pop、peek、empty）：

实现 MyQueue 类：

    void push(int x) 将元素 x 推到队列的末尾
    int pop() 从队列的开头移除并返回元素
    int peek() 返回队列开头的元素
    boolean empty() 如果队列为空，返回 true ；否则，返回 false

说明：

    你 只能 使用标准的栈操作 —— 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。
    你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。

示例 1：

```
输入：
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 1, 1, false]
```

解释：

```
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```

提示：

    1 <= x <= 9
    最多调用 100 次 push、pop、peek 和 empty
    假设所有操作都是有效的 （例如，一个空的队列不会调用 pop 或者 peek 操作）







# ACWING算法基础课

## 基础算法

### 快速排序

指定一个数，比他大的放在后面，比他小的放在前面

中间如果遇到不符合规定的数

则将后面第一个比他小的数和前面第一个比他大的数进行交换，以此类推，最终定下这个数在哪个位置

然后再以这个数为分界线，前后再进行快速排序

eg

```java
public static void quicksort(int[] q,int l,int j){
    if(l>=r) return;
    int x=q[(l+r)>>1];//防止边界出问题
    int i=l-1;
    int j=r+1;
    while(i<j){
        do i++;while(q[i]<x);
        do j--;while(q[j]>x);
        if(i<j) {
            int temp=q[i];
            q[i]=q[j];
            q[j]=temp;
        }//在这里被指定的那个数会在这个过程中分在左侧或者右侧，总的来说是左右两侧满足一个大小关系的，具体的位置会定在交界处，但是交界处不一定是那个数，只是前k个小数和后g个大数。
    }
    quicksort(q,l,j);//这种传参可以防止边界出问题
    quicksort(q,j+1,r);
}
```

需要注意的是在java中参数传的是引用，所以会直接造成影响。

#### 785.快速排序

```java
给定你一个长度为 n的整数数列。

请你使用快速排序对这个数列按照从小到大进行排序。

并将排好序的数列按顺序输出。
输入格式

输入共两行，第一行包含整数 n
第二行包含 n个整数（所有整数均在 1∼109范围内），表示整个数列。

输出格式
输出共一行，包含 n个整数，表示排好序的数列。
    
数据范围
1≤n≤100000
    
输入样例：
5
3 1 2 4 5
    
输出样例：
1 2 3 4 5

```

题解：

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
public class Main{
    
    public static void quicksort(int[] q,int l,int r){
        if(l>=r) return;
        int x=q[(l+r)>>1];
        int i=l-1;
        int j=r+1;
        while(i<j){
            do i++; while(q[i]<x);
            do j--; while(q[j]>x);
            if(i<j){
                int t=q[i];
                q[i]=q[j];
                q[j]=t;
            }
        }
        quicksort(q,l,j);
        quicksort(q,j+1,r);
    } 
    public static void main(String[] args) throws IOException{
        InputStreamReader in = new InputStreamReader(System.in);
        BufferedReader buf = new BufferedReader(in);
        int n=Integer.parseInt(buf.readLine());
        String[] res=buf.readLine().split(" ");
        int[] q=new int[n];
        for(int i=0;i<n;i++){
            q[i]=Integer.parseInt(res[i]);
        }
        quicksort(q,0,n-1);
        for(int i=0;i<n;i++){
            System.out.print(q[i]+" ");
        }
        buf.close();
    }
}

```



这里要注意的是

```java
1.java的输入输出使用bufferedReader更快
    InputStreamReader in = new InputStreamReader(System.in);
    BufferedReader buf = new BufferedReader(in);
使用上，读的是字节流转字符流，所以要转化为Integer类型
    int n=Integer.parseInt(buf.readLine());
    String[] res=buf.readLine().split(" ");
    int[] q=new int[n];
    for(int i=0;i<n;i++){
        q[i]=Integer.parseInt(res[i]);
    }
2.JAVA函数传参是引用，要注意在函数里面设置
```



#### 786.第k个数

```
给定一个长度为 n 的整数数列，以及一个整数 k，请用快速选择算法求出数列从小到大排序后的第 k个数。

输入格式
第一行包含两个整数 n和 k。
第二行包含 n个整数（所有整数均在 1∼109范围内），表示整数数列。

输出格式
输出一个整数，表示数列的第 k小数。

数据范围
1≤n≤100000,
1≤k≤n

输入样例：
5 3
2 4 1 5 3

输出样例：
3

```



```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
public class Main{
    
    public static void quicksort(int[] q,int l,int r,int k){
        if(l>=r) return;
        int x=q[(l+r)>>1];
        int i=l-1;
        int j=r+1;
        while(i<j){
            do i++; while(q[i]<x);
            do j--; while(q[j]>x);
            if(i<j){
                int t=q[i];
                q[i]=q[j];
                q[j]=t;
            }
        }
        if(j>=k-1)
        quicksort(q,l,j,k);
        else
        quicksort(q,j+1,r,k);
    } 
    public static void main(String[] args) throws IOException{
        InputStreamReader in = new InputStreamReader(System.in);
        BufferedReader buf = new BufferedReader(in);
        String[] res1=buf.readLine().split(" ");
        int n=Integer.parseInt(res1[0]);
        int k=Integer.parseInt(res1[1]);
        String[] res=buf.readLine().split(" ");
        int[] q=new int[n];
        for(int i=0;i<n;i++){
            q[i]=Integer.parseInt(res[i]);
        }
        quicksort(q,0,n-1,k);
        System.out.print(q[k-1]);
        buf.close();
    }
}
```

主要是是看k在前面还是后面哪一段，对这一段进行快速排序

细节

```java
1.第k个数，下标是k-1,所以判断边界的时候要看j和k-1的关系，j>=k-1则quicksort(q,l,j,k)包含下标k-1，否则选择(j+1,r)段
if(j>=k-1)
        quicksort(q,l,j,k);
        else
        quicksort(q,j+1,r,k);
```



 

