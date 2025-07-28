- java
	- 在本地测试代码
		```java
		class Solution {
			public int sum(int num1, int num2) {
				return num1 + num2;
			}
		
			public static void main(String[] args) {
				// 力扣评测机对每个测试数据，都会重新创建一个 Solution 对象
				System.out.println(new Solution().sum(12, 5));  // 示例 1
				System.out.println(new Solution().sum(-10, 4)); // 示例 2
			}
		}
		```
	- 求最小值：Math.min
	- 初始化为最小值：int a = Integer.MIN_VALUE;
	- 
- 读取数据
	- 字符串(字母数字)：string a; cin >> a;   
	- 有空格读取整行，可以逐行读取：getline(cin, a);
	- 单行，单字符：cin >> a >> b >> c;
- (a||b)
	因为题目确保当 " 𝑎 和 𝑏同时为零" 时程序结束，所以不满足 " 𝑎 和 𝑏 同时为零" 这个条件的时候，该一直能够输入，也就是 !(a= =0 && b= =0)；
	化简后得到 (a != 0 || b != 0)，又表达式expr != 0和expr是等价的，所以这个条件又可以表示成(a||b)，也就有了这种写法。
- `while(t--)`等价于`while(t-- != 0)`
- ### 二分查找
	- 闭区间
	- 左闭右开
	- 错误
- ### 哈希表
	- 什么是哈希表：想象成一本字典
		-  **键 (Key)**： 相当于字典里的“字”或者“词”。
		- **值 (Value)**： 相当于这个“字”或者“词”对应的“解释”或“含义”。
		- **哈希函数**： 相当于字典前面的“拼音检字表”或者“部首检字表”，它告诉你如何根据一个字（键）快速找到它在字典中对应的页码（索引）。
		- **哈希表（底层数组）**： 相当于字典本身，按页码顺序存放着所有字的解释。
		- **核心思想**：通过某种转换（哈希函数），将任意的键（Key）映射到数组的某个下标（索引），从而实现**通过键快速查找、插入和删除对应的值**。
	- c++使用
		- 创建：`std::unordered_map<KeyType,ValueType> myMap;`
		- 插入值：`myMap[key] = value;
		- 查找值：`ValueType value = myMap[Key];`
		- 删除键值对：`myMap.erase(key);`
		- 遍历哈希表：
	- JAVA
		- 初始化：Map< Integer, Integer> hashTable = new HashMap<>(n);  n为容量（即cnt的可能最大值）。
		- cnt.getOrDefault( j - k, 0 ); 查找 j - k 是否在 cnt 中存在，如果存在则返回其出现次数，否则返回 `0`。
		- cnt.merge ( j, 1, Integer : :sum);  更新 j 在 cnt 中出现的次数，如果不存在初始化为1，存在加1。
		- **查找值**：通过key查找value = ht.get(key);
		- ht.containsKey( target - nums[i])
	- 将vector< int>& nums转换为哈希集合：unordered_set< int> hashSet( nums.begin(), nums.end());
- ### 动态规划
	- ####  **记忆化DFS**
		- 用 `dfs(i, c)` 表示**从前 `i` 个数中选出若干数，使它们的和等于 `c` 的方法数**。
		- 递归关系：
		    - 如果不选 `nums[i]`，方法数 = `dfs(i-1, c)`。
	        - 如果选 `nums[i]`，方法数 = `dfs(i-1, c - nums[i])`。
	        - 总方法数 = 不选 + 选。
	    - ##### 初始化记忆数组
		    - 记忆化（Memoization）是一种优化递归算法的技术，通过**存储已经计算过的结果**，避免重复计算，从而显著提高效率。
		    - `vector memo(n, vector<int>(m + 1, -1));`
			    - `memo` 是一个 `n x (m+1)` 的二维数组，初始值为 `-1`。
			    - `memo[i][c]` 存储 `dfs(i, c)` 的结果：如果 `memo[i][c] == -1`，表示未计算，需要递归求解。否则，直接返回 `memo[i][c]`
			    - 内层`vector<int>(m + 1, -1)`：每个内层 `vector` 的大小为 `m + 1`，初始值全部为 -1。-1表示表示该状态未被计算过（`dfs(i, c)` 尚未求解）
	- #### 树形DP
	- 
- 计算 `nums` 的**所有元素之和**：`reduce(nums.begin(), nums.end())`
- `vector<T>(size, init_value)`：创建一个 `vector`，大小为 `size`，初始值为 `init_value`.
	- 嵌套 `vector` 实现二维数组、
- ### 定长滑窗套路
	- 定长滑窗套路
		我总结成三步：入-更新-出。
		- 先定义`ans`和`vowel`
		- ans  = INT_MIN； 表示最小值
		**入**：下标为 i 的元素进入窗口，更新相关统计量。如果 i<k−1 则重复第一步。
		- vowel改变
		- `if(i < k-1) continue;`
		**更新**：更新答案。一般是更新最大值/最小值。
		- ans = max(ans , vowel);
		**出**：下标为 i−k+1 的元素离开窗口，更新相关统计量。
		- 定义 out = nums[ i-k+1 ];
		- vowel 除去out部分；
		以上三步适用于所有定长滑窗题目。
		- ![[Pasted image 20250516155013.png]]
- 将i接入ans：            ans.push_back(i); //。        
- 删除最后一个字符：ans.pop_back(); //
- 表示最后一个字符串：ans.back();
- **给nums从小到大排序**：ranges::sort(nums);
- **范围 for 循环**（C++11 特性），遍历 `words` 列表中的每个单词 `w`：
	- `for (auto& w : words)`   {    cnt [ w [ 0 ]  - ' a ' ]  [ w [ 1 ]  -  ' a ' ] + +;  }
	- `auto& w` 表示 `w` 是 `words` 中元素的引用（避免拷贝，提高效率）
	- `w[0] - 'a'`将字母转换为 `0-25` 的索引（例如 `'a' - 'a' = 0`，`'b' - 'a' = 1`，依此类推）
	- `cnt[first][second]++` 对对应的字母组合的计数加 1
- ### 广度优先搜索BFS，用双列表
	- 蛇梯棋
	```c
	class Solution {
	public:
	    int snakesAndLadders(vector<vector<int>>& board) {
	        int n = board.size();
	        vector<int8_t> vis(n * n+1); //创建访问标记数组。int8_t是8位整数类型(通常等同于char)，用于节省空间
	        vis[1] = true; //保证起点无蛇梯，不写也可以
	        vector<int>q={1};// 起点，初始化BFS队列，包含起点1
	        for(int step = 0; !q.empty(); step++)  //BFS双列表，二叉树
	        {
	            // 每次循环处理一"层"（即一步能到达的所有位置）
	            // 当发现终点时，当前的step就是最小步数
	            auto tmp = q; //创建当前队列的副本
	            q.clear();   //清空主队列，准备存储下一层的节点，二叉树的做法
	            for(int x:tmp)  //遍历当前层的所有节点
	            {
	                if(x == n*n) return step; //终点
	                for(int y=x+1; y <= min(x+6,n*n); y++) //下一步棋，y为棋盘上的编号/蛇形顺序
	                {
	                    int r = (y-1)/n; //行
	                    int c = (y-1)%n; //列
	                    if(r%2) c = n-1-c; //奇数行从右到左，蛇形,反转列号(因为棋盘是蛇形排列)
	                    int nxt = board[n-1-r][c];//获取棋盘上的值,将逻辑行号转换为实际的数组索引(棋盘底部是数组第0行)
	                    if(nxt <0) nxt = y; //普通方格-1不传送
	                    if(!vis[nxt])  //未被访问过
	                    {
	                        vis[nxt] = true;  //标记为已访问
	                        q.push_back(nxt); //加入队列，等待下一轮处理
	                    }
	                }
	            }
	        }
	        return -1; //无法到达终点
	    }
	};
	```
