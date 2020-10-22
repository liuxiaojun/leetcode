给定一个整数数组nums和一个目标值target，请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。   
你可以假设没中输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。  

```
给定 nums=[2,7,11,15]
target=9

因为nums[0]+nums[1]=2+7=9
所以返回[0,1]
```


##  暴力枚举
思路和方法： 最容易想到的是枚举数组中的每个数x, 寻找数组中是否存在 target-x  
当我们遍历整个数组的方式寻找 target-x 时, 需要注意到每一个位于x 之前的元素都已经和x匹配过,因此不需要再进行匹配。 而每一个元素不能被使用两次,所以只需要在x后面的元素寻找 target-x  

代码：  
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int n = nums.length;
        for (int i = 0; i < n; ++i) {
            for (int j = i + 1; j < n; ++j) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return new int[0];
    }
}
```
* 时间复杂度： O(N2)，其中 NN 是数组中的元素数量。最坏情况下数组中任意两个数都要被匹配一次。
* 空间复杂度：O(1)

## 哈希表
上面的暴力枚举的时间复杂度较高的原因是在寻找 target-x 的时间复杂度过高。因此, 我们需要一种更好的方法，能够快速寻找数组中是否存在目标元素。 如果存在，需要找出它的索引。  
使用哈希表，可以将target-x的时间复杂度从O(N)降到O(1) 

创建一个哈希表，对于每一个x，首先查询哈希表中是否存在target-x, 然后将x插入到哈希表中,即可保证不会让x和自己匹配
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> hashtable = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; ++i) {
            if (hashtable.containsKey(target - nums[i])) {
                return new int[]{hashtable.get(target - nums[i]), i};
            }
            hashtable.put(nums[i], i);
        }
        return new int[0];
    }
}
```
时间复杂度： O(N)，其中 NN 是数组中的元素数量。对于每一个元素 x，我们可以 O(1)O(1) 地寻找 target-x  
空间复杂度： O(N)，其中 NN 是数组中的元素数量。主要为哈希表的开销

