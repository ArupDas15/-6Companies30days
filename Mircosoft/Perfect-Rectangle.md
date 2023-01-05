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

### Approach: 
https://leetcode.com/problems/perfect-rectangle/solutions/87180/o-n-solution-by-counting-corners-with-detailed-explaination/

### Solution
```cpp
class Solution {
public:
inline bool insert_corner(unordered_map<int, unordered_map<int, int>>& corner_count, int x, int y, int pos) {
    int& m = corner_count[x][y];
    if (m & pos) return false;
    m |= pos;
    return true;
}

    bool isRectangleCover(vector<vector<int>>& rectangles) {
    // step 1: counting
    unordered_map<int, unordered_map<int, int>> corner_count;
    int minx = INT_MAX, maxx=INT_MIN, miny=INT_MAX, maxy=INT_MIN;
    for (auto& rect : rectangles) {
        minx = min(minx, rect[0]);
        maxx = max(maxx, rect[2]);
        miny = min(miny, rect[1]);
        maxy = max(maxy, rect[3]);
        if (!insert_corner(corner_count, rect[0], rect[1], 1)) return false;
        if (!insert_corner(corner_count, rect[2], rect[1], 2)) return false;
        if (!insert_corner(corner_count, rect[0], rect[3], 4)) return false;
        if (!insert_corner(corner_count, rect[2], rect[3], 8)) return false;
    }
    
    //step2: checking
    bool valid_corner[16] = {false};
    bool valid_interior[16] = {false};
    valid_corner[1] = valid_corner[2] = valid_corner[4] = valid_corner[8] = true;
    valid_interior[3] = valid_interior[5] = valid_interior[10] = valid_interior[12] = valid_interior[15] = true;
    
    for (auto itx = corner_count.begin(); itx != corner_count.end(); ++itx) {
        int x = itx->first;
        for (auto ity = itx->second.begin(); ity != itx->second.end(); ++ity) {
            int y = ity->first;
            int mask = ity->second;
            if (((x != minx && x != maxx) || (y != miny && y != maxy)) && !valid_interior[mask]) 
                return false;
        }
    }
    return true;        
    }
};
```


