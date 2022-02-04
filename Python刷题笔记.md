

### 常用语法

1. nlargest(k, arr) return first k largest values in arr

   

2. arr.sort(key = lambda x:x[0])    sort x by x[0] in ascending order

   

3. ```python
   pq = []
   heappush.(pq,numbers[i])
   heappop(pq)
   ```

   python 为小根堆，若要取最大值，需要存入相反数
   
   
   
4. mq = collections.defaultdict(list)

   mq[key].append(value)
   
   
   
5. ans = sum(nums[i] for i in range(n))

   

6. math.sqrt()

   

7. ASCII to char: char(10)

   

8. char to ASCII : ord('a')

   

### 经典题目

#### 1. 回溯，dfs 

1. 子集： [1，2，2，4] 返回不重复子集

   ![image-20220120003402274](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220120003402274.png)

   当递归进入下一层时，遍历起点为上一层的index+1。因为遍历只能有一个方向且不能重复选择元素，所以index要加1。

   

2. 全排列：nums = [1,1,2] 返回所有不同排列方式：

   ![image-20220120003428039](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220120003428039.png)

   全排列的题目与元素位置有关，所有每次递归都要遍历所有元素。因此递归进入下一层时，遍历起点都是0。因为有可能前面的元素在当前path还没遍历到，所以要遍历所有元素找出未被访问的值。与上一题不一样。

   

3. 组数总和 I

   nums = [2,3,6,7]，target=7，nums中元素unique。找出元素中所有组合使得和为target，所有元素可以重复使用

   ![image-20220119015414647](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220119015414647.png)

   这类题目与元素位置无关，所以遍历起点为begin。元素可以多次使用，所以16行为i，而不是i+1。

   

4. 组数总和 II 

   candidates = [10,1,2,7,6,1,5], target=8，nums中元素不unique。找出所有组合使得和为target，所有元素只能使用一次

   ![image-20220119020241763](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220119020241763.png)

   这题与找子集十分类似，只是退出递归的条件为 target == 0

   

5. 总结

   子集问题，元素位置与结果无关，因此每次遍历起点都为当前上一层起点+1，从而改变来减少遍历。

   全排列问题，元素位置影响结果，所以每次都得从头遍历，同时需要维护 visited 数组来避免重复访问。

   组数综合问题，元素位置与结果无关，递归起点发生改变。与子集问题类似。

   回溯问题模板：

   ```python
   result=[]
   def backtrack(路径，选择列表)：
   	if 满足条件：
       	result.add(路径)
           return
       
       for 选择 in 选择列表：
       	做选择
           backtrack(路径，选择列表)
           撤销回溯
   ```

   

6. Word Search, Input:  board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"

   output: True. 通常回溯类的题目都是找所有路径/方案，而这题比较例外，是找是否存在该值/方案：

   ![image-20220120013835428](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220120013835428.png)
   
   dfs返回一个bool。在每次dfs前，都要判断该dfs是否能找到满足条件的值(第16, 31行)。注意，此处不能定义全局变量find = false 然后在递归中修改，因为当退出递归时候，find值会发生更改，无法保持一致性。
   
   
   
7. 判断两个str是否为anagram有两个方法，一是排序后进行比较，二是生成26位的数组充当哈希表，并统计每个字符串出现次数。一的时间复杂度为 O(nklogk)，k是字符串最大长度，二的时间复杂度为 O(n(k+∣Σ∣)) k为字符串最大长度，Σ 为哈希表大小，此处为26。

#### 2. 链表删除

1. 删除链表中的重复元素：

<img src="C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220121154856436.png" alt="image-20220121154856436" style="zoom:80%;" /><img src="C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220121154918175.png" alt="image-20220121154918175" style="zoom:80%;" />

一次遍历可以完成。值得注意的是，虽然在23 行涉及了cur.next.next, 但是并未涉及到他的value值，所以该节点可以为空，即while中不需要保证 cue.next.next 不为空。 同时，因为头节点必然出现在答案中，所以不需要设置哑节点，直接使用head即可

2. 删除列表中重复元素II:

<img src="C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220121155247245.png" alt="image-20220121155247245" style="zoom:80%;" /><img src="C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220121155305284.png" alt="image-20220121155305284" style="zoom: 80%;" />

此题与上一题不同在，头节点可能被删除，所以必须设置哑节点。同时第17行需要用到fast.next.next.val， 所以fast.next.next不能为空。

#### 3. 解码方法

<img src="C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220124234114583.png" alt="image-20220124234114583" style="zoom:80%;" /><img src="C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20220124234131545.png" alt="image-20220124234131545" style="zoom: 80%;" />

若dp容量为n，需要判断dp[0], dp[1]，且还需要判断n的值，比较麻烦。此处直接将容量设为n+1，dp[i]代表前i个元素。

