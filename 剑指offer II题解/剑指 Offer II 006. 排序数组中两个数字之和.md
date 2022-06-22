#### [剑指 Offer II 006. 排序数组中两个数字之和](https://leetcode.cn/problems/kLl5u1/)

给定一个已按照 升序排列  的整数数组 numbers ，请你从数组中找出两个数满足相加之和等于目标数 target 。

函数应该以长度为 2 的整数数组的形式返回这两个数的下标值。numbers 的下标 从 0 开始计数 ，所以答案数组应当满足 0 <= answer[0] < answer[1] < numbers.length 。

假设数组中存在且只存在一对符合条件的数字，同时一个数字不能使用两次。

**示例 1：**

~~~java
输入：numbers = [1,2,4,6,10], target = 8
输出：[1,3]
解释：2 与 6 之和等于目标数 8 。因此 index1 = 1, index2 = 3 。
~~~

**示例 2：**

~~~
输入：numbers = [2,3,4], target = 6
输出：[0,2]
~~~

**示例 3：**

~~~
输入：numbers = [-1,0], target = -1
输出：[0,1]
~~~

**提示：**

~~~
2 <= numbers.length <= 3 * 104
-1000 <= numbers[i] <= 1000
numbers 按 递增顺序 排列
-1000 <= target <= 1000
仅存在一个有效答案
~~~



#### 解法一：

暴力法：从下标0逐个遍历

~~~java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int len=numbers.length;
        int x=0,y=0;
        for(int i=0;i<len;++i){
            x=numbers[i];
            for(int j=i+1;j<len;++j){
                y=numbers[j];
                // 两个数之和已经大于目标之和，就进行下一轮循环
                if(x+y>target){
                    break;
                // 等于就返回
                }else if(x+y==target){
                    return new int[]{i,j};
                }
            }
        }
        return new int[]{-1,-1};
    }
}
~~~

时间复杂度：O(n^2)

空间复杂度：O(1)



#### 解法二

双指针法：首尾两个指针，大于target右指针左移，小于target左指针右移

~~~java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int len=numbers.length;
        int low=0;
        int high=len-1;
        while(low<high){
            int sum=numbers[low]+numbers[high];
            if(sum==target){
                return new int[]{low,high};
            }else if(sum<target){
                low++;
            }else{
                high--;
            }
        }
        return new int[]{-1,-1};
    }
}
~~~

时间复杂度：O(n)

空间复杂度：O(1)



#### 解法三：

哈希集合：放入当前元素之前，先判断target-当前元素是否存在，不存在则放进去，存在则return

~~~java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int len=numbers.length;
        HashMap<Integer,Integer>hashMap=new HashMap<>();
        for(int i=0;i<len;++i){
            if(!hashMap.containsKey(target-numbers[i])){
                hashMap.put(numbers[i],i);
            }else{
                return new int[]{hashMap.get(target-numbers[i]),i};
            }
        }
        return new int[]{-1,-1};
    }
}
~~~

时间复杂度：O(n)

空间复杂度：O(n)



#### 解法四

二分查找：固定一个下标，再右侧元素中二分查找与固定元素相加为target的元素

~~~java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int len=numbers.length;
        for(int i=0;i<len;++i){
            int low=i+1;
            int high=len-1;
            while(low<=high){
                // 避免相加溢出，先减再除最后再加上
                int mid=((high-low)>>1)+low;
                if(numbers[mid]==target-numbers[i]){
                    return new int[]{i,mid};
                }else if(numbers[mid]>target-numbers[i]){
                    high=mid-1;
                }else{
                    low=mid+1;
                }
            }
        }
        return new int[]{-1,-1};
    }
}
~~~

时间复杂度：O(nlogn)

空间复杂度：O(1)



