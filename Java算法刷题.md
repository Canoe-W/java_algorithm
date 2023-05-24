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



###  归并排序

分治

1. 确定分界点 mid=(l+r)/2
2. 递归排序 left,right mergesort(q,l,mid) mergesort(q,mid+1,r)
3. 归并 合二为一
   1. 在归并过程中为了保持稳定性，两个值相同时，选择前面那个加入

#### 787.归并排序

```
给定你一个长度为 n的整数数列。
请你使用归并排序对这个数列按照从小到大进行排序。并将排好序的数列按顺序输出。

输入格式
输入共两行，第一行包含整数 n。
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
    public static void main(String[] args)throws IOException{
        InputStreamReader in=new InputStreamReader(System.in);
        BufferedReader buf=new BufferedReader(in);
        int n=Integer.parseInt(buf.readLine());
        String[] res=buf.readLine().split(" ");
        int[] q=new int[n];
        for(int i=0;i<n;i++){
            q[i]=Integer.parseInt(res[i]);
        }
        mergesort(q,0,n-1);
        for(int i=0;i<n;i++){
            System.out.print(q[i]+" ");
        }
        buf.close();
    }
    public static void mergesort(int[] q,int l,int r){
        if(l>=r) return;
        int mid=l+((r-l)>>1);
        mergesort(q,l,mid);
        mergesort(q,mid+1,r);
        int i=l,j=mid+1;
        int count=0;
        int[] temp=new int[r-l+1];//在归并过程中，注意数组大小
        while(i<=mid&&j<=r){
            if(q[i]<=q[j]) temp[count++]=q[i++];
            else temp[count++]=q[j++];
        }
        while(i<=mid) temp[count++]=q[i++];
        while(j<=r) temp[count++]=q[j++];
        for(i=l,j=0;i<=r;i++,j++){
            q[i]=temp[j];
        }
    } 
}
```



#### 788.逆序对的数量



```
给定一个长度为 n的整数数列，请你计算数列中的逆序对的数量。
逆序对的定义如下：对于数列的第 i个和第 j 个元素，如果满足 i<j 且 a[i]>a[j]，则其为一个逆序对；否则不是。

输入格式
第一行包含整数 n，表示数列的长度。第二行包含 n个整数，表示整个数列。

输出格式
输出一个整数，表示逆序对的个数。

数据范围
1≤n≤100000，数列中的元素的取值范围 [1,109]。

输入样例：
6
2 3 4 5 6 1

输出样例：
5
```



暴力解法会超时

分治，归并排序，在合并阶段，比较两个区间的数的大小，将右边区间的数和左边的进行比较，两端都是非降序，所以比一个可以判断之后的，锁定右边，找左边第一个比它大的，然后算个数，然后右边往后挪，用前一个的左边开始算，同时也要合并入新的数组排序



merge_sort() 归并排序与逆序对统计：

    1.终止条件：当l≥r 时，代表子数组长度为 1 ，此时终止划分；
    2.递归划分：计算数组中点m ，递归划分左子数组 merge_sort(l, m) 和右子数组 merge_sort(m + 1, r) ；
    3.合并与逆序对统计：
        1.暂存数组nums 闭区间[i,r] 内的元素至辅助数组tmp ；
        2.循环合并： 设置双指针i,j 分别指向左 / 右子数组的首元素；
            当i=m+1 时： 代表左子数组已合并完，因此添加右子数组当前元素 tmp[j]，并执行j=j+1 ；
            否则，当j=r+1 时： 代表右子数组已合并完，因此添加左子数组当前元素 tmp[i]，并执行i=i+1 ；
            否则，当tmp[i]≤tmp[j] 时：添加左子数组当前元素 tmp[i]，并执行i=i+1；
            否则（即tmp[i]>tmp[j]）时：添加右子数组当前元素 tmp[j]，并执行j=j+1 ；此时构成m−i+1个「逆序对」，统计添加至res ；
    4.返回值： 返回直至目前的逆序对总数res ；



题解：

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main{
    
    public static void main(String[] args)throws IOException{
        InputStreamReader in=new InputStreamReader(System.in);
        BufferedReader buf=new BufferedReader(in);
        int n=Integer.parseInt(buf.readLine());
        String[] res=buf.readLine().split(" ");
        int[] q=new int[n];
        
        for(int i=0;i<n;i++){
            q[i]=Integer.parseInt(res[i]);
        }
        long result=mergesort(q,0,n-1);
        System.out.print(result);
        buf.close();
    }
    public static long mergesort(int[] q,int l,int r){
        if(l>=r) return 0;
        int mid=l+((r-l)>>1);
        long res=mergesort(q,l,mid)+mergesort(q,mid+1,r);
        int i=l,j=mid+1,count=0;
        int[] temp=new int[r-l+1];//在归并过程中，注意数组大小
        while(i<=mid&&j<=r){
            if(q[i]<=q[j]) temp[count++]=q[i++];
            else {
                temp[count++]=q[j++];
                res+=mid-i+1;
            }
        }
        while(i<=mid) temp[count++]=q[i++];
        while(j<=r) temp[count++]=q[j++];
        for(i=l,j=0;i<=r;i++,j++){
            q[i]=temp[j];
        }
        return res;
    } 
}
```

注意点

```java
1.数据大小，需要用long来存
2.初始化上可以更完善
	eg.
		    static int N = 100010;  // 数据规模为 10w
    		static int[] arr = new int[N];
    		在psvm之外，然后在函数调用中就不需要再传arr了，就是自己的代码中的q
3.在数据的归并上有另一种做法
  这里直接有一个一样长的数组tmp来做替换缓冲，tmp存的是分开排序后的，nums存的是归并排序后的，并且在每一次递归都重新的写入一次这次递归区间的tmp来做归并。
class Solution {
    int[] nums, tmp;
    public int reversePairs(int[] nums) {
        this.nums = nums;
        tmp = new int[nums.length];
        return mergeSort(0, nums.length - 1);
    }
    private int mergeSort(int l, int r) {
        // 终止条件
        if (l >= r) return 0;
        // 递归划分
        int m = (l + r) / 2;
        int res = mergeSort(l, m) + mergeSort(m + 1, r);
        // 合并阶段
        int i = l, j = m + 1;
        for (int k = l; k <= r; k++)
            tmp[k] = nums[k];
        for (int k = l; k <= r; k++) {
            if (i == m + 1)
                nums[k] = tmp[j++];
            else if (j == r + 1 || tmp[i] <= tmp[j])
                nums[k] = tmp[i++];
            else {
                nums[k] = tmp[j++];
                res += m - i + 1; // 统计逆序对
            }
        }
        return res;
    }
}
```



### 二分查找

分为左半边和右半边

eg.右边满足某种性质，左边不满足，进行一个划分

去找那个左右两个分界点

第一种

```
mid=(l+r+1)/2
if(check(mid))
	true: [mid,r] l=mid
	false:[l,mid-1] r=mid-1
这里的check(mid)是针对是否满足左边的性质来看的
所以true的时候mid可能是边界点，在下一次查询中要包含，接着看右边
false的时候一定不是边界点，所以下一次不包含，回看这个点左边
+1是因为l=r-1时，如果mid=(l+r)/2=l，if true l=l陷入死循环
```

第二种

```
mid=(l+r)/2
if(check(mid))
	true:[l,mid] r=mid
	flase:[mid+1,r] l=mid+1
这里的check检查的是否满足右半边，满足则可能是边界点，下次查询包含，看这个点和左边
不满足则不是边界点，下次不包含，直接看右边
```



```java
//区间[l,r]划分为[l,mid]和[mid+1,r]时使用：
int bsearch_1(int l,int r){
    while(l<r)//判断条件
    {
        int mid=l+r>>1;
        if(check(mid)) r=mid;
        else l=mid+1;
    }
    return l;
}
//区间[l,r]划分为[l,mid-1]和[mid,r]使用
int bsearch_2(int l,int r){
    while(l<r){
        int mid=l+r+1>>1;
        if(check(mid)) l=mid;
        else r=mid-1;
    }
    return l;
}
```





#### 789.数的范围

```
给定一个按照升序排列的长度为 n 的整数数组，以及 q个查询。
对于每个查询，返回一个元素 k的起始位置和终止位置（位置从 0开始计数）。
如果数组中不存在该元素，则返回 -1 -1。

输入格式
第一行包含整数 n和 q，表示数组长度和询问个数。
第二行包含 n个整数（均在 1∼10000范围内），表示完整数组。
接下来 q行，每行包含一个整数 k，表示一个询问元素。

输出格式
共 q行，每行包含两个整数，表示所求元素的起始位置和终止位置。
如果数组中不存在该元素，则返回 -1 -1。

数据范围
1≤n≤100000
1≤q≤10000
1≤k≤10000

输入样例：
6 3
1 2 2 3 3 4
3
4
5

输出样例：
3 4
5 5
-1 -1
```



题解：

```java
import java.io.*;
import java.util.*;

public class Main {
    static final int N = 100010;
    static int[] a = new int[N];

    public static void main(String[] args) throws IOException {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String[] s1 = in.readLine().split(" ");
        int n = Integer.parseInt(s1[0]);
        int q = Integer.parseInt(s1[1]);
        String[] s2 = in.readLine().split(" ");
        for(int i = 0; i < n; i ++) a[i] = Integer.parseInt(s2[i]);

        while(q -- > 0) {
            int k = Integer.parseInt(in.readLine());
            int l = 0, r = n - 1;
            while(l < r) {
                int mid = l + r >> 1;
                if(a[mid] >= k) r = mid;
                else l = mid + 1;
            }
            if(a[l] != k) System.out.println("-1 -1");
            else {
                int left = l;
                l = 0;
                r = n - 1;
                while(l < r) {
                    int mid = l + r + 1 >> 1;
                    if(a[mid] <= k) l = mid;
                    else r = mid -1;
                }
                System.out.println(left + " " + l);
            }
        }
    }
}
```

重点

```
在查找两个边界的时候看边界满足的要求是什么
比如左边界的要求时右边都大于等于x
右边界的要求是左边都小于等于x
这种左右的划分要求我们在进行mid的计算的时候要区分什么时候+1,算右边界的时候要+1
自己的方法不知道为什么超出时间限制
以后补充：
```

自己的题解

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;
public class Main{
    static int N=10010;
    static int n,q;
    public static void main(String[] args) throws IOException{
        BufferedReader buf=new BufferedReader(new InputStreamReader(System.in));
        String[] res1=buf.readLine().split(" ");
        n=Integer.parseInt(res1[0]);
        q=Integer.parseInt(res1[1]);
        int[] nums=new int[n];
        String[] res2=buf.readLine().split(" ");
        for(int i=0;i<n;i++){
            nums[i]=Integer.parseInt(res2[i]);
        }
        while(q-->0){
            
            int x=Integer.parseInt(buf.readLine());
            int l=0,r=n-1;
            while(l<r){
                //System.out.println("l"+l);
                int mid=l+r>>1;
                if(nums[mid]>=x) r=mid;
                else l=mid+1;
            }
            if(nums[l]<x) System.out.println("-1 -1");
            else {
                System.out.print(l+" ");
                int l2=0,r2=n-1;
                while(l2<r2){
                    //System.out.println("l2"+l2);
                    int mid2=l2+r2+1>>1;
                    while(l2<r2){
                        if(nums[mid2]<=x) l2=mid2;
                        else r2=mid2-1;
                    }
                    System.out.println(l2);
                }
            }
        }
        buf.close();
    }
}
```



#### 790.数的三次方根

```
给定一个浮点数 n，求它的三次方根。

输入格式
共一行，包含一个浮点数 n。

输出格式
共一行，包含一个浮点数，表示问题的解。
注意，结果保留 6位小数。

数据范围
−10000≤n≤10000

输入样例：
1000.00

输出样例：
10.000000
```



二分法，判断这个根是比目标值大还是小

```java
import java.util.Scanner;

public class Main{
    public static void main(String[] args){
        double x;
        Scanner sc=new Scanner(System.in);
        x=sc.nextDouble();
        double l=-10000,r=Math.max(1,Math.abs(x));
        while(r-l>10e-8){
            double mid=(l+r)/2;
            if(mid*mid*mid>=Math.abs(x)) r=mid;
            else l=mid;
        }
       if (x >= 0)
            System.out.println(String.format("%.6f", l)); // 保留 6位小数
        else
            System.out.println("-" + String.format("%.6f", l));
    }
}
```



注意点

```
1.取绝对值判断，之后再看符号
2.对于小于1的值，在取右边界的时候要取1，所以有一个对比r=Math.max(1,Math.abs(x))
3.找根，判断三次方位置，比给定值大，则要取的值在现在的左边，这一点不q
```



### 高精度

#### 高精度加法

````
题目描述

给定两个正整数（不含前导 0），计算它们的和。


输入格式

共两行，每行包含一个整数。


输出格式

共一行，包含所求的和。


数据范围

1≤整数长度≤100000


输入样例：

```
12
23
```
输出样例：

```
35
```
````



思路

加法计算是从低位逐渐相加，向高位进位，所以将数的每一位拆开对齐计算，利用数组或者vector，反向存储，比如12345存储在容器里面就是54321，然后从低位相加，高位进位。

注意点：

```

存放结果的也是容器，在低位相加时进1则提前在高位放入1防止下一位加数不存在但是有进位
也可以实时进位，不需要先存完再算

Java中有两个类可以来处理高精度的计算

分别是处理整数的BigInteger和处理小数的BigDecimal
BigInteger 只可用于整数

构造方法

BigInteger(byte[] val) 
将包含BigInteger的二进制补码二进制表达式的字节数组转换为BigInteger 
BigInteger(int numBits, Random rnd) 
构造一个随机生成的BigInteger，均匀分布在0到（2 numBits - 1）的范围内。  
BigInteger(String val) 
将BigInteger的十进制字符串表示形式转换为BigInteger。   

```







代码：

```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Main{
    public static void main(String[] args){
        Scanner scanner=new Scanner(new BufferedInputStream(System.in));
        String a=scanner.next();
        String b=scanner.next();
        int aLength=a.length()-1;
        int bLength=b.length()-1;
        List<Integer> list=new ArrayList<>((int)(1e6+10));
        int carry=0;//进位
        int max=Math.max(aLength,bLength)+1;
        while(max-->0){
            int x=aLength<0?0:a.charAt(aLength)-'0';
            int y=bLength<0?0:b.charAt(bLength)-'0';
            int sum=x+y+carry;
            list.add(sum%10);
            carry=sum/10;
            aLength--;
            bLength--;
            
        }
        if(carry!=0) list.add(1);
        for(int i=list.size()-1;i>=0;i--){
            System.out.print(list.get(i));
        }
        
    }
}
```





#### 高精度减法

```
给定两个正整数（不含前导 0），计算它们的差，计算结果可能为负数。

输入格式
共两行，每行包含一个整数。

输出格式
共一行，包含所求的差。
数据范围

1≤整数长度≤105

输入样例：

32
11

输出样例：

21

```



思路

```
先比较AB的大小
A>B A-B
A<B -(B-A)
然后类同加法，每一位从低位开始运算，有一个向上的借位t
Ai-Bi-t
>=0 Ai-Bi-t
<0  Ai-Bi+10-t
简化为（t+10)%10
```



代码

```java
import java.util.Scanner;
import java.util.List;
import java.util.ArrayList;

public class Main{
    public static void main(String[] args){
        Scanner scanner =new Scanner(System.in);
        String a=scanner.next();
        String b=scanner.next();
        List<Integer> A = new ArrayList<>();
        List<Integer> B = new ArrayList<>();
        for(int i=a.length()-1;i>=0;i--) A.add(a.charAt(i)-'0');
        for(int i=b.length()-1;i>=0;i--) B.add(b.charAt(i)-'0');
        if(!cmp(A,B)){
            System.out.print("-");
        }
        List<Integer> C=sub(A,B);
        for(int i=C.size()-1;i>=0;i--){
            System.out.print(C.get(i));
        }
    }
    public static List<Integer> sub(List<Integer> A,List<Integer> B){
        if(!cmp(A,B)){
            return sub(B,A);
        }
        
        List<Integer> C=new ArrayList<>();
        for(int i=0,t=0;i<A.size();i++){
            t=A.get(i)-t;
            if(i<B.size()) t-=B.get(i);
            C.add((t+10)%10);
            if(t<0) t=1;
            else t=0;
        }
        while(C.size()>1&&C.get(C.size()-1)==0) C.remove(C.size()-1);
        return C;
    }
    public static boolean cmp(List<Integer> A,List<Integer> B){
        if(A.size()!=B.size()) return A.size()>B.size();
        for(int i=A.size()-1;i>=0;i--){
            if(A.get(i)!=B.get(i)){
                return A.get(i)>B.get(i);
            }
        }
        return true;
    }
}
```



#### 高精度乘法

```
给定两个非负整数（不含前导 0） A 和 B，请你计算 A×B的值。

输入格式
共两行，第一行包含整数 A，第二行包含整数 B。

输出格式
共一行，包含 A×B的值。

数据范围
1≤A的长度≤100000,
0≤B≤10000

输入样例：
2
3

输出样例：
6

```



思路

```
高精度×低精度
用高精度的每一位去×低精度整个数
然后个位保留，其他的进位
所以在保留的过程中要加上前一次计算的进位再%10
```



代码

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        String a=scanner.next();
        int b=scanner.nextInt();
        List<Integer> A=new ArrayList<>();
        for(int i=a.length()-1;i>=0;i--){
            A.add(a.charAt(i)-'0');
        }
        List<Integer> C=mul(A,b);
        for(int i=C.size()-1;i>=0;i--){
            System.out.print(C.get(i));
        }
        
    }
    
    public static List<Integer> mul(List<Integer> A,int b){
        List<Integer> C=new ArrayList<>();
        int t=0;
        for(int i=0;i<A.size()||t!=0;i++){
            if(i<A.size()) t+=A.get(i)*b;
            C.add(t%10);
            t/=10;
            
        }
        while(C.size()>1&&C.get(C.size()-1)==0) C.remove(C.size()-1);
        //这里其实可以在代码最开头加一个特判是不是有0
        return C;
    }
    
}
```



#### 高精度除法



```
给定两个非负整数（不含前导 0） A，B，请你计算 A/B的商和余数。

输入格式
共两行，第一行包含整数 A，第二行包含整数 B。

输出格式
共两行，第一行输出所求的商，第二行输出所求余数。

数据范围
1≤A的长度≤100000,
1≤B≤10000,
B 一定不为 0

输入样例：
7
2

输出样例：
3
1

```



思路

```
从高位开始除，前一次的余数×10再加这一位进行除法
```



代码

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner scanner =new Scanner(System.in);
        String a=scanner.next();
        int b=scanner.nextInt();
        List<Integer> A=new ArrayList<>(a.length());
        for(int i=a.length()-1;i>=0;i--) A.add(a.charAt(i)-'0');
        List<Integer> C=div(A,b);
        for(int i=C.size()-2;i>=0;i--) System.out.print(C.get(i));
        
        System.out.println();
        System.out.print(C.get(C.size()-1));
    }
    public static List<Integer> div(List<Integer> A,int b){
        List<Integer> C=new ArrayList<>();
        int r=0;
        for(int i=A.size()-1;i>=0;i--){
            r=r*10+A.get(i);
            C.add(r/b);
            r%=b;
        }
        Collections.reverse(C);
        while(C.size()>1&&C.get(C.size()-1)==0) C.remove(C.size()-1);
        C.add(r);
        return C;
        }
}
```







#### 高精度汇总——java特用（ 不可用于赛事



加法 add( )



    import java.math.BigInteger;
    import java.io.*;
    
    public class Main {
        public static void main(String[] args) throws IOException{
            BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
    
            BigInteger a = new BigInteger(reader.readLine());
            BigInteger b = new BigInteger(reader.readLine());
            System.out.println(a.add(b));
            reader.close();
        }
    }


减法 subtract( )

import java.io.*;
import java.math.BigInteger;

public class Main {

    public static void main(String[] args) throws IOException{
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        BigInteger a = new BigInteger(reader.readLine());
        BigInteger b = new BigInteger(reader.readLine());
        System.out.println(a.subtract(b));
        reader.close();
    }
}

乘法 multiply( )

import java.io.*;
import java.math.BigInteger;

public class Main {

    public static void main(String[] args) throws IOException{
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        BigInteger a = new BigInteger(reader.readLine());
        BigInteger b = new BigInteger(reader.readLine());
        System.out.println(a.multiply(b));
        reader.close();
    }
}

除法 divideAndRemainder( )

import java.io.*;
import java.math.BigInteger;

public class Main {

    public static void main(String[] args) throws IOException{
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        BigInteger a = new BigInteger(reader.readLine());
        BigInteger b = new BigInteger(reader.readLine());
        //divide 返回值为 a/b
        BigInteger[] c = a.divideAndRemainder(b); //返回值为数组，分别为a/b和a%b
        System.out.println(c[0]);
        System.out.println(c[1]);
        reader.close();
    }
}

取余 mod( )



    import java.io.*;
    import java.math.BigInteger;
    
    public class Main {
        public static void main(String[] args) throws IOException {
            BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
            BigInteger a = new BigInteger(reader.readLine());
            BigInteger b = new BigInteger(reader.readLine());
            System.out.println(a.mod(b));
            reader.close();
        }
    }




BigDecimal 处理浮点数运算

构造方法

BigDecimal(char[] in) 
一个转换的字符数组表示 BigDecimal成 BigDecimal ，接受字符作为的相同序列 BigDecimal(String)构造。  
BigDecimal(char[] in, int offset, int len) 
一个转换的字符数组表示 BigDecimal成 BigDecimal ，接受字符作为的相同序列 BigDecimal(String)构造，同时允许一个子阵列被指定。    
BigDecimal(double val) 
将 double转换为 BigDecimal ，这是 double的二进制浮点值的精确十进制表示 
BigDecimal(int val)
将 int成 BigDecimal
BigDecimal(long val) 
将 long成 BigDecimal
BigDecimal(String val)  

加法 add( )



    import java.io.*;
    import java.math.BigDecimal;
    
    public class Main {
        public static void main(String[] args) throws IOException {
            BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
            BigDecimal a = new BigDecimal(reader.readLine());
            BigDecimal b = new BigDecimal(reader.readLine());
            System.out.println(a.add(b));
            reader.close();
        }
    }


取余 remainder( )



    import java.io.*;
    import java.math.BigDecimal;
    
        public class Main {
        public static void main(String[] args) throws IOException {
            BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
            BigDecimal a = new BigDecimal(reader.readLine());
            BigDecimal b = new BigDecimal(reader.readLine());
            System.out.println(a.remainder(b));
            reader.close();
        }
    }


除法 divide( )



    import java.io.*;
    import java.math.BigDecimal;
    
        public class Main {
        public static void main(String[] args) throws IOException {
            BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
            BigDecimal a = new BigDecimal(reader.readLine());
            BigDecimal b = new BigDecimal(reader.readLine());
            System.out.println(a.divide(b));
            reader.close();
        }
    }



## 前缀和与差分



#### 前缀和

```
输入一个长度为 n的整数序列。
接下来再输入 m个询问，每个询问输入一对 l,r。
对于每个询问，输出原序列中从第 l个数到第 r个数的和。

输入格式
第一行包含两个整数 n和 m。第二行包含 n个整数，表示整数数列。
接下来 m行，每行包含两个整数 l 和 r，表示一个询问的区间范围。

输出格式
共 m行，每行输出一个询问的结果。

数据范围

1≤l≤r≤n,
1≤n,m≤100000,
−1000≤数列中元素的值≤1000

输入样例：

5 3
2 1 3 6 4
1 2
1 3
2 4

输出样例：

3
6
10

```



思路

```
实时计算到第i个数时累计大小
a[i]从a[1]开始
s[i]有s[0]=0,后面也是从s[1]开始
s[i]=s[i-1]+a[i]
这个并不固定，根据自己习惯来
然后数组大小可以定一个比最大长度大的就行
计算[l,r]区间的和时s[r]-s[l-1]
```







代码

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner scanner=new Scanner(System.in);
        int n=scanner.nextInt();
        int m=scanner.nextInt();
        int[] M=new int[100010];
        int[] S=new int[100010];
        S[0]=0;
        for(int i=0;i<n;i++){
            M[i]=scanner.nextInt();
            S[i+1]=S[i]+M[i];
        }
        int l,r;
        while(m!=0){
            m--;
            l=scanner.nextInt();
            r=scanner.nextInt();
            System.out.println(S[r]-S[l-1]);
            
        }
    }
}
```







#### 子矩阵的和

```
输入一个 n 行 m 列的整数矩阵，再输入 q 个询问，每个询问包含四个整数 x1,y1,x2,y2，表示一个子矩阵的左上角坐标和右下角坐标。
对于每个询问输出子矩阵中所有数的和。

输入格式
第一行包含三个整数 n，m，q。
接下来 n行，每行包含 m个整数，表示整数矩阵。
接下来 q行，每行包含四个整数 x1,y1,x2,y2，表示一组询问。

输出格式
共 q行，每行输出一个询问的结果。

数据范围
1≤n,m≤1000,
1≤q≤200000,
1≤x1≤x2≤n,
1≤y1≤y2≤m,
−1000≤矩阵内元素的值≤1000

输入样例：

3 4 3
1 7 2 4
3 6 2 8
2 1 2 3
1 1 2 2
2 1 3 4
1 3 3 4

输出样例：

17
27
21

```

思路

```
有点类似求面积
交叠的地方减两次后再加一次重复的
每一次算前缀和则是竖着加横着减去重叠再加这个点
前缀和
s[i][j]=s[i-1][j]+s[i][j-1]-s[i-1][j-1]
子矩阵的和
[x1,y1][x2,y2]=s[x2][y2]-s[x1-1][y2]-s[x2][y1-1]+s[x1-1][y1-1]
```



代码

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner scanner=new Scanner(System.in);
        int n=scanner.nextInt();
        int m=scanner.nextInt();
        int q=scanner.nextInt();
        
        int[][] a=new int[n+1][m+1];
        int[][] s=new int[n+1][m+1];
        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                a[i][j]=scanner.nextInt();
                s[i][j]=a[i][j]+s[i-1][j]+s[i][j-1]-s[i-1][j-1];
            }
        }
        int x1,y1,x2,y2,res;
        while(q!=0){
            q--;
            x1=scanner.nextInt();
            y1=scanner.nextInt();
            x2=scanner.nextInt();
            y2=scanner.nextInt();
            res=s[x2][y2]-s[x1-1][y2]-s[x2][y1-1]+s[x1-1][y1-1];
            System.out.println(res);
        }
    }
}
```

