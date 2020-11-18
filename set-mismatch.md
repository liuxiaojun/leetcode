## 错误的集合
集合 S 包含从1到 n 的整数。不幸的是，因为数据错误，导致集合里面某一个元素复制了成了集合里面的另外一个元素的值，导致集合丢失了一个整数并且有一个元素重复。
给定一个数组 nums 代表了集合 S 发生错误后的结果。你的任务是首先寻找到重复出现的整数，再找到丢失的整数，将它们以数组的形式返回。

示例 1:
```
输入: nums = [1,2,2,4]
输出: [2,3]
```
注意:

给定数组的长度范围是 [2, 10000]。
给定的数组是无序的。


## 暴力解法
最直接的做法就是单独检查 11 到 nn 的所有数字。在检查每个数字时都遍历整个 numsnums 数组，检查当前数字在 numsnums 中是否出现了两次，或者一次都没有出现。使用 dupdup 和 missingmissing 记录重复数字和缺失数字。
```
public class Solution {
    public int[] findErrorNums(int[] nums) {
        int dup = -1, missing = -1;
        for (int i = 1; i <= nums.length; i++) {
            int count = 0;
            for (int j = 0; j < nums.length; j++) {
                if (nums[j] == i)
                    count++;
            }
            if (count == 2)
                dup = i;
            else if (count == 0)
                missing = i;
        }
        return new int[] {dup, missing};
    }
}
```
* 时间复杂度：O(n^2)O(n2)，在 11 到 nn 的每个数字上，都需要遍历一次 numsnums。
* 空间复杂度：O(1)O(1)，使用恒定的额外空间。

## 使用排序
排序 numsnums 数组后，相等的两个数字将会连续出现。此外，检查相邻的两个数字是否只相差 1 可以找到缺失数字。
```
public class Solution {
    public int[] findErrorNums(int[] nums) {
        Arrays.sort(nums);
        int dup = -1, missing = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1])
                dup = nums[i];
            else if (nums[i] > nums[i - 1] + 1)
                missing = nums[i - 1] + 1;
        }
        return new int[] {dup, nums[nums.length - 1] != nums.length ? nums.length : missing};
    }
}
```
## 使用Map
吧1到n 分别放到的map的key中，遍历数组，遇到key的对应value加1，
然后判断value的数值即可
