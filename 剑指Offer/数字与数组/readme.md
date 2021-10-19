# [12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

```
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        if(word.empty()) return false;
        for(int i=0; i<board.size(); ++i)
        {
            for(int j=0; j<board[0].size(); ++j)
            {
                if(dfs(board, word, i, j, 0)) 
					return true;
            }
        }
        return false;
    }
	
    bool dfs(vector<vector<char>>& board, string& word, int i, int j, int len)
    {
        if(i<0 || i >= board.size() || j<0 || j >= board[0].size() || board[i][j] != word[len]) 
			return false;
        if(len == word.length() - 1) 
			return true;
        char temp = board[i][j]; 
        board[i][j] = '\0';
        if(dfs(board,word,i-1,j,len+1) 		|| 
			dfs(board,word,i+1,j,len+1) 	|| 
			dfs(board,word,i,j-1,len+1)   	|| 
			dfs(board,word,i,j+1,len+1))
        {
            return true;
        }

		board[i][j] = temp; 
        return false;
    }
};
```

# [13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

```
class Solution {
public:
    int movingCount(int m, int n, int k) {
        std::vector<std::vector<bool>> visited(m, std::vector<bool>(n));
        return dfs(0, 0, m, n, k, visited);
    }

    int dfs(int i, int j, int m, int n, int k, vector<vector<bool>>& visited) 
    {
        if (i < 0 || j < 0 || i == m || j == n || sum_n(i) + sum_n(j) > k || visited[i][j]) 
            return 0;
        visited[i][j] = 1;
        return dfs(i + 1, j, m, n, k, visited) + dfs(i, j + 1, m, n, k, visited) + 1;
    }

    int sum_n(int num) 
    {
        int sum = 0;
        while (num) 
        {
            sum += num % 10;
            num /= 10;
        }
        return sum;
    }
};
```

# [16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

```
class Solution {
public:
    double myPow(double x, int n) {
        if(n == 0)
            return 1;
        long exp = n;
        if(exp < 0)
            exp = -exp;
        if(n < 0)
            return 1.0 / quick_pow(x,exp);
        else
            return quick_pow(x,exp);
    }
    
    double quick_pow(double x,long n)
    {
        if(n == 0)
            return 1.0;
        if(n == 1)
            return x;
        double t = quick_pow(x,n >> 1);
        double res = t * t;
        
        return n & 0x01 ? res * x : res;
    }
};
```

# [17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

```
class Solution {
public:
    vector<int> printNumbers(int n) {
        std::vector<int> res;
        int max = pow(10,n);
        for(int i = 1;i < max;i++)
            res.push_back(i);
        return res;
    }
};
```

# [21. 调整数组顺序使奇数位于偶数前面](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

```
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        int left = 0,right = nums.size() - 1;
        while(left < right)
        {
            while((nums[left] & 0x1) && (left < right))
                left++;
            while(!(nums[right] & 0x1) && (left < right))
                right--;
            
            if(left >= right)
                break;
            
            std::swap(nums[left],nums[right]);
            left++;
            right--;
        }
        return nums;
    }
};
```

# [29. 顺时针打印矩阵](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

```
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.empty() || matrix[0].empty())
            return {};
        int rows = matrix.size(),cols = matrix[0].size();
        std::vector<std::vector<bool>> visited(rows,std::vector<bool>(cols,false));

        std::vector<int> res;
        int dx[4] = {0,1,0,-1},dy[4] = {1,0,-1,0}; 
        int x = 0,y = 0,d = 0;
        for(int i = 0;i < rows*cols;i++)
        {
            res.push_back(matrix[x][y]);
            visited[x][y] = true;
            int a = x + dx[d],b = y + dy[d];
            if(a < 0 || a>= rows || b < 0 || b >= cols || visited[a][b])
            {
                d = (d + 1) % 4;
                 a = x + dx[d],b = y + dy[d];
            }
            x = a,y = b;
        }

        return res;
    }
};
```

# [39. 数组中出现次数超过一半的数字](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        std::sort(nums.begin(),nums.end());
        return nums[nums.size()/2];
    }
};
```

# [40. 最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

```
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        if(arr.empty())
            return {};
        
        std::sort(arr.begin(),arr.end());
        if(arr.size() < k)
            return {};
        return std::vector<int>(arr.begin(),arr.begin()+k);
    }
};
```

# [41. 数据流中的中位数](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

```
class MedianFinder {
public:
    /** initialize your data structure here. */
    MedianFinder() {

    }
    
    void addNum(int num) {
        max_q.push(num);
        min_q.push(max_q.top());
        max_q.pop();

        while(max_q.size() < min_q.size())
        {
            max_q.push(min_q.top());
            min_q.pop();
        }
    }
    
    double findMedian() {
        return max_q.size() > min_q.size() ? (double) max_q.top() : (max_q.top() + min_q.top()) * 0.5;
    }

private:
    std::priority_queue<int,std::vector<int>,std::greater<int>> min_q;
    std::priority_queue<int,std::vector<int>,std::less<int>> max_q;
};
```


# [43. 1～n 整数中 1 出现的次数](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

```
class Solution {
public:
    int countDigitOne(int n) {
		int res = 0;
		long i = 1; //@ 遍历的位数
		while(n / i)
		{
			long high = n / (10 * i);  //@ 高位数值 
			long curr = (n / i) % 10;  //@ 当前位数值
			long low = n - (n / i) * i; //@ 低位数值
			if(curr == 0)
				res += high * i;
			else if(curr == 1)
				res += high * i + low + 1;
			else
				res += high * i + i;
			i *= 10;  //@ 位数增加
		}
		return res;
    }
};
```

# [44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

```
class Solution {
public:
    int findNthDigit(int n) {
        int i = 1;
        while(n > 0.9 * pow(10,i) * i)
        {
            n -= 0.9 * pow(10,i) * i;
            i++;
        }

        std::string res = std::to_string(pow(10,i-1) + (n -1) / i);
        return res[(n-1)%i] - '0';
    }
};
```

# [45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

```
class Solution {
public:
    string minNumber(vector<int>& nums) {
        std::vector<std::string> strs;
        for(const auto n : nums)
            strs.push_back(std::to_string(n));
        
        std::sort(strs.begin(),strs.end(),[](const std::string& s1,const std::string& s2){
            return s1 + s2 < s2 + s1;
        });

        std::string res;
        for(const auto& s : strs)
            res += s;
        return res;
    }
};
```

# [46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

```
class Solution {
public:
    int translateNum(int num) {
        std::string str = std::to_string(num);
        int n = str.size();
        std::vector<int> dp(n+1,0);
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2;i <= n;i++)
        {
           dp[i] = dp[i-1];
           if(str[i-2] != '0' && (str[i-2]-'0')*10+(str[i-1]-'0') <= 25)
                dp[i] += dp[i-2];
        }
        return dp.back();
    }
};
```

```
class Solution {
public:
    int translateNum(int num) {
        std::string str = std::to_string(num);
        return back_trace(str,0);
    }

    int back_trace(std::string& s,int i)
    {
        int n = s.length();
        if(i == n)
            return 1;
        if(i == n-1 || s[i] == '0' || s.substr(i,2) > "25")
            return back_trace(s,i+1);
        return back_trace(s,i+1) + back_trace(s,i+2);
    }
};
```

# [49. 丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)

```
class Solution {
public:
    int nthUglyNumber(int n) {
        std::vector<int> dp(n,1);
        int i = 0,j = 0,k = 0;
        for(int m = 1;m < n ;m++)
        {
            int n2 = dp[i] * 2,n3 = dp[j] * 3,n5 = dp[k] * 5;
            dp[m] = min(n2,min(n3,n5));
            if(dp[m] == n2)
                i++;
            if(dp[m] == n3)
                j++;
            if(dp[m] == n5)
                k++;
        }
        return dp.back();
    }
};
```

# [51. 数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

```
class Solution {
public:
    int reversePairs(vector<int>& nums) {
        vector<int> tmp(nums.size());
        return mergeSort(0, nums.size() - 1, nums, tmp);
    }
private:
    int mergeSort(int l, int r, vector<int>& nums, vector<int>& tmp) {
        // 终止条件
        if (l >= r) return 0;
        // 递归划分
        int m = (l + r) / 2;
        int res = mergeSort(l, m, nums, tmp) + mergeSort(m + 1, r, nums, tmp);
        // 合并阶段
        int i = l, j = m + 1;
        for (int k = l; k <= r; k++)
            tmp[k] = nums[k];
        for (int k = l; k <= r; k++) {
            if (i == m + 1)
                nums[k] = tmp[j++];
            else if (j == r + 1 || tmp[i] <= tmp[j])
                nums[k] = tmp[i++];
            else {
                nums[k] = tmp[j++];
                res += m - i + 1; // 统计逆序对
            }
        }
        return res;
    }
};
```

# [56 - I. 数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

```
class Solution {
public:
    vector<int> singleNumbers(vector<int>& nums) {
        int sum = 0;
        for(auto n : nums)
            sum ^= n;        
        int mask = 1;
        while((mask & sum) == 0)
            mask <<= 1;
        int a = 0,b = 0;
        for(auto n : nums)
        {
            if(n & mask)
                a ^= n;
            else 
                b ^= n;
        }
        return {a,b};
    }
};
```

# [56 - II. 数组中数字出现的次数 II](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

```
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        std::unordered_map<int,int> hash;
        for(const auto n : nums)
        {
            hash[n]++;
            if(hash[n] == 3)
                hash.erase(n);
        }
        return hash.begin()->first;
    }
};
```

# [57. 和为s的两个数字](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int left = 0,right = nums.size()-1;
        while(left < right)
        {
            if(nums[left] + nums[right] == target)
                return {nums[left],nums[right]};
            else if(nums[left] + nums[right] > target)
                right--;
            else 
                left++;
        }
        return {};
    }
};
```

# [57 - II. 和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

```
class Solution {
public:
    vector<vector<int>> findContinuousSequence(int target) {
        int left = 1,right = 1;
        vector<vector<int>>  res;
		int sum = 0;
        while(left <= target/2)
        {
            if(sum < target)
			{
				sum += right;
				right++;		
			}
			else if(sum > target)
			{
				sum -= left;
				left++;	
			}
			else
			{
				vector<int> v;
				for(int i = left;i < right;i++)
					v.push_back(i);
				res.push_back(v);	
				sum -= left;
				left ++;	
			}			
        }
        return res;
    }
};
```

# [ 61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

```
class Solution {
public:
    bool isStraight(vector<int>& nums) {
        std::sort(nums.begin(),nums.end());
        int min_index = 0;
        while(nums[min_index] == 0)
            min_index++;
        for(int i = min_index;i < nums.size()-1;i++)
        {
            if(nums[i] == nums[i+1])
                return false;
        }
        return nums[4] - nums[min_index] <= 4;
    }
};
```

# [64. 求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof/)

```
class Solution {
public:
    int sumNums(int n) {
        n && (n+=sumNums(n-1));
        return n;
    }
};
```

# [66. 构建乘积数组](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

```
class Solution {
public:
    vector<int> constructArr(vector<int>& a) {
        int size = a.size();
        std::vector<int> res(size,1);
        for(int i = 1;i < size;i++)
            res[i] = res[i-1] * a[i-1];

        int tmp = 1;
        for(int i = size-2;i >= 0;i--)
        {
            tmp *= a[i+1];
            res[i] *= tmp;
        }
        return res;
    }
};
```

