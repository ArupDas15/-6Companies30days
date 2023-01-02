# 396. Rotate Function

Problem Link: https://leetcode.com/problems/rotate-function/

You are given an integer array nums of length n.

Assume arrk to be an array obtained by rotating nums by k positions clock-wise. We define the rotation function F on nums as follow:

* ```F(k) = 0 * arrk[0] + 1 * arrk[1] + ... + (n - 1) * arrk[n - 1].```

Return the maximum value of ```F(0), F(1), ..., F(n-1)```.

The test cases are generated so that the answer fits in a 32-bit integer.

Example 1:
```
Input: nums = [4,3,2,6]
Output: 26
Explanation:
F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26
So the maximum value of F(0), F(1), F(2), F(3) is F(3) = 26.
```

Example 2:
```
Input: nums = [100]
Output: 0
```

### Constraints
```
* n == nums.length
* 1 <= n <= 10^5
* -100 <= nums[i] <= 100
```

### Approach
![acc1](https://user-images.githubusercontent.com/37553488/210244245-2b104984-dc5f-4b64-95dd-9ba17dcda46a.jpeg)
![acc2](https://user-images.githubusercontent.com/37553488/210244253-9861445d-f745-4b9b-9b9c-04ac2911c833.jpeg)



### Solution
```cpp
class Solution {
public:
    // Reference: https://leetcode.com/problems/rotate-function/solutions/2945111/simple-mathematics-solution/
    // Time Complexity: O(n)
    // Space Complexity: O(1)
    int maxRotateFunction(vector<int>& nums) {
       int sum=0;
       int f=0;
       int ans;
       for(int i=0;i<nums.size();i++){
           f+=(i*nums[i]);
           sum+=nums[i];
       }
       ans = f;
       int n = nums.size();
       for(int i = n - 1;i > 0; i--){
           ans = max(ans,f+sum-(n*nums[i]));
           f=f+sum-(n*nums[i]);
       }
       return ans;
    }
};
```


