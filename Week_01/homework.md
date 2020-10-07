# 第一周作业
## 11. 盛最多水的容器  https://leetcode-cn.com/problems/container-with-most-water/

```java
    public int maxArea(int[] height) {
        int i = 0;
        int j = height.length - 1;
        int res = 0;
        while (i != j) {

            int v = (j - i) * Math.min(height[i], height[j]);
            if (v > res) {
                res = v;
            }
            if (height[i] > height[j]) {
                j--;
            } else {
                i++;
            }

        }
        return res;
    }

```

## 283. 移动零  https://leetcode-cn.com/problems/move-zeroes/

```java
    public void moveZeroes(int[] nums) {
        int j = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                if (i != j) {
                    nums[j] = nums[i];
                    nums[i] = 0;
                }
                j++;
            }
        }
    }

```

## 70. 爬楼梯 https://leetcode-cn.com/problems/climbing-stairs

```java 
    public int climbStairs(int n) {
        int[] res = new int[n + 2];
        res[0] = 0;
        res[1] = 1;
        res[2] = 2;
        for (int i = 3; i <= n; i++) {
            res[i] = res[i - 1] + res[i - 2];
        }
        return res[n];
    }

```

## 1. 两数之和  https://leetcode-cn.com/problems/two-sum/
```
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> res = new HashMap<>();
        int num = -1;
        for (int i = 0; i < nums.length; i++) {
            num = target - nums[i];
            if (res.containsKey(num)) {
                int value = res.get(num);
                if (value != i) {
                    return new int[]{i, value};
                }
            }
            res.put(nums[i], i);
        }
        return new int[]{};
    }
```

## 15. 三数之和 https://leetcode-cn.com/problems/3sum/

```java
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> results = new ArrayList();
        // 判断长度是否足够
        if (nums == null || nums.length < 3) {
            return results;
        }
        Arrays.sort(nums);
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            if (nums[i] > 0) {
                // 大于0 必然没有结果
                break;
            }
            if (i > 0 && nums[i] == nums[i - 1]) {
                // 去重
                continue;
            }
            int L = i + 1;
            int R = len - 1;

            while (L < R) {
                int sum = nums[i] + nums[L] + nums[R];
                if (sum == 0) {
                    // 添加结果到数组
                    results.add(Arrays.asList(nums[i], nums[L], nums[R]));

                    while (L < R && nums[L] == nums[L + 1]) {
                        L++;
                        // 去重
                    }
                    while (L < R && nums[R] == nums[R - 1]) {
                        R--;
                        // 去重
                    }
                    L++;
                    R--;
                } else if (sum < 0) {
                    L++;
                    // 结果小于0 表示左侧下标过小
                } else if (sum > 0) {
                    // 结果大于0 表示右侧下标过大
                    R--;
                }
            }
        }
        return results;
    }
```


## 206. 反转链表  https://leetcode-cn.com/problems/reverse-linked-list/

```java
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode current = head;

        while (current != null) {
            // 获取下一个节点
            ListNode tem = current.next;
            // 设置当前节点的下一个节点为之前的上一个节点
            current.next = prev;
            // 将上一个节点记录下来
            prev = current;
            // 记录当前节点的下一个节点，用于下次迭代
            current = tem;
        }
        return prev;
    }



    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        // 递归到最后的节点
        ListNode cur = reverseList(head.next);
        // 将当前节点的下一个的下一个节点设置为当前的节点对象
        head.next.next = head;
        // 断开当前 节点的下一个节点的链接
        head.next = null;
        // 返回当前节点对象
        return cur;
    }

```

## 24. 两两交换链表中的节点  https://leetcode-cn.com/problems/swap-nodes-in-pairs/

```java

    public ListNode swapPairs(ListNode head) {
        ListNode prev = new ListNode(0);
        prev.next = head;
        ListNode cur = prev;

        while (cur.next != null && cur.next.next != null) {
            ListNode firstNode = cur.next;
            ListNode secendNode = cur.next.next;
            cur.next = secendNode;
            firstNode.next = secendNode.next;
            secendNode.next = firstNode;
            cur = firstNode;
        }

        return prev.next;
    }

```

## 141. 环形链表 https://leetcode-cn.com/problems/linked-list-cycle/
```java

  public boolean hasCycle(ListNode head) {

        // 哈希表

        Set<ListNode> map = new HashSet<>();

        ListNode curr = head;
        while (curr != null) {
            if (map.contains(curr)) {
                return true;
            }
            map.add(curr);
            curr = curr.next;
        }
        return false;

        // 快慢指针
//
//        if (head == null || head.next == null) {
//            return false;
//        }
//        ListNode slow = head;
//        ListNode fast = head.next;
//        while (slow != fast) {
//            if (fast == null || fast.next == null) {
//                return false;
//            }
//            slow = slow.next;
//            fast = fast.next.next;
//        }
//        return true;
    }

```

## 142. 环形链表 II https://leetcode-cn.com/problems/linked-list-cycle-ii/

```java
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            // 快慢指针
            slow = slow.next;
            fast = fast.next.next;
            //找到环形点
            if (slow == fast) {
                break;
            }
        }
        // 判断是否到了尾指针了
        if (fast == null || fast.next == null) {
            return null;
        }

        fast = head;
        // 开始计算索引
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        return fast;
    }
```


## 25. K 个一组翻转链表  https://leetcode-cn.com/problems/reverse-nodes-in-k-group/

```java
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || head.next == null) {
            return head;
        }
        // 定义一个临时头节点
        ListNode dummy = new ListNode(-1);
        // 将临时节点链接起来
        dummy.next = head;
        // 记录上一次的翻转的头结点的上一个节点和尾节点
        ListNode pre = dummy, end = dummy;
        // 循环下一次节点
        while (end.next != null) {
            // 记录尾节点
            for (int i = 0; i < k && end != null; i++) {
                end = end.next;
            }
            // 如果节点数量不够K的倍数。终止翻转
            if (end == null) {
                break;
            }
            // 记录下一次的翻转的头部节点。也就是要链接的后序头结点
            ListNode next = end.next;
            // 断开链接。要准备开始翻转了
            end.next = null;
            // 记录要翻转的头部节点
            ListNode start = pre.next;
            // 翻转链表，并链接头节点
            pre.next = reverse(start);
            // 链接尾节点
            start.next = next;
            // 记录下次要链接的头部节点.为翻转前的头节点。也就是翻转后的尾节点。进行下次链接使用
            pre = start;
            // 翻转结束。记录下次要开始翻转的头部节点，就是翻转前的头节点。翻转后的尾节点。进行下次循环。
            end = start;
        }
        // 返回新的链表对象头
        return dummy.next;
    }


    /**
     * 翻转链表
     *
     * @param head
     * @return
     */
    private static ListNode reverse(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        // 前指针
        ListNode pre = null;
        // 当前对象
        ListNode curr = head;
        while (curr != null) {
            ListNode tem = curr.next;
            curr.next = pre;
            pre = curr;
            curr = tem;
        }
        return pre;
    }
```