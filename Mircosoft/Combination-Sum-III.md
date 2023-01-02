# 216. Combination Sum III

Problem Link: https://leetcode.com/problems/combination-sum-iii/


Find all valid combinations of k numbers that sum up to n such that the following conditions are true:

* Only numbers 1 through 9 are used.
* Each number is used at most once.

Return a list of all possible valid combinations. The list must not contain the same combination twice, and the combinations may be returned in any order.

Example 1:
```
Input: k = 3, n = 7
Output: [[1,2,4]]
Explanation:
1 + 2 + 4 = 7
There are no other valid combinations.
```

Example 2:
```
Input: k = 3, n = 9
Output: [[1,2,6],[1,3,5],[2,3,4]]
Explanation:
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
There are no other valid combinations.
```


Example 3:
```
Input: k = 4, n = 1
Output: []
Explanation: There are no valid combinations.
Using 4 different numbers in the range [1,9], the smallest sum we can get is 1+2+3+4 = 10 and since 10 > 1, there are no valid combination.
```
### Constraints
```
* 2 <= k <= 9
* 1 <= n <= 60
```

### Solution
```cpp
// Reference: https://www.youtube.com/watch?v=GUhqiRULHrA
class Solution {
public:
    // Solution uses Backtracking approach. We try out all possible combinations.
    // Space Complexity: O(k)
    // Time Complexity: O(3^n) - need to confirm this.
    void fillRes(int n, int k, vector<int> r, vector<vector<int>>&res){
	 if(n==0 or k==0){
	 	if(n==0 and k==0 and r.size()>0) res.push_back(r);
		return;
	 }
	 int pre = 0;
	 if (r.size() > 0) pre = r[r.size()-1];
	 for(int x = pre + 1; x < 10; x++){
	 	if(n - x < 0)break;
		r.push_back(x);
		fillRes(n - x, k - 1, r, res);
        	r.pop_back();
	 }
    }
    vector<vector<int>> combinationSum3(int k, int n) {
	 vector<vector<int>>res;
	 vector<int> r;
	 fillRes(n, k, r, res);
	 return res;
    }
};
```


