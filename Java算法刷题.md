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









 

