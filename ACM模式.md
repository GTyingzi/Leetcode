## 1、输入数组

### 1、1 整数数组

例子：[Leetcode.977](https://leetcode-cn.com/problems/squares-of-a-sorted-array/)

<img src="https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042136783.png" style="zoom: 67%;" />

```java
public class Integer_array {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (sc.hasNext()){
            String[] split = sc.next().toString().split(",");
            int n = split.length;
            int[] nums = new int[n];
            for (int i = 0;i < n;i++){
                nums[i] = parseInt(split[i]);
            }

            //-------------------------------------
            int[] result = sortedSquares(nums);
            for (int i : result) {
                System.out.print( i + " ");
            }
        }
    }

    private static int[] sortedSquares(int[] nums) {
        int left = 0,right = nums.length -1;
        int[] result = new int[nums.length];
        int index = nums.length - 1;
        while (left <= right){
            if(nums[left] * nums[left] > nums[right] * nums[right]){
                result[index--] = nums[left] * nums[left];
                left++;
            }else{
                result[index--] = nums[right] * nums[right];
                right--;
            }
        }
        return result;
    }
}
```

### 1、2 字符串数组

[Leetcode.14](https://leetcode-cn.com/problems/longest-common-prefix/)

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042215838.png)

```java
public class String_array {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (true){
            String[] split = sc.next().toString().split(",");
            //---------------------------------------------------
            String s = longestCommonPrefix(split);
            System.out.println(s);
        }
    }

    public static String longestCommonPrefix(String[] strs){
        if(strs.length == 0) return "";

        int rows = strs.length;
        int cols = strs[0].length();

        for (int i=0; i<cols; i++){
            char firstChar = strs[0].charAt(i);
            for (int j=1; j<rows; j++){
                if(strs[j].length() == i || strs[j].charAt(i) != firstChar){
                    return strs[0].substring(0,i);
                }
            }
        }
        return strs[0];
    }
}
```

## 2、多行输入

### 2、1 整数数组+单个值

例子：[Leetcode704](https://leetcode-cn.com/problems/binary-search/)

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042223686.png)

```java
public class Multiple {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (true){
            String[] split = sc.next().toString().split(",");
            int k = sc.nextInt();
            int[] nums = new int[split.length];
            for (int i = 0; i < nums.length; i++) {
                nums[i] = parseInt(split[i]);
            }
            
            //------------------------------------------
            int search = search(nums, k);
            System.out.println(search);
        }
    }

    public static int search(int[] nums, int target) {
        // 避免当 target 小于nums[0] nums[nums.length - 1]时多次循环运算
        if (target < nums[0] || target > nums[nums.length - 1]) {
            return -1;
        }
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + ((right - left) >> 1);
            if (nums[mid] == target)
                return mid;
            else if (nums[mid] < target)
                left = mid + 1;
            else if (nums[mid] > target)
                right = mid - 1;
        }
        return -1;
    }
}
```

### 2、2 整数数组+整数数组

例题：[Leetcode.349](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042225402.png)

```java
public class Multiple2 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (true) {
            String[] split1 = sc.next().toString().split(",");
            String[] split2 = sc.next().toString().split(",");
            int[] nums1 = new int[split1.length];
            int[] nums2 = new int[split2.length];
            for (int i = 0; i < nums1.length; i++) {
                nums1[i] = parseInt(split1[i]);
            }
            for (int i = 0; i < nums2.length; i++) {
                nums2[i] = parseInt(split2[i]);
            }
            //------------------------------------------------
            int[] intersection = intersection(nums1, nums2);
            for (int i : intersection) {
                System.out.print(i + " ");
            }
        }
    }

    public static int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set1 = new HashSet<>();
        Set<Integer> resSet = new HashSet<>();

        // 遍历数组1
        for (int i : nums1){
            set1.add(i);
        }
        // 遍历数组2的过程判断哈希表中是否存在该元素
        for (int i : nums2){
            if (set1.contains(i)){
                resSet.add(i);
            }
        }
        // 将结果 集合转为 数组
        return resSet.stream().mapToInt(x -> x).toArray();
    }

}
```

## 3、链表

### 3、1 单链表

[Leetcode.206](https://leetcode-cn.com/problems/reverse-linked-list/)

<img src="https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042248561.png" style="zoom:67%;" />

```java
public class LinkList1 {

    static class ListNode{
        int val;
        ListNode next;
        ListNode(){}
        ListNode(int val){this.val = val;}
        ListNode(int val,ListNode next){this.val = val;this.next = next;}
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] split = sc.next().toString().split(",");
        ListNode pre = new ListNode(-1);
        ListNode head = pre;
        for (String s : split) {
            head.next = new ListNode(parseInt(s));
            head = head.next;
        }
        head = pre.next;

        //------------------------------------------
        ListNode head1 = reverseList(head);
        while (head1 != null){
            System.out.print(head1.val + " ");
            head1 = head1.next;
        }
    }
    public static ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode cur = head;
        ListNode temp = null;
        while (cur != null) {
            temp = cur.next;// 保存下一个节点
            cur.next = prev;
            prev = cur;
            cur = temp;
        }
        return prev;
    }

}
```



## 4、树

### 4、1 二叉树

[Leetcode.102](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042251484.png)

```java
public class Tree {

    static class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;

        public TreeNode() {
        }

        public TreeNode(int val) {
            this.val = val;
        }

        public TreeNode(int val, TreeNode left, TreeNode right) {
            this.val = val;
            this.left = left;
            this.right = right;
        }
    }

    public static void main(String[] args) {
        //输入
        Integer[] nums = new Integer[]{1, null, 4, null, null, 8, 2, null, null, null, null, null, null, 3, 6};
        //构建二叉树
        TreeNode root = createBT(nums, 1);

        //层序遍历二叉树
        List<List<Integer>> lists = levelOrder(root);
        for (List<Integer> list : lists) {
            System.out.print(list);
        }

    }

    //构建二叉树
    public static TreeNode createBT(Integer[] arr, int i) // 初始时,传入的i==1
    {
        if (i > arr.length) {// i >= arr.length 时,表示已经到达了根节点
            return null;
        }
        if (arr[i - 1] == null) return null;
        
        TreeNode root = new TreeNode(arr[i - 1]); // 根节点
        root.left = createBT(arr, 2 * i); // 递归建立左孩子结点
        root.right = createBT(arr, 2 * i + 1); // 递归建立右孩子结点

        return root;
    }


    //层序遍历
    public static List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        if (root != null) queue.offer(root);
        List<List<Integer>> resList = new ArrayList<>();

        while (!queue.isEmpty()) {
            int len = queue.size();
            List<Integer> tmpList = new ArrayList<>();

            while (len > 0) {
                TreeNode tmpNode = queue.poll();
                tmpList.add(tmpNode.val);

                if (tmpNode.left != null) queue.offer(tmpNode.left);
                if (tmpNode.right != null) queue.offer(tmpNode.right);
                len--;
            }
            resList.add(tmpList);
        }
        return resList;
    }
}
```





## 牛客练习区域---------------------------

https://ac.nowcoder.com/acm/contest/5657#question

### A+B（1）

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042139751.png)

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while(sc.hasNextInt()){
            int a = sc.nextInt();
            int b = sc.nextInt();
            System.out.println(a+b);
        }
    }
}
```

### A+B（2）

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042143653.png)

```java
import java.util.*;

public class Main{
    
    public static void main(String[] args){
        
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();
        while (t-- > 0){
            int a = sc.nextInt();
            int b = sc.nextInt();
            System.out.println(a + b);
        }
    }
}
```

### A+B（3）

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042148347.png)

```java
import java.util.*;

public class Main{
    
    public static void main(String[] args){
        
        Scanner sc = new Scanner(System.in);
        
        while (sc.hasNext()){
            int a = sc.nextInt();
            int b = sc.nextInt();
            
            if (a == 0 && b == 0) break;
            
            System.out.println(a + b);
        }
    }
}
```



### A+B（4）

<img src="https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042149839.png" style="zoom:67%;" />

```java
import java.util.*;

public class Main{
    
    public static void main(String[] args){
        
        Scanner sc = new Scanner(System.in);
        
        while (sc.hasNext()){
            int n = sc.nextInt();
            
            int sum = 0;
            if (n == 0) break;
            
            while (n-- > 0){
                int a = sc.nextInt();
                sum += a;
            }
            System.out.println(sum);
        }
    }
}
```

### A+B（5）

<img src="https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042153720.png" style="zoom:67%;" />

```java
import java.util.*;

public class Main{
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();
        
        while (t-- > 0){
            int n = sc.nextInt();
            int sum = 0;
            
            while (n-- > 0){
                int a = sc.nextInt();
                sum += a;
            }
            System.out.println(sum);
        }
    }
}
```

### A+B（6）

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042156607.png)

```java
import java.util.*;

public class Main{
    
    public static void main(String[] args){
        
        Scanner sc = new Scanner(System.in);
        
        while (sc.hasNext()){
            int n = sc.nextInt();
            
            int sum = 0;
            
            while (n-- > 0){
                int a = sc.nextInt();
                sum += a;
            }
            System.out.println(sum);
        }
    }
}
```



### A+B（7）***

<img src="https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042158279.png" style="zoom:67%;" />

```java
import java.util.*;

public class Main{
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        
        while (sc.hasNext()){
            String[] s = sc.nextLine().split(" ");
            int sum = 0;
            for (int i = 0;i < s.length;i++){
                sum += Integer.parseInt(s[i]);
            }
            System.out.println(sum);
        }
    }
}
```

### 字符串排序（1）

<img src="https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042201489.png" style="zoom:67%;" />

```java
import java.util.*;

public class Main{
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        sc.nextLine();
        
        String[] s = sc.nextLine().split(" ");
        Arrays.sort(s);
        for (String str : s){
            System.out.print(str + " ");
        }
    }
}
```

### 字符串排序（2）

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042204366.png)

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while (sc.hasNext()){
            String[] s = sc.nextLine().split(" ");
            Arrays.sort(s);
            for (String str : s){
                System.out.print(str + " ");
            }
            System.out.println();
        }
    }
}
```

### 字符串排序（3）

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042205206.png)

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while (sc.hasNext()){
            String[] s = sc.nextLine().split(",");
            Arrays.sort(s);
            for (int i = 0;i < s.length;i++){
                if (i < s.length - 1){
                    System.out.print(s[i] + ",");
                }else {
                    System.out.print(s[i]);
                }
            }
            System.out.println();
        }
    }
}
```

### 注意事项

![](https://yingziimage.oss-cn-beijing.aliyuncs.com/img/202303042213670.png)

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while (sc.hasNext()){
            String[] s = sc.nextLine().split(" ");
            Long sum = 0L;
            for (String str : s){
                sum += Long.parseLong(str);
            }
            System.out.println(sum);
        }
    }
}
```

