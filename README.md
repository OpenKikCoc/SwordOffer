

### SwordOffer

[toc]

#### [03.数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/) [EASY]

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        unordered_map<int, bool> m;
        int len = nums.size();
        for (int i = 0; i < len; ++ i )
            if (m[nums[i]] == true)
                return nums[i];
            else
                m[nums[i]] = true;
        return -1;
    }
};
```

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int len = nums.size(), tmp;
        for (int i = 0; i < len; ++ i ) {
            while (nums[i] != i) {
                if (nums[i] == nums[nums[i]])
                    return nums[i];
                swap(nums[i], nums[nums[i]]);
            }
        }
        return -1;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int duplicateInArray(vector<int>& nums) {
        int n = nums.size();
        for (auto v : nums)
            if (v < 0 || v > n - 1)
                return -1;
        
        unordered_set<int> S;
        for (auto v : nums)
            if (S.count(v))
                return v;
            else
                S.insert(v);
        return -1;
    }
};
```



```python
# python3
# ========= another solution 一个萝卜一个坑
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:  
        for i in range(len(nums)):
            while nums[i] != i:
                if nums[i] == nums[nums[i]]:
                    return nums[i]
                else:
                    nums[i], nums[nums[i]] =  nums[nums[i]], nums[i]
        return -1

class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        i = 0
        while i < len(nums):
            if nums[i] == i:
                i += 1
            elif nums[nums[i]] == nums[i]:return nums[i]
            else:
                nums[nums[i]], nums[i] = nums[i], nums[nums[i]]
        return -1


# 用集合判断 nums[i] 是否存在于集合中，如果存在，则返回该值。但需要用到额外空间，时间复杂度和空间复杂度都是O(N)
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        my_set = set()
        for c in nums:
            if c in my_set:
                return c
            else:
                my_set.add(c)

#把集合换成哈希表也可以
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        dict={}
        for i in nums:
           if i not in dic:
               dic[i] = 0
           else:
               return i   
            
# 用defaultdict哈希            
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        my_dict = collections.defaultdict(int)
        for x in nums:
            my_dict[x] += 1
            if my_dict[x] > 1:
                return x             
```



#### 03.1不修改数组找出重复的数字 [TAG]

```c++
class Solution {
public:
    int duplicateInArray(vector<int>& nums) {
        int l = 1, r = nums.size() - 1;
        while (l < r) {
            int m = l + r >> 1;
            
            int s = 0;
            for (auto v : nums)
                if (v >= l && v <= m)
                    ++ s ;
            
            if (s > m - l + 1)
                r = m;
            else
                l = m + 1;
        }
        return l;
    }
};
```



```python
# 前提：不修改数组找出重复的数字

```





#### [04.二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/) [EASY]

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if (matrix.empty())
            return false;
        int m = matrix.size(), n = matrix[0].size();
        int u = 0, r = n - 1;
        while (u < m && r >= 0) {
            if (matrix[u][r] > target) -- r ;
            else if (matrix[u][r] < target) ++ u ;
            else return true;
        }
        return false;
    }
};
```

```c++
// AcWing
class Solution {
public:
    bool searchArray(vector<vector<int>> array, int target) {
        if (array.empty())
            return false;
        
        int n = array.size(), m = array[0].size();
        int u = 0, r = m - 1;
        while (u < n && r >= 0) {
            if (array[u][r] == target)
                return true;
            else if (array[u][r] > target)
                -- r ;
            else
                ++ u ;
        }
        return false;
    }
};
```



```python
# python3
# 从右上角开始查找，当前数比target大，就i -= 1; 当前数小，就j += 1
class Solution:
    def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
        if not matrix:return False
        i, j = 0, len(matrix[0]) - 1
        while i < len(matrix) and j >= 0:
            if matrix[i][j] > target:
                j -= 1
            elif matrix[i][j] < target:
                i += 1
            else:return True 
        return False
```



#### [05.替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/) [EASY]

```c++
class Solution {
public:
    string replaceSpace(string s) {
        int len = s.size();
        string res;
        for (int i = 0; i < len; ++ i ) {
            if (s[i] == ' ')
                res+= "%20";
            else
                res.push_back(s[i]);
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    string replaceSpaces(string &str) {
        string res;
        for (auto c : str)
            if (c == ' ')
                res += "%20";
            else
                res += c;
        return res;
    }
};
```



```python
# python3
# 正序遍历，用一个列表记录，遇到了空格，就插入字符串；最后用join进行操作返回字符串即可
# 对比直接用字符串记录结果的，用列表记录 效率更高。
class Solution:
    def replaceSpace(self,s:str)->str:
        res = []
        for c in s:
            if c == '':res.append("%20")
            else:res.append(c)
        return ''.join(res)
                    
# ========= another solution, 用python的内置函数（在面试中不推荐使用）           
class Solution:
    def replaceSpace(self, s: str) -> str:
        s = s.replace(' ','%20')
        return s

      
#创建一个新的字符串，对字符串进行遍历；该方法不如法一用列表好，因为字符串为不可变类型，每加一个字符就会变成新的字符串，太消耗内存了。     
class Solution:
    def replaceSpace(self, s: str) -> str:
        res = ''
        for i in s:
            if i == ' ':
                res += '%20'
            else:
                res += i
        return res
```



#### [06.从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/) [EASY]

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> res;
        while (head != nullptr) {
            res.push_back(head->val);
            head = head->next;
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```

```c++
// AcWing
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> res;
    
    void dfs(ListNode * r) {
        if (!r)
            return;
        dfs(r->next);
        res.push_back(r->val);
    }
    
    vector<int> printListReversingly(ListNode* head) {
        dfs(head);
        return res;
    }
};
```



```python
# python3
# 用一个指针记录，把值压入列表中，最后反转输出即可
#========= 反转
class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        res = []
        p = head
        while head:
            res.append(head.val)
            p = p.next
        return res[::-1]  # 或者 reverse(res)


#堆栈法
class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        stack = []
        while head: # push
            stack.append(head.val)
            head = head.next
        res = []
        while stack: # pop
            res.append(stack.pop())
        return res

#========= 递归
class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        if not head: return []
        return self.reversePrint(head.next) + [head.val]
```



#### [07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/) [MID]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* helper(unordered_map<int, int>& h, vector<int>& pre, int s0, int e0, int s1) {
        if (s0 > e0) return nullptr;
        // 父节点 父节点在中序序列的idx
        int mid = pre[s1], idx = h[mid], leftLen = idx - s0;
        TreeNode* node = new TreeNode(mid);
        node->left = helper(h, pre, s0, idx - 1, s1 + 1);
        node->right = helper(h, pre, idx + 1, e0, s1 + 1 + leftLen);
        return node;
    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int n = preorder.size();
        unordered_map<int, int> hash;
        for (int i = 0; i < n; ++ i ) hash[inorder[i]] = i;
        return helper(hash, preorder, 0, n - 1, 0);
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int n;
    unordered_map<int, int> mp;

    TreeNode* helper(vector<int> & pre, int l, int r, int p) {
        if (l > r)
            return nullptr;
        
        int pa = pre[p], id = mp[pa], llen = id - l;
        TreeNode * ret = new TreeNode(pa);
        ret->left = helper(pre, l, id - 1, p + 1);
        ret->right = helper(pre, id + 1, r, p + 1 + llen);
        return ret;
    }

    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        n = inorder.size();
        for (int i = 0; i < n; ++ i )
            mp[inorder[i]] = i;
        return helper(preorder, 0, n - 1, 0);
    }
};
```



```python
#算法流程：
#1. 在前序遍历中找到根节点：前序遍历的第一个数 就是根节点的值
#2. 在中序遍历中找到根节点对应的位置k，则 k的左边就是左子树的中序遍历，k的右边就是右子树的中序遍历 （这一步需要用一个字典来存储对应的位置）
#3. 假设左子树的长度为l,那么在前序遍历里，根节点后l个数 是左子树的前序遍历，剩下的树就是右子树的前序遍历
#4. 有了左右子树的前序遍历和中序遍历，我们可以先递归创建出左右子树，然后再创建根节点；
class Solution:
    def buildTree(self, pre: List[int], ino: List[int]) -> TreeNode:
        my_dict = dict()
        for i in range(len(ino)):
            my_dict[ino[i]] = i

        def dfs(pre_L, pre_R, ino_L, ino_R):
            if pre_L > pre_R:return    # 踩坑： 只能 大于 的时候 才能return
            root = TreeNode(pre[pre_L])
            idx = my_dict[pre[pre_L]]
            root.left = dfs(pre_L + 1, idx - ino_L + pre_L, ino_L, idx - 1)
            root.right = dfs(idx - ino_L + pre_L + 1, pre_R, idx + 1, ino_R)
            return root   # 递归返回这一层对应的root , 也就是重建后的二叉树
        
        return dfs(0, len(pre) - 1, 0, len(ino) - 1)      
      
```



#### [09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/) [EASY]

```c++
class CQueue {
    stack<int> in, out;
public:
    CQueue() {
    }
    
    void appendTail(int value) {
        in.push(value);
    }
    
    int deleteHead() {
        if (out.size()) {
            int res = out.top();
            out.pop();
            return res;
        } else if (in.size()) {
            while (in.size() > 1) {
                int v = in.top();
                in.pop();
                out.push(v);
            }
            int res = in.top();
            in.pop();
            return res;
        } else return -1;
    }
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
```

```c++
// AcWing
class MyQueue {
public:
    stack<int> in, out;

    /** Initialize your data structure here. */
    MyQueue() {
    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        in.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        if (out.empty()) {
            while (in.size()) {
                out.push(in.top());
                in.pop();
            }
        }
        int t = out.top();
        out.pop();
        return t;
    }
    
    /** Get the front element. */
    int peek() {
        if (out.empty()) {
            while (in.size()) {
                out.push(in.top());
                in.pop();
            }
        }
        return out.top();
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return in.empty() && out.empty();
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * bool param_4 = obj.empty();
 */
```



```python
class CQueue:
    def __init__(self):
        self.A = []
        self.B = []

    def appendTail(self, value: int) -> None:
        self.A.append(value)

    def deleteHead(self) -> int:
        if self.B:return self.B.pop()  #先判断self.B是否有元素，有的话 直接弹出
        if not self.A:return -1 # 如果B中没有元素，那就看A是不是有新加入的元素，没有的话 返回-1.
        while self.A: # 有的话，再把A中元素全部压入到B中
            self.B.append(self.A.pop())
        return self.B.pop()
```





```python
# 需要一个辅助栈；
# A栈负责入栈所有元素，辅助栈B就负责pop和peek
class MyQueue(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.A = []
        self.B = []

    def push(self, x):
        """
        Push element x to the back of queue.
        :type x: int
        :rtype: void
        """
        self.A.append(x)
        

    def pop(self):
        """
        Removes the element from in front of queue and returns that element.
        :rtype:int
        """
        if self.B:return self.B.pop()
        while self.A:
            self.B.append(self.A.pop())
        return self.B.pop()

    def peek(self):
        """
        Get the front element.
        :rtype: int
        """
        if self.B:return self.B[-1]
        while self.A:
            self.B.append(self.A.pop())
        return self.B[-1]

    def empty(self):
        """
        Returns whether the queue is empty.
        :rtype: bool
        """
        return not self.A and not self.B
```



#### [10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/) [EASY]

```c++
class Solution {
public:
    int mod = 1e9+7;
    int fib(int n) {
        if (n <= 1) return n;
        int a = 0, b = 1, tmp;
        for (int i = 2; i <= n; ++ i ) {
            tmp = a;
            a = b % mod;
            b = (tmp + b) % mod;
        }
        return b;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int Fibonacci(int n) {
        vector<int> f(n + 1);
        f[1] = f[2] = 1;
        for (int i = 3; i <= n; ++ i )
            f[i] = f[i - 1] + f[i - 2];
        return f[n];
    }
};
```



```python
# python3
class Solution:
    def fib(self, n: int) -> int:
        a, b = 0, 1
        for _ in range(0,n):
            a, b = b, a + b  #踩坑：需要同步交换，不能写成2行
        return a % 1000000007
      
#       
class Solution:
    def fib(self, n: int) -> int:
        if n <= 1:return n 
        a, b = 1, 1
        for i in range(2, n):
            a, b = b, a + b
        return b % 1000000007      
```



#### [10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/) [EASY]

```c++
// 同上
```



```python
# python3
class Solution:
    def numWays(self, n: int) -> int:
        a, b = 1, 1
        for _ in range(n):
            a, b = b, a + b
        return a % 1000000007
```



#### [11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/) [EASY]

```c++
class Solution {
public:
    int minArray(vector<int>& numbers) {
        int n = numbers.size();
        int l = 0, r = n - 1;
        while (l <= r) {
            while (l <= r && numbers[l] == numbers[r]) -- r ;
            if (l > r || numbers[l] < numbers[r]) break;
            int mid = l + (r - l) / 2;
            if (numbers[mid] >= numbers[l]) l = mid + 1;    // must mid > r
            else r = mid;
        }
        return numbers[l];
    }
};
```

```c++
// AcWing
class Solution {
public:
    int findMin(vector<int>& nums) {
        if (nums.empty())
            return -1;
        int n = nums.size();
        int l = 0, r = n - 1;
        while (l < r) {
            int m = l + r >> 1;
            if (nums[m] < nums[r])
                r = m;
            else if (nums[m] > nums[r])
                l = m + 1;
            else
                -- r ;
        }
        return nums[l];
    }
};
```



```python
# python3
# 用二分法模板，每次二分 都抛弃一半的数据的思想。

class Solution:
    def minArray(self,numbers:List[int])->int:
        i, j = 0, len(numbers)-1
        while i < j:
            m = (i + j) // 2
            if numbers[m] > numbers[j]:i = m + 1
            elif numbers[m] < numbers[j]:j = m
            else:j -= 1   # 踩坑：当数字相同的时候，直接把右指针向左移动一个。如果当前数为最小数，删除掉右边的这个数 不会对结果产生影响
        return numbers[i]
```



#### [12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/) [MID]

```c++
class Solution {
public:
    int wordlen;
    int m, n;
    int dx[4] = {0, -1, 1, 0}, dy[4] = {-1, 0, 0, 1};
    bool dfs(int x, int y, int idx, vector<vector<bool>>& vis, vector<vector<char>>& board, string word) {
        if (board[x][y] != word[idx]) return false;
        if (idx == wordlen - 1) return true;
        for (int i = 0; i < 4; ++ i ) {
            int nx = x + dx[i], ny = y + dy[i];
            if (nx >= 0 && nx < m && ny >= 0 && ny < n) {
                if (vis[nx][ny]) continue;
                vis[nx][ny] = true;
                if (dfs(nx, ny, idx + 1, vis, board, word)) return true;
                vis[nx][ny] = false;
            }
        }
        return false;
    }
    bool exist(vector<vector<char>>& board, string word) {
        if (board.empty()) return false;
        wordlen = word.size();
        m = board.size();
        n = board[0].size();
        vector<vector<bool>> vis(m, vector<bool>(n));
        for (int i = 0; i < m; ++ i ) {
            for (int j = 0; j < n; ++ j ) {
                vis[i][j] = true;
                if (dfs(i, j, 0, vis, board, word)) return true;
                vis[i][j] = false;
            }
        }
        return false;
    }
};
```

```c++
// AcWing
class Solution {
public:
    vector<vector<char>> g;
    vector<vector<bool>> st;
    int n, m, k;
    string s;
    int dx[4] = {-1, 0, 0, 1}, dy[4] = {0, -1, 1, 0};
    
    bool dfs(int x, int y, int u) {
        if (g[x][y] != s[u])
            return false;
        if (u == k - 1)
            return true;
        
        st[x][y] = true;
        for (int i = 0; i < 4; ++ i ) {
            int nx = x + dx[i], ny = y + dy[i];
            if (nx < 0 || nx >= n || ny < 0 || ny >= m || st[nx][ny])
                continue;
            if (dfs(nx, ny, u + 1))
                return true;
        }
        st[x][y] = false;
        return false;
    }
    
    bool hasPath(vector<vector<char>>& matrix, string &str) {
        if (matrix.empty() || matrix[0].empty())
            return false;
        
        g = matrix;
        n = g.size(), m = g[0].size();
        st = vector<vector<bool>>(n, vector<bool>(m));
        s = str, k = s.size();
        
        for (int i = 0; i < n; ++ i )
            for (int j = 0; j < n; ++ j )
                if (dfs(i, j, 0))
                    return true;
        return false;
    }
};
```



```python
# DFS, 经典的搜索问题。最重要的是考虑顺序！
# 在进入递归的时候，首先要考虑 什么情况下就要返回！（满足条件/不满足条件）
# 我们首先枚举单词的起点，然后依次枚举单词的每个字母，在这过程中需要将已经用过的字母做标记，以避免重复使用字符。
# 这道题需要记录 具体的路径，BFS不方便记录，所以DFS更适合。
      
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        n, m = len(board), len(board[0])

        def dfs(x, y, word):
            if len(word) == 0:
                return True   # 踩坑1 ：首先要考虑啥时候返回True！！！
            tmp = board[x][y]
            board[x][y] = '/'
            dx, dy = [1, -1, 0, 0], [0, 0, 1, -1]
            for i in range(4):
                nx, ny = x + dx[i], y + dy[i]
                if 0 <= nx < n and 0 <= ny < m and board[nx][ny] == word[0]:
                    if dfs(nx, ny, word[1:]):
                        return True
            board[x][y] = tmp   # 踩坑2:记得恢复现场
            return False  # 踩坑3:上述条件不满足 就返回False

        for i in range(n):
            for j in range(m):
                if board[i][j] == word[0]:
                    if dfs(i, j, word[1:]):
                        return True
        return False
```



#### [13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/) [MID]

```c++
class Solution {
public:
    int res = 0;
    int dx[4] = {-1, 0, 0, 1}, dy[4] = {0, -1, 1, 0};
    void dfs(int x, int y, vector<vector<bool>>& vis, int m, int n, int k) {
        if (!check(x, y, k)) return;
        res ++ ;
        for (int i = 0; i < 4; ++ i ) {
            int nx = x + dx[i], ny = y + dy[i];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || vis[nx][ny]) continue;
            vis[nx][ny] = true;
            dfs(nx, ny, vis, m, n, k);
        }
        return;
    }
    bool check(int x, int y, int k) {
        int cnt = 0;
        while (x) {
            cnt += x % 10;
            x /= 10;
        }
        while (y) {
            cnt += y % 10;
            y /= 10;
        }
        return cnt <= k;
    }
    int movingCount(int m, int n, int k) {
        vector<vector<bool>> vis(m, vector<bool>(n));
        res = 0;
        vis[0][0] = true;
        dfs(0, 0, vis, m, n, k);
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int th, r, c;
    int res;
    bool st[55][55];
    
    int dx[4] = {-1, 0, 0, 1}, dy[4] = {0, -1, 1, 0};
    
    int get(int x) {
        int ret = 0;
        while (x)
            ret += x % 10, x /= 10;
        return ret;
    }
    
    void dfs(int x, int y) {
        if (x >= r || y >= c || get(x) + get(y) > th)
            return;
            
        st[x][y] = true;
        res ++ ;
        for (int i = 0; i < 4; ++ i ) {
            int nx = x + dx[i], ny = y + dy[i];
            if (nx < 0 || nx >= r || ny < 0 || ny >= c || st[nx][ny])
                continue;
            dfs(nx, ny);
        }
    }

    int movingCount(int threshold, int rows, int cols) {
        th = threshold, r = rows, c = cols;
        
        res = 0;
        dfs(0, 0);
        
        return res;
    }
};
```



```python
# 经典的BFS/DFS(也可以做)
# 从起点开始往下走，并且需要一个函数来判断 当前格子能不能走（sumALL)
# 如果当前格子走过 或者 当前格子数字之和太大，都需要Continue(直接跳过)

class Solution(object):
    def movingCount(self, n, m, k):
        if not n or not m:return 0
        st = [[False] * m for _ in range(n)]
        
        def sumAll(x, y):
            res = 0
            while x > 0:
                res += x % 10
                x //= 10
            while y > 0:
                res += y % 10
                y //= 10
            return res
        
        
        # DFS遍历
        def dfs(x, y):
            # nonlocal ans  #这个也可以，ans定义在外面，初始值为0 
            # if st[x][y] or sumAll(x, y) > k:return  # 这一条是多余的，因为进入的时候已经做了判断
            st[x][y] = True   #踩坑：记得把遍历过的格子状态更新
            self.res += 1
            dx, dy = [0,0,1,-1], [1,-1,0,0]
            for i in range(4):
                a, b = x + dx[i], y + dy[i]
                if 0 <= a < n and 0 <= b < m and not st[a][b] and sumAll(a, b) <= k:
                    dfs(a, b)
        self.res = 0 
        dfs(0, 0)
        return self.res
        
        
        # BFS
        from collections import deque
        q = deque()
        q.append([0,0])
        ans = 0 
        dx, dy = [0,0,1,-1], [1,-1,0,0]
        while q:
            t = q.popleft()
            x, y = t[0], t[1]
            if st[x][y] or sumAll(x,y) > k:continue # 这里有优化空间，可以提前遍历
            ans +=1 
            st[x][y] = True
            for i in range(4):
                nx, ny = x + dx[i], y + dy[i]
                if 0 <= nx < n and 0 <= ny < m and not st[nx][ny]:
                    q.append([nx,ny])
        return ans
        
        
        
        #BFS 提前判断：（DFS也可以提前判断，可以少一些进入到队列或者递归的次数）
        from collections import deque
        q = deque()
        res = 0
        q.append([0,0])
        st[0][0] = True
        while q:
            x, y = q.popleft()
            res += 1
            dx, dy = [0,0,1,-1], [1,-1,0,0]
            for i in range(4):
                nx, ny = x + dx[i], y + dy[i]
                if 0 <= nx < n and 0 <= ny < m and not st[nx][ny] and sumAll(nx, ny) <= k:
                    st[nx][ny] = True
                    q.append([nx, ny])
        return res
```



#### [14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/) [MID]

```c++
class Solution {
public:
    int cuttingRope(int n) {
        if (n <= 3) return n-1;
        int res = 1;
        if (n % 3 == 1) {
            res *= 4;
            n -= 4;
        }
        while (n >= 3) {
            res *= 3;
            n -= 3;
        }
        if (n == 2) res *= 2;
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int maxProductAfterCutting(int n) {
        if (n <= 3)
            return n - 1;
        
        int res = 1;
        if (n % 3 == 1)
            res *= 4, n -= 4;
        while (n >= 3)
            res *= 3, n -= 3;
        if (n == 2)
            res *= 2;
        return res;
    }
};
```



```python
# python3
# dp
# 状态表示：f[i] : 表示长度为i时的乘积方案数；属性：Max
# 状态转移：第一刀剪在长度为j, 那区别在于：后面的（i-j)是否还要再剪：
#          要剪：那就是j * f[i-j];不剪：j *(i-j)
class Solution(object):
    def maxProductAfterCutting(self,n):
        f = [0] * (n + 1)
        for i in range(2, n + 1):
            for j in range(1, i):
                f[i] = max(f[i], j * (i - j), j * f[i - j])
 
# 数学方法
class Solution:
    def cuttingRope(self, n: int) -> int:
        if n <= 3:return n - 1
        a, b = n // 3,n % 3
        if b == 0:return int(math.pow(3, a))
        if b == 1:return int(math.pow(3, a-1) * 4)
        return int(math.pow(3, a) * 2)
```



#### [14- II. 剪绳子 II](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/) [MID]

```c++
class Solution {
public:
    long long mod = 1e9+7;
    int cuttingRope(int n) {
        if (n <= 3) return n - 1;
        long long res = 1;
        if (n % 3 == 1) {
            res *= 4;
            n -= 4;
        }
        while (n >= 3) {
            res *= 3;
            res %= mod;
            n -= 3;
        }
        if (n == 2) res *= 2;
        return res % mod;    
    }
};
```



```python
# python3

```



#### [15. 二进制中1的个数](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/) [EASY]

```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int res = 0;
        while (n) {
            n = n & (n - 1);
            ++ res ;
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int NumberOf1(int n) {
        int res = 0;
        while (n)
            n = n & (n - 1), ++ res ;
        return res;
    }
};
```



```python
# python3
# 1. 需要考虑是负数的情况：如果是负数 需要做处理：把它与oxffffff做 & 运算
# 2. 然后其他都是一样的处理逻辑：用lowbit函数的方法来确认有多少个1
# 3. lowbit方法：x * (-x) : 可以得到x的最后一位的1

# 以下做法是没有考虑n为负数的情况
class Solution:
    def hammingWeight(self, n: int) -> int:
        res = 0
        while n:
            res += n & 1
            n >>= 1
        return res
      
# 当n为负数时，python和c++/java语言的存储处理不一致。所以需要对数 先进行处理。
class Solution(object):
    def NumberOf1(self,n):
        res = 0
        n = n & ((1 << 32) - 1)   # 正数的32位2进制表示不变，但负数变为正数
        while n:
            res +=  1
            n -= (n & -n)
        return res
```



#### [16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/) [MID]

```c++
class Solution {
public:
    double myPow(double x, int n) {
          // case
        if (x == 1) return 1;
        else if (x == -1) return n & 1 ? -1 : 1;
        if (n == INT_MIN) return 0;
        int N = n;
        if (n < 0) {
            N = -N;
            x = 1.0 / x;
        }
        double res = 1;
        while (N) {
            if (N & 1) res *= x;
            x *= x;
            N >>= 1;
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    // LL 解决 INT_MIN 的问题 [TAG]
    using LL = long long;
    double Power(double x, int exp) {
        bool is_minus = exp < 0;
        
        double res = 1;
        LL n = abs((LL)exp);
        while (n) {
            if (n & 1)
                res *= x;
            x *= x;
            n >>= 1;
        }
        return is_minus ? 1 / res : res;
    }
};
```



```python
# python3

```



#### [17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/) [EASY]

```c++
class Solution {
public:
    vector<int> printNumbers(int n) {
        int tot = 1;
        while (n -- ) tot *= 10;
        vector<int> res;
        for (int i = 1; i < tot; ++ i )
            res.push_back(i);
        return res;
    }
};
```



```python
# python3
class Solution:
    def printNumbers(self, n: int) -> List[int]:
        return [i for i in range(1,10**n)]
```



#### [18. 删除链表的节点](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/) [EASY]

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* deleteNode(ListNode* head, int val) {
        ListNode* dummy = new ListNode(-1);
        dummy->next = head;
        ListNode * pre = dummy, * now = dummy->next;
        while (now != nullptr && now->val != val) {
            pre = pre->next;
            now = now->next;
        }
        if (now == nullptr) return dummy->next;
        pre->next = now->next;
        return dummy->next;
    }
};
```



```python
# python3
# 需要一个辅助节点pre, cur, 然后画图就很好理解

class Solution:
    def deleteNode(self, head: ListNode, val: int) -> ListNode:
        dummy = ListNode(None)
        dummy.next = head 
        pre = dummy 
        cur = head 
        while cur and cur.val != val:
            cur = cur.next 
            pre = pre.next 
        pre.next = cur.next 
        return dummy.next

      
class Solution:
    def deleteNode(self,head:ListNode,val:int)->ListNode:
        if head.val == val:
            return head.next
        pre, cur = head, head.next
        while cur and cur.val!=val:
            pre, cur = cur, cur.next
        if cur:
            pre.next = cur.next
        return head
      
# 在O(1)的时间复杂度删除链表节点
# 由于是单链表，我们不能找到前驱节点，所以我们不能按常规方法将该节点删除。换一种思路，将下一个节点的值复制到当前节点，然后将下一个节点删除即可。
class Solution(object):
    def deleteNode(self, node):
        # p = node.next
        # node.val = p.val
        # node.next = p.next
        node.val, node.next = node.next.val, node.next.next
```



#### Plus: 删除链表中重复的节点(重复的节点都不保留)

```c++
// AcWing
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* deleteDuplication(ListNode* head) {
        ListNode * dummy = new ListNode(-1);
        dummy->next = head;
        
        ListNode * pre = dummy;
        
        while (pre->next) {
            auto cur = pre->next;
            while (cur && cur->val == pre->next->val)
                cur = cur->next;
            
            if (cur == pre->next->next)
                pre = pre->next;
            
            pre->next = cur;
        }
        
        return dummy->next;
    }
};
```

```python
# python3

class Solution(object):
    def deleteDuplication(self, head):
        dummy = ListNode(None)
        dummy.next = head

        pre = dummy
        cur = pre.next
        while cur:
            while cur and cur.val == pre.next.val:
                cur = cur.next
            if cur == pre.next.next: #当结束上述循环
                pre = pre.next
            pre.next = cur
        pre.next = None  #pre是最后一个节点
        return dummy.next
```



#### [19. 正则表达式匹配](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/) [HARD]

```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.size();
        int n = p.size();
        vector<vector<bool>> dp(m + 1, vector<bool>(n + 1));
        dp[0][0] = true;
        for (int i = 2; i <= n; ++ i )
            if (p[i-1] == '*') dp[0][i] = dp[0][i-2];
        for (int i = 1; i <= m; ++ i ) {
            for (int j = 1; j <= n; ++ j ) {
                if (s[i - 1] == p[j - 1] || p[j - 1] == '.') {
                    // s[i-1] p[j-1] 可以匹配
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (p[j-1] == '*') {
                    // 此时显然s[i-1] p[j-1] 不可以匹配 考虑使用p[j-2]位置
                    // if 不能匹配->不使用p[j-2]与p[j-1]组成的模式串
                    // else 能匹配->使用p[j-2]与p[j-1]组成的模式串1或多次
                    if (p[j - 2] != '.' && p[j - 2] != s[i - 1]) dp[i][j] = dp[i][j - 2];
                    else dp[i][j] = dp[i][j - 2] || dp[i - 1][j];
                }
            }
        }
        return dp[m][n];
    }
};
```

```c++
// AcWing
class Solution {
public:
    bool isMatch(string s, string p) {
        int n = s.size(), m = p.size();
        vector<vector<bool>> f(n + 1, vector<bool>(m + 1));
        f[0][0] = true;
        for (int i = 2; i <= m; ++ i )
            if (p[i - 1] == '*')
                f[0][i] = f[0][i - 2];
        for (int i = 1; i <= n; ++ i )
            for (int j = 1; j <= m; ++ j )
                if (s[i - 1] == p[j - 1] || p[j - 1] == '.')
                    f[i][j] = f[i - 1][j - 1];
                else if (p[j - 1] == '*') {
                    if (p[j - 2] != '.' && p[j - 2] != s[i - 1])
                        f[i][j] = f[i][j - 2];
                    else
                        f[i][j] = f[i][j - 2] | f[i - 1][j];
                }
        return f[n][m];
    }
};
```



```python
# 状态表示：f[i,j]: 表示 s[1-i] 和 p[1-j] 是否匹配；
# 状态转移：当前p[j]字符是什么？以p[j] 是否为 '*' 来区分
# 1) p[j] != '*'：那当且仅当s[i] == p[j] 或者 p[j] == '.'时，f[i][j] = f[i-1][j-1]
# 2）p[j] == '*'：那就是枚举通配符 '*' 可以匹配多少个p[j-1]
# 2.1）如果匹配0个，表示丢弃这一次的 '*' 和它之前的那个字符:f[i][j] = f[i][j-2]（不管前一个字符的s和前一个字符的p是否能匹配，都有这个情况）
# 2.2) 匹配一个，不丢弃前面那个字符，并且只保留一次字符，f[i][j] = f[i-1][j-2]
# 2.3）匹配2个（及以上），那s[i]这个字符是一定能被匹配的，就看前面的字符了: f[i][j] = f[i-1][j]
# 由于 f[i-1][j]是由f[i-1][j-2]转移过来的，所以前者包含了后者的情况。
# 2.2 和 2.3 可以统一写成 当s[i]和p[j-1]匹配，并且*匹配>=1的情况下 : f[i][j] = f[i-1][j]


# 最好的写法，把特殊情况拎出来
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        n, m = len(s), len(p)
        s, p = ' ' + s, ' ' + p
        f = [[False] * (m + 1) for _ in range(n + 1)]
        f[0][0] = True  # 初始值
        for i in range(2, m + 1):  # 特殊情况判断：当s字符串为空的时候
            if p[i] == '*':
                f[0][i] = f[0][i-2]
        for i in range(1, n + 1):
            for j in range(1, m + 1):
                if s[i] == p[j] or p[j] == '.':
                    f[i][j] = f[i-1][j-1]
                elif p[j] == '*':
                    if p[j-1] == s[i] or p[j-1] == '.':
                        f[i][j] = f[i][j-2] or f[i-1][j]  # 踩坑：这里也有舍弃前一个字符的时候
                    else:
                        f[i][j] = f[i][j-2]
        return f[n][m]
```



#### [20. 表示数值的字符串](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/) [MID]

```c++
class Solution {
public:
    bool isNumber(string s) {
        int len = s.size();
          // d1:整数部分 d2:小数部分 d3:幂次部分
        int p = 0, d1 = 0, dot = 0, d2 = 0, e = 0, d3 = 0;
        while (p < len && s[p] == ' ') ++ p ;
        if (s[p] == '-' || s[p] == '+') ++ p ;
        while (p < len && s[p] >= '0' && s[p] <= '9') d1 = ++ p ;
        if (p < len && s[p] == '.') {
            dot = ++ p ;
            while (p < len && s[p] >= '0' && s[p] <= '9') d2 = ++ p ;
        }
        if (dot && !d1 && !d2) return false;
        if (p < len && (d1 || d2) && s[p] == 'e') e = ++ p ;
        if (p < len && e && (s[p] == '+' | s[p] == '-')) ++ p ;
        while (p < len && s[p] >= '0' && s[p] <= '9') d3 = ++ p ;
        if (e && (!(d1 || d2) || !d3)) return false;
        while (p < len && s[p] == ' ') ++p;
        if (!d1 && !d2) return false;
        return p == len;
    }
};
```



```python
# python3
class Solution:
    def isNumber(self, s):
        s = s.strip()
        met_dot = met_e = met_digit = False
        for i, char in enumerate(s):
            if char in ['+', '-']:
                if i > 0 and (s[i-1] != 'e' and s[i-1] != 'E'):
                    return False
            elif char == '.':
                if met_dot or met_e: return False
                met_dot = True
            elif char == 'e' or char == 'E':
                if met_e or not met_digit:
                    return False
                met_e, met_digit = True, False
            elif char.isdigit():
                met_digit = True
            else:
                return False
        return met_digit
```



#### [21. 调整数组顺序使奇数位于偶数前面](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/) [EASY]

```c++
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        int len = nums.size();
        if (len <= 1) return nums;
        int l = 0, r = len-1;
        while (l < r) {
            while (l < r && nums[l] & 1) ++l;
            if (l >= r) break;
            while (l < r && (nums[r] % 2 == 0)) --r;
            // attention 不能写nums[r] & 1 == 0
            if (l >= r) break;
            swap(nums[l ++ ], nums[r -- ]);
        }
        return nums;
    }
};
```

```c++
// AcWing
class Solution {
public:
    void reOrderArray(vector<int> &array) {
        int l = 0, r = array.size() - 1;
        while (l < r) {
            while (l < r && array[l] & 1)
                ++ l ;
            while (l < r && !(array[r] & 1))
                -- r ;
            if (l < r)
                swap(array[l], array[r]);
        }
    }
};
```



```python
# python3
#双指针法
class Solution(object):
    def reOrderArray(self, arr):
        l, r = 0, len(arr) -1
        while l < r :
            while l < r and arr[l] % 2 == 1:
                l += 1
            while l < r and arr[r] % 2 == 0:
                r -= 1
            arr[l], arr[r] = arr[r], arr[l]
        return arr
```



#### [22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/) [EASY]

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* getKthFromEnd(ListNode* head, int k) {
        ListNode* dummy = new ListNode(-1);
        dummy->next = head;
        ListNode * slow = dummy, * fast = dummy;
        while (k -- ) {
            fast = fast->next;
        }
        while (fast->next != nullptr) {
            slow = slow->next;
            fast = fast->next;
        }
        return slow->next;
    }
      // another solution
      ListNode* getKthFromEnd(ListNode* head, int k) {
          ListNode* slow = head, *fast = head;
          while (k -- ) fast = fast->next;
          while (fast) {
              slow = slow->next;
              fast = fast->next;
        }
          return slow;
    }
};
```

```c++
// AcWing
class Solution {
public:
    ListNode* findKthToTail(ListNode* pListHead, int k) {
        auto p = pListHead;
        while (k -- ) {
            if (!p)
                return nullptr;
            p = p->next;
        }
            
        
        auto q = pListHead;
        while (p)
            p = p->next, q = q->next;
        return q;
    }
};
```



```python
# 双指针法：1. 让指针1先走k步， 2. 然后指针p1和p2一起走 直到p1为空 输出p2即可

class Solution(object):
    def findKthToTail(self, head, k):
        if not head:
            return None

        p1, p2 = head, head 
        for _ in range(k):
            if p1:
                p1 = p1.next 
            else:
                return None
        while p1:
            p1, p2 = p1.next, p2.next 
        return p2
```

#### Plus: 链表中环的入口结点

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *entryNodeOfLoop(ListNode *head) {
        ListNode * fast = head, * slow = head, * ret = nullptr;
        while (fast && fast->next) {
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) {
                // fast run more a circle
                ret = head;
                while (ret != slow)
                    ret = ret->next, slow = slow->next;
                break;
            }
        }
        return ret;
    }
};
```

​	

```python
# 1. 快慢指针：快指针一次走两步，慢指针一次走一步；
# 2. 如果两个指针相遇了，说明有环；
# 3. 如果有环的话，再让快指针指向head，然后 和慢指针同时走。快慢指针此时每次都只走一步，当两者再次相遇时，就是环入口。

class Solution(object):
    def entryNodeOfLoop(self, head):
        if not head or not head.next:return None
        pFast, pSlow = head, head
        while pFast and pFast.next:
            pFast = pFast.next.next
            pSlow = pSlow.next 
            if pFast == pSlow:
                pFast = head 
                while pFast != pSlow:
                    pFast, pSlow = pFast.next, pSlow.next 
                return pSlow
        return None
```





#### [24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/) [EASY]

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *cur = head, *pre = nullptr, *next;
        while (cur) {
            next = cur->next;
            cur->next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
};
```

```c++
// AcWing
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode * pre = nullptr, * cur = head;
        while (cur) {
            ListNode * next = cur->next;
            cur->next = pre;
            pre = cur, cur = next;
        }
        return pre;
    }
};
```



```python
# python3
#========= 迭代
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self,head:ListNode)->ListNode:
        cur,pre,p=head,None,None
        while cur:
            p=cur.next
            cur.next=pre
            pre=cur
            cur=p
        return pre


#========= 递归
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if not head or not head.next:  # 踩坑！
            return head
        cur = self.reverseList(head.next) # 这里最终递归返回的是尾节点
        head.next.next = head   # 对于任意一个节点，将它的next指向他本身
        head.next = None  # 最后将head.next置为None 
        return cur # 所以将它输出即可
```



#### [25. 合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/) [EASY]

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode(-1);
        ListNode* pre = dummy;
        while (l1 != nullptr && l2 != nullptr) {
            if (l1->val <= l2->val) {
                pre->next = l1;
                pre = l1;
                l1 = l1->next;
            } else {
                pre->next = l2;
                pre = l2;
                l2 = l2->next;
            }
        }
        if (l1 == nullptr) pre->next = l2;
        else pre->next = l1;
        return dummy->next;
    }
  
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1 == nullptr) return l2;
        else if (l2 == nullptr) return l1;
        else if (l1->val < l2->val) {
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        } else {
            l2->next = mergeTwoLists(l1, l2->next);
            return l2;
        }
    }
};
```

```c++
// AcWing
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* merge(ListNode* l1, ListNode* l2) {
        ListNode * ret = new ListNode(-1);
        ListNode * pre = ret;
        while (l1 && l2) {
            if (l1->val <= l2->val)
                pre->next = l1, l1 = l1->next;
            else
                pre->next = l2, l2 = l2->next;
            pre = pre->next;
        }
        pre->next = l1 ? l1 : l2;
        return ret->next;
    }
};
```



```python
# python3
#伪头节点dum节点，两个指针同时向后走即可。
class Solution:
    def mergeTwoLists(self,l1:ListNode,l2:ListNode)->ListNode:
        cur = dum = ListNode(0)
        while l1 and l2:
            if l1.val < l2.val:
                cur.next, l1 = l1, l1.next
            else:
                cur.next, l2 = l2, l2.next
            cur = cur.next
        cur.next = l1 if l1 else l2
        return dum.next
```



#### [26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/) [MID]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool helper(TreeNode* A, TreeNode* B) {
        if (!B) return true;
        if (!A) return false;
        if (A->val != B->val) return false;
        return helper(A->left, B->left) && helper(A->right, B->right);
    }
    bool isSubStructure(TreeNode* A, TreeNode* B) {
        if (!B || !A) return false;
        if (A->val == B->val) return helper(A, B) || isSubStructure(A->left, B) || isSubStructure(A->right, B);
        return isSubStructure(A->left, B) || isSubStructure(A->right, B);
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isSame(TreeNode * p1, TreeNode * p2) {
        if (!p2)
            return true;
        if (!p1 || p1->val != p2->val)
            return false;
        return isSame(p1->left, p2->left) && isSame(p1->right, p2->right);
    }

    bool hasSubtree(TreeNode* pRoot1, TreeNode* pRoot2) {
        if (!pRoot1 || !pRoot2)
            return false;

        return hasSubtree(pRoot1->left, pRoot2) || hasSubtree(pRoot1->right, pRoot2)
            || isSame(pRoot1, pRoot2);
    }
};
```



```python
# python3
# DFS，关注本层会发生的事情，递归的过程 就是其他层在重复本层的过程

class Solution(object):
    def hasSubtree(self, A, B):
        """
        :type pRoot1: TreeNode
        :type pRoot2: TreeNode
        :rtype: bool
        """
        def dfs(A, B):
            if not B:return True  # 踩坑，这一条需要放在下一条前面。因为当B为空的时候，已经可以返回True了
            if not A or A.val != B.val:return False
            return dfs(A.left, B.left) and dfs(A.right, B.right)
        
        if not A or not B:return False
        return dfs(A, B) or self.hasSubtree(A.left, B) or self.hasSubtree(A.right, B)
```



#### [27. 二叉树的镜像](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/) [EASY]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* mirrorTree(TreeNode* root) {
        if (!root) return root;
        TreeNode* l, *r;
        l = mirrorTree(root->right);
        r = mirrorTree(root->left);
        root->left = l;
        root->right = r;
        return root;
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    void mirror(TreeNode* root) {
        if (!root)
            return;
        
        mirror(root->left);
        mirror(root->right);
        
        swap(root->left, root->right);
    }
};
```



```python
# python3
#递归
class Solution:
    def mirrorTree(self,root:TreeNode)->TreeNode:
        if not root:
            return None
        root.left,root.right = self.mirrorTree(root.right), self.mirrorTree(root.left)
        return root

#不省略tmp的写法
class Solution:
    def mirrorTree(self, root: TreeNode) -> TreeNode:
        if not root: 
            return None
        tmp = root.left
        root.left = self.mirrorTree(root.right)
        root.right = self.mirrorTree(tmp)
        return root


```



#### [28. 对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/) [EASY]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool helper(TreeNode* l, TreeNode* r) {
        if (!l && !r) return true;
        else if (!l || !r) return false;
        return l->val == r->val && helper(l->left, r->right) && helper(l->right, r->left);
    }
    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        return helper(root->left, root->right);
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool mirror(TreeNode * l, TreeNode * r) {
        if (!l && !r)
            return true;
        if (!l || !r || l->val != r->val)
            return false;
        
        return mirror(l->left, r->right) && mirror(l->right, r->left);
    }

    bool isSymmetric(TreeNode* root) {
        if (!root)
            return true;
        return mirror(root->left, root->right);
    }
};
```



```python
# python3
# 递归中非常重要的两点：
# 1. 找到递归的出口（就是什么时候return 判断为True 或者加入到要求的结果中；
# 2. 递归的类似于 剪枝 的部分。不然递归会无穷止境下去。也就是找到不符合条件 不需要往下递归去做的部分

# 本题中：递归的出口就是 递归到L和R都不存在了，也就是所有的元素都递归判断过了，如果中间有过程不满足，中间就会判断为False，所以在这里最后就是return True
# 不符合条件，直接return False，要么就是有一颗子树已经遍历完了，要么就是两个值不相等

class Solution(object):
    def isSymmetric(self, root):
        def dfs(L, R):
            if not L and not R:  # 这个判断条件写在第一条
                return True
            if not L or not R or R.val != L.val:
                return False
            return dfs(L.left, R.right) and dfs(L.right, R.left)
    
        if not root:return True
        return dfs(root.left, root.right)
```



#### [29. 顺时针打印矩阵](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/) [EASY]

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> res;
        int m = matrix.size();
        if (!m) return res;
        int n = matrix[0].size();
        int u = 0, d = m - 1, l = 0, r = n - 1;
        while (u <= d && l <= r) {
            for (int i = l; i <= r; ++ i ) res.push_back(matrix[u][i]);
            if ( ++ u > d) break;
            for (int i = u; i <= d; ++ i ) res.push_back(matrix[i][r]);
            if ( -- r < l) break;
            for (int i = r; i >= l; -- i ) res.push_back(matrix[d][i]);
            if ( -- d < u) break;
            for (int i = d; i >= u; -- i ) res.push_back(matrix[i][l]);
            if ( ++ l > r) break;
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    vector<int> printMatrix(vector<vector<int> > matrix) {
        if (matrix.empty() || matrix[0].empty())
            return vector<int>();
        
        vector<int> res;
        int n = matrix.size(), m = matrix[0].size();
        int u = 0, d = n - 1, l = 0, r = m - 1;
        for (;;) {
            for (int i = l; i <= r; ++ i )
                res.push_back(matrix[u][i]);
            if ( ++ u > d)
                break;
            
            for (int i = u; i <= d; ++ i )
                res.push_back(matrix[i][r]);
            if ( -- r < l)
                break;
            
            for (int i = r; i >= l; -- i )
                res.push_back(matrix[d][i]);
            if ( -- d < u)
                break;
            
            for (int i = d; i >= u; -- i )
                res.push_back(matrix[i][l]);
            if ( ++ l > r)
                break;
        }
        return res;
    }
};
```



```python
# python3
class Solution(object):
    def printMatrix(self, arr):
        if len(arr) == 0 or len(arr[0]) == 0:  # 测试的数据很恶心，需要加le n(arr[0]) == 0的特殊case
            return []
        n, m =len(arr), len(arr[0])
        L, R, T, B = 0, m-1, 0, n-1
        res = []
        while True:
            for i in range(L, R + 1):
                res.append(arr[T][i])
            T += 1
            if T > B:break
            for i in range(T, B + 1):
                res.append(arr[i][R])
            R -= 1
            if L > R:break
            for i in range(R, L-1, -1):
                res.append(arr[B][i])
            B -= 1
            if T > B:break
            for i in range(B, T-1, -1):
                res.append(arr[i][L])
            L += 1
            if L > R:break
        return res
```



#### [30. 包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/) [EASY]

```c++
class MinStack {
    stack<int> s, mins;
public:
    /** initialize your data structure here. */
    MinStack() {
    }
    
    void push(int x) {
        if (s.empty() || x <= mins.top()) mins.push(x);
        else mins.push(mins.top());
        s.push(x);
    }
    
    void pop() {
        s.pop();
        mins.pop();
    }
    
    int top() {
        return s.top();
    }
    
    int min() {
        return mins.top();
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->min();
 */
```

```c++
// AcWing
class MinStack {
public:
    stack<int> st, mst;

    /** initialize your data structure here. */
    MinStack() {

    }
    
    void push(int x) {
        st.push(x);
        if (mst.empty() || mst.top() >= x)
            mst.push(x);
    }
    
    void pop() {
        if (st.top() == mst.top())
            mst.pop();
        st.pop();
    }
    
    int top() {
        return st.top();
    }
    
    int getMin() {
        return mst.top();
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```



```python
# python3
# 借助一个辅助栈min-B 专门存储最小，返回最小元素。
# 压入栈的时候，需要判断B中的情况，如果B不存在 or B中栈顶元素大于当前元素，那么应该把当前元素压入栈中；
# 在pop的时候， 需要判断A pop出去的元素是否还在B中存在，如果相等 就也要把B中的元素pop出去

class MinStack(object):
    def __init__(self):
        self.A,self.B = [], []

    def push(self, x):
        self.A.append(x)
        if not self.B or self.B[-1] >= x:
            self.B.append(x)

    def pop(self):
        if not self.A:return 
        x = self.A.pop()
        if self.B and self.B[-1] == x:
            self.B.pop()

    def top(self):
        if self.A:
            return self.A[-1]

    def getMin(self):
        return self.B[-1]
```



#### [31. 栈的压入、弹出序列](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/) [MID]

```c++
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        int m = pushed.size(), n = popped.size();
        if (m != n) return false;
        int p = 0;
        stack<int> s;
        for (int i = 0; i < n; ++ i ) {
            s.push(pushed[i]);
            while (!s.empty() && s.top() == popped[p]) {
                s.pop();
                 ++ p;
            }
        }
        return p == n;
    }
};
```

```c++
// AcWing
class Solution {
public:
    bool isPopOrder(vector<int> pushV,vector<int> popV) {
        int n = pushV.size(), m = popV.size();
        if (n != m)
            return false;
        
        int p = 0;
        stack<int> st;
        for (int i = 0; i < n; ++ i ) {
            st.push(pushV[i]);
            while (st.size() && st.top() == popV[p])
                st.pop(), p ++ ;
        }
        return p == m;
    }
};
```



```python
# python3 

# 思路：相当于在比较两个字符串是否匹配；但是 对于A而言，当前字符不一定能和B马上匹配使用，可能后续才会用到，所以需要用到栈的结构
# 用一个辅助栈s，将入栈序列压入s, 压入后 栈顶元素 和 出栈序列做对比，如果相同 就把用过的元素都pop出去（对于s 是pop出去，对于出栈序列 是指针++1）

class Solution(object):
    def isPopOrder(self, A, B):
        if len(A) != len(B):return False  # 踩坑：特殊case
        if not A and not B :return True   #踩坑： 特殊case
        stack = []
        p = 0
        for i in range(len(A)):
            stack.append(A[i])  # 踩坑，需要先压入再判断，否则会存在最后一个元素在栈内 没有被比较pop出去
            while stack and stack[-1] == B[p]:
                stack.pop()
                p += 1
        return p == len(B)
```



#### [32 - I. 从上到下打印二叉树](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/) [MID]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> levelOrder(TreeNode* root) {
        vector<int> res;
        if (!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        TreeNode* v;
        while (!q.empty()) {
            v = q.front();
            q.pop();
            res.push_back(v->val);
            if (v->left) q.push(v->left);
            if (v->right) q.push(v->right);
        }
        return res;
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> printFromTopToBottom(TreeNode* root) {
        vector<int> res;
        if (!root)
            return res;
        
        queue<TreeNode*> q;
        q.push(root);
        while (q.size()) {
            auto t = q.front(); q.pop();
            res.push_back(t->val);
            if (t->left)
                q.push(t->left);
            if (t->right)
                q.push(t->right);
        }
        return res;
    }
};
```



```python
# python3
# deque是双端队列，popleft的效率更高
# BFS 需要用到队列，然后按根 左 右的顺利append进入到队列中，再一个个popleft出来即可

class Solution:
    def printFromTopToBottom(self, root):
        if not root:return []
        from collections import deque
        q = deque()
        res = []
        q.append(root)
        
        while q:
            t = q.popleft()
            res.append(t.val)  # 踩坑：需要append进去的是val值
            if t.left:
                q.append(t.left)
            if t.right:
                q.append(t.right)
        return res
```



#### [32 - II. 从上到下打印二叉树 II](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/) [EASY]

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if (!root) return res;
        queue<TreeNode*> q;
        q.push(root);
        TreeNode* v;
        while (!q.empty()) {
            int tot = q.size();
            vector<int> tmp;
            for (int i = 0; i < tot; ++ i ) {
                v = q.front();
                tmp.push_back(v->val);
                q.pop();
                if (v->left) q.push(v->left);
                if (v->right) q.push(v->right);
            }
            res.push_back(tmp);
        }
        return res;
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> printFromTopToBottom(TreeNode* root) {
        vector<vector<int>> res;
        if (!root)
            return res;
        
        queue<TreeNode*> q;
        q.push(root);
        while (q.size()) {
            int sz = q.size();
            vector<int> ve;
            while (sz -- ) {
                auto t = q.front(); q.pop();
                ve.push_back(t->val);
                if (t->left)
                    q.push(t->left);
                if (t->right)
                    q.push(t->right);
            }
            res.push_back(ve);
        }
        return res;
    }
};
```



```python
# python3
# 和上一题不同的是，需要用一个临时数组来存储每一层的元素
# 1. 用一个for循环来遍历每一层的元素，在这个for循环中 将本层数据append到tmp中
# 2. 当退出当前for循环时，就把tmp存储的数据append到res中

class Solution(object):
    def printFromTopToBottom(self, root):
        if not root:return []
        from collections import deque 
        q = deque()
        q.append(root)
        res = []
        while q:
            tmp = []
            for _ in range(len(q)):
                t = q.popleft()
                tmp.append(t.val)
                if t.left:q.append(t.left)
                if t.right:q.append(t.right)
            res.append(tmp)
        return res
```



#### [32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/) [MID]

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if (!root) return res;
        stack<TreeNode*> sl, sr;
        sl.push(root);
        TreeNode* v;
        while (!sl.empty() || !sr.empty()) {
            vector<int> tmp;
            if (sl.empty()) {
                int tot = sr.size();
                for (int i = 0; i < tot; ++ i ) {
                    v = sr.top();
                    sr.pop();
                    tmp.push_back(v->val);
                    if (v->right) sl.push(v->right);
                    if (v->left) sl.push(v->left);
                }
            } else {
                int tot = sl.size();
                for (int i = 0; i < tot; ++ i ) {
                    v = sl.top();
                    sl.pop();
                    tmp.push_back(v->val);
                    if (v->left) sr.push(v->left);
                    if (v->right) sr.push(v->right);
                }
            }
            res.push_back(tmp);
        }
        return res;
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> printFromTopToBottom(TreeNode* root) {
        vector<vector<int>> res;
        if (!root)
            return res;
        
        queue<TreeNode*> q;
        q.push(root);
        int d = 0;
        while (q.size()) {
            int sz = q.size();
            vector<int> ve;
            while (sz -- ) {
                auto t = q.front(); q.pop();
                ve.push_back(t->val);
                if (t->left)
                    q.push(t->left);
                if (t->right)
                    q.push(t->right);
            }
            if (d & 1)
                reverse(ve.begin(), ve.end());
            d ++ ;
            res.push_back(ve);
        }
        return res;
    }
};
```



```python
# python3
# 需要判断一下 当前res长度的奇偶性，来判别是正序push进去 还是需要逆序

class Solution(object):
    def printFromTopToBottom(self, root):
        if not root:return []
        from collections import deque
        q = deque()
        q.append(root)
        res = []
        while q:
            tmp = []
            for _ in range(len(q)):
                t = q.popleft()
                tmp.append(t.val)
                if t.left:q.append(t.left)
                if t.right:q.append(t.right)
            if len(res) % 2 == 0:   # 如果当前的res的长度是偶数，说明本次tmp中存储的是偶数层(设根为 0 层)
                res.append(tmp)
            else:
                res.append(tmp[::-1]) # 否则将tmp翻转再加入结果中
        return res
```



#### [33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/) [MID]

[单调栈解法](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/solution/dan-diao-di-zeng-zhan-by-shi-huo-de-xia-tian/)

```c++
class Solution {
public:
    bool verifyPostorder(vector<int>& postorder) {
        int n = postorder.size();
        if (n<=1) return true;
        stack<int> s;
        int pre = INT_MAX;
        for (int i = n - 1; i >= 0; -- i ) {
            if (postorder[i] > pre) {
                return false;
            }
            while (!s.empty() && postorder[i] < s.top()) {
                pre = s.top();
                s.pop();
            }
            s.push(postorder[i]);
        }
        return true;
    }
};
```

```c++
// AcWing
class Solution {
public:
    bool verifySequenceOfBST(vector<int> sequence) {
        int n = sequence.size();
        stack<int> st;
        int pre = INT_MAX;
        for (int i = n - 1; i >= 0; -- i ) {
            if (sequence[i] > pre)
                return false;
            while (st.size() && sequence[i] < st.top()) {
                pre = st.top();
                st.pop();
            }
            st.push(sequence[i]);
        }
        return true;
    }
};

class Solution {
public:
    vector<int> seq;
    bool verifySequenceOfBST(vector<int> sequence) {
        seq = sequence;
        if (seq.empty()) return true;
        return dfs(0, seq.size() - 1);
    }
    bool dfs(int l, int r) {
        if (l >= r) return true;
        int root = seq[r];
        int k = l;
        while (k < r && seq[k] < root) k ++ ;
        for (int i = k; i < r; i ++ )
            if (seq[i] < root)
                return false;
        return dfs(l, k - 1) && dfs(k, r - 1);
    }
};
```



```python
# python3
# 普通做法：
# 二叉搜索树是：左 < 根 < 右；后续遍历顺序：左 右 根
# 1. 所以就先从头到尾遍历，找到第一个比 最后一个节点（也就是根节点）的值 大的位置，那个位置就是右子树的起点p。
# 2. 然后从p继续往后遍历直到根节点，如果这过程中 有数值小于 根节点的数值，那就返回false；如果没有的话，说明这一段是符合要求的，那么继续向下递归判断即可。

class Solution:
    def verifySequenceOfBST(self, seq):
        def dfs(l, r):
            if l >= r:return True
            for i in range(r)
                if seq[i] < seq[r]:
                    continue
            p = i
            while p < r:
                if seq[p] > seq[n]:
                    p += 1
                else:
                    return False
            return dfs(l, p - 1) and dfs(p, r - 1)
        
        n = len(seq)
        if n <= 1 :return True
        dfs(0, n - 1)
       
# 单调队列优化版
# 找到 根节点 的 左边 第一个比它 小 的数值的位置i, 该位置i + 1就是右子树的起点；

```



#### [34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/) [MID]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    void helper(TreeNode* root, int target) {
        if (!root) return;
        path.push_back(root->val);
        if (root->val == target && !root->left && !root->right) res.push_back(path);
        helper(root->left, target-root->val);
        helper(root->right, target-root->val);
        path.pop_back(); 
    }
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        helper(root, sum);
        return res;
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> res;
    vector<int> t;
    
    void dfs(TreeNode * r, int s) {
        if (!r)
            return;
        
        t.push_back(r->val);
        s -= r->val;
        
        if (!r->left && !r->right && !s)
            res.push_back(t);
        else {
            dfs(r->left, s);
            dfs(r->right, s);
        }
        
        t.pop_back();
    }
    
    vector<vector<int>> findPath(TreeNode* root, int sum) {
        dfs(root, sum);
        return res;
    }
};
```



```python
# python3
# DFS, 递归遍历左右两个子树有没有满足条件的。
# 递归出口：当sum ==0 并且当前节点没有左右子树，就把路径给append到res中
# 剪枝：当p不存在，或p的值大于sum的值，这个应该是一进入dfs函数就要判断，因为第一层root也需要立刻判断
# 
class Solution(object):
    def findPath(self, root, sum):
        def dfs(p, sum): 
            if not p or p.val > sum:return  # 踩坑1: 这个放在入口
            sum -= p.val   # 踩坑2:满足条件的话，先把满足条件的这个点加入
            path.append(p.val)
            if sum == 0 and not p.left and not p.right:# 然后才进入这里判断
                res.append(path[:])
            dfs(p.left, sum)   # 踩坑3： 需要把sum放入到递归函数入参里
            dfs(p.right, sum) # （不能用nonlocal sum）
            									 # 否则在dfs(p.left,sum)执行后，sum值发生了改变
            path.pop() # 踩坑4: 记得每次dfs后 都要把path清空
                           
        if not root:return []
        res, path = [], []
        dfs(root, sum)
        return res
```



#### [35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/) [MID]

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/
class Solution {
public:
    Node* copyRandomList(Node* head) {
        if (!head) return head;
        Node* p = head;
        while (p) {
            Node* n = new Node(p->val);
            n->next = p->next;
            n->random = p->random;
            p->next = n;
            p = n->next;
        }
        p = head;
        while (p) {
            if (p->next->random) p->next->random = p->next->random->next;
            p = p->next->next;
        }
        Node * oldp = head, * newp = head->next;
        Node * newl = newp;
        while (oldp) {
            oldp->next = oldp->next->next;
            if (newp->next) newp->next = newp->next->next;
            oldp = oldp->next;
            newp = newp->next;
        }
        return newl;
    }
};
```

```c++
// AcWing
/**
 * Definition for singly-linked list with a random pointer.
 * struct ListNode {
 *     int val;
 *     ListNode *next, *random;
 *     ListNode(int x) : val(x), next(NULL), random(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *copyRandomList(ListNode *head) {
        for (auto p = head; p; ) {
            auto np = new ListNode(p->val);
            np->next = p->next;
            p->next = np;
            p = np->next;
        }
        for (auto p = head; p; p = p->next->next )
            if (p->random)
                // p->next->random = p->next->random->next;
                p->next->random = p->random->next;
        
        auto dummy = new ListNode(-1);
        auto pre = dummy;
        for (auto p = head; p; p = p->next ) {
            pre->next = p->next;
            pre = pre->next;
            p->next = p->next->next;    // You can't modify the original list!
        }
        return dummy->next;
    }
};

```



```python
# python3
# 很经典的题。巧妙的方法：可以省掉一个哈希表的额外空间>
# 思路方法：1. 在每个节点的后面加上这个点的复制；2. 从前向后遍历所有点，对于有random指针的点，让p.next.random = p.random.next就OK; 3.把所有点拆出来

class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head:return head

        p = head    # 第一步：复制一个小弟
        while p:
            q = Node(p.val)
            q.next = p.next 
            p.next = q 
            p = p.next.next 

        p = head  # 第二步：赋值random指针
        while p:
            if p.random:
                p.next.random = p.random.next 
            p = p.next.next

        dummy = ListNode(None)  # 第三步：拆分
        cur = dummy
        p = head 
        while p:
            cur.next = p.next
            cur = cur.next 
            p = p.next.next
        return dummy.next
```



#### [36. 二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/) [MID]

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;

    Node() {}

    Node(int _val) {
        val = _val;
        left = NULL;
        right = NULL;
    }

    Node(int _val, Node* _left, Node* _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
public:
    void helper(Node* root, Node*& head, Node*& pre) {
        if (!root) return;
        helper(root->left, head, pre);
        if (!head) {
            head = root;    // 初始化
            pre = root;
        } else {
            pre->right = root;
            root->left = pre;
            pre = root;
        }
        helper(root->right, head, pre);
    }
    Node* treeToDoublyList(Node* root) {
        if (!root) return root;
        Node *head = nullptr,  *pre = nullptr;
        helper(root, head, pre);
        head->left = pre;
        pre->right = head;
        return head;
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode * head, * pre;
    
    void dfs(TreeNode * r) {
        if (!r)
            return;
        
        dfs(r->left);
        
        if (!pre)
            head = r, head->left = nullptr;
        else
            pre->right = r, r->left = pre;
        pre = r;
        
        dfs(r->right);
    }
    
    TreeNode* convert(TreeNode* root) {
        pre = nullptr;
        dfs(root);
        
        return head;
    }
};
```



```python
# python3
```



#### [37. 序列化二叉树](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/) [HARD]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Codec {
public:
    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        ostringstream out;
        queue<TreeNode*> q;
        q.push(root);
        TreeNode* tmp;
        while (!q.empty()) {
            tmp = q.front();
            q.pop();
            if (tmp != nullptr) {
                out << tmp->val<<" ";
                q.push(tmp->left);
                q.push(tmp->right);
            } else {
                out << "null ";
            }
        }
        return out.str();
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        istringstream in(data);
        string val;
        vector<TreeNode*> vec;
        while (in >> val) {
            if (val == "null") {
                vec.push_back(nullptr);
            } else vec.push_back(new TreeNode(stoi(val)));
        }
        int j = 1;
        for (int i = 0; i < vec.size(); ++ i ) {
            if (vec[i] == nullptr) continue;
            if (j<vec.size()) vec[i]->left = vec[j ++ ];
            if (j<vec.size()) vec[i]->right = vec[j ++ ];
        }
        return vec[0];
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        ostringstream out;
        queue<TreeNode*> q;
        q.push(root);
        while (q.size()) {
            auto t = q.front(); q.pop();
            if (t) {
                out << t->val << " ";
                q.push(t->left);
                q.push(t->right);
            } else
                out << "null ";
        }
        return out.str();
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        istringstream in(data);
        string val;
        vector<TreeNode*> ve;
        while (in >> val)
            if (val == "null")
                ve.push_back(nullptr);
            else
                ve.push_back(new TreeNode(stoi(val)));
        
        int j = 1, n = ve.size();
        for (int i = 0; i < n; ++ i ) {
            if (ve[i] == nullptr)
                continue;
            if (j < n)
                ve[i]->left = ve[j ++ ];
            if (j < n)
                ve[i]->right = ve[j ++ ];
        }
        return ve[0];
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        string res;
        dfs_s(root, res);
        return res;
    }

    void dfs_s(TreeNode *root, string &res)
    {
        if (!root) {
            res += "null ";
            return;
        }
        res += to_string(root->val) + ' ';
        dfs_s(root->left, res);
        dfs_s(root->right, res);
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        int u = 0;
        return dfs_d(data, u);
    }

    TreeNode* dfs_d(string data, int &u)
    {
        if (u == data.size()) return NULL;
        int k = u;
        while (data[k] != ' ') k ++ ;
        if (data[u] == 'n') {
            u = k + 1;
            return NULL;
        }
        int val = 0, sign = 1;
        if (u < k && data[u] == '-') sign = -1, u ++ ;
        for (int i = u; i < k; i ++ ) val = val * 10 + data[i] - '0';
        val *= sign;
        u = k + 1;
        auto root = new TreeNode(val);
        root->left = dfs_d(data, u);
        root->right = dfs_d(data, u);
        return root;
    }
};
```





```python
# python3

class Codec:
    def serialize(self, root):
        if not root:return "[]"
        queue=collections.deque()
        queue.append(root)
        res=[]
        while queue:
            node=queue.popleft()
            if node:
                res.append(str(node.val))
                queue.append(node.left)
                queue.append(node.right)
            else:res.append("null")
        return '['+','.join(res)+']'

    def deserialize(self,data):
        if data=="[]":return
        vals,i=data[1:-1].split(','),1
        root=TreeNode(int(vals[0]))
        queue=collections.deque()
        queue.append(root)
        while queue:
            node=queue.popleft()
            if vals[i]!="null":
                node.left=TreeNode(int(vals[i]))
                queue.append(node.left)
            i+=1
            if vals[i]!="null":
                node.right=TreeNode(int(vals[i]))
                queue.append(node.right)
            i+=1
        return root
```



#### [38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/) [MID]

```c++
class Solution {
public:
    void dfs(vector<string>& res, string s, string& track, vector<bool>& vis) {
        if (track.size() == s.size()) {
            res.push_back(track);
            return;
        }
        for (int i = 0; i < s.size(); ++ i ) {
            if (vis[i]) continue;
            if (i > 0 && vis[i - 1] && s[i - 1] == s[i]) continue;
            vis[i] = true;
            track.push_back(s[i]);
            dfs(res, s, track, vis);
            track.pop_back();
            vis[i] = false;
        }
    }
    vector<string> permutation(string s) {
        vector<string> res;
        if (s.empty()) return res;
        sort(s.begin(), s.end());
        int n = s.size();
        vector<bool> vis(n, false);
        string track;
        dfs(res, s, track, vis);
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    vector<vector<int>> res;
    vector<int> t, a;
    vector<bool> st;
    int n;
    
    void dfs(int u) {
        if (u == n) {
            res.push_back(t);
            return;
        }
        
        for (int i = 0; i < n; ++ i )
            if (!st[i]) {
                if (i && a[i] == a[i - 1] && !st[i - 1])
                    continue;
                
                st[i] = true;
                t.push_back(a[i]);
                dfs(u + 1);
                t.pop_back();
                st[i] = false;
            }
    }
    
    vector<vector<int>> permutation(vector<int>& nums) {
        a = nums;
        n = a.size();
        st = vector<bool>(n);
        sort(a.begin(), a.end());
        
        dfs(0);
        
        return res;
    }
};
```



```python
# python3
# 搜索：1. 需要一个数组判断当前数是不是被用过 2.需要排序判断当前数和前面一个数是否相同，如果当前数没有被用过，并且和前一个数相同，并且前一个数也没被用过，那么就跳过。

class Solution:
    def permutation(self, nums):
        if not nums:return None
        n = len(nums)
        nums.sort()
        used = [False] * n
        res = []
        
        def dfs(path, used):
            if len(path) == n:
                res.append(path[:])
                return 
            for i in range(n):
                if not used[i] : # 踩坑1: 首先就必须判断当前数 有没有被用过，没有被用过 才能进入到后续的判断中
                    if i > 0 and nums[i] == nums[i-1] and not used[i-1]:continue  #踩坑2: 判断条件写漏了not used[i-1] 踩坑2: i>0 (不是i > =0)!!!!会导致很多特殊case过不了，比如[3], [1,1,1]
                    used[i] = True  #踩坑3:只能先进行上述判断后，才能把当前数的状态改为true
                    path.append(nums[i])

                    dfs(path, used)
                    used[i] = False
                    path.pop()

        dfs([], used)
        return res
        # return res
```



#### [39. 数组中出现次数超过一半的数字](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/) [EASY]

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n = nums.size();
        int value = nums[0], votes = 1;
        for (int i = 1; i < n; ++ i ) {
            if (nums[i] == value) ++ votes ;
            else {
                votes ? --votes : (value = nums[i], votes = 1);
                // if (votes) -- votes;
                // else value = nums[i], votes = 1;
            }
       }
       return value;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int moreThanHalfNum_Solution(vector<int>& nums) {
        int n = nums.size();
        int vote = 1, val = nums[0];
        for (int i = 1; i < n; ++ i )
            if (nums[i] == val)
                ++ vote;
            else {
                -- vote;
                if (!vote)
                    vote = 1, val = nums[i];
            }
        return val;
    }
};
```



```python
# python3
# #投票计数法
class Solution(object):
    def moreThanHalfNum_Solution(self, nums):
        vote = 0 
        for x in nums:
            if vote == 0:
                a = x   # 踩坑1: 这里不需要再加一条vote += 1 ；后续if判断中会有。不然就会出错[4,2,2]
            if x == a:
                vote += 1
            else:vote -= 1
        return a
```



#### [40. 最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/) [EASY]

```c++
class Solution {
public:
    int partition(vector<int>& nums, int l, int r) {
        int pivot = nums[l];    // privot = nums[rand((r-l)%l+l)]
        while (l < r) {
            while (l < r && nums[r] >= pivot) -- r ;
            nums[l] = nums[r];
            while (l < r && nums[l] <= pivot) ++ l ;
            nums[r] = nums[l];
        }
        nums[l] = pivot;
        return l;
    }
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        int len = arr.size();
        vector<int> res;
        int l = 0, r = len - 1;
        while (l <= r) {
            int index = partition(arr, l, r);
            if (index == k - 1) {
                for (int i = 0; i < k; ++ i ) res.push_back(arr[i]);
                return res;
            } else if (index < k) {
                l = index + 1;
            } else r = index - 1;
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    // https://www.acwing.com/problem/content/submission/code_detail/4671993/
    int partition(vector<int> & a, int l, int r) {
        if (l >= r)
            return l;
        
        int i = l - 1, j = r + 1, x = a[l + r >> 1];
        while (i < j) {
            do i ++ ; while (a[i] < x);
            do j -- ; while (a[j] > x);
            if (i < j)
                swap(a[i], a[j]);
        }
        return j;
    }

    vector<int> getLeastNumbers_Solution(vector<int> input, int k) {
        vector<int> res;
        
        int n = input.size();
        int l = 0, r = n - 1;
        
        while (l <= r) {
            int m = partition(input, l, r);
            if (m == k - 1) {
                for (int i = 0; i < k; ++ i )
                    res.push_back(input[i]);
                break;
            } else if (m < k - 1)
                l = m + 1;
            else
                r = m;
        }
        sort(res.begin(), res.end());
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    vector<int> getLeastNumbers_Solution(vector<int> input, int k) {
        priority_queue<int> heap;
        for (auto x : input) {
            if (heap.size() < k || heap.top() > x) heap.push(x);
            if (heap.size() > k) heap.pop();
        }
        vector<int> res;
        while (heap.size()) res.push_back(heap.top()), heap.pop();
        reverse(res.begin(), res.end());
        return res;
    }
};
```



```python
# python3
# 快排的思想
class Solution:
    def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
        def partition(l, r):
            import random
            i = random.randint(l,r)
            arr[l], arr[i] = arr[i], arr[l]
            pivot = arr[l]
            while l < r:
                while l < r and pivot <= arr[r]:
                    r -= 1
                arr[l] = arr[r]    
                while l < r and arr[l] <= pivot:
                    l += 1
                arr[r] = arr[l]
            arr[l] = pivot    
            return l

        if k == 0: return []
        l, r = 0, len(arr) - 1
        while l < r:   # 本质上：在排除不合法的区间（思想和二分的思想相似）
            idx = partition(l,r)
            if idx < k - 1:
                l = idx + 1
            else:r = idx 
        return arr[:k]
        res.sort()   #最后再排序一下
        return res
```



#### [41. 数据流中的中位数](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/) [HARD]

```c++
class MedianFinder {
    priority_queue<int> lo;                              // 大顶堆 都比中位数小
    priority_queue<int, vector<int>, greater<int>> hi;   // 小顶堆
public:
    /** initialize your data structure here. */
    MedianFinder() {
    }
    
    void addNum(int num) {
        lo.push(num);
        hi.push(lo.top());
        lo.pop();
        if (lo.size() < hi.size()) {
            lo.push(hi.top());
            hi.pop();
        }
    }
    
    double findMedian() {
        return lo.size() > hi.size() ? (double)lo.top() : (lo.top() + hi.top())*0.5;
    }
};
```

```c++
// AcWing
class Solution {
public:
    priority_queue<int> lo;
    priority_queue<int, vector<int>, greater<int>> hi;

    void insert(int num){
        lo.push(num);
        hi.push(lo.top());
        lo.pop();
        
        if (lo.size() < hi.size()) {
            lo.push(hi.top());
            hi.pop();
        }
    }

    double getMedian(){
        return lo.size() > hi.size() ? lo.top() : (double)(lo.top() + hi.top()) / 2.0;
    }
};
```



```python
# python3

# 思路比较精巧：利用大小堆求解一个不断更新的数组的中位数
# 将数分为两个部分，用大根堆存储较小的那部分数；用小根堆存储较大的那部分数；大根堆/小根堆的顶部就是我们需要的数字。
# 我们必须维护好两个堆中元素的个数关系，元素的大小关系，即大根堆的所有元素理应比小根堆的所有元素要小，如果违反了此规则，就需要进行元素的对换。
# 如果当前数的个数是奇数，那么就返回大根堆的堆顶；如果当前数的个数是偶数，那么就返回 大根堆和小根堆的堆顶的平均值。
# 数据流过来一个数，就直接加入到大根堆中，做了调整后（维护成了一个大根堆后）然后再判断：
# 1. 如果大根堆的堆顶元素 > 小根堆的堆顶元素，那么就交换两个堆顶元素（在交换2个堆的元素的时候，一定要 先判断上面的小根堆中有没有元素。 上面的小根堆中 没有元素是不能交换的）
# 2. 当大根堆的元素总数 > 小根堆的元素总数 + 1( 也就是多2个的时候，就需要把大根堆的堆顶放到小根堆中去)


from heapq import *
class Solution:
    def __init__ (self):
        self.maxheap = [] # 大根堆放置较小的一半元素
        self.minheap = [] # 小根放置较大的一半元素
    def insert(self, num):
        heappush(self.maxheap, -num) # 新元素无条件先插到大根堆, 由于python默认结构为小根堆，所以对大根堆插入和弹出元素都要取相反数  踩坑！：记得数字取反后 再加入到大根堆里
        if len(self.minheap) and -self.maxheap[0] > self.minheap[0]:  # 若小根堆非空，且大根堆堆顶元素大于小根堆堆顶元素，则交换两个数所在堆
            maxv = -heappop(self.maxheap) #heappop弹出最小的元素（总是位于索引0处），并确保剩余元素中最小的那个位于索引0处（保持堆特征）
            minv = heappop(self.minheap)
            heappush(self.maxheap, - minv)  # ！！！踩坑2: 同理！！要取反！
            heappush(self.minheap, maxv)
        if len(self.maxheap) > len(self.minheap) + 1:
            heappush(self.minheap, - heappop(self.maxheap)) 

    def getMedian(self):
        if len(self.maxheap) + len(self.minheap) & 1: # 若总数为奇数，返回大根堆堆顶元素
            return -self.maxheap[0]
        return (-self.maxheap[0] + self.minheap[0])/2.0 # 否则返回两个堆的堆顶元素求平均； python中对整数的除法是：//, 对保留小数是：/
```



#### [42. 连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/) [EASY]

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        if (!n) return 0;
        int res = INT_MIN, sum = 0;
        for (int i = 0; i < n; ++ i ) {
            sum = max(nums[i], nums[i] + sum);
            res = max(res, pre);
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res = INT_MIN, s = 0;
        for (auto v : nums) {
            s = max(s, 0) + v;
            if (s > res)
                res = s;
        }
        return res;
    }
};
```



```python
# python3
# dp, 比较特殊，只需要用一个变量来表示就可以 s: 表示的是以前一个数为结尾的子数组的和的最大值是多少
class Solution(object):
    def maxSubArray(self, nums):
        # 更新：1. s > 0，以当前数为结尾的子数组的和为：s + x； 2. s <= 0, 那以当前数为结尾的子数组的和为： x
        res, s = float('-inf'), 0
        for x in nums:
            if s < 0:s = 0
            s += x
            res = max(res, s)
        return res
```



#### [43. 1～n整数中1出现的次数](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/) [MID]

```c++
class Solution {
public:
    int countDigitOne(int n) {
        int res = 0;
        long long base = 1;
        while (base <= n) {
            int t = (n / base) % 10;
            if (t == 0) res += n / (base * 10) * base; // front
            else if (t == 1) res += n / (base * 10) * base + n % base + 1;
            else res += (n / (base * 10) + 1) * base;
            base *= 10;
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int numberOf1Between1AndN_Solution(int n) {
        int res = 0;
        for (int i = 1; i <= n; i *= 10) {
            int a = n / i, b = n % i;
            // 之所以补8，是因为当百位为0，则a/10==(a+8)/10，
            // 当百位>=2，补8会产生进位位，效果等同于(a/10+1)
            res += (a + 8) / 10 * i + ((a % 10 == 1) ? b + 1 : 0);
        }
        return res;
    }
};
// 总结一下以上的算法，可以看到，当计算右数第 i 位包含的 X 的个数时：

// 取第 i 位左边（高位）的数字，乘以 10i−1，得到基础值 a。
// 取第 i 位数字，计算修正值： 
// 如果大于 X，则结果为 a+10i−1。
// 如果小于 X，则结果为 a。
// 如果等 X，则取第 i 位右边（低位）数字，设为 b，最后结果为 a+b+1。

class Solution {
public:
    int numberOf1Between1AndN_Solution(int n) {
        if (!n) return 0;
        vector<int> number;
        while (n) number.push_back(n % 10), n /= 10;
        long long res = 0;
        for (int i = number.size() - 1; i >= 0; i -- ) {
            int left = 0, right = 0, t = 1;
            for (int j = number.size() - 1; j > i; j -- ) left = left * 10 + number[j];
            for (int j = i - 1; j >= 0; j -- ) right = right * 10 + number[j], t *= 10;
            res += left * t;
            if (number[i] == 1) res += right + 1;
            else if (number[i] > 1) res += t;
        }
        return res;
    }
}
```



```python
# python3
```



#### [44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/) [MID]

```c++
class Solution {
public:
    int findNthDigit(int n) {
        if (n < 10) return n;
        int base = 1;
        // 0-9 10-99 100-999
        // 9 90*2 900*3
        while (n > 9 * pow(10, base - 1) * base){
            n -= 9 * pow(10, base - 1) * base;
            ++ base ;
        }
        // pow(10, base-1) 为该位宽的第一个数
        int value = pow(10, base - 1) + n / base;
        int mod = n % base;
        if (mod) return (value / (int)pow(10, base - mod)) % 10;// 当前数的某一位
        return (value - 1) % 10;    // 上个数的末尾
    }
};
```

```c++
// AcWing
// [TAG]
class Solution {
public:
    int digitAtIndex(int n) {
        long long i = 1, num = 9, base = 1;
        while (n > i * num) {
            n -= i * num;
            i ++ ;
            num *= 10;
            base *= 10;
        }
        int number = base + (n + i - 1) / i - 1;
        int r = n % i ? n % i : i;
        for (int j = 0; j < i - r; ++ j )
            number /= 10;
        return number % 10;
    }
};
```



```python
# python3
```



#### [45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/) [MID]

```c++
class Solution {
public:
    string minNumber(vector<int>& nums) {
        auto cmp = [](string sa, string sb){return sa + sb < sb + sa;};
        vector<string> t;
        for (auto v : nums) t.push_back(to_string(v));
        sort(t.begin(), t.end(), cmp);
        string res;
        for (auto s : t) res+=s;
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    string printMinNumber(vector<int>& nums) {
        vector<string> ve;
        for (auto v : nums)
            ve.push_back(to_string(v));
        sort(ve.begin(), ve.end(), [](const string & a, const string & b) {
            return a + b < b + a;
        });
        
        string res;
        for (auto v : ve)
            res += v;
        return res;
    }
};
```



```python
# python3

# 思路不好想，需要反复思考记忆一下,类似于插入排序的思想
class Solution(object):
    def printMinNumber(self, nums):
        n = len(nums)
        if n == 0:return ''
        snums = list(map(str, nums))
        
        for i in range(n):
            for j in range(i + 1, n):
                if snums[i] + snums[j] > snums[j] + snums[i]:
                    snums[i], snums[j] = snums[j], snums[i]
        return ''.join(snums)
```



#### [46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/) [MID]

```c++
class Solution {
public:
    int translateNum(int num) {
        string v = to_string(num);
        int n = v.size();
        if (n <= 1) return 1;
        vector<int> dp(n + 1);
        dp[1] = 1;dp[0] = 1;
        for (int i = 2; i <= n; ++ i ) {
            dp[i] = dp[i - 1];        // dp[i] 为v[i-1]字符对应的dp值
            if (v[i - 2] == '1' && v[i - 1] >= '0' && v[i - 1] <= '9')
                dp[i] += dp[i - 2];
            else if (v[i - 2] == '2' && v[i - 1] >= '0' && v[i - 1] <= '5')
                dp[i] += dp[i - 2];
        }
        return dp[n];
    }
};
```

```c++
// AcWing
class Solution {
public:
    int getTranslationCount(string s) {
        int n = s.size();
        vector<int> f(n + 1);
        f[0] = 1;
        for (int i = 1; i <= n; ++ i ) {
            f[i] = f[i - 1];
            int t = (i >= 2) * (s[i - 2] - '0') * 10 + s[i - 1] - '0';
            if (t >= 10 && t <= 25)
                f[i] += f[i - 2];
        }
        return f[n];
    }
};
```



```python
# python3
class Solution:
    def translateNum(self, num: int) -> int:
        s=str(num)
        n=len(s)
        dp=[1 for _ in range(n+1)]
        for i in range(2,n+1):
            dp[i]=dp[i-1]
            if s[i-2]=='1':
                dp[i]+=dp[i-2]
            elif s[i-2]=='2' and s[i-1]<'6':
                dp[i]+=dp[i-2]
        return dp[n]
      
 # python3    
class Solution:
    def translateNum(self, num: int) -> int:
        s = str(num)
        a = b = 1
        for i in range(2, len(s) + 1):
            a, b = (a + b if "10" <= s[i - 2:i] <= "25" else a), a
        return a
```



#### [47. 礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/) [MID]

```c++
class Solution {
public:
    int maxValue(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        vector<int> dp(n + 1);
        for (int i = 0; i < n; ++ i ) dp[i + 1] = dp[i] + grid[0][i];
        for (int i = 1; i < m; ++ i )
            for (int j = 0; j < n; ++ j )
                dp[j + 1] = max(dp[j], dp[j + 1]) + grid[i][j];
        return dp[n];
    }
};
```

```c++
// AcWing
class Solution {
public:
    int getMaxValue(vector<vector<int>>& grid) {
        if (grid.empty() || grid[0].empty())
            return 0;
        
        int n = grid.size(), m = grid[0].size();
        
        vector<int> f(m + 1);
        for (int i = 1; i <= n; ++ i )
            for (int j = 1; j <= m; ++ j )
                f[j] = max(f[j], f[j - 1]) + grid[i - 1][j - 1];
        return f[m];
    }
};
```





```python
# python3
# 当已知n, m 都大于0       
class Solution(object):
    def getMaxValue(self, grid):
        if not grid:return 0
        n, m = len(grid), len(grid[0])
        f = [[0] * (m + 1) for _ in range(n + 1)]
        for i in range(n):
            for j in range(m):
                f[i][j] = max(f[i-1][j],f[i][j-1]) + grid[i][j]
        return f[n-1][m-1]

# n,m 可能一方为0的情况
class Solution:
    def maxValue(self,grid:List[List[int]])->int:
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if i == 0 and j == 0:continue
                if i == 0:grid[i][j] += grid[i][j-1]
                elif j == 0:grid[i][j] += grid[i-1][j]
                else:grid[i][j]+=max(grid[i][j-1],grid[i-1][j])
        return grid[-1][-1]
```



#### [48. 最长不含重复字符的子字符串](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/) [MID]

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> m(300, -1);
        int res = 0, n = s.size(), l = -1;
        for (int i = 0; i < n; ++ i ) {
            if (m[s[i]] > l)
                l = m[s[i]];
            res = max(res, i - l);
            m[s[i]] = i;
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int longestSubstringWithoutDuplication(string s) {
        int n = s.size();
        unordered_map<char, int> hash;
        
        int res = 0;
        for (int i = 0, j = 0; j < n; ++ j ) {
            hash[s[j]] ++ ;
            while (i < j && hash[s[j]] > 1)
                hash[s[i ++ ]] -- ;
            res = max(res, j - i + 1);
        }
        return res;
    }
};
```



```python
# python3
###双指针法
class Solution:
    def longestSubstringWithoutDuplication(self, s):
        if len(s) <= 1:return len(s)
        n = len(s)
        res = 0
        l, r = 0, 0
        while r < n - 1:
            r += 1
            if s[r] not in s[l:r]:
                res = max(r - l +1, res)
            else:
                while s[r] in s[l:r]:
                    l += 1
        return res


      
#双指针+hash表优化，hash表记录每一个字符出现的位置的后面一个位置
class Solution:
    def longestSubstringWithoutDuplication(self, s):
        n = len(s)-1
        dic = {}
        l, r, res=0, 0, 0
        for r in range(n + 1):
            if s[r] in dic:
                l = max(my_dic[s[r]], l)
            dic[s[r]] = r + 1
            res = max(res,r - l + 1)
        return res
```



#### [49. 丑数](https://leetcode-cn.com/problems/chou-shu-lcof/) [MID]

```c++
class Solution {
public:
    int nthUglyNumber(int n) {
        int two = 0, three = 0, five = 0;
        vector<long long> ugly;
        ugly.push_back(1ll);
        long long v = 1;
        while ( -- n) {
            v = min(ugly[two] * 2, ugly[three] * 3);
            v = min(v, ugly[five] * 5);
            ugly.push_back(v);
            if (v % 2 == 0) ++ two ;
            if (v % 3 == 0) ++ three ;
            if (v % 5 == 0) ++ five ;
        }
        return v;
    }
};
```

```c++
class Solution {
public:
    int getUglyNumber(int n) {
        int p2 = 0, p3 = 0, p5 = 0;
        vector<int> u;
        u.push_back(1);
        while ( -- n) {
            int t = min(min(u[p2] * 2, u[p3] * 3), u[p5] * 5);
            u.push_back(t);
            if (u[p2] * 2 == t)
                ++ p2 ;
            if (u[p3] * 3 == t)
                ++ p3 ;
            if (u[p5] * 5 == t)
                ++ p5 ;
        }
        return u.back();
    }
};
```



```python
# python3

# 法一：dp
# f[i]: 从小到大排列的第i个丑数值
# 如何转移过来呢？用k个指针指向dp中的元素，最小的丑数只可能出现在如dp[l2]的2倍、dp[l7]的7倍、dp[l13]的13倍和dp[l19]的19倍四者中间。通过移动k个指针，就能保证生成的丑数是有序的。通过求到最小值来保证丑数数组有序排列。
# 初始条件：题目给定条件为1 是任何给定 primes 的超级丑数。所以dp[0] = 1

class Solution:
    def nthUglyNumber(self, n: int) -> int:
        # a, b, c = 0, 0, 0
        # f = [1] * n 
        # for i in range(1, n):
        #     p2, p3, p5 = f[a] * 2, f[b] * 3, f[c]  * 5
        #     f[i] = min(p2, p3, p5)
        #     if f[i] == p2:a += 1
        #     if f[i] == p3:b += 1
        #     if f[i] == p5:c += 1
        # return f[-1]


        # 统一dp写法
        nums = [2, 3, 5]
        m = len(nums)
        p = [0] * m
        f = [1] * n 
        for i in range(1, n):
            f[i] = min(x * f[y] for x, y in zip(nums, p))  # zip用得非常秒啊
            for j in range(m):
                if f[i] == nums[j] * f[p[j]]:
                    p[j] += 1 
        return f[-1]
      
# 最小堆：因为丑数是2, 3, 5的倍数，我们不断把它们的倍数压入栈中，再按顺序弹出
# 法2: 小根堆
        import heapq
        # heap = [1]
        # heapq.heapify(heap)
        heap = []
        heapq.heappush(heap, 1)
        res = 0
        for _ in range(n):
            res = heapq.heappop(heap)
            while heap and res == heap[0]:
                res = heapq.heappop(heap)
            a, b, c = res * 2, res * 3, res * 5
            for t in [a, b, c]:
                heapq.heappush(heap, t)
            print(heap)
        return res

```



#### Plus: [263. 丑数](https://leetcode-cn.com/problems/ugly-number/)

```c++







```

```python
# 法1: 递归
# class Solution:
#     def isUgly(self, n: int) -> bool:
#         if n == 0:return False
#         if n == 1:return True
#         if n % 2 == 0:return self.isUgly(n // 2)
#         if n % 3 == 0:return self.isUgly(n // 3)
#         if n % 5 == 0:return self.isUgly(n // 5)
#         return False

# 法2: 迭代
class Solution:
    def isUgly(self, n: int) -> bool:
        if n == 0:return False 
        for p in 2,3,5:
            while n and n % p == 0:
                n //= p 
        return n == 1
```



#### Plus: [313. 超级丑数](https://leetcode-cn.com/problems/super-ugly-number/)

```c++

```

```python
class Solution:
    def nthSuperUglyNumber(self, n: int, primes: List[int]) -> int:
        m = len(primes)
        p = [0] * m 
        f = [1] * n  #初始化
        for i in range(1, n):
            f[i] = min( x * f[y] for x, y in zip(primes, p))
            for j in range(m):
                if f[i] == f[p[j]] * primes[j]:
                    p[j] += 1
        return f[-1]
```



#### [50. 第一个只出现一次的字符](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/) [EASY]

```c++
class Solution {
public:
    char firstUniqChar(string s) {
        int n = s.size();
        if (!n) return ' ';
        vector<int> cnt(26);
        for (int i = 0; i < n; ++ i )
            ++ cnt[s[i] - 'a'] ;
        for (int i = 0; i < n; ++ i )
            if (cnt[s[i] - 'a'] == 1) return s[i];
        return ' ';
    }
};
```

```c++
// AcWing
class Solution {
public:
    char firstNotRepeatingChar(string s) {
        unordered_map<char, int> hash;
        for (auto c : s)
            hash[c] ++ ;
        for (auto c : s)
            if (hash[c] == 1)
                return c;
        return '#';
    }
};
```



```python
# python3
# 用collections模块里的defaultdict，方法里填入类型，比如int,表示当为空的时候，默认初始化为0

class Solution:
    def firstNotRepeatingChar(self, s):
        import collections
        if not s:return '#'
        my_dic = collections.defaultdict(int)
        for x in s:
            my_dic[x] += 1
        for x in s:
            if my_dic[x] == 1:
                return x
                break
        return '#'
```

#### Plus: 字符流中第一个只出现一次的字符

```c++
// AcWing
class Solution{
public:
    unordered_map<char, int> hash;
    queue<char> q;

    //Insert one char from stringstream
    void insert(char ch){
        q.push(ch);
        if ( ++ hash[ch] > 1)
            while (q.size() && hash[q.front()] > 1)
                q.pop();
    }
    //return the first appearence once char in current stringstream
    char firstAppearingOnce(){
        return q.empty() ? '#' : q.front();
    }
};
```



```python
# 如何把O(n*n)算法优化成O(N) : 双指针，单调队列（找工作面试时的优化方式）
# 首先看一下答案是不是单调的？从前往后走，找第一个没有被划掉的位置。（答案的位置是从前往后递增的，具备一定的单调性）
# 可以用双指针算法 进行优化。（具备单调性，才能用双指针算法）
# 在实现的时候，可以换一种实现方式，比如队列（队列本身就是个双指针）
# 判断队头元素出现的次数是否大于1，如果大于1了，就直接删除。

from collections import deque

class Solution:  
    def __init__(self):
        self.dic = {}
        self.q = deque()
        
    def firstAppearingOnce(self):
        if not self.q:return '#'
        return self.q[0]
        
    def insert(self, char):
        if char in self.dic:
            self.dic[char] += 1
            while self.q and self.dic[self.q[0]] > 1:
                self.q.popleft()
        else:
            self.dic[char] = 1
            self.q.append(char)
```





#### [51. 数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/) [HARD]

```c++
class Solution {
public:
    int mergeSort(vector<int>& nums, vector<int>& tmp, int l, int r) {
        if (l >= r) return 0;
        int mid = l + (r - l) / 2;
        int cnt = mergeSort(nums, tmp, l, mid) + mergeSort(nums, tmp, mid + 1, r);
        int i = l, j = mid + 1, pos = l;
        while (i <= mid && j <= r) {
            if (nums[i] <= nums[j]) {
                tmp[pos ++ ] = nums[i ++ ];
            } else {
                cnt += mid + 1 - i;
                tmp[pos ++ ] = nums[j ++ ];
            }
        }
        for (int k = i; k <= mid; ++ k ) tmp[pos ++ ] = nums[k];
        for (int k = j; k <= r; ++ k ) tmp[pos ++ ] = nums[k];
        copy(tmp.begin() + l, tmp.begin() + r + 1, nums.begin() + l);
        return cnt;
    }
    int reversePairs(vector<int>& nums) {
        int n = nums.size();
        vector<int> tmp(n);
        return mergeSort(nums, tmp, 0, n - 1);
    }
};
```

```c++
// AcWing
class Solution {
public:
    vector<int> a, t;
    int n;
    
    int merge(int l, int r) {
        if (l >= r)
            return 0;
        
        int m = l + r >> 1;
        int ret = merge(l, m) + merge(m + 1, r);
        int i = l, j = m + 1, p = l;
        while (i <= m && j <= r)
            if (a[i] <= a[j])
                t[p ++ ] = a[i ++ ];
            else
                ret += m - i + 1, t[p ++ ] = a[j ++ ];
        
        while (i <= m)
            t[p ++ ] = a[i ++ ];
        while (j <= r)
            t[p ++ ] = a[j ++ ];
        for (int i = l; i <= r; ++ i )
            a[i] = t[i];
        
        return ret;
    }
    
    int inversePairs(vector<int>& nums) {
        a = t = nums;
        n = a.size();
        return merge(0, n - 1);
    }
};
```



```python
class Solution(object):
    def inversePairs(self, nums):
        def mergeSort(l, r):
            nonlocal res   # 踩坑1. 注意res需要在递归中变化 所以要用nonlocal才能改变全局变量的值
            if l >= r:return  # 注意 l == r的时候 也需要return. 不需要继续递归了
            m = l + (r - l)//2
            mergeSort(l, m)
            mergeSort(m + 1, r)
            
            p1, p2 = l, m + 1
            tmp = []
            while p1 <= m and p2 <= r:
                if nums[p1] > nums[p2]:
                    res += m - p1 + 1
                    tmp.append(nums[p2])
                    p2 += 1
                else:
                    tmp.append(nums[p1])
                    p1 += 1
            while p1 <= m:
                tmp.append(nums[p1])
                p1 += 1
            while p2 <= r:
                tmp.append(nums[p2])
                p2 += 1
            for i in range(len(tmp)):
                nums[l + i] = tmp[i]
        
        n = len(nums)
        if n <=1 :return 0
        res = 0
        mergeSort(0, n - 1)
        return res
```



#### [52. 两个链表的第一个公共节点](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/) [EASY]

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* l1 = headA, *l2 = headB;
        while (l1 != l2) {
            l1 = l1 ? l1->next : headB;
            l2 = l2 ? l2->next : headA;
        }
        return l1;
    }
};
```

```c++
// AcWing
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *findFirstCommonNode(ListNode *headA, ListNode *headB) {
        auto l1 = headA, l2 = headB;
        while (l1 != l2) {
            l1 = l1 ? l1->next : headB;
            l2 = l2 ? l2->next : headA;
        }
        return l1;
    }
};
```



```python
# python3
# 比较精巧的一道题，方法如下：
# 1. 两个指针分别指向两个链表头，当p1走到第一条链表的尾部时，就让他指向第二条链表的表头；，当p2走到第一条链表的尾部时，就让他指向第一条链表的表头
# 2. 当两个指针指向同一个节点的时候输出答案即可：要么相遇走到了同一节点，要么就是同时走到了链表尾部null

class Solution(object):
    def findFirstCommonNode(self, headA, headB):
        if not headB or not headA:return None
        p1, p2 = headA, headB
        while p1 != p2:
            if p1:
                p1 = p1.next 
            else:
                p1 = headB
            if p2:
                p2 = p2.next
            else:
                p2 = headA 
        return p1
```



#### [53 - I. 在排序数组中查找数字 I](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/) [EASY]

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int n = nums.size();
        if (!n) return 0;
      
        int l = 0, r = n - 1, s, t;
        while (l<=r) {
            int mid = l + (r - l)/2;
            if (nums[mid] < target) l = mid + 1;
            else r = mid - 1;
        }
        if (l >= n || nums[l] != target) s = -1;
        else s = l;
        if (s == -1) return 0;
      
        l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] <= target) l = mid + 1;
            else r = mid - 1;
        }
        if (r < 0 || nums[r] != target) t = -1;
        else t = r;
          
        return t - s + 1;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int getNumberOfK(vector<int>& nums , int k) {
        int n = nums.size();
        
        int l = 0, r = n;
        while (l < r) {
            int m = l + r >> 1;
            if (nums[m] < k)
                l = m + 1;
            else
                r = m;
        }
        int lid = l;
        
        l = 0, r = n;
        while (l < r) {
            int m = l + r >> 1;
            if (nums[m] <= k)
                l = m + 1;
            else
                r = m;
        }
        int rid = l;
        
        return max(0, rid - lid);
    }
};
```



```python
# python3
class Solution(object):
    def getNumberOfK(self, nums, k):
        #找到等于target的目标值的位置;
        p1,p2 = -1, -1
        l,r = 0, len(nums)
        while l < r:
            m = l + (r - l) // 2
            if nums[m] < k:
                l = m + 1
            else:r = m
        if 0 <= l < len(nums) and nums[l] == k:
            p1 = l
        else:return 0

        #找到第一个比target大的整数
        l, r = 0, len(nums)
        while l < r:
            m = l + (r - l) // 2
            if nums[m] <= k:
                l = m + 1
            else:r = m
        #不用再做判断了，因为如果不存在target，第一步已经返回了【-1，-1】
        p2 = l - 1
        return (p2 - p1 + 1)
```



#### [53 - II. 0～n-1中缺失的数字](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/) [EASY]

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int target = (n + 1) * n / 2;
        int tot = 0;
        for (auto v : nums) tot += v;
        return target - tot;
    }
    // another
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == mid) l = mid + 1;
            else r = mid - 1;
        }
        return l;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int getMissingNumber(vector<int>& nums) {
        int n = nums.size();
        int l = 0, r = n;
        while (l < r) {
            int m = l + r >> 1;
            if (nums[m] == m)
                l = m + 1;
            else
                r = m;
        }
        return l;
    }
};
```



```python
# python3
class Solution(object):
    def getMissingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:return 0
        l, r = 0, len(nums)
        while l < r:
            m = l + (r - l) // 2
            if nums[m] == m:
                l = m + 1
            else:
                r = m 
        return l
```



#### [54. 二叉搜索树的第k大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/) [EASY]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int kthLargest(TreeNode* root, int k) {
        stack<TreeNode*> st;
        int cnt = 0;
        while (!st.empty() || root) {
            while (root) {
                st.push(root);
                root = root->right;
            }
            root = st.top();
            st.pop();
            ++ cnt ;
            if (cnt == k) return root->val;
            root = root->left;
        }
        return 0;
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode * res;
    int k;
    
    void dfs(TreeNode * r) {
        if (!r || !k)
            return;
        
        dfs(r->left);
        -- k ;
        if (!k)
            res = r;
        dfs(r->right);
    }

    TreeNode* kthNode(TreeNode* root, int k) {
        this->k = k;
        dfs(root);
        return res;
    }
};
```



```python
# python3

# 二叉搜索树的第k小的节点，就是正常的中序遍历
class Solution(object):
    def kthNode(self, root, k):
        
        def dfs(p):
            nonlocal res, k
            if not p:
                return 
            dfs(p.left)
            k -= 1
            if k == 0:
                res = p
            if k > 0:
                dfs(p.right)

        res = None 
        dfs(root)
        return res
      
# 二叉搜索树的第k大的节点，中序遍历的逆序      
class Solution:
    def kthLargest(self, root: TreeNode, k: int) -> int:
        self.res,self.k=None,k

        def dfs(root):
            if not root:
                return
            else:
                dfs(root.right)
                self.k -= 1
                if self.k==0:
                    self.res=root.val
                elif self.k>0:
                    dfs(root.left)

        dfs(root)
        return self.res
```



#### [55 - I. 二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/) [EASY]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (!root) return 0;
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int res;
    
    void dfs(TreeNode * r, int d) {
        if (!r)
            return;
        
        res = max(res, d);
        dfs(r->left, d + 1);
        dfs(r->right, d + 1);
    }

    int treeDepth(TreeNode* root) {
        res = 0;
        dfs(root, 1);
        return res;
    }
};

class Solution {
public:
    int treeDepth(TreeNode* root) {
        if (!root) return 0;
        return max(treeDepth(root->left), treeDepth(root->right)) + 1;
    }
};
```



```python
# python3
class Solution:
    def treeDepth(self, root):
        if not root:return 0
        return max(self.treeDepth(root.left), self.treeDepth(root.right)) + 1
```



#### [55 - II. 平衡二叉树](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/) [EASY]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int helper(TreeNode* root) {
        if (!root) return 0;
        int left = helper(root->left);
        if (left == -1) return -1;
        int right = helper(root->right);
        if (right == -1) return -1;
        return abs(left - right) <= 1 ? max(left, right) + 1 : -1; 
    }
    bool isBalanced(TreeNode* root) {
        if (!root) return true;
        return helper(root) != -1;
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int dfs(TreeNode * r) {
        if (!r)
            return 0;
        int ld = dfs(r->left), rd = dfs(r->right);
        if (ld == -1 || rd == -1 || abs(ld - rd) > 1)
            return -1;
        return max(ld, rd) + 1;
    }

    bool isBalanced(TreeNode* root) {
        if (!root)
            return true;
        return dfs(root) != -1;
    }
};
```



```python
# python3
class Solution(object):
    def isBalanced(self, root):
        def dfs(p):
            nonlocal ans
            if not p:return 0
            left, right = dfs(p.left), dfs(p.right)
            if abs(left - right) >1:
                ans = False
            return max(left, right) + 1 #这是递归函数的return的值
          
        ans = True
        dfs(root)
        return ans
```



#### [56 - II. 数组中数字出现的次数 II](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)  [MID]

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;
        for (int i = 0; i < 32; ++ i ) {
            int p = 1 << i;
            int cnt = 0;
            for (auto v : nums) {
                if (v & p) ++ cnt ;
            }
            if (cnt % 3) res |= p;
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int findNumberAppearingOnce(vector<int>& nums) {
        int res = 0;
        for (int i = 0; i < 32; ++ i ) {
            int cnt = 0;
            for (auto v : nums)
                if (v >> i & 1)
                    cnt ++ ;
            if (cnt % 3)
                res |= 1 << i;
        }
        return res;
    }
};

class Solution {
public:
    int findNumberAppearingOnce(vector<int>& nums) {
        int ones = 0, twos = 0;
        for (auto x : nums) {
            ones = (ones ^ x) & ~twos;
            twos = (twos ^ x) & ~ones;
        }
        return ones;
    }
};
```



```python
# python3
#56-I的解答：一个数组，只有两个数字只出现一次，其他的都出现了两次，找出这两个数

# 1. 先把所有的数 异或一遍； 
# 2. 异或的结果就是x^y的结果，并且一定不为0；
# 3. 找到最低的那位 不为1 的位；
# 4. 根据这一位 把集合划分为两个集合；相同的数肯定是属于统一集合
#  次数两个集合内部 各自异或一遍 得到的结果 就是这两个不同的数。
class Solution(object):
    def findNumsAppearOnce(self, nums):
        res, a, b = 0, 0, 0
        for c in nums:
            res ^= c 
        k = 0 
        while not res >> k & 1:
            k += 1
        for c in nums:
            if c >> k & 1 == 0:
                a ^= c
            else:
                b ^= c 
        return [a,b]


#56-II的解答
#Method1：dict{"key":"value"}
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        dict={}
        for num in nums:
            if num not in dict:
                dict[num]=1
            else:
                dict[num]+=1
        for num in dict:
            if dict[num]==1:
                return num
           
#Method2: bit operation
# 方法比较跳跃性，需要多思考回顾
# 1. 建立一个长度为 32 的数组counts ，记录所有数字的各二进制位的 11 的出现次数。
# 2. 将 counts各元素对 33 求余，则结果为 “只出现一次的数字” 的各二进制位。
# 3. 利用 左移操作 和 或运算 ，可将 counts数组中各二进位的值恢复到数字 res 上，最后返回 res

# 实际上，只需要修改求余数值 mm ，即可实现解决 除了一个数字以外，其余数字都出现 mm 次 的通用问题
class Solution(object):
    def findNumberAppearingOnce(self, nums):
        counts = [0] * 32
        for num in nums:
            for j in range(32):
                counts[j] += num & 1
                num >>= 1
        res, m = 0, 3
        for i in range(32):
            res <<= 1
            res |= counts[31 - i] % m
        return res if counts[31] % m == 0 else ~(res ^ 0xffffffff) # 对负数的处理     
```



#### [57. 和为s的两个数字](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/) [EASY]

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        vector<int> res;
        if (!n) return res;
        int l = 0, r = n-1;
        while (l <= r) {
            if (nums[l] + nums[r] == target) {
                res.push_back(nums[l]);
                res.push_back(nums[r]);
                return res;
            } else if (nums[l] + nums[r] < target) {
                ++ l ;
            } else -- r ;
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    vector<int> findNumbersWithSum(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        int l = 0, r = n - 1;
        while (l < r) {
            int t = nums[l] + nums[r];
            if (t == target)
                return {nums[l], nums[r]};
            else if (t > target)
                -- r ;
            else
                ++ l ;
        }
        return {};
    }
};
```



```python
# python3
class Solution(object):
    def findNumbersWithSum(self, nums, target):
        nums.sort()  # 如果给定的题意已经是排序，则无需再排序
        l, r = 0 ,len(nums) - 1
        while l < r:
            if nums[l] + nums[r] > target:
                r -= 1
            elif nums[l] + nums[r] < target:
                l += 1
            else:
                return [nums[l], nums[r]]
```



#### [57 - II. 和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/) [EASY]

```c++
class Solution {
public:
    vector<vector<int>> findContinuousSequence(int target) {
        vector<vector<int>> res;
        if (target == 1) return res;
        int l = 1, r = 1, v;
        while (l <= target / 2) {
            int sum = (l + r) * (r - l + 1) / 2;
            if (sum == target) {
                vector<int> t;
                for (int i = l; i <= r; ++ i ) t.emplace_back(i);
                res.emplace_back(t);
                ++ l ;
            } else if (sum < target) ++ r ;
            else ++ l ;
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    vector<vector<int> > findContinuousSequence(int sum) {
        vector<vector<int>> res;
        for (int l = 1, r = 1, s = 0; r <= sum; ++ r ) {
            s += r;
            while (l < r && s > sum)
                s -= l ++ ;
            if (l < r && s == sum) {
                vector<int> t;
                for (int i = l; i <= r; ++ i )
                    t.push_back(i);
                res.push_back(t);
            }
        }
        return res;
    }
};
```



```python
# python3
# 双指针法

class Solution(object):
    def findContinuousSequence(self, num):
        if num <= 2:return []
        s = num//2 + 1
        l, r = 1, 2
        res = []
        while r <= s:
            cur_sum = sum(range(l, r + 1))
            if cur_sum < num:
                r += 1
            elif cur_sum > num:
                l += 1 
            else:
                res.append(list(range(l, r + 1)))  # 相等就把指针形成的窗口添加进输出列表中
          
                r += 1    # 别忘了，这里还要继续扩大寻找下一个可能的窗口哦
        return res
```



#### [58 - I. 翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/) [EASY]

```c++
class Solution {
public:
    string reverseWords(string s) {
        int n = s.size(), cnt = 0;
        string res;
        for (int i = n-1; i >= 0; -- i ) {
            if (s[i] == ' ') {
                if (!cnt) continue;
                res += s.substr(i + 1, cnt) + " ";
                cnt = 0;
            } else ++ cnt ;
        }
        if (cnt) res += s.substr(0, cnt) + " ";
        if (res.size() > 0) res.erase(res.size() - 1, 1);
        return res;
    }
  
    string reverseWords(string s) {
        int n = s.size(), cnt = 0;
        string res, sub;
        bool f = true;
        for (int i = n-1; i >= 0; -- i ) {
            if (s[i] == ' ') {
                if (cnt == 0) continue;
                if (f) f = false;
                else res.push_back(' ');
                res += s.substr(i + 1, cnt);
                cnt = 0;
            } else ++cnt;
        }
        if (cnt) {
            if (!f) res.push_back(' ');
            res += s.substr(0, cnt);
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    string reverseWords(string s) {
        int n = s.size();
        for (int i = 0; i < n; ++ i ) {
            int j = i + 1;
            while (j < n && s[j] != ' ')
                j ++ ;
            reverse(s.begin() + i, s.begin() + j);
            i = j;
        }
        reverse(s.begin(), s.end());
        return s;
    }
};
```



```python
# python3
# 双指针法：1. 首先去掉首尾的空格 2.两个指针都从尾部开始扫描遍历 

class Solution(object):
    def reverseWords(self, s):
        n = len(s)
        if n <= 1:return s
        s = s.strip()  
        p1 = p2 =  n - 1  
        res = []  
        while p1 >= 0:
            while p1 >= 0 and s[p1] != ' ': 
                p1 -= 1
            res.append(s[p1 + 1 : p2 + 1])
            while s[p1] == ' ':  # 踩坑： 防止有多个连续的空格符号
                p1 -= 1
            p2 = p1
        return ' '.join(res)
```



#### [58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/) [EASY]

```c++
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        reverse(s.begin(), s.begin() + n);
        reverse(s.begin() + n, s.end());
        reverse(s.begin(), s.end());
        return s;
    }
};
```

```c++
// AcWing
class Solution {
public:
    string leftRotateString(string str, int n) {
        reverse(str.begin(), str.begin() + n);
        reverse(str.begin() + n, str.end());
        reverse(str.begin(), str.end());
        return str;
    }
};
```





```python
# python3
#slice
class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        return s[n:] + s[:n]

#list
class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        res = []
        for i in range(n, len(s)):
            res.append(s[i])
        for i in range(n):
            res.append(s[i])
        return ''.join(res)


#string 字符串不可以改拜年，但是可以进行拼接
class Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        res = ""
        for i in range(n, len(s)):
            res += s[i]
        for i in range(n):
            res += s[i]
        return res

```



#### [59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/) [EASY]

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> res;
        deque<int> dq;        // 保存下标
        int n = nums.size();
        for (int i = 0; i < n; ++ i ) {
            while (!dq.empty() && dq.front() <= i - k)
                dq.pop_front();
            while (!dq.empty() && nums[dq.back()] < nums[i]) dq.pop_back();
            dq.push_back(i);
            if (i >= k - 1) res.push_back(nums[dq.front()]);
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    vector<int> maxInWindows(vector<int>& nums, int k) {
        int n = nums.size();
        deque<int> q;
        vector<int> res;
        for (int i = 0; i < n; ++ i ) {
            if (!q.empty() && q.front() <= i - k)
                q.pop_front();
            while (!q.empty() && nums[q.back()] <= nums[i])
                q.pop_back();
            q.push_back(i);
            if (i >= k - 1)
                res.push_back(nums[q.front()]);
        }
        return res;
    }
};
```



```python
# python3
# 单调队列的使用

class Solution(object):
    def maxInWindows(self, nums, k):
        if not nums:return []
        from collections import deque 
        q = deque()
        # l = 0
        res = []
        for r in range(len(nums)):
            if q and q[0] <= r - k:  # 踩坑 ：不需要l指针，直接用队列里的元素来表示；队列里存的就是当前数的下标
                q.popleft()
            while q and nums[q[-1]] < nums[r]:
                q.pop()
            q.append(r)
            if r >= k - 1:
                res.append(nums[q[0]])
        return res
```



#### [59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/) [MID]

```c++
class MaxQueue {
public:
    queue<int> q;
    deque<int> mq;   // mq单调递减
    MaxQueue() {
    }
    
    int max_value() {
        if (q.empty()) return -1;
        return mq.front();
    }
    
    void push_back(int value) {
        q.push(value);
        while (!mq.empty() && mq.back() < value) mq.pop_back();
        mq.push_back(value);
    }
    
    int pop_front() {
        if (q.empty()) return -1;
        int v = q.front();
        q.pop();
        if (v >= mq.front()) mq.pop_front();
        return v;
    }
};
```



```python
# python3

import collections
class MaxQueue:
    def __init__(self):
        self.A ,self.B = deque(), deque()

    def max_value(self) -> int:
        if self.B:
            return self.B[0]
        else:
            return -1

    def push_back(self, value: int) -> None:
        self.A.append(value)
        while self.B and self.B[-1] < value:
            self.B.pop()
        self.B.append(value)

    def pop_front(self) -> int:
        if not self.A:return -1
        x = self.A.popleft()
        if x == self.B[0]:  # 踩坑：这里是0！！popfront是取出队首元素
            self.B.popleft()
        return x
```



#### [60. n个骰子的点数](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/) [EASY]

```c++
class Solution {
public:
    vector<double> twoSum(int n) {
        vector<vector<int>> dp(15, vector<int>(70));
        for (int i = 1; i <= 6; ++ i ) dp[1][i] = 1;
        for (int i = 2; i <= n; ++ i ) {
            for (int j = 1 * i; j <= 6 * i; ++ j ) {
                for (int k = 1; k <= 6; ++ k ) {
                    if (j - k <= 0) break;
                    dp[i][j] += dp[i - 1][j - k];
                }
            }
        }
        int all = pow(6, n);
        vector<double> res;
        for (int i = n; i <= 6 * n; ++ i )
            res.push_back(dp[n][i] * 1.0 / all);
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    vector<int> numberOfDice(int n) {
        vector<vector<int>> f(n + 1, vector<int>(6 * n + 1, 0));
        f[0][0] = 1;
        for (int i = 1; i <= n; ++ i )
            for (int j = i; j <= i * 6; ++ j )
                for (int k = 1; k <= 6; ++ k )
                    if (j >= k)
                        f[i][j] += f[i - 1][j - k];
        return vector<int>(f[n].begin() + n, f[n].end());
    }
};
```



```python
# python3

# 分组背包问题： 有n次取物品的机会，每组物品的价值在[1,6]范围内，每组物品只能选一个，凑出总和在n-6n的方案数
# 状态表示：f[i,j]: 前i次投骰子，总和为j的方案数；属性：Max
# 状态转移：按照最后一次划分为6个集合，1点，2点，3点，...，6点；当最后一次点数是k时，对应的方案数：f[i-1][j-k]

class Solution(object):
    def numberOfDice(self, n):
        f = [[0] * (6 * n + 1) for _ in range(n + 1)]
        for i in range(1,7):  # 初始化，当只有一个骰子的时候，所有的方案数都是1 
            f[1][i] = 1   
        for i in range(2, n + 1):
            for j in range(i, 6 * i + 1):
                for k in range(1, 7):
                    if j > k:
                        f[i][j] += f[i - 1][j - k]
        res = []
        for i in range(n, n * 6 + 1):
            res.append(f[n][i])
        return res
```



#### [61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/) [EASY]

```c++
class Solution {
public:
    bool isStraight(vector<int>& nums) {
        int minv = INT_MAX, maxv = INT_MIN;
        vector<bool> vis(15);
        for (auto v : nums)
            if (v) {
                if (vis[v]) return false;
                else vis[v] = true;
                minv = min(v, minv);
                maxv = max(v, maxv);
            }
        return (maxv - minv) < 5;
    }
};
```

```c++
// AcWing
class Solution {
public:
    bool isContinuous(vector<int> numbers ) {
        if (numbers.empty())
            return false;
        int minv = INT_MAX, maxv = INT_MIN;
        vector<bool> vis(15);
        for (auto v : numbers)
            if (v) {
                if (vis[v])
                    return false;
                else
                    vis[v] = true;
                minv = min(minv, v);
                maxv = max(maxv, v);
            }
        return (maxv - minv) < 5;
    }
};
```



```python
# python3

class Solution(object):
    def isContinuous(self, nums):
        if not nums:return False
        my_set = set()
        minv, maxv = 14, 1
        for x in nums:
            if x == 0:continue  # 踩坑1: 当数值为0时，则不进入minv, maxv的判断
            minv = min(x, minv)
            maxv = max(x, maxv)
            if x in my_set:  # 踩坑2: 注意判断 是否存在相同的数！所以需要加一个if判断！！！不要写成for了！！
                return False
            my_set.add(x)
        return maxv - minv <= 4
```



#### [62. 圆圈中最后剩下的数字](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/) [EASY]

```c++
class Solution {
public:
    int lastRemaining(int n, int m) {
        int ans = 0;
        // 最后一轮剩下2个人，所以从2开始反推
        for (int i = 2; i <= n; i ++ )
            ans = (ans + m) % i;
        return ans;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int lastRemaining(int n, int m) {
        if (n == 1)
            return 0;
        return (lastRemaining(n - 1, m) + m)% n;
    }

    int lastRemaining2(int n, int m){
        int res = 0;
        for (int i = 2; i <= n; ++ i )
            res = (res + m) % i;
        return res;
    }
};
```



```python
# python3

# 很经典的数学问题---约瑟夫问题
class Solution(object):
    def lastRemaining(self, n, m):
        if n == 1:return 0
        res = 0
        for i in range(2, n + 1):
            res = (m + res) % i 
        return res   
```



#### [63. 股票的最大利润](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/) [MID]

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int minv = INT_MAX, res = 0;
        for (auto v : prices) {
            if (minv == INT_MAX) minv = v;
            res = max(res, v - minv);
            minv = min(minv, v);
        }
        return res;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int maxDiff(vector<int>& nums) {
        int res = 0, minv = 1e9;
        for (auto v : nums)
            res = max(res, v - minv), minv = min(minv, v);
        return res;
    }
};
```



```python
# python3

# 不用两次暴力遍历，可以用一个变量记录前i-1天的最小值，可以省一层循环（每次更新这个变量）
class Solution(object):
    def maxDiff(self, nums):

        n = len(nums)
        if n <= 1:return 0
        res, minv = 0, nums[0]  # minv: 表示前i天的最小值
        for i in range(1, n):
            minv = min(minv, nums[i])
            res = max(res, nums[i] - minv)
        return res
```



#### [64. 求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof/) [MID]

```c++
class Solution {
public:
    int sumNums(int n) {
        n && (n += sumNums(n - 1));
        return n;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int getSum(int n) {
        n && (n += getSum(n - 1));
        return n;
    }
};
```



```python
# python3
class Solution:
    def __init__(self):
        self.res = 0

    def sumNums(self, n: int) -> int:
        n>1 and self.sumNums(n-1)
        self.res+=n
        return self.res
      
      
class Solution(object):
    def getSum(self, n):
        # self.sum = 0  #递归会爆栈
        # n > 0 and self.getSum(n - 1)
        # self.sum += n 
        # return self.sum
        import functools
        return functools.reduce(lambda x, y: x+y, range(n+1))      
```



#### [65. 不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/) [EASY]

```c++
class Solution {
public:
    int add(int a, int b) {
        while (b) {
            int carry = (unsigned int)(a & b) << 1;
            a ^= b;        // 求和
            b = carry;
        }
        return a;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int add(int num1, int num2){
        while (num2) {
            int sum = num1 ^ num2;
            int carry = (unsigned int)(num1 & num2) << 1;
            num1 = sum, num2 = carry;
        }
        return num1;
    }
};
```



```python
# python3

# Python 中会自动把超过 int 类型的最大值转换成 long 类型，所以代码实现上要做一定处理。
# 思路：先计算不进位的和，再计算进位

class Solution(object):
    def add(self, num1, num2):
        while True:  # 不进位加法
            s = num1 ^ num2
            carry = num1 & num2   # 计算进位
            num1 = s & 0xFFFFFFFF   # 手动把高于 32 位的部分变成 0
            num2 = carry << 1

            if carry == 0:break
     
        if num1 >> 31 == 0:   # 如果是正数和 0 ，就直接返回这个正数好了
            return num1
        return num1 - (1 << 32)    # 如果是负数
```



#### [66. 构建乘积数组](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/) [EASY]

```c++
class Solution {
public:
    vector<int> constructArr(vector<int>& a) {
        int n = a.size();
        vector<int> b(n, 1);
        for (int i = 1; i < n; ++ i ) {
            b[i] = b[i-1] * a[i-1]; // b[1] = a[0]; b[n-1] = ...*a[n-2];
        }
        for (int i = n-2; i >= 0; --i) {
            a[i] = a[i] * a[i+1];
            b[i] = b[i] * a[i+1];
        }
        /*
        for (int i = 1; i < n; ++ i ) {
            a[n-i-1] = a[n-i-1] * a[n-i];
        }
        for (int i = 0; i < n-1; ++ i ) {
            b[i] *= a[i+1];
        }
        */
        return b;
    }
};
```

```c++
// AcWing
class Solution {
public:
    vector<int> multiply(const vector<int>& A) {
        if (A.empty())
            return {};
        int n = A.size();
        vector<int> res(n);
        res[0] = 1;
        for (int i = 1, p = A[0]; i < n; ++ i )
            res[i] = p, p *= A[i];
        for (int i = n - 2, p = A[n - 1]; i >= 0; -- i )
            res[i] *= p, p *= A[i];
        return res;
    }
};
```



```python
#python3
#  只能使用常数O(1)的空间，只能开一个数组
#  想一个循环的顺序，算B[i]的时候拆成两步来做，曲线救国！
#  B[i] = 左半边 * 右半边 （这样就可以不用除法了）

class Solution(object):
    def multiply(self, A):
        n = len(A)
        if not A or n == 0: return []
        B = [0] * n
        p = 1
        for i in range(n):
            B[i] = p
            p *= A[i]
        # B[i] = [1, 1, 2, 6, 24] #下标i之前所有数字乘积
        p = 1
        for i in range(n-1, -1, -1):
            B[i] *= p
            p *=A[i]
        return B
```



#### [67. 把字符串转换成整数](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/) [MID]

```c++
class Solution {
public:
    int strToInt(string str) {
        int n = str.size();
        if (!n) return 0;
        int p = 0, flag = 1;
        while (str[p] == ' ') ++ p ;
        if (str[p] == '-') {
            flag = -1;
            ++ p ;
        } else if (str[p] == '+') ++ p ;
        int res = 0, v;
        while (str[p] >= '0' && str[p] <= '9') {
            v = str[p]-'0';
            if (res > INT_MAX / 10 || (res == INT_MAX / 10 && str[p] - '0' > 7)) return INT_MAX;
            else if (res < INT_MIN / 10 || (res == INT_MIN / 10 && str[p] - '0' > 8)) return INT_MIN;
            res = res * 10 + flag * v;
            ++ p ;
        }
        if (res) return res;
        return 0;
    }
};
```

```c++
// AcWing
class Solution {
public:
    int strToInt(string str) {
        if (str.empty())
            return 0;
        int n = str.size();
        int p = 0, flag = 1;
        while (str[p] == ' ')
            p ++ ;
        if (str[p] == '-')
            p ++ , flag = -1;
        else if (str[p] == '+')
            p ++ ;
        
        int res = 0;
        while (str[p] >= '0' && str[p] <= '9') {
            int v = str[p] - '0';
            if (res > INT_MAX / 10 || res == INT_MAX / 10 && v > 7)
                return INT_MAX;
            else if (res < INT_MIN / 10 || res == INT_MIN / 10 && v > 8)
                return INT_MIN;
            res = res * 10 + flag * v;
            p ++ ;
        }
        return res;
    }
};
```



```python
# python3
class Solution:
    def strToInt(self, str: str) -> int:
        str=str.strip()
        if not str:return 0
        res,i,flag,max_int=0,1,1,2**31-1
        if str[0]=='-':flag=-1
        elif str[0]!='+':i=0
        for c in str[i:]:
            if not '0'<=c<='9':break
            res=10*res+ord(c)-ord('0')
            if res>max_int:
                return max_int if flag==1 else -max_int-1
        return flag*res  
```



#### [68 - I. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/) [EASY]

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || root == p || root == q) return root;
        TreeNode* l = lowestCommonAncestor(root->left, p, q);
        TreeNode* r = lowestCommonAncestor(root->right, p, q);
        if (l && r) return root;
        if (l) return l;
        else return r;
    }
};
```

```c++
// AcWing
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || root == p || root == q)
            return root;
        auto l = lowestCommonAncestor(root->left, p, q);
        auto r = lowestCommonAncestor(root->right, p, q);
        if (l && r)
            return root;
        return l ? l : r;
    }
};
```



```python
# python3
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        while root:
            if root.val <p.val and root.val <q.val:
                root=root.right
            elif root.val>p.val and root.val >q.val:
                root=root.left
            else:break
        return root
```



#### [68 - II. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/) [EASY]

```c++
// 同上
```

```python
# python3
class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        def dfs(r):
            if not r:return None
            if p == r or q ==r:return r  
            left = dfs(r.left)
            right = dfs(r.right)
            if left and right:return r 
            if not left:return right
            if not right:return left

        return dfs(root)
```

