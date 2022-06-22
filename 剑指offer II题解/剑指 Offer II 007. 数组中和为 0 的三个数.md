#### [剑指 Offer II 007. 数组中和为 0 的三个数](https://leetcode.cn/problems/1fGaJU/)

给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a ，b ，c ，使得 a + b + c = 0 ？请找出所有和为 0 且 不重复 的三元组。

**示例 1：**

~~~
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
~~~

**示例 2：**

~~~
输入：nums = []
输出：[]
~~~

**示例 3：**

~~~
输入：nums = [0]
输出：[]
~~~

**提示：**

~~~
0 <= nums.length <= 3000
-105 <= nums[i] <= 105
~~~



#### 题解：

思路：固定一个下标，再用双指针遍历下标后面的所有元素

~~~java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>>list=new ArrayList<>();
        int len=nums.length;
        // 根据题意，小于3的直接返回
        if(len<3){
            return list;
        }

        // 先把数组排序
        Arrays.sort(nums);

        for(int i=0;i<len-2;++i){
            // 当前元素和前一个元素一样，则没必要再找了，避免重复
            if(i>0&&nums[i]==nums[i-1]){
                continue;
            }
        
            int left=i+1;   // 左指针为i后面的第一个指针
            int right=len-1;    // 右指针指向末尾元素
            int target=-nums[i];    // 因为nums[i]+nums[left]+nums[right]=0，也就是只需nums[left]+nums[right]=-nums[i]即可
            while(left<right){
                int sum=nums[left]+nums[right];
                if(sum==target){
                    list.add(Arrays.asList(nums[i],nums[left],nums[right]));
                    // 为了避免重复寻找，若当前元素等于之前找过的元素，则跳过
                    while (left < right && nums[left] == nums[++left]);
                    while (left < right && nums[right] == nums[--right]);
                }else if(sum<target){
                    left++;
                }else{
                    right--;
                }
            }
        }
        return list;
    }
}
~~~

时间复杂度：O(n^2)

分析：快速排序时间复杂度为O(nlogn)，双指针遍历复杂度为O(n^2)，最终即为O(n^2)

空间复杂度：O(logN)

分析：快速排序的空间复杂度为O(logn)