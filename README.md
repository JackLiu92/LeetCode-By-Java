# LeetCode-By-Java
> cLeetCode解题的Java实现
> 
[**1.数组**](#Array)

#### <a name="Array"></a> Array

##### 1. Two Sum

>Given an array of integers, return indices of the two numbers such that they add up to a specific target.

>You may assume that each input would have exactly one solution, and you may not use the same element twice.

>Example:

>Given nums = [2, 7, 11, 15], target = 9,

>Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].


思路为利用哈希表储存想要结果的索引. 代码为:

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> resultMap = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
        		int sub = target - nums[i];
        		if (resultMap.containsKey(sub)) {
        			int result = resultMap.get(sub);
        			return new int[]{result, i};
        		} else {
        			resultMap.put(nums[i], i);	
			}
        }
        return new int[]{-1, -1};
    }
}
```

如果测试数据的在一定范围内,如`2047`之内, 可以用数组代替哈希表, 优化搜索时间. 其中`nums[i]) & t`保证值不大于`t`即`2047`.

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        short t = 2047;
        short arr[] = new short[2048];
        for(short i = 0,numsLength=(short)nums.length; i <numsLength ; ++i){
            short diff = (short)((target - nums[i]) & t);
            if(arr[diff] != 0)
                return new int[]{
                        arr[diff] - 1, i
                };
            
            arr[nums[i] & t] = (short)(i+1);
        }
        return new int[]{0, 0};
    }
}
```

