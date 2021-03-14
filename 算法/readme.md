
[小浩算法](https://www.geekxh.com/)

[小浩微信网页](https://mp.weixin.qq.com/s/3eJNKDTZ5y5icMnfv9Is_w)

[geekxh](https://github.com/geekxh/hello-algorithm)

[TOP 48 算法和编程面试题](https://mp.weixin.qq.com/s/eKrdrW-KaF-am7MXpNQnXA)

[labuladong的算法小炒](https://labuladong.gitbook.io/algo/)

[labuladong算法github](https://github.com/labuladong/fucking-algorithm)

[DuHouAn/Java](https://github.com/DuHouAn/Java)

[LeetCodeAnimation](https://github.com/MisterBooo/LeetCodeAnimation)

[剑指☞offer](https://github.com/todorex/Coding-Interviews)

[剑指offer视频](https://github.com/ljz756245026/jianzhi-offer-code-videos)

## 二叉堆
```
二叉堆就是一种完全二叉树，所以适合存储在数组中，而且二叉堆拥有一些特殊性质。
二叉堆的操作很简单，主要就是上浮和下沉，来维护堆的性质（堆有序），核心代码也就十行。
优先级队列是基于二叉堆实现的，主要操作是插入和删除。
**插入**是先插到最后，然后上浮到正确位置；
**删除**是调换位置后再删除，然后下沉到正确位置
```
## LRU
[LRU](https://github.com/labuladong/fucking-algorithm/blob/master/%E9%AB%98%E9%A2%91%E9%9D%A2%E8%AF%95%E7%B3%BB%E5%88%97/LRU%E7%AE%97%E6%B3%95.md)
实现原理是HashMap+双向列表的结合体，即：LinkedHashMap
- 1、如果我们每次默认从链表尾部添加元素，那么显然越靠尾部的元素就是最近使用的，越靠头部的元素就是最久未使用的。
- 2、对于某一个 key，我们可以通过哈希表快速定位到链表中的节点，从而取得对应 val。
- 3、链表显然是支持在任意位置快速插入和删除的，改改指针就行。只不过传统的链表无法按照索引快速访问某一个位置的元素，而这里借助哈希表，可以通过 key 快速映射到任意一个链表节点，然后进行插入和删除。

![put操作流程](https://github.com/labuladong/fucking-algorithm/blob/master/pictures/LRU%E7%AE%97%E6%B3%95/put.jpg)

```
class Node {
    public int key, val;
    public Node next, prev;
    public Node(int k, int v) {
        this.key = k;
        this.val = v;
    }
}

class DoubleList {  
    // 头尾虚节点
    private Node head, tail;  
    // 链表元素数
    private int size;
    
    public DoubleList() {
        // 初始化双向链表的数据
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
        size = 0;
    }

    // 在链表尾部添加节点 x，时间 O(1)
    public void addLast(Node x) {
        x.prev = tail.prev;
        x.next = tail;
        tail.prev.next = x;
        tail.prev = x;
        size++;
    }

    // 删除链表中的 x 节点（x 一定存在）
    // 由于是双链表且给的是目标 Node 节点，时间 O(1)
    public void remove(Node x) {
        x.prev.next = x.next;
        x.next.prev = x.prev;
        size--;
    }
    
    // 删除链表中第一个节点，并返回该节点，时间 O(1)
    public Node removeFirst() {
        if (head.next == tail)
            return null;
        Node first = head.next;
        remove(first);
        return first;
    }

    // 返回链表长度，时间 O(1)
    public int size() { return size; }

}
```

## 移动零
【移动零】(https://leetcode-cn.com/problems/move-zeroes/)
```
class Solution {
    public void moveZeroes(int[] nums) {
        int j = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                if (i > j) {
                    nums[j] = nums[i];
                    nums[i] = 0;
                }
                j++;
            }
        }
    }
}
```

## 爬楼梯 斐波那契数列
【爬楼梯】(https://leetcode.com/problems/climbing-stairs/)

【解题思路】

![解题思路](./20210312121934.jpg)
```
public class Solution {
    public int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        int first = 1;
        int second = 2;
        for (int i = 3; i <= n; i++) {
            int third = first + second;
            first = second;
            second = third;
        }
        return second;
    }
}
```
## 盛最多水的容器
【盛最多水的容器】(https://leetcode-cn.com/problems/container-with-most-water/)
```
class Solution {
    public int maxArea(int[] height) {
        int maxArea = 0;
        for(int i = 0;i<height.length - 1; i++){
            for(int j = i+1;j<height.length; j++){
                int area = (j - i) * Math.min(height[i],height[j]);
                maxArea = Math.max(area,maxArea);
            }
        }
        return maxArea;
    }
}

class Solution {
    public int maxArea(int[] height) {
        int maxArea = 0;
        for(int i = 0, j = height.length - 1;i < j;){
            int minHeight = height[i] < height[j] ? height[i++] : height[j--];
            int tempArea = (j - i + 1) * minHeight;
            maxArea = Math.max(maxArea,tempArea);
        }
        return maxArea;
    }
}
```
## 三数之和
【三数之和】(https://leetcode-cn.com/problems/3sum/)
```
//暴力
private List<List<Integer>> directlySolution(int[] nums) {
    if (nums == null || nums.length <= 2) {
        return Collections.emptyList();
    }
    Arrays.sort(nums);
    Set<List<Integer>> result = new LinkedHashSet<>();
    for (int i = 0; i < nums.length; i++) {
        for (int j = i+1; j < nums.length; j++) {
            for (int k = j+1; k < nums.length; k++) {
                if (nums[i] + nums[j] + nums[k] == 0) {
                    List<Integer> value = Arrays.asList(nums[i], nums[j], nums[k]);
                    result.add(value);
                }
            }
        }
    }

    return new ArrayList<>(result);
}
//夹逼
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        for(int k = 0; k < nums.length - 2; k++){
            if(nums[k] > 0) break;
            if(k > 0 && nums[k] == nums[k - 1]) continue;
            int i = k + 1, j = nums.length - 1;
            while(i < j){
                int sum = nums[k] + nums[i] + nums[j];
                if(sum < 0){
                    while(i < j && nums[i] == nums[++i]);
                } else if (sum > 0) {
                    while(i < j && nums[j] == nums[--j]);
                } else {
                    res.add(new ArrayList<Integer>(Arrays.asList(nums[k], nums[i], nums[j])));
                    while(i < j && nums[i] == nums[++i]);
                    while(i < j && nums[j] == nums[--j]);
                }
            }
        }
        return res;
    }
}
```
