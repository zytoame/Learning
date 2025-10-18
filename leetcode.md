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
	- **截取字符串**： `substring(int start, int end)` 方法接受两个参数：`start` 和 `end`。
	    截取字符串  中从 start 到 end（不包括 end 索引位置）的部分
	    - `start` 是子字符串的起始位置（包含该位置的字符）。
	    - `end` 是子字符串的结束位置（不包含该位置的字符）。
	- 对**数组**进行**排序**：Arrays.sort()
	- `(p, q) -> p[0] - q[0]`：这是一个 **lambda 表达式**，实现了 `Comparator` 接口的`compare(p, q)` 方法。
		- `p[0] - q[0]`是 `Comparator` 的比较规则。如果 `p[0]` 小于 `q[0]`，则 `p` 会排在 `q` 前面（因为结果是负数）。
		- `compare(p, q)` 方法返回一个整数：如果返回负数，`p` 排在 `q` 前面。
	- 高效复制数组元素：arraycopy(Object src源数组, int srcPos源数组要复制的起始位置, Object dest目标数组, int destPos目标数组接收复制的起始位置, int length复制的数据长度)
		
- c++
	- 将i接入ans：            ans.push_back(i);         
	- 删除最后一个字符：ans.pop_back(); 
	- 表示最后一个字符串：ans.back();
	- **给nums从小到大排序**：ranges::sort(nums);
	
- **读取数据**
	- 字符串(字母数字)：string a; cin >> a;   
	- 有空格读取整行，可以逐行读取：getline(cin, a);
	- 单行，单字符：cin >> a >> b >> c;
	-  多种输入方式
		
		- 方式1：固定长度数组
		```java
		// 已知数组长度
		int n = scanner.nextInt();
		int[] prices = new int[n];
		for (int i = 0; i < n; i++) {
		    prices[i] = scanner.nextInt();
		}
		```
		- 方式2：不确定长度的数组
		
		```java
		// 输入以-1结束（特殊值）
		List<Integer> list = new ArrayList<>();
		while (scanner.hasNextInt()) {
		    int num = scanner.nextInt();
		    if (num == -1) break;
		    list.add(num);
		}
		int[] prices = list.stream().mapToInt(i -> i).toArray();
		
		// 不确定长度，没有结束标志
		// 读取一行输入，按空格分割
        String input = scanner.nextLine();
        String[] strArray = input.split(" ");
        
        // 转换为整数数组
        int[] prices = new int[strArray.length];
        for (int i = 0; i < strArray.length; i++) {
            prices[i] = Integer.parseInt(strArray[i]);
        }
		```
		
		-  方式3：从字符串读取
		
		```java
		// 输入如："[7,1,5,3,6,4]"
		String input = scanner.nextLine();
		input = input.replace("[", "").replace("]", "");
		String[] parts = input.split(",");
		int[] prices = new int[parts.length];
		for (int i = 0; i < parts.length; i++) {
		    prices[i] = Integer.parseInt(parts[i].trim());
		}
		```
		
- (a||b)
	因为题目确保当 " 𝑎 和 𝑏同时为零" 时程序结束，所以不满足 " 𝑎 和 𝑏 同时为零" 这个条件的时候，该一直能够输入，也就是 !(a= =0 && b= =0)；
	化简后得到 (a != 0 || b != 0)，又表达式expr != 0和expr是等价的，所以这个条件又可以表示成(a||b)，也就有了这种写法。
- `while(t--)`等价于`while(t-- != 0)`
## 数组
- ### 二分查找O(logn)
	- 区间范围的选择，开还是闭
	- 左闭右开
	```java
		int left = 0, right = n, ans = 0;
		while(left < right){
			int mid = left + (right - left)/2;
			if(关于mid < target) left = mid+1;
			else if(关于mid > target) right = mid;
			else ans = mid;
		}
	```
	- 开区间
	```java
		int left = -1, right = n, ans = 0;
		while(left+1 < right){  //注意是开区间，要保证区间内有值
			int mid = left + (right - left)/2;
			if(关于mid < target) left = mid;
			else if(关于mid > target) right = mid;
			else ans = mid;
		}
	```
	- 错误
		- 计算平方根的时候防止溢出
			- // 64 位整数的平方根上限private static final long SQRT_LONG_MAX = (long) **Math.sqrt**(Long.MAX_VALUE);
- ### 双指针
	- 快慢指针
		- 快指针：寻找新数组的元素 ，新数组就是不含有⽬标元素的数组
		- 慢指针：指向更新 新数组下标的位置
	- 双向指针O（n）
		```java
		for(int left = 0，right = n-1; left <= right ;){
			if(){left++;}
			if(){right--;}
		}
		```
	- 滑动窗口：时间复杂度O（n）
		```java
		int left = 0;
		for(int right = 0; right < n; right++){
			计算right，移动右边窗口
			while(超出范围){
				将左边移出窗口
				left++；
			}
			计算答案:窗口长度：ans = Math.max/min(anx, right-left+1);
		}	
		```
- ### 螺旋矩阵
	- 时间复杂度O（mn）

## ![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250916163123410.png)
## 链表

1. 反转链表
	```java
	//双指针时间复杂度O（n），空间1
	ListNode pre = null; ListNode cur = head;
	ListNode tmp;
	while(cur != null){
		tmp = cur.next;
		//反转链表
		cur.next = pre;
		//移动指针
		cur = tmp; pre = cur;
	}
	return cur;
	//头插法,虚拟头结点
	ListNode dummyHead = new ListNode(-1); dummyHead.next = null;
	ListNode cur = head;
	while(cur != null){
		ListNode tmp = cur.next;
		//头插法
		cur.next = dummyHead.next;
		dummyHead.next = cur;  cur = tmp; 
	}
	return dummyHead.next;
	```
2. 设计链表
	```java
	class Node{
	        Node next;
	        int val;
	        public Node(int val){
	            this.val = val;
	        }
	    }
	class MyLinkedList {
	    Node head;
	    int size;
	    //初始化
	    public MyLinkedList() {
	        size = 0;
	        head = new Node(0);
	    }
	    //获取索引对应的链表的值
	    public int get(int index) {
	        if(index < 0 || index >= size) return -1;
	        Node cur = head;
	        for(int i = 0; i <= index; i++){
	            cur = cur.next;
	        }
	        return cur.val;
	    }
	    //插入头节点
	    public void addAtHead(int val) {
	        addAtIndex(0,val);
	    }
	    //添加尾节点
	    public void addAtTail(int val) {
	        addAtIndex(size,val);
	    }
	    //在指定位置插入节点
	    public void addAtIndex(int index, int val) {
	        if(index > size) return;
	        size++;
	        Node pre = head;
	        for(int i = 0; i < index; i++){
	            pre = pre.next;
	        }
	        Node add = new Node(val);
	        add.next = pre.next;
	        pre.next = add;
	    }
	    //在指定位置删除节点
	    public void deleteAtIndex(int index) {
	        if(index < 0 || index >= size) return;
	        size--;
	        Node pre = head;
	        for(int i = 0; i < index; i++){
	            pre = pre.next;
	        }
	        pre.next = pre.next.next;
	    }
	}
	```
## 单调栈

1. 模版1
	```java
	Stack<Integer> s = new Stack<>();
	s.push(0);
	for(int j = 0; j < nums2.length; j++){
		while(!s.isEmpty() && nums2[j] > nums2[s.peek()]){
			int index = s.pop();
			if(map.containsKey(nums2[index])){
				ans[map.get(nums2[index])] = nums2[j];  
			}
		}
		s.push(j);
	}
```

2. 接雨水（找左侧最高和右侧最高）
	```java
	class Solution {
	    public int trap(int[] height) {
	        //单调栈
	        int n = height.length;
	        int ans = 0;
	        Stack<Integer> s = new Stack<>();
	        s.push(0);
	        /*for(int i = 1; i < n; i++){
	            if(height[i] < height[s.peek()]){
	                s.push(i);
	            }else if(height[i] == height[s.peek()]){
	                s.pop();
	                s.push(i);
	            }else{
	                while(!s.isEmpty() && height[i] > height[s.peek()]){
	                    int midH = height[s.pop()];
	                    if(!s.isEmpty()){
	                        int leftH = height[s.peek()];
	                        ans += (Math.min(leftH, height[i]) - midH) * (i-s.peek()-1);
	                    }
	                }
	                s.push(i);
	            }
	        }*/
	        for(int i = 0; i < n; i++){
		        while(!s.isEmpty() && height[i] > height[s.peek()]){
					int midH = height[s.pop()];
					if(!s.isEmpty()){
						int leftH = height[s.peek()];
						ans += (Math.min(leftH, height[i]) - midH) * (i-s.peek()-1);
					}
				}
				s.push(i);
	        }
	        return ans;
	    }
	}
	```
	```java
	class Solution {
	    public int trap(int[] height) {
	        //双指针
	        int n = height.length;
	        int ans = 0;
	        int[] leftH = new int[n]; //当前的左侧最高柱子
	        int[] rightH = new int[n];//当前的右侧最高柱子
	
	        leftH[0] = height[0];
	        for(int i = 1; i < n; i++){
	            leftH[i] = Math.max(leftH[i-1], height[i]);
	        }
	
	        rightH[n-1] = height[n-1];
	        for(int i = n-2; i >= 0; i--){
	            rightH[i] = Math.max(height[i], rightH[i+1]);
	        }
	
	        for(int i = 0; i < n; i++){
	            int count = Math.min(leftH[i], rightH[i]) - height[i];
	            if(count > 0) ans += count;
	        }
	        return ans;
	    }
	}
	```
	```java
	class Solution {
	    public int trap(int[] height) {
	        //双指针
	        int n = height.length;
	        int res = 0;
	        int left = 0, right = n - 1;
	        int leftMax = height[left], rightMax = height[right];
	        while(left < right){
	            if(height[left] < height[right]){
	                left++;
	                leftMax = Math.max(leftMax, height[left]);
	                res += leftMax - height[left];
	            }else{
	                right--;
	                rightMax = Math.max(rightMax, height[right]);
	                res += rightMax - height[right];
	            }
	        }
	        return res;
	    }
	}
	```

3. 连续柱子面积（找左侧第一个小的和右侧第一个小的）
	```java
	class Solution {
	    public int largestRectangleArea(int[] heights) {
	        int n = heights.length;
	        int ans = 0;
	        Stack<Integer> s = new Stack<>();
	        s.push(-1);
	        s.push(0);
	        /*for(int i = 1; i < n; i++){
	            if(heights[i] > heights[s.peek()]){
	                s.push(i);
	            }else if(heights[i] == heights[s.peek()]){
	                s.pop();
	                s.push(i);
	            }else{
	                while(s.peek() != -1 && heights[i] < heights[s.peek()]){
	                    int h = heights[s.pop()];
	                    int left = s.peek();
	                    ans = Math.max(ans, h*(i-left-1));
	                }
	                s.push(i);
	            }
	        }*/
	        for(int i = 1; i < n; i++){
	            while(s.peek() != -1 && heights[i] <= heights[s.peek()]){
	                int h = heights[s.pop()];
	                int left = s.peek();
	                ans = Math.max(ans, h*(i-left-1));
	            }
	            s.push(i);
	        }
	        //处理剩余元素
	        while(s.peek() != -1){
	            int h = heights[s.pop()];
	            int left = s.peek();
	            ans = Math.max(ans, h*(n-left-1));
	        }
	        return ans;
	    }
	}
	```
	```java
	class Solution {
	    public int largestRectangleArea(int[] heights) {
	        int n = heights.length;
	        int[] left = new int[n]; //左侧第一个小于当前值的下标
	        int[] right = new int[n];
	        int res = 0;
	
	        left[0] = -1;
	        for(int i = 1; i < n; i++){
	            int x = i-1;
	            //向左遍历
	            while(x >= 0 && heights[x] >= heights[i]){
	                x = left[x];
	            }
	            left[i] = x;
	        }
	
	        right[n-1] = n;
	        for(int i = n-2; i >= 0; i--){
	            int x = i+1;
	            //向右遍历
	            while(x < n && heights[x] >= heights[i]){
	                x = right[x];
	            }
	            right[i] = x;
	        }
	
	        for(int i = 0; i < n; i++){
	            int sum = heights[i] * (right[i] - left[i] - 1);
	            res = Math.max(res, sum);
	        }
	        return res;
	    }
	}
	```

## 动态规划
1. 思路
	1. 确定dp含义和下标含义
	2. 初始化dp
	3. 确定状态转移方程
	4. 确定遍历方向顺序
2. 背包递推公式
	1. 能否能装满背包（最多能装多少）：dp[i] = Math.max(dp[i], dp[i-nums[j]]+nums[j]);
	2. 装满背包有几种方法：dp[i] += dp[i-nums[j]];
	3. 背包装满最大价值：dp[i] = Math.max(dp[i], dp[i-weight[j]]+value[j]);
	4. 装满背包所有物品的最小个数：dp[i] = Math.min(dp[i-nums[j]]+1, dp[i]);
3. 爬楼梯（m阶的爬法）
	```java
	int[] dp = new int[n+1];
	dp[0] = 0; dp[1] = 1;
	for(int i = 2; i <= n; i++){
		if(i <= m) dp[i] += 1;
		for(int j = 1; j <= i && j <= m; j++){
			dp[i] += dp[i-j];
		}
	}
	return dp[n];
	```
	
4. 01背包
	```java
	//二维dp，dp[i][j]表示最大价值，i表示物品0-i，j表示背包容量,value[]表示物品0-i的价值
	int[][] dp = new int[m][n];
	//初始化为0；初始化物品1
	for(int i = weight[0]; i < n; i++){
		dp[0][i] = value[0];
	}
	//遍历
	for(int i = 1; i < m; i++){
		for(int j = 0; j < n; j++){
			if(j < weight[i]) dp[i][j] = dp[i-1][j];
			else dp[i][j] = Math.max(dp[i-1][j], dp[i-1][j-weight[i]]+value[i]);
		}
	}
	
	//一维
	int[] dp = new int[n];//初始化为0
	for(int i = 0; i < m; i++){         
		for(int j = n; j >= weight[i]; j--){//从后往前遍历，确保只放入一个物品
			dp[j] = Math.max(dp[j], dp[j-weight[i]]+value[i]);
		}
	}
	
	//装满背包有几种方法
	dp[j] += dp[j-weight[i]];
	```
	纯 0 - 1 背包 是求 给定背包容量 装满背包 的最⼤价值是多少。
	416分割等和⼦集 是求 给定背包容量，能不能装满这个背包。
	```java
	//确定dp含义，dp为和，下标也是和
	int[] dp = new int[target+1];
	//确定递归公式，以及遍历顺序
	for(int i = 0; i < n; i++){
		for(int j = target; j >= nums[i]; j--){  //从后往前顺序
			dp[j] = Math.max(dp[j], dp[j-nums[i]] + nums[i]);
		}
	}
	return dp[target] == target ? true : false;
	```
	1049最后⼀块⽯头的重量 II 是求 给定背包容量，尽可能装，最多能装多少
	```java
	int target = sum/2;//背包容量
		int[] dp = new int[target+1];//最大价值，最大石头和
		for(int i = 0; i < n; i++){
			for(int j = target; j >= stones[i]; j--){
				dp[j] = Math.max(dp[j], dp[j-stones[i]]+ stones[i]);
			}
		}
		return sum-2*dp[target];
	```
	494⽬标和 是求 给定背包容量，装满背包有多少种⽅法。
	```java
	int t = (sum-target)/2; //背包容量
	int[] dp = new int[t+1];//方法数
	dp[0] = 1;
	for(int i = 0; i < n; i++){
		for(int j = t; j >= nums[i]; j--){
			dp[j] += dp[j-nums[i]];
		}
	}
	return dp[t];
	```
	474一和零 是求 给定背包容量，装满背包最多有多少个物品。
	```java
	//01背包问题，两个背包
	int[][] dp = new int[m+1][n+1];//最大子集的长度，即背包的最大价值
	dp[0][0] = 0;
	//遍历物品
	for(String str : strs){
		int zero = 0, one = 0;//物品的重量
		for(char c : str.toCharArray()){
			if(c == '1') one++;
			if(c == '0') zero++;
		}
		//遍历背包
		for(int j = m; j>= zero; j--){
			for(int k = n; k >= one; k--){
				dp[j][k] = Math.max(dp[j][k], dp[j-zero][k-one]+1);
			}
		}
	}
	return dp[m][n];
	```
	
5. 完全背包
	1. 装满背包有几种方法：
		1. 求组合数：外层for遍历物品内层for遍历背包
		```java
		int[] dp = new int[amount+1];
		dp[0] = 1;
		for(int i = 0; i < coins.length; i++){       //物品
			for(int j = coins[i]; j <= amount; j++){ //背包
				dp[j] += dp[j-coins[i]];
			}
		}
		return dp[amount];
		```
		2. 求排列数：外层for遍历背包内层for遍历物品
		```java
		int[] dp = new int[target+1];
		dp[0] = 1; //因为递推公式dp[i] += dp[i - nums[j]]的缘故，dp[0]要初始化为1，这样递归其他dp[i]的时候才会有数值基础。
		for(int i = 1; i <= target; i++){            //背包
			for(int j = 0; j < nums.length; j++){    //物品
				if(nums[j] <= i) dp[i] += dp[i-nums[j]];
			}
		}
		return dp[target];
		```
	2. 装满背包最少的物件数：要求最少硬币数量，硬币是组合数还是排列数都⽆所谓！所以两个for循环先后顺序怎样都可以！
		```java
		int[] dp = new int[amount+1];
		Arrays.fill(dp, Integer.MAX_VALUE);
		dp[0] = 0;
		for(int i = 1; i <= amount; i++){          //背包
			for(int j = 0; j < coins.length; j++){ //物品
				if(coins[j] <= i && dp[i-coins[j]]!=Integer.MAX_VALUE) dp[i] = Math.min(dp[i-coins[j]]+1, dp[i]);
			}
		}
		return dp[amount]!=Integer.MAX_VALUE ? dp[amount] : -1;
		
		for(int i = 0; i < coins.length; i++){          //物品
			for(int j = coin[i]; j <= amount; j++){ //背包
				if(dp[i-coins[j]]!=Integer.MAX_VALUE){
					dp[i] = Math.min(dp[i-coins[j]]+1, dp[i]);
				} 
			}
		}
		```
	1. 背包如何装满
6. 多重背包：O(m × n × k)，m：物品种类个数，n背包容量，k单类物品数量
	```java
	for(int i = 0; i < weight.size(); i++) { // 遍历物品
	       for(int j = bagWeight; j >= weight[i]; j--) { // 遍历背包容量
	           // 以上为01背包，然后加⼀个遍历个数
	           for (int k = 1; k <= nums[i] && (j - k * weight[i]) >= 0; k++) { // 遍历个数
	               dp[j] = max(dp[j], dp[j - k * weight[i]] + k * value[i]);       }}}
	```
7. 打家劫舍
	1. 常规
	2. 连成环：考虑两种情况（包头不包尾，包尾不包头）
		```java
		public int rob(int[] nums) {
		        int n = nums.length;
		        if(n == 1) return nums[0];
		        int res1 = money(nums, 0, n-2);
		        int res2 = money(nums, 1, n-1);
		        return Math.max(res1, res2);
		    }
		
		    private int money(int[] nums, int start, int end){
		        if(start == end) return nums[start];
		        int[] dp = new int[nums.length];
		        dp[start] = nums[start];
		        dp[start+1] = Math.max(nums[start], nums[start+1]);
		        for(int i = start+2; i <= end; i++){
		            dp[i] = Math.max(dp[i-1], dp[i-2]+nums[i]);
		        }
		        return dp[end];
		    }
		```
	1. 连成树（树形dp入门）
```java
public int rob(TreeNode root) {
	//递归，后序遍历，因为要根据返回值计算
	int[] ans = robTree(root);
	return Math.max(ans[0], ans[1]);
}
private int[] robTree(TreeNode cur){
	int[] res = new int[2];         //确定dp含义，0代表不偷，1代表偷，dp代表最高金额
	if(cur == null) return res;        //初始化dp，确定递归终点
	int[] left = robTree(cur.left);    //左
	int[] right = robTree(cur.right);  //右
	//不偷
	res[0] = left[1] + right[1];
	//偷
	res[1] = left[0] + right[0] + cur.val;
	return res;
}
```
8. 买卖股票时机
	1. 只有一次买卖
		```java
		int[][] dp = new int[n][2];
        //0表示持有（包括买入和继续持有），1表示不持有（包括卖出和空仓）
        dp[0][0] = -prices[0];
        dp[0][1] = 0;
        for(int i = 1; i < n; i++){
            dp[i][0] = Math.max(-prices[i], dp[i-1][0]);          //买入或者持有
            dp[i][1] = Math.max(dp[i-1][0]+prices[i], dp[i-1][1]);//卖出或不持有
        }
        return dp[n-1][1];
		```
	2. 一次只能持有一只股票，可以多次买卖
		```java
		int n = prices.length;
        int[][] dp = new int[n][2];
        dp[0][0] = -prices[0];  //持有股票时候的最大利润
        dp[0][1] = 0;           //不持有股票时的最大利润
        for(int i = 1; i < n; i++){
            dp[i][0] = Math.max(dp[i-1][1]-prices[i], dp[i-1][0]);//买入或者保持
            dp[i][1] = Math.max(dp[i-1][0]+prices[i], dp[i-1][1]);//卖出或者保持
        }
        return dp[n-1][1];
		```
	3. 一次只能持有一只股票，最多买卖k次
		```java
		//奇数买入，偶数卖出
        int[][] dp = new int[n][2*k+1];
        for(int i = 1 ; i < 2*k; i += 2){
            dp[0][i] = -prices[0];
        }
        for(int i = 1; i < n; i++){
            for(int j = 0; j < 2*k-1; j +=2){
                dp[i][j+1] = Math.max(dp[i-1][j]-prices[i], dp[i-1][j+1]);
                dp[i][j+2] = Math.max(dp[i-1][j+1]+prices[i], dp[i-1][j+2]);
            }
        }
        return dp[n-1][2*k];
		```
	4. 含一天冷冻期，卖出后需要经过冷冻期才能买入
		```java
		//0:买入，1：保持卖出，2：卖出，3：冷冻
        int[][] dp = new int[n+1][4];
        dp[1][0] = -prices[0];  
        for(int i = 2; i <= n; i++){
            dp[i][0] = Math.max(dp[i-1][0],Math.max(dp[i-1][3] - prices[i-1], dp[i-1][1]-prices[i-1]));
            dp[i][1] = Math.max(dp[i-1][2], dp[i-1][1]);
            dp[i][2] = dp[i-1][0]+prices[i-1];
            dp[i][3] = dp[i-1][2];
        }
        return Math.max(dp[n][1],dp[n][2]);
		```
9. 子序列
	1. 最长公共子序列（不要求连续）
		```java
		char[] t1 = text1.toCharArray();
        char[] t2 = text2.toCharArray();
        int n = t1.length, m = t2.length;
        int[][] dp = new int[n+1][m+1];
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(t1[i-1] == t2[j-1]){
                    dp[i][j] = dp[i-1][j-1]+1;
                }else{
                    dp[i][j] = Math.max(dp[i][j-1],dp[i-1][j]);
                }
            }
        }
        return dp[n][m];
		```
	2. 最长重复子数组（要求连续）
		```java
		int n = nums1.length, m = nums2.length;
        int[][] dp = new int[n+1][m+1];
        int res = 0;
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(nums1[i-1] == nums2[j-1]){
                    dp[i][j] = dp[i-1][j-1] + 1;
                }
                res = Math.max(res, dp[i][j]);
            }
        }
        return res;
```
## 数论

1. 计算Cmn，即从m中任取n。注意防止int溢出，使用longlong，边乘边除
	```java
	int fenmu = m-1; long long fenzi = 1;
	while(n--){
		fenzi *= (n--);
		while(fenmu != 0 && fenzi % fenmu == 0){
			fenzi /= fenmu;
			fenmu--;
		}
	}
	return fenzi;
	```

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
		- **初始化**：Map< Integer, Integer> hashTable = new HashMap<>(n);  n为容量（即cnt的可能最大值）。
		- **hashTable.put(key.value)**
		- **查找值**：通过key查找value：value = hashTable.get(key)
		- **cnt.getOrDefault( j - k, 0 )**; 查找 j - k 是否在 cnt 中存在，如果存在则返回其出现次数，否则返回 `0`。
		- **cnt.merge ( j, 1, Integer : :sum)**;  更新 j 在 cnt 中出现的次数，如果不存在初始化为1，存在加1。
		- **ht.containsKey( target - nums[i])**
		- **for(Map.Entry<Integer, Integer> c : cnt.entrySet())**{ itn key = c.getKey(); int value = c.getValue();} ：遍历哈希表，同时访问键和值
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

### 栈stack

#### **`Stack<TreeNode> stack = new Stack<>();` 详解**

在Java中，`Stack` 是一种 **后进先出（LIFO, Last In First Out）** 的线性数据结构，专门用于存储和操作数据。在您的代码中：

```java
Stack<TreeNode> stack = new Stack<>();
```

- **`Stack<TreeNode>`** 表示这是一个 **存储 `TreeNode` 对象** 的栈。
- **`new Stack<>()`** 创建了一个 **空栈**（使用 **泛型** 确保类型安全）。

---

##### **1. `Stack` 的基本特性**
| **特性**       | **说明** |
|--------------|---------|
| **数据结构**   | 后进先出（LIFO） |
| **继承关系**   | `Stack` 继承自 `Vector`（线程安全，但性能较低） |
| **主要方法**   | `push()`、`pop()`、`peek()`、`empty()`、`search()` |
| **线程安全**   | ✅ 是（所有方法用 `synchronized` 修饰） |
| **推荐替代**   | `Deque`（如 `ArrayDeque`，性能更高） |

---

##### **2. `Stack` 的常用方法**
###### **（1）`push(E item)` - 入栈**
```java
stack.push(node1);  // 将元素压入栈顶
stack.push(node2);
```
- **栈状态**：`[node2, node1]`（`node2` 在栈顶）

###### **（2）`pop()` - 出栈**
```java
TreeNode topNode = stack.pop();  // 移除并返回栈顶元素
```
- **栈状态**：`[node1]`（`node2` 被移除）
- **如果栈为空**：抛出 `EmptyStackException`

###### **（3）`peek()` - 查看栈顶元素（不移除）**
```java
TreeNode topNode = stack.peek();  // 返回栈顶元素但不移除
```
- **栈状态**：`[node2, node1]`（仍保留 `node2`）

###### **（4）`empty()` - 判断栈是否为空**
```java
boolean isEmpty = stack.empty();  // true 或 false
```

###### **（5）`search(Object o)` - 查找元素位置**
```java
int position = stack.search(node1);  // 返回元素位置（从栈顶开始计数，1-based）
```
- **如果不存在**：返回 `-1`

---

##### **3. `Stack` 的底层实现**
- **基于 `Vector`**（动态数组）实现：
  ```java
  public class Stack<E> extends Vector<E> { ... }
  ```
- **核心操作**：
  - `push()`：调用 `addElement(item)`（在数组末尾添加）
  - `pop()`：调用 `removeElementAt(size() - 1)`（移除最后一个元素）
- **线程安全**：所有方法用 `synchronized` 修饰（性能较低）。

---

##### **4. 为什么推荐使用 `Deque` 替代 `Stack`？**
| **对比项**       | **`Stack`** | **`Deque`（如 `ArrayDeque`）** |
|----------------|------------|-----------------------------|
| **继承体系**     | 继承 `Vector`（历史遗留） | 独立接口，实现类更灵活 |
| **线程安全**     | ✅ 是（同步开销大） | ❌ 否（但性能更高） |
| **功能扩展**     | 仅支持LIFO | 支持LIFO和FIFO（双端操作） |
| **性能**        | 较低（同步锁） | 更高（无锁竞争） |
| **推荐场景**     | 旧代码兼容 | 新代码首选 |

###### **使用 `ArrayDeque` 实现栈**
```java
Deque<TreeNode> stack = new ArrayDeque<>();  // 推荐替代方案
stack.push(node1);  // 入栈
TreeNode topNode = stack.pop();  // 出栈
```

---

##### **5. 典型应用场景**
###### **（1）深度优先搜索（DFS）**
```java
Stack<TreeNode> stack = new Stack<>();
stack.push(root);
while (!stack.empty()) {
    TreeNode node = stack.pop();
    if (node.right != null) stack.push(node.right);
    if (node.left != null) stack.push(node.left);
}
```

###### **（2）括号匹配检查**
```java
Stack<Character> stack = new Stack<>();
for (char c : s.toCharArray()) {
    if (c == '(') stack.push(')');
    else if (stack.isEmpty() || stack.pop() != c) return false;
}
return stack.isEmpty();
```

---

##### **6. 总结**
- **`Stack<TreeNode> stack = new Stack<>();`** 创建了一个 **存储 `TreeNode` 的栈**。
- **核心操作**：`push()`、`pop()`、`peek()`。
- **底层实现**：基于 `Vector`（动态数组），线程安全但性能较低。
- **现代替代方案**：优先使用 `Deque`（如 `ArrayDeque`），性能更高。

如果不需要线程安全，建议使用 `ArrayDeque` 代替 `Stack`！ 🚀

### 滑动窗口
```java
//长度最小的子数组
int n = nums.length, ans = n+1;
int left = 0;
for(int right = 0; right < n; right++){
	// 右边入
	sum += nums[right];
	while(sum >= target){
	//更新答案
		ans = Math.max(ans, right-left+1);
	//左边出
		sum -= nums[left];
		left++;
	}
	if(ans > n){
		ans = 0;
	}
	return ans;
}
```
### 单调队列
- 创建基于动态数组实现的队列：Deque< Integer> q = new ArrayDeque<>();

1. **`removeLast()`的作用**：它会从队列末尾开始，移除所有小于当前新元素的元素
### 双端队列（Deque）
```java
Deque<Integer> deque = new LinkedList<>();
```
- deque.addLast(10); // 将10添加到队列的末尾
- **`peekFirst`**: 该方法返回队列**头部**（或称“前端”）的元素，但**不删除**该元素。它用于查看队列的第一个元素，而不改变队列的状态。
- **`removeLast`**: 该方法删除队列**尾部**（或称“后端”）的元素，并返回该被删除的元素。即从队列的末尾移除一个元素。

### LinkedList和ArrayDeque

`Deque<Integer> deque = new LinkedList<>();` 和 `Deque<Integer> q = new ArrayDeque<>();` 都是 Java 中实现 `Deque` 接口的不同类，它们有一些关键的区别，主要体现在性能、实现方式和适用场景上。下面是这两者的区别：

#### 1. **实现类的区别**

- **`LinkedList`**：是基于双向链表实现的，支持从队列的两端进行插入和删除操作。每个元素都包含指向前后元素的指针。
- **`ArrayDeque`**：是基于动态数组实现的队列，底层使用数组来存储元素，通过数组的循环操作实现队列的双端插入和删除。

#### 2. **性能**

- **`LinkedList`**：
    - **插入和删除操作**：在队列的两端插入和删除元素的时间复杂度是 O(1)。
    - **访问元素**：访问队列中的元素需要遍历链表，时间复杂度为 O(n)。
- **`ArrayDeque`**：
    - **插入和删除操作**：在队列的两端插入和删除元素的时间复杂度是 O(1)，因为底层数组可以动态扩展。
    - **访问元素**：由于底层是数组，随机访问元素的时间复杂度是 O(1)，但这在 `Deque` 中的使用场景中较少。

#### 3. **内存消耗**

- **`LinkedList`**：由于使用双向链表实现，每个元素都需要存储前后指针，因此比 `ArrayDeque` 占用更多的内存。
- **`ArrayDeque`**：是基于数组的实现，因此内存使用更加紧凑，尤其在元素数量较少时，它比 `LinkedList` 更加高效。

#### 4. **扩展性**

- **`LinkedList`**：没有容量限制，只要有足够的内存，链表可以扩展，因此没有类似 `ArrayDeque` 的扩容问题。
- **`ArrayDeque`**：底层使用数组，因此会根据需要自动扩容，通常是按原数组大小的两倍进行扩展。当数组容量达到上限时，会重新分配一个更大的数组。

#### 5. **线程安全性**

- **`LinkedList`** 和 **`ArrayDeque`** 都 **不是线程安全的**。如果需要在多线程环境中使用这些集合类，可以通过外部同步机制（例如 `Collections.synchronizedDeque()`）来保证线程安全，或者使用 `ConcurrentLinkedDeque` 等线程安全的队列实现。

#### 6. **适用场景**

- **`LinkedList`**：适合需要频繁在队列两端进行插入和删除操作的场景。它适合元素数量较大且插入和删除较频繁的情况。
- **`ArrayDeque`**：适合队列中元素数量较小且访问速度较为重要的场景。由于 `ArrayDeque` 是基于数组实现的，它在处理小规模队列时比 `LinkedList` 更高效。

#### 总结：

- **内存和性能**：`ArrayDeque` 更节省内存并且具有较高的性能，尤其是对于小型队列和随机访问场景，`ArrayDeque` 更优。
- **灵活性**：`LinkedList` 更适合在数据量较大，且需要频繁的插入和删除操作时使用。



### **范围 for 循环**（C++11 特性），遍历 `words` 列表中的每个单词 `w`：
- `for (auto& w : words)`   {    cnt [ w [ 0 ]  - ' a ' ]  [ w [ 1 ]  -  ' a ' ] + +;  }
- `auto& w` 表示 `w` 是 `words` 中元素的引用（避免拷贝，提高效率）
- `w[0] - 'a'`将字母转换为 `0-25` 的索引（例如 `'a' - 'a' = 0`，`'b' - 'a' = 1`，依此类推）
- `cnt[first][second]++` 对对应的字母组合的计数加 1

###  广度优先搜索BFS，用双列表
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



### 链表

用原来的链表操作：
```java
/**
 * 时间复杂度 O(n)
 * 空间复杂度 O(1)
 * @param head
 * @param val
 * @return
 */
public ListNode removeElements(ListNode head, int val) {
    while(head!=null && head.val==val) {
        head = head.next;
    }
    ListNode curr = head;
    while(curr!=null && curr.next !=null) {
        if(curr.next.val == val){
            curr.next = curr.next.next;
        } else {
            curr = curr.next;
        }
    }
    return head;
}
```

**迭代/虚拟头结点**

```java
/**
 * 时间复杂度 O(n)
 * 空间复杂度 O(1)
 * @param head
 * @param val
 * @return
 */
public ListNode removeElements(ListNode head, int val) {
    // 设置一个虚拟的头结点
    ListNode dummy = new ListNode();
    dummy.next = head;

    ListNode cur = dummy;
    while (cur.next != null) {
        if (cur.next.val == val) {
            cur.next = cur.next.next;
        } else {
            cur = cur.next;        
        }
    }
    return dummy.next;
}
```

- **递归：**

	```java
	public ListNode removeElements(ListNode head, int val) {
	    if (head == null) {
	        return head;
	    }
	
	    head.next = removeElements(head.next, val);
	    if (head.val == val) {
	        return head.next;
	    }
	    return head;
	}
	```

	假设链表为 `1 -> 2 -> 6 -> 3 -> 4 -> 5 -> 6`，要删除所有值为 `6` 的节点：
	
	1. 递归调用栈：
	    - removeElements(1, 6)
	        
	        - removeElements(2, 6)
	            
	            - removeElements(6, 6)
	                
	                - removeElements(3, 6)
	                    
	                    - removeElements(4, 6)
	                        
	                        - removeElements(5, 6)
	                            
	                            - removeElements(6, 6)
	                                
	                                - removeElements(null, 6) → 返回 null
	                                    
	2. 递归返回过程：
	    
	    - 最内层返回 null
	        
	    - 6.next=null，判断6 == 6，返回6.next(null)
	        
	    - 5.next=null，判断5!=6，返回5
	        
	    - 4.next=5，判断4!=6，返回4
	        
	    - 3.next=4，判断3!=6，返回3
	        
	    - 6.next=3，判断6== 6，返回3
	        
	    - 2.next=3，判断2!=6，返回2
	        
	    - 1.next=2，判断1!=6，返回1
	        
	最终结果：`1 -> 2 -> 3 -> 4 -> 5`
	- 时间复杂度：O(n)，需要遍历整个链表
	- 空间复杂度：O(n)，递归调用栈的深度
	
	1. 递归的核心思想是"先处理后面的链表，再处理当前节点"
	2. 通过 `head.next = removeElements(head.next, val)` 先处理剩余部分

单链表

```java
//单链表
class MyLinkedList {
    class ListNode {
        int val;
        ListNode next;
        ListNode(int val) {
            this.val=val;
        }
    }
    //size存储链表元素的个数
    private int size;
    //注意这里记录的是虚拟头结点
    private ListNode head;

    //初始化链表
    public MyLinkedList() {
        this.size = 0;
        this.head = new ListNode(0);
    }

    //获取第index个节点的数值，注意index是从0开始的，第0个节点就是虚拟头结点
    public int get(int index) {
        //如果index非法，返回-1
        if (index < 0 || index >= size) {
            return -1;
        }
        ListNode cur = head;
        //第0个节点是虚拟头节点，所以查找第 index+1 个节点
        for (int i = 0; i <= index; i++) {
            cur = cur.next;
        }
        return cur.val;
    }
	public void addAtHead(int val) {
        ListNode newNode = new ListNode(val);
        newNode.next = head.next;
        head.next = newNode;
        size++;
        // 在链表最前面插入一个节点，等价于在第0个元素前添加
        // addAtIndex(0, val);
    }
	// 在第 index 个节点之前插入一个新节点，例如index为0，那么新插入的节点为链表的新头节点。
    // 如果 index 等于链表的长度，则说明是新插入的节点为链表的尾结点
    // 如果 index 大于链表的长度，则返回空
    public void addAtIndex(int index, int val) {
        if (index < 0 || index > size) {
            return;
        }
        //找到要插入节点的前驱
        ListNode pre = head;
        for (int i = 0; i < index; i++) {
            pre = pre.next;
        }
        ListNode newNode = new ListNode(val);
        newNode.next = pre.next;
        pre.next = newNode;
        size++;
    }
```

双链表

```java
//双链表
class MyLinkedList {  
    class ListNode{
        int val;
        ListNode next, prev;
        ListNode(int val){
            this.val = val;
        }
    }

    //记录链表中元素的数量
    private int size;
    //记录链表的虚拟头结点和尾结点
    private ListNode head, tail;
    
    public MyLinkedList() {
        //初始化操作
        this.size = 0;
        this.head = new ListNode(0);
        this.tail = new ListNode(0);
        //这一步非常关键，否则在加入头结点的操作中会出现null.next的错误！！！
        this.head.next = tail;
        this.tail.prev = head;
    }
	public void addAtTail(int val) {
		//等价于在最后一个元素(null)前添加
		addAtIndex(size, val);
	}
```


### 二叉树

- 定义
- 二叉树遍历方式
	- 深度优先遍历
	    - 前序遍历（递归法，迭代法）
	    - 中序遍历（递归法，迭代法）
	    - 后序遍历（递归法，迭代法）
	    - ![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250803161525322.png)
	- 
	- 使用栈来模拟深度遍历，使用队列来模拟广度遍历。
	- 
	- 广度优先遍历
	    - 层次遍历（迭代法）
	- 
	```java
	public class TreeNode {
	    int val;
	    TreeNode left;
	    TreeNode right;
	
	    TreeNode() {}
	    TreeNode(int val) { this.val = val; }
	    TreeNode(int val, TreeNode left, TreeNode right) {
	        this.val = val;
	        this.left = left;
	        this.right = right;
	    }
	}
	```

- 前序遍历
	```java
	class Solution {
	    public List<Integer> preorderTraversal(TreeNode root) {
	        List<Integer> result = new ArrayList<Integer>();
	        preorder(root, result);
	        return result;
	    }
	
	    public void preorder(TreeNode root, List<Integer> result) {
	        if (root == null) {
	            return;
	        }
	        result.add(root.val);            //中
	        preorder(root.left, result);     //左
	        preorder(root.right, result);    //右
	    }
	}
	```

- 中序遍历
	```java
	public void inorder(TreeNode root, List<Integer> result) {
	        if (root == null) {
	            return;
	        }
	        inorder(root.left, result);     //左
	        result.add(root.val);           //中
	        inorder(root.right, result);    //右
	    }
	```

- 后序遍历
	```java
	public void postorder(TreeNode root, List<Integer> result) {
	        if (root == null) {
	            return;
	        }
	        postorder(root.left, result);     //左
	        postorder(root.right, result);    //右
	        result.add(root.val);             //中
	    }
	```

- 迭代遍历
	```java
	// 前序遍历顺序：中-左-右，入栈顺序：中-右-左
	class Solution {
	    public List<Integer> preorderTraversal(TreeNode root) {
	        List<Integer> result = new ArrayList<>();
	        if (root == null){
	            return result;
	        }
	        Stack<TreeNode> stack = new Stack<>();
	        stack.push(root);
	        while (!stack.isEmpty()){
	            TreeNode node = stack.pop();
	            result.add(node.val);
	            if (node.right != null){
	                stack.push(node.right);
	            }
	            if (node.left != null){
	                stack.push(node.left);
	            }
	        }
	        return result;
	    }
	}
	
	// 中序遍历顺序: 左-中-右 入栈顺序： 左-右
	class Solution {
	    public List<Integer> inorderTraversal(TreeNode root) {
	        List<Integer> result = new ArrayList<>();
	        if (root == null){
	            return result;
	        }
	        Stack<TreeNode> stack = new Stack<>();
	        TreeNode cur = root; //使用指针来访问节点
	        while (cur != null || !stack.isEmpty()){
	           if (cur != null){
	               stack.push(cur);//一直访问到最底层，优先左子树
	               cur = cur.left;//左
	           }else{
	               cur = stack.pop();
	               result.add(cur.val);//中
	               cur = cur.right;//右
	           }
	        }
	        return result;
	    }
	}
	
	// 后序遍历顺序 左-右-中 入栈顺序：中-左-右 出栈顺序：中-右-左， 最后翻转结果
	//对前序遍历的代码稍作修改，前序：中左右，入栈顺序改为中右左，最后反转就是左右中
	class Solution {
	    public List<Integer> postorderTraversal(TreeNode root) {
	        List<Integer> result = new ArrayList<>();
	        if (root == null){
	            return result;
	        }
	        Stack<TreeNode> stack = new Stack<>();
	        stack.push(root);
	        while (!stack.isEmpty()){
	            TreeNode node = stack.pop();
	            result.add(node.val);//中
	            if (node.left != null){
	                stack.push(node.left);//左
	            }
	            if (node.right != null){
	                stack.push(node.right);//右
	            }
	        }
	        Collections.reverse(result);//反转
	        return result;
	    }
	}
	```


```java
class Solution {
	public List<Integer> preorderTraversal(TreeNode root) {
		//迭代同一写法，使用栈,前序遍历,中左右,入栈顺序是右左中
		if(root == null) return null;
		Stack<TreeNode> s = new Stack<>();
		List<Integer> res = new ArrayList<>();
		s.push(root);
		while(!s.isEmpty()){
			TreeNode cur = s.peek();
			if(cur != null){ //如果不是null就继续遍历节点
				s.pop();
				if(cur.right != null) s.push(cur.right); //右
				if(cur.left != null) s.push(cur.left);   //左
				s.push(cur);                             //中
				s.push(null);//使用null指针标记
			}else{ //遇到null就可以处理节点
				s.pop();
				cur = s.pop();
				res.add(cur.val);
			}
		}
	}
}
```

- 统一迭代法
	```java
	//中序遍历（左-中-右）：添加右节点-中-null-左
	//后序遍历（左-右-中）：添加左节点-右-中-null
	class Solution {
	    public List<Integer> preorderTraversal(TreeNode root) {
	    //前序遍历
	        List<Integer> result = new LinkedList<>();
	        Stack<TreeNode> st = new Stack<>();
	        if (root != null) st.push(root);
	        while (!st.empty()) {
	            TreeNode node = st.peek();
	            if (node != null) {
	                st.pop(); // 将该节点弹出，避免重复操作，下面再将右左中节点添加到栈中（前序遍历-中左右，入栈顺序右左中）
	                if (node.right!=null) st.push(node.right);  // 添加右节点（空节点不入栈）
	                if (node.left!=null) st.push(node.left);    // 添加左节点（空节点不入栈）
	                st.push(node);                              // 添加中节点
	                st.push(null); // 中节点访问过，但是还没有处理，加入空节点做为标记。
	                
	            } else { // 只有遇到空节点的时候，才将下一个节点放进结果集
	                st.pop();           // 将空节点弹出
	                node = st.peek();    // 重新取出栈中元素
	                st.pop();
	                result.add(node.val); // 加入到结果集
	            }
	        }
	        return result;
	    }
	}
	```

- 层序遍历
```
public void levelOrder(TreeNode node){
	int height = 0; //树深度
	List<List<Integer>> res = new ArrayList<List<Integer>>();
	if(node == null) return null;
	//使用队列，先进先出，逐层遍历
	Deque<TreeNode> que = new LinkedList<>();
	que.offer(node);
	while(!que.isEmpty()){
		int size = que.size();
		List<Integer> path = new ArrayList<>();
		for(int i = 0; i < size; i++){
			TreeNode cur = que.poll();
			path.add(cur.val);
			if(cur.left != null) que.offer(cur.left);
			if(cur.right != null) que.offer(cur.right);
		}
		height++;
		res.add(new ArrayList<>(path));
	}
}
```

- 层级遍历（BFS迭代-队列）
	- 1. **`len = que.size()` 的作用**
	    - 确保内层循环只处理当前层的节点，避免混淆层级。
	        
	    - 例如，第1层 `len=1`（只有根节点 `1`），第2层 `len=2`（节点 `2` 和 `3`）。
	        
	2. **队列的作用**
	    
	    - 按层级顺序存储待访问的节点（BFS核心思想）。
	        
	3. **时间复杂度**
	    - **O(n)**，其中 `n` 是节点数量，每个节点进出队列一次。
	        
	4. **空间复杂度**
	    - **O(n)**，最坏情况下队列存储所有叶子节点（满二叉树约`n/2`）。
	    
	```java
	public void checkFun02(TreeNode node) {
	    if (node == null) return;  // 空树直接返回
	    
	    Queue<TreeNode> que = new LinkedList<>();  // 初始化队列
	    que.offer(node);  // 根节点入队
	    
	    while (!que.isEmpty()) {  // 只要队列不为空，就继续处理
	        List<Integer> itemList = new ArrayList<>();  // 存储当前层的节点值
	        int len = que.size();  // 当前层的节点数量
	        
	        while (len > 0) {  // 遍历当前层的所有节点
	            TreeNode tmpNode = que.poll();  // 出队一个节点
	            itemList.add(tmpNode.val);  // 记录节点值
	            
	            // 将该节点的左右子节点（下一层）入队
	            if (tmpNode.left != null) que.offer(tmpNode.left);
	            if (tmpNode.right != null) que.offer(tmpNode.right);
	            len--;  // 当前层节点数减1
	        }
	        
	        resList.add(itemList);  // 将当前层的节点值列表加入结果
	    }
	}
	```

- 层级遍历（BFS递归）
	```java
	class Solution {
	    public List<List<Integer>> resList = new ArrayList<List<Integer>>();
	
	    public List<List<Integer>> levelOrder(TreeNode root) {
	        dfs(root,0);
	        return resList;
	    }
	    public void dfs(TreeNode node, Integer deep){
	        if(node == null) return;
	
	        //进入新层级
	        deep++;
	
	        //如果resList大小不够，新建层级列表
	        while(resList.size() < deep){
	            resList.add(new ArrayList<>());
	        }
	        //将当前节点加入当前层级
	        resList.get(deep-1).add(node.val); //deep从1开始，deep-1转换为列表索引从0开始
	        dfs(node.left, deep);
	        dfs(node.right,deep);
	    }
	}
	```

- 变种问题
	### **自底向上的层序遍历**
	只需在最后反转 `resList`：
	```java
	Collections.reverse(resList);
	```

	**只返回某一层的节点**
	例如返回第 `k` 层：
	```java
	if (k == resList.size()) {
	    return resList.get(k - 1);
	}
	```
### 递归

- 三要素
	- 确定参数和返回值类型
	- 确定终止条件
	- 确定单层递归逻辑


### 回溯

| 问题类型  | 时间复杂度            | 空间复杂度            |
| ----- | ---------------- | ---------------- |
| 组合问题  | `O(k × C(n, k))` | `O(n × C(n, k))` |
| 排列问题  | `O(n × n!)`      | `O(n × n!)`      |
| 子集问题  | `O(n × 2^n)`     | `O(n × 2^n)`     |
| 分割回文串 | `O(n × 2^n)`     | `O(n × 2^n)`     |

程序运行的时候对unordered_set 频繁的insert，unordered_set需要做哈希映射（也就是把key通过hash function映射为唯一的哈希值）相对费时间，而且每次重新定义set，insert的时候其底层的符号表也要做相应的扩充，也是费事的。

子集问题分析：

- 时间复杂度：O(2^n)，因为每一个元素的状态无外乎取与不取，所以时间复杂度为O(2^n)
- 空间复杂度：O(n)，递归深度为n，所以系统栈所用空间为O(n)，每一层递归所用的空间都是常数级别，注意代码里的result和path都是全局变量，就算是放在参数里，传的也是引用，并不会新申请内存空间，最终空间复杂度为O(n)

排列问题分析：

- 时间复杂度：O(n!)，这个可以从排列的树形图中很明显发现，每一层节点为n，第二层每一个分支都延伸了n-1个分支，再往下又是n-2个分支，所以一直到叶子节点一共就是 n * n-1 * n-2 * ..... 1 = n!。
- 空间复杂度：O(n)，和子集问题同理。

组合问题分析：

- 时间复杂度：O(2^n)，组合问题其实就是一种子集的问题，所以组合问题最坏的情况，也不会超过子集问题的时间复杂度。
- 空间复杂度：O(n)，和子集问题同理。

N皇后问题分析：

- 时间复杂度：O(n!) ，其实如果看树形图的话，直觉上是O(n^n)，但皇后之间不能见面所以在搜索的过程中是有剪枝的，最差也就是O（n!），n!表示n * (n-1) * .... * 1。
- 空间复杂度：O(n)，和子集问题同理。

解数独问题分析：

- 时间复杂度：O(9^m) , m是'.'的数目。
- 空间复杂度：O(n^2)，递归的深度是n^2

#### 总结
![image.png](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/20250815212945025.png)


### 思路

1. 前缀后缀
2. 位置对调
3. 哈希
4. 要求时间空间复杂度分别为 O(nlogn) 和 O(1)，根据时间复杂度我们自然想到二分法，从而联想到归并排序；
5. 使用栈来模拟深度遍历，使用队列来模拟广度遍历。
6. 求二叉树深度 和 二叉树高度的差异，求深度适合用前序遍历，而求高度适合用后序遍历。
7. 只有寻找某一条边（或者一个节点）的时候，递归函数会有bool类型的返回值。
8. 如果需要搜索整棵二叉树且不用处理递归返回值，递归函数就**不要返回值**。（这种情况就是本文下半部分介绍的113.路径总和ii）
9. 如果需要搜索整棵二叉树且需要处理递归返回值，递归函数就**需要返回值**。 （这种情况我们在[236. 二叉树的最近公共祖先 (opens new window)](https://programmercarl.com/0236.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E8%BF%91%E5%85%AC%E5%85%B1%E7%A5%96%E5%85%88.html)中介绍）
10. 如果要搜索其中一条符合条件的路径，那么递归一定需要返回值，因为遇到符合条件的路径了就要及时返回。

|**判断条件**|**需要返回值**|**不需要返回值**|
|---|---|---|
|**是否依赖子问题的结果**|是（如累加、判断存在性）|否（如遍历、记录所有解）|
|**是否需要传递结果到顶层**|是|否（结果通过参数或全局变量存储）|
|**典型问题**|数值计算、搜索终止条件|全排列、回溯尝试所有可能性|

12. 回溯法，一般可以解决如下几种问题：
	
	- 组合问题：N个数里面按一定规则找出k个数的集合
	- 切割问题：一个字符串按一定规则有几种切割方式
	- 子集问题：一个N个数的集合里有多少符合条件的子集
	- 排列问题：N个数按一定规则全排列，有几种排列方式
	- 棋盘问题：N皇后，解数独等等
13. 如果是一个集合来求组合的话，就需要startIndex，
	如果是多个集合取组合，各个集合之间相互不影响，那么就不用startIndex，

### 复杂度分析

子集问题分析：

- 时间复杂度：O(2^n)，因为每一个元素的状态无外乎取与不取，所以时间复杂度为O(2^n)
- 空间复杂度：O(n)，递归深度为n，所以系统栈所用空间为O(n)，每一层递归所用的空间都是常数级别，注意代码里的result和path都是全局变量，就算是放在参数里，传的也是引用，并不会新申请内存空间，最终空间复杂度为O(n)

排列问题分析：

- 时间复杂度：O(n!)，这个可以从排列的树形图中很明显发现，每一层节点为n，第二层每一个分支都延伸了n-1个分支，再往下又是n-2个分支，所以一直到叶子节点一共就是 n * n-1 * n-2 * ..... 1 = n!。
- 空间复杂度：O(n)，和子集问题同理。

组合问题分析：

- 时间复杂度：O(2^n)，组合问题其实就是一种子集的问题，所以组合问题最坏的情况，也不会超过子集问题的时间复杂度。
- 空间复杂度：O(n)，和子集问题同理。

N皇后问题分析：

- 时间复杂度：O(n!) ，其实如果看树形图的话，直觉上是O(n^n)，但皇后之间不能见面所以在搜索的过程中是有剪枝的，最差也就是O（n!），n!表示n * (n-1) * .... * 1。
- 空间复杂度：O(n)，和子集问题同理。

解数独问题分析：

- 时间复杂度：O(9^m) , m是'.'的数目。
- 空间复杂度：O(n^2)，递归的深度是n^2

### **1. 数组 & 哈希表**

|题目|难度|关键点|频率|
|---|---|---|---|
|[1. 两数之和](https://leetcode.cn/problems/two-sum/)|Easy|哈希表|⭐⭐⭐⭐⭐|
|[49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams/)|Medium|哈希 + 字符串排序|⭐⭐⭐⭐|
|[128. 最长连续序列](https://leetcode.cn/problems/longest-consecutive-sequence/)|Medium|哈希 + 并查集思想|⭐⭐⭐⭐|
|[560. 和为 K 的子数组](https://leetcode.cn/problems/subarray-sum-equals-k/)|Medium|前缀和 + 哈希|⭐⭐⭐⭐|

---

### **2. 链表**

|题目|难度|关键点|频率|
|---|---|---|---|
|[206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)|Easy|迭代/递归|⭐⭐⭐⭐⭐|
|[141. 环形链表](https://leetcode.cn/problems/linked-list-cycle/)|Easy|快慢指针|⭐⭐⭐⭐|
|[21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)|Easy|双指针|⭐⭐⭐⭐|
|[146. LRU 缓存](https://leetcode.cn/problems/lru-cache/)|Medium|哈希 + 双向链表|⭐⭐⭐⭐⭐|

---

### **3. 二叉树**

|题目|难度|关键点|频率|
|---|---|---|---|
|[94. 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)|Easy|递归/迭代|⭐⭐⭐⭐|
|[102. 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/)|Medium|BFS|⭐⭐⭐⭐⭐|
|[104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)|Easy|递归/DFS|⭐⭐⭐⭐|
|[543. 二叉树的直径](https://leetcode.cn/problems/diameter-of-binary-tree/)|Easy|后序遍历|⭐⭐⭐⭐|

---

### **4. 动态规划（DP）**

|题目|难度|关键点|频率|
|---|---|---|---|
|[70. 爬楼梯](https://leetcode.cn/problems/climbing-stairs/)|Easy|基础DP|⭐⭐⭐⭐|
|[53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)|Easy|Kadane算法|⭐⭐⭐⭐⭐|
|[322. 零钱兑换](https://leetcode.cn/problems/coin-change/)|Medium|背包DP|⭐⭐⭐⭐|
|[300. 最长递增子序列](https://leetcode.cn/problems/longest-increasing-subsequence/)|Medium|二分优化DP|⭐⭐⭐⭐⭐|

---

### **5. 回溯 & DFS/BFS**

|题目|难度|关键点|频率|
|---|---|---|---|
|[46. 全排列](https://leetcode.cn/problems/permutations/)|Medium|回溯模板|⭐⭐⭐⭐|
|[78. 子集](https://leetcode.cn/problems/subsets/)|Medium|回溯/位运算|⭐⭐⭐⭐|
|[200. 岛屿数量](https://leetcode.cn/problems/number-of-islands/)|Medium|DFS/BFS|⭐⭐⭐⭐⭐|
|[79. 单词搜索](https://leetcode.cn/problems/word-search/)|Medium|回溯 + 剪枝|⭐⭐⭐⭐|

---

### **6. 堆 & 优先队列**

|题目|难度|关键点|频率|
|---|---|---|---|
|[215. 数组中的第K个最大元素](https://leetcode.cn/problems/kth-largest-element-in-an-array/)|Medium|快排思想/堆|⭐⭐⭐⭐⭐|
|[347. 前 K 个高频元素](https://leetcode.cn/problems/top-k-frequent-elements/)|Medium|哈希 + 堆|⭐⭐⭐⭐|

---

### **7. 滑动窗口 & 双指针**

|题目|难度|关键点|频率|
|---|---|---|---|
|[3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)|Medium|滑动窗口|⭐⭐⭐⭐⭐|
|[11. 盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/)|Medium|双指针|⭐⭐⭐⭐|
|[438. 找到字符串中所有字母异位词](https://leetcode.cn/problems/find-all-anagrams-in-a-string/)|Medium|滑动窗口|⭐⭐⭐⭐|

---

### **✅ 如何高效刷题？**

1. **优先掌握 ⭐⭐⭐⭐⭐ 题目**，尤其是：
    
    - **两数之和**、**LRU缓存**、**反转链表**
        
    - **二叉树层序遍历**、**岛屿数量**
        
    - **最大子数组和**、**零钱兑换**
        
    - **无重复字符的最长子串**
        
2. **同类题目一起刷**（如先刷完所有二叉树题目再刷DP）。
    
3. **面试前重点复习 Hot 100**，80% 的面试题都来自这里。