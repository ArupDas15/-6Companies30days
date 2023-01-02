# 368. Largest Divisible Subset

Problem Link: https://leetcode.com/problems/largest-divisible-subset/


Given a set of distinct positive integers nums, return the largest subset answer such that every pair (answer[i], answer[j]) of elements in this subset satisfies:
* ```answer[i] % answer[j] == 0,``` or
* ```answer[j] % answer[i] == 0```

If there are multiple solutions, return any of them.


Example 1:
```
Input: nums = [1,2,3]
Output: [1,2]
Explanation: [1,3] is also accepted.
```

Example 2:
```
Input: nums = [1,2,4,8]
Output: [1,2,4,8]
```

### Constraints
```
* 1 <= nums.length <= 1000
* 1 <= nums[i] <= 2 * 10^9
* All the integers in nums are unique.
```

### Solution
```cpp
class Solution {
public:
    // Reference: https://www.youtube.com/watch?v=Wv6DlL0Sawg&t=86s
    // Time Complexity: O(N^2)
    // Space Complexity: O(N)
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        int n=nums.size();
        vector<int>ans;
        if(n==0)return ans;
        sort(nums.begin(),nums.end()); // O(N logN)
        int mx=1;
        vector<int>dp(n+1,1);
        // O(N^2)
        for(int i=1;i<n;i++){
            for(int j=0;j<i;j++){
                if(nums[i]%nums[j]==0){
                    dp[i]=max(1+dp[j], dp[i]);
                    mx = max(mx,dp[i]);
                }
            }
        }
        int prev = -1;
        // O(N)
        for(int i=n-1;i>=0;i--){
            if(dp[i]==mx && (prev%nums[i]==0 || prev==-1)){
                ans.push_back(nums[i]);
                mx = mx-1;
                prev = nums[i];
            }
        }
        return ans;
    }
};
```


