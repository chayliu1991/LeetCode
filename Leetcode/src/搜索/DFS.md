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
    int dfs(vector<vector<int>>& grid, int cur_i, int cur_j) {
        if (cur_i < 0 || cur_j < 0 || cur_i >= grid.size() || cur_j >= grid[0].size() || grid[cur_i][cur_j] == 0) 
            return 0;
        
        grid[cur_i][cur_j] = 0;
		constexpr static int dx[4] = {0, 0, 1, -1};
        constexpr static int dy[4] = {1, -1, 0, 0};
        int res = 1;
        for (int k = 0; k < 4; ++k) 
        {
            int next_i = cur_i + dx[k], next_j = cur_j + dy[k];
            res += dfs(grid, next_i, next_j);
        }
        return res;
    }
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int res = 0;
        for (int i = 0; i < grid.size(); ++i) 
		{
            for (int j = 0; j < grid[0].size(); ++j) 
                res = max(res, dfs(grid, i, j));
        }
        return res;
    }
};
```

# [200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

```
class Solution {
public:
	 void dfs(vector<vector<char>>& grid, int cur_i, int cur_j) 
	 {
        if (cur_i < 0 || cur_j < 0 || cur_i >= grid.size() || cur_j >= grid[0].size() || grid[cur_i][cur_j] == '0') 
            return;
		
		grid[cur_i][cur_j] = '0';
		constexpr static int dx[4] = {0, 0, 1, -1};
        constexpr static int dy[4] = {1, -1, 0, 0};
  
        for (int k = 0; k < 4; ++k) 
		{
            int next_i = cur_i + dx[k], next_j = cur_j + dy[k];
            dfs(grid, next_i, next_j);
        }
	 }
	 
    int numIslands(vector<vector<char>>& grid) {
		int res = 0;
        for (int i = 0; i < grid.size(); ++i) 
		{
            for (int j = 0; j < grid[0].size(); ++j) 
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
};
```

# [547. 朋友圈](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/friend-circles/)



# [130. 被围绕的区域](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/surrounded-regions/)





# [417. 太平洋大西洋水流问题](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/problems/pacific-atlantic-water-flow/)



