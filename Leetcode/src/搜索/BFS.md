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
			
		constexpr static int dx[4] = {0, 1, 0, -1};
		constexpr static int dy[4] = {1, 0, -1, 0};        
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
						for(int k = 0;k < 4;k++)
						{
							int x = row + dx[k];
							int y = col + dy[k];
							if(x >=0 && x < m && y >=0 && y < n && grid[x][y] == '1')
							{
								q.push({x,y});
								grid[x][y] = '0';
							}
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
		
		constexpr static int dx[4] = {0, 1, 0, -1};
		constexpr static int dy[4] = {1, 0, -1, 0}; 		
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
						for(int k =0;k < 4;k++)
						{
							int x = row + dx[k];
							int y = col + dy[k];
							if(x >=0 && x < m && y >=0 && y < n && grid[x][y] == 1)
							{
								q.push({x,y});
								grid[x][y] = 0;
								curr++;  
							}
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

# [542. 01 矩阵](https://leetcode-cn.com/problems/01-matrix/)

```
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& matrix) {
        if(matrix.empty() || matrix[0].empty())
            return {};
        
        constexpr int dx[4] = {1,0,-1,0};
        constexpr int dy[4] = {0,1,0,-1};
        int m = matrix.size(),n = matrix[0].size();
        vector<vector<int>> res(m,vector<int>(n,0)),visited(m,vector<int>(n,0));
        queue<pair<int,int>> q;
        for(int i = 0;i < m;i++)
        {
            for(int j = 0;j < n;j++)
            {
                if(matrix[i][j] == 0)
                {
                    q.emplace(i,j);
                    visited[i][j] = 1;
                }
            }
        }

        while(!q.empty())
        {
            auto it= q.front();
            q.pop();
            int row = it.first,col = it.second;
            for(int k = 0;k < 4;k++)
            {
                int x = row + dx[k];
                int y = col + dy[k];
                if(x >= 0 && x < m && y >= 0 && y < n && !visited[x][y])
                {
                    res[x][y] = res[row][col] + 1;
                    q.emplace(x,y);
                    visited[x][y] = 1;
                }
            }
        }
        return res;
    }
};
```









