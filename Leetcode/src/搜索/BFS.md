# [127. 单词接龙](https://leetcode-cn.com/problems/word-ladder/)

```
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {    
        unordered_set<string> dict(wordList.begin(), wordList.end());    
        if (dict.find(endWord) == dict.end()) 
			return 0; 
       
        queue<string> q;
        q.push(beginWord);
        unordered_map<string, int> visited; 
        visited.insert({beginWord, 1});

        while(!q.empty()) {
            string word = q.front();
            q.pop();
            int path = visited[word]; 
            for (int i = 0; i < word.size(); i++) 
            {
                string new_word = word; 
                for (int j = 0 ; j < 26; j++) 
                {
                    new_word[i] = j + 'a';
                    if (new_word == endWord) 
						return path + 1; 

                    if (dict.find(new_word) != dict.end() && visited.find(new_word) == visited.end()) 
                    {
                        
                        visited.insert({new_word, path + 1});
                        q.push(new_word);
                    }
                }
            }
        }
        return 0;
    }
};
```

# [200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

````
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        if(grid.empty())
            return 0;
        
        int m = grid.size(),n = grid[0].size();
        int res = 0;

        for(int i = 0;i < m;i++)
        {
            for(int j = 0;j < n;j++)
            {
                if(grid[i][j] == '1')
                {
                    grid[i][j] = '0';
                    queue<pair<int,int>> q;
                    q.push({i,j});
                    res++;
                    while(!q.empty())
                    {
                        auto front = q.front();
                        q.pop();
                        int row = front.first,col = front.second;

                        if(row-1 >= 0 && grid[row-1][col] == '1')
                        {
                            q.push({row-1,col});
                            grid[row-1][col] = '0';
                        }
                        if(row+1 < m && grid[row+1][col] == '1')
                        {
                            q.push({row+1,col});
                            grid[row+1][col] = '0';
                        }
                        if(col-1 >= 0 && grid[row][col-1] == '1')
                        {
                            q.push({row,col-1});
                            grid[row][col-1] = '0';
                        }
                        if(col + 1 < n && grid[row][col+1] == '1')
                        {
                            q.push({row,col+1});
                            grid[row][col+1] = '0';
                        }
                    }
                }             
            }
        }
        return res;
    }
};
````

# [695. 岛屿的最大面积](https://leetcode-cn.com/problems/max-area-of-island/)

```
class Solution {
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        if(grid.empty())
            return 0;
        int m = grid.size(),n = grid[0].size();
        int res = INT_MIN;

        for(int i = 0;i < m;i++)
        {
            for(int j = 0;j < n;j++)
            {
                int curr = 0;
                if(grid[i][j] == 1)
                {
                    grid[i][j] = 0;
                    queue<pair<int,int>> q;
                    q.push({i,j});
                    curr++;   

                    while(!q.empty())
                    {
                        auto front = q.front();
                        q.pop();
                        int row = front.first,col = front.second;

                        if(row-1 >= 0 && grid[row-1][col] == 1)
                        {
                            q.push({row-1,col});
                            grid[row-1][col] = 0;
                            curr++;  
                        }
                        if(row+1 < m && grid[row+1][col] == 1)
                        {
                            q.push({row+1,col});
                            grid[row+1][col] = 0;
                            curr++;  
                        }
                        if(col-1 >= 0 && grid[row][col-1] == 1)
                        {
                            q.push({row,col-1});
                            grid[row][col-1] = 0;
                            curr++;  
                        }
                        if(col + 1 < n && grid[row][col+1] == 1)
                        {
                            q.push({row,col+1});
                            grid[row][col+1] = 0;
                            curr++;  
                        }
                    }  
                }
                res = max(res,curr);
            }
        }

        return res;
    }
};
```

# [463. 岛屿的周长](https://leetcode-cn.com/problems/island-perimeter/)

```
class Solution {
    constexpr static int dx[4] = {0, 1, 0, -1};
    constexpr static int dy[4] = {1, 0, -1, 0};
public:
    int islandPerimeter(vector<vector<int>> &grid) {
        int n = grid.size(), m = grid[0].size();
        int ans = 0;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (grid[i][j]) {
                    int cnt = 0;
                    for (int k = 0; k < 4; ++k) {
                        int tx = i + dx[k];
                        int ty = j + dy[k];
                        if (tx < 0 || tx >= n || ty < 0 || ty >= m || !grid[tx][ty]) {
                            cnt += 1;
                        }
                    }
                    ans += cnt;
                }
            }
        }
        return ans;
    }
};
```

# [542. 01 矩阵](https://leetcode-cn.com/problems/01-matrix/)









