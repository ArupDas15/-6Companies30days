# 391. Perfect Rectangle

Problem Link: https://leetcode.com/problems/perfect-rectangle/


Given an array rectangles where rectangles[i] = [xi, yi, ai, bi] represents an axis-aligned rectangle. The bottom-left point of the rectangle is (xi, yi) and the top-right point of it is (ai, bi).

Return true if all the rectangles together form an exact cover of a rectangular region.

Example 1:
![ex1](https://user-images.githubusercontent.com/37553488/210267706-03a60c28-4271-4b22-b684-b3c229de3d51.jpg)
```
Input: rectangles = [[1,1,3,3],[3,1,4,2],[3,2,4,4],[1,3,2,4],[2,3,3,4]]
Output: true
Explanation: All 5 rectangles together form an exact cover of a rectangular region.
```

Example 2:
![ex2](https://user-images.githubusercontent.com/37553488/210267717-ee080ba0-a187-43f0-86eb-5254f954198a.jpg)
```
Input: rectangles = [[1,1,2,3],[1,3,2,4],[3,1,4,2],[3,2,4,4]]
Output: false
Explanation: Because there is a gap between the two rectangular regions.
```

Example 3:
![ex3](https://user-images.githubusercontent.com/37553488/210267727-14f2fd00-0728-4004-bcab-2e4262dfba9e.jpg)
```
Input: rectangles = [[1,1,3,3],[3,1,4,2],[1,3,2,4],[2,2,4,4]]
Output: false
Explanation: Because two of the rectangles overlap with each other.
```

### Constraints
```
* 1 <= rectangles.length <= 2 * 10^4
* rectangles[i].length == 4
* -10^5 <= x_i, y_i, a_i, b_i <= 10^5
```

### Solution
```cpp
class Solution {
public:
    bool isRectangleCover(vector<vector<int>>& rectangles) {
        
    }
};```


