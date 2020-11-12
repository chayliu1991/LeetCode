# 概述

- 深度优先搜索算法（Depth-First-Search，简称DFS）是一种用于遍历或搜索树或图的算法。
- 思想：一直往深处走，直到找到解或者走不下去后回溯。
- DFS和BFS的区别： 深搜和广搜在实现上分别用的是栈（栈和函数递归本质是一样）和队列。

# [17. 电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

```
class Solution {
public:
    unordered_map<char,string> dict = {
        {'2', "abc"}, {'3', "def"}, {'4', "ghi"}, {'5', "jkl"}, {'6', "mno"},
        {'7', "pqrs"}, {'8', "tuv"}, {'9', "wxyz"}};

    vector<string> res;
    string tmp;

    void dfs(int index,string digits)
    {
        if(index == digits.size())
        {
            res.push_back(tmp);
            return;
        }
        
        for(int i = 0;i < dict[digits[index]].size();i++)
        {
            tmp.push_back(dict[digits[index]][i]);
            dfs(index+1,digits);
            tmp.pop_back();
        }
    }

    vector<string> letterCombinations(string digits) {
        if(digits.empty())
            return {};
        dfs(0,digits);
        return res;
    }
};
```

# [695. 岛屿的最大面积](https://leetcode-cn.com/problems/max-area-of-island/)

```
class Solution {
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        if(grid.empty())
            return 0;
        int res  = 0;
        for(int i = 0;i < grid.size();i++)
        {
            for(int j = 0;j < grid[0].size();j++)
            {
                if(grid[i][j] == 1)
                    res = max(res,dfs(grid,i,j));
            }
        }
        return res;
    }

    int dfs(vector<vector<int>>& grid,int i,int j)
    {
        if(i < 0 || j <0 || i >= grid.size() || j >= grid[0].size() || grid[i][j] == 0)
            return 0;

        grid[i][j] = 0;
        int count = 1;
        vector<vector<int>> dir{{1,0},{-1,0},{0,1},{0,-1}};
        for(const auto d : dir)
            count += dfs(grid,i+d[0],j+d[1]);
        return count;
    }
};
```

# [200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

```
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        if(grid.empty())
            return 0;
        int res  = 0;
        for(int i = 0;i < grid.size();i++)
        {
            for(int j = 0;j < grid[0].size();j++)
            {
                if(grid[i][j] == '1')
                {
                    res++;
                    dfs(grid,i,j);
                }
            }
        }
        return res;
    }

    void dfs(vector<vector<char>>& grid,int i,int j)
    {
        if(i < 0 || j < 0 || i >= grid.size() || j >= grid[0].size() || grid[i][j] == '0')
            return;
        grid[i][j] = '0';

        vector<vector<int>> dir{{1,0},{-1,0},{0,1},{0,-1}};
        for(const auto d : dir)
            dfs(grid,i+d[0],j+d[1]);
    }
};
```

# [547. 朋友圈](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/friend-circles/)



# [130. 被围绕的区域](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/surrounded-regions/)





# [417. 太平洋大西洋水流问题](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/pacific-atlantic-water-flow/)



