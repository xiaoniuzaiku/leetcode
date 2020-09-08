<<<<<<< HEAD
# 剑指offer题解

### [一.树和栈](树和栈.md)





=======
# Introduction



| Title-Link                                                   | Method | Describe                                                     | TODO           |
| ------------------------------------------------------------ | ------ | ------------------------------------------------------------ | -------------- |
| [面试题26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/) | Tree   | 输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构) | 利用遍历和递归 |
| [面试题27. 二叉树的镜像](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/) | Tree   | 数的镜像，题解：利用递归交换子树                             |                |

## [面试题26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)

```java
class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        return (A!=null&&B!=null)&&(recur(A,B)||isSubStructure(A.left,B)||isSubStructure(A.right,B));
    }
    boolean recur(TreeNode A,TreeNode B){
        if(B==null)return true;
        if(A==null||A.val!=B.val)return false;
        return recur(A.left,B.left)&&recur(A.right,B.right);
    }

}
```

利用遍历和递归，递归结束的条件是：如果B为空，则遍历结束返回true，如果A！=B的值则返回false，接着遍历。主函数利用前序遍历，来判断子树是否成立。

#### [面试题09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

```java
class CQueue {
    Stack<Integer> in;
    Stack<Integer> out;
    int size;

    public CQueue() {
        in=new Stack<Integer>();
        out=new Stack<Integer>();
        size=0;
    }
    
    public void appendTail(int value) {
        in.push(value);
        size++;
    }
    
    public int deleteHead() {
        if(size==0)
        return -1;
        if(out.isEmpty()){
            while(!in.isEmpty())
            out.push(in.pop());
        }
        size--;
        return out.pop();
    }
}

```

两个栈一个负责出队列，一个负责入队列，特别注意出队列时要判断out栈是否为空。

#### [面试题54. 二叉搜索树的第k大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

给定一棵二叉搜索树，请找出其中第k大的节点。

树的另外一种形式的后序遍历。

#### [面试题55 - II. 平衡二叉树](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root==null)
        return true;
        return Math.abs(deep(root.left)-deep(root.right))<=1&&isBalanced(root.left)&&isBalanced(root.right);
    }
    //树的深度函数
    int deep(TreeNode root){
        if(root==null)
        return 0;
        return Math.max(deep(root.left),deep(root.right))+1;
    }
}
```

题解：还是利用递归，和先序遍历，先判断当前左右子树的深度是否符合要求，在判断左右子树是否为平衡二叉树。

#### [面试题68 - I. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root==null)
        return null;
        if(p.val<root.val&&q.val<root.val)
        return lowestCommonAncestor(root.left,p,q);
        if(p.val>root.val&&q.val>root.val)
        return lowestCommonAncestor(root.right,p,q);
        return root;
    }
}
```

题解：利用递归，搜索二叉树，如果两个节点都在右边，那么就向右递归，两个节点都在左边，那么久向左递归。

重点在于看两个节点是否在根节点的两边。

#### [面试题68 - II. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left == null && right == null) return null;
        else if(left != null && right != null) return root;
        else return left == null ? right : left;
    }
}
```

#### [面试题30. 包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

 设置两个栈，一个用来存储，另外一个用来存储最小值。

#### [面试题59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums == null || nums.length < 2) return nums;
        // 双向队列 保存当前窗口最大值的数组位置 保证队列中数组位置的数值按从大到小排序
        LinkedList<Integer> queue = new LinkedList();
        // 结果数组
        int[] result = new int[nums.length-k+1];
        // 遍历nums数组
        for(int i = 0;i < nums.length;i++){
            // 保证从大到小 如果前面数小则需要依次弹出，直至满足要求
            while(!queue.isEmpty() && nums[queue.peekLast()] <= nums[i]){
                queue.pollLast();
            }
            // 添加当前值对应的数组下标
            queue.addLast(i);
            // 判断当前队列中队首的值是否有效
            if(queue.peek() <= i-k){
                queue.poll();   
            } 
            // 当窗口长度为k时 保存当前窗口中最大值
            if(i+1 >= k){
                result[i+1-k] = nums[queue.peek()];
            }
        }
        return result;
    }
}

```

单调队列的典型应用，重点在与判断队列队首的值是否有效
>>>>>>> ec764c4f14b48a2ee393a0241d7b7be341e62c68
