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

