# 两数之和
## 题目
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标

示例:  

```
给定 nums = [2, 7, 11, 15], target = 9  
因为 nums[0] + nums[1] = 2 + 7 = 9  
所以返回 [0, 1]    
```

解题思路：

1. 暴力法
暴力法很简单。遍历每个元素 xx，并查找是否存在一个值与 target - xtarget−x 相等的目标元素。

   *   **复杂性分析**：  
       *   时间复杂度：O(n^2)，对于每个元素，我们试图通过遍历数组的其余部分来寻找它所对应的目标元素，这将耗费O(n)的时间。因此时间复杂度为O(n^2)。
       *   空间复杂度：O(1)。 

2. 两遍哈希表
为了对运行时间复杂度进行优化，我们需要一种更有效的方法来检查数组中是否存在目标元素。如果存在，我们需要找出它的索引。保持数组中的每个元素与其索引相互对应的最好方法是什么？哈希表。
通过以空间换取速度的方式，我们可以将查找时间从 O(n) 降低到 O(1)。哈希表正是为此目的而构建的，它支持以 近似 恒定的时间进行快速查找。我用“近似”来描述，是因为一旦出现冲突，查找用时可能会退化到 O(n)。但只要你仔细地挑选哈希函数，在哈希表中进行查找的用时应当被摊销为 O(1)。
一个简单的实现使用了两次迭代。在第一次迭代中，我们将每个元素的值和它的索引添加到表中。然后，在第二次迭代中，我们将检查每个元素所对应的目标元素（target - nums[i]）是否存在于表中。注意，该目标元素不能是 nums[i] 本身！

    *   **复杂性分析**
        *   时间复杂度：O(n)， 我们把包含有 n 个元素的列表遍历两次。由于哈希表将查找时间缩短到 O(1) ，所以时间复杂度为 O(n)。
        *   空间复杂度：O(n)， 所需的额外空间取决于哈希表中存储的元素数量，该表中存储了 n 个元素。 

3. 一遍哈希表
事实证明，我们可以一次完成。在进行迭代并将元素插入到表中的同时，我们还会回过头来检查表中是否已经存在当前元素所对应的目标元素。如果它存在，那我们已经找到了对应解，并立即将其返回。

     *   **复杂性分析**
        *   时间复杂度：O(n)， 我们只遍历了包含有 n 个元素的列表一次。在表中进行的每次查找只花费 O(1) 的时间。
        *   空间复杂度：O(n)， 所需的额外空间取决于哈希表中存储的元素数量，该表最多需要存储 n 个元素。


### 暴力法，遍历查找加起来的和是否等于target，也是很多人一开始就想到的办法
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum(array $nums = [], int $target) {
        $count = count($nums);
        for($i=0; $i<$count; $i++) {
            if ($nums[$i] > $target) continue;
            for ($j=$i+1; $j<$count; $j++) {
                if ($nums[$j] > $target) continue;
                if ($nums[$i] + $nums[$j] == $target) {
                    return [$i, $j]; 
                }
            }
        }
    }
}
```

其实循环2次的效率是非常低的，发现执行用时492MS

### 利用php array foreach中的下标 其实array底层实现也是一个hashtable，包括熟练使用php数组函数
```php
/**
 * @param Integer[] $nums
 * @param Integer $target
 * @return Integer[]
 */
function twoSum($nums, $target) {
    foreach((array)$nums as $key => $value ){
        $k = array_search($target-$value,$nums);
        if($k){
            return [$key,$k];                
        }
    }
}
```

优化后执行用时: 24 ms

### C++ 利用map， 效率更快
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target){
        map <int, int> mp;
        vector <int> res(2);
        int n = nums.size();
        for (int i = 0; i < n; i++) {
            int another = target - nums[i];
            if (mp.count(another)) {
                res[0] = mp[another];
                res[1] = i;
                break;
            }
            mp[nums[i]] = i;
        }
        return res;
    }
};
```

优化后执行用时: 4 ms

## 做题总结
开始不用刻意考虑效率，以思考为准，后面在学习优化

## 后续

```
如果给定 nums = [8, 7, 11, 4], target = 15  
就会产生2个结果集 
预期 [0, 1] 事实返回[2, 3]   
```
在下个算法思考中会出现
