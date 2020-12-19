# 官方题解
## 法一：哈希表
```java
class Solution {
    private Map<Integer, Integer> countNums(int[] nums) {
        Map<Integer, Integer> counts = new HashMap<Integer, Integer>();
        for (int num : nums) {
            if (!counts.containsKey(num)) {
                counts.put(num, 1);
            } else {
                counts.put(num, counts.get(num) + 1);
            }
        }
        return counts;
    }

    public int majorityElement(int[] nums) {
        Map<Integer, Integer> counts = countNums(nums);

        Map.Entry<Integer, Integer> majorityEntry = null;
        for (Map.Entry<Integer, Integer> entry : counts.entrySet()) {
            if (majorityEntry == null || entry.getValue() > majorityEntry.getValue()) {
                majorityEntry = entry;
            }
        }

        return majorityEntry.getKey();
    }
}
```
```
执行用时：19 ms, 在所有 Java 提交中击败了13.03%的用户
内存消耗：43.6 MB, 在所有 Java 提交中击败了28.80%的用户
```
时间复杂度：O(n)  
空间复杂度：O(n)

## 法二：排序
```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length / 2];
    }
}
```
```
执行用时：2 ms, 在所有 Java 提交中击败了75.79%的用户
内存消耗：41.4 MB, 在所有 Java 提交中击败了95.51%的用户
```
时间复杂度：O(nlogn)  
空间复杂度：O(logn)

## 法三：随机化
```java
class Solution {
    private int randRange(Random rand, int min, int max) {
        return rand.nextInt(max - min) + min;
    }

    private int countOccurences(int[] nums, int num) {
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == num) {
                count++;
            }
        }
        return count;
    }

    public int majorityElement(int[] nums) {
        Random rand = new Random();

        int majorityCount = nums.length / 2;

        while (true) {
            int candidate = nums[randRange(rand, 0, nums.length)];
            if (countOccurences(nums, candidate) > majorityCount) {
                return candidate;
            }
        }
    }
}
```
```
执行用时：2 ms, 在所有 Java 提交中击败了75.79%的用户
内存消耗：44.3 MB, 在所有 Java 提交中击败了5.03%的用户
```
时间复杂度：理论上最坏情况下的时间复杂度为O(∞)，期望的时间复杂度为 O(n)。  
空间复杂度：O(1)

## 法四：分治
```java
class Solution {
    private int countInRange(int[] nums, int num, int lo, int hi) {
        int count = 0;
        for (int i = lo; i <= hi; i++) {
            if (nums[i] == num) {
                count++;
            }
        }
        return count;
    }

    private int majorityElementRec(int[] nums, int lo, int hi) {
        // base case; the only element in an array of size 1 is the majority
        // element.
        if (lo == hi) {
            return nums[lo];
        }

        // recurse on left and right halves of this slice.
        int mid = (hi - lo) / 2 + lo;
        int left = majorityElementRec(nums, lo, mid);
        int right = majorityElementRec(nums, mid + 1, hi);

        // if the two halves agree on the majority element, return it.
        if (left == right) {
            return left;
        }

        // otherwise, count each element and return the "winner".
        int leftCount = countInRange(nums, left, lo, hi);
        int rightCount = countInRange(nums, right, lo, hi);

        return leftCount > rightCount ? left : right;
    }

    public int majorityElement(int[] nums) {
        return majorityElementRec(nums, 0, nums.length - 1);
    }
}
```
```
执行用时：2 ms, 在所有 Java 提交中击败了75.79%的用户
内存消耗：44.3 MB, 在所有 Java 提交中击败了5.03%的用户
```
时间复杂度：O(nlogn)  
空间复杂度：O(logn)

## 法五：Boyer-Moore 投票算法
如果候选人不是maj，则maj会和其他非候选人一起反对 会反对候选人，所以候选人一定会下台（maj==0时发生换届选举）。  
如果候选人是maj，则maj会支持自己，其他候选人会反对，同样因为maj票数超过一半，所以maj一定会成功当选。
```java
class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        Integer candidate = null;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }
}
```
```
执行用时：3 ms, 在所有 Java 提交中击败了43.75%的用户
内存消耗：44.2 MB, 在所有 Java 提交中击败了8.76%的用户
```
时间复杂度：O(n)  
空间复杂度：O(1)
