 
 
 
## Medium (160)
**0. [Anagrams.java](https://github.com/awangdev/LintCode/blob/master/Java/Anagrams.java)**      Level: Medium
      

1. HashMap 的做法. sort每个string, 存进HashMap, 重复的就是anagrams,最后输出。   
   toCharArray
   Arrays.sort
   Stirng.valueOf(char[])
   时间n*L*O(logL),L是最长string的长度。

2. Arrays.toString(arr)的做法。arr是int[26], assuming only have 26 lowercase letters.    
Count occurrance, 然后convert to String，作为map的key.
Time complexity: nO(L)

3. 另一种做法：http://www.jiuzhang.com/solutions/anagrams/   
   1. take each string, count the occurrance of the 26 letters. save in int[]count.   
   2. hash the int[] count and output a unique hash value.   
      hash = hash * a + num   
      a = a * b.   
   3. save to hashmap in the same way as we do. 

这一步把for s: strs 里面的时间复杂度降到了O(L). L = s.length().   
Need to work on the getHash() function.

时间变成n*O(L). Better.




---

**1. [Binary Tree Level Order Traversal II.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Level%20Order%20Traversal%20II.java)**      Level: Medium
      
方法1:
跟Binary Tree Level Order Traversal一样,只不过存result一直存在存在0位.

方法2(略复杂, 不需要):
普通BFS，用一个queue，加上一个queue.size()来交替换行. 
或者多用一个queue来存下个level的nodes

方法3:
DFS, 根据level来append每个list
rst里面add(0,...)每次都add在list开头



---

**2. [Binary Tree Level Order Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Level%20Order%20Traversal.java)**      Level: Medium
      
方法1. 最普通,Non-recursive: BFS, queue, 用个queue.size()来end for loop:换行。   
   或者用两个queue. 当常规queue empty，把backup queue贴上去。

方法2. Recursive with dfs:   
   每个level都应该有个ArrayList. 那么用一个int level来查看：是否每一层都有了相应的ArrayList。   
   如果没有，就加上一层。    
   之后每次都通过DFS在相应的level上面加数字。




---

**3. [Binary Tree Longest Consecutive Sequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Longest%20Consecutive%20Sequence.java)**      Level: Medium
      
屌炸天的4行代码。Divide and Conquer

主要想法：    
Recursive用好。首先在这个level比一比，可否成。   
不成的话，另立门户, count = 1。    
然后左右开弓。再把结果拿过来比较一下就好了。



---

**4. [Binary Tree Maximum Path Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Maximum%20Path%20Sum%20II.java)**      Level: Medium
      
比Binary Tree Maximum Path Sum I 简单许多. 因为条件给的更多：at least 1 node + have to start from root => have to have root.

方法1:   
维持一个global或者recursive里的sum。traversal entire tree via DFS. 简单明了。


方法2:   
Single path: either left or right.   
If the path sum < 0, just skip it.   



---

**5. [Binary Tree Right Side View.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Right%20Side%20View.java)**      Level: Medium
      
最右:即level traversal每一行的最末尾.   

BFS，用queue.size()来出发saving result.



---

**6. [Binary Tree Serialization.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Serialization.java)**      Level: Medium
      
方法1: BFS. Non-recursive, using queue. 想法直观。level-order traversal. save到一个string里面就好。

方法2: DFS. Recursive. 需要一点思考。basically divide and conquer. 但是代码相对来说短。



---

**7. [Binary Tree Zigzag Level Order Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Zigzag%20Level%20Order%20Traversal.java)**      Level: Medium
      
简单的level traversal.根据level奇数偶数而add到不同位子.



---

**8. [ColorGrid.java](https://github.com/awangdev/LintCode/blob/master/Java/ColorGrid.java)**      Level: Medium
      
用HashMap， 理解题目规律，因为重复的计算可以被覆盖，所以是个优化题。

消灭重合点:       
如果process当下col, 其实要减去过去所有加过的row的交接点。。。     
再分析，就是每次碰到row 取一个单点, sumRow += xxx。       
然后process当下col时候， sum += colValue * N - sumRow. 就等于把交叉所有row（曾经Process过的row）的点减去了。很方便。

最后read in 是O(P),  process也是O(P).




---

**9. [Combination Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum%20II.java)**      Level: Medium
      
还是DFS. 和Combination Sum I 类似.      
确保Helper是用i+1，下一层的数字, 不允许重复。



---

**10. [Combination Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Combination%20Sum.java)**      Level: Medium
      
递归，backtracking. 非常normal。需要先sort.    
记得求sum时候也pass 一个sum进去，backtracking一下sum也，这样就不必每次都sum the list了。   

题目里面所同一个元素可以用n次，但是，同一种solution不能重复出现。如何handle?

1. 用一个index （我们这里用了start）来mark每次recursive的起始点。
2. 每个recursive都从for loop里面的i开始，而i = start。 也就是，下一个iteration,这个数字会有机会被重复使用。
3. 同时，确定在同一个for loop里面，不同的Index上面相同的数字，不Process两遍。用一个prev 作为checker.

假如[x1, x2, y, z], where x1 == x2， 上面做法的效果: 
我们可能有这样的结果: x1,x1,x1,y,z    
但是不会有:x1,x2,x2,y,z   
两个solution从数字上是一样的，也就是duplicated solution, 要杜绝第二种。



---

**11. [Combinations.java](https://github.com/awangdev/LintCode/blob/master/Java/Combinations.java)**      Level: Medium
      
Combination DFS。 画个图想想. 每次从1~n里面pick一个数字i

因为下一层不能重新回去 [0~i]选，所以下一层recursive要从i+1开始选。



---

**12. [Construct Binary Tree from Inorder and Postorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Construct%20Binary%20Tree%20from%20Inorder%20and%20Postorder%20Traversal.java)**      Level: Medium
      
写个Inorder和Postorder的例子。利用他们分left/right subtree的规律解题。

Postorder array 的末尾， 就是当下层的root.   
在Inorder array 里面找到这个root,就刚好把左右两边分割成left/right tree。

这题比较tricky地用了一个helper做recursive。 特别要注意处理index的变化, precisely考虑开头结尾

可惜有个不可避免的O(n) find element in array.



---

**13. [Container With Most Water.java](https://github.com/awangdev/LintCode/blob/master/Java/Container%20With%20Most%20Water.java)**      Level: Medium
      
类似木桶理论。盛水的最高取决于最低的那面墙。
左右两墙，往中间跑动。
另，若一面墙已经小于另外一面，就要移动，换掉矮墙（可能下一面更高，或更低）；但决不能换掉当下的高墙，因为低墙已经limit的盛水的上限，若高墙移动，导致两墙之间距离减少，就注定水量更少了。（弄啥来，不能缺心眼啊）


---

**14. [Convert Binary Search Tree to Doubly Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Binary%20Search%20Tree%20to%20Doubly%20Linked%20List.java)**      Level: Medium
      

会iterative traverse Binary Search Tree就好（Stack && handle left-dig-down）, 然后create Doubly-ListNode 时候注意就好.

注意inorder traversal在check right node的事后，    
不论right == null or != null, 每次都要强行move to right.    

如果不node = node.right,     
很可能发生窘境：       
node alays = stack.top(), 然后stack.top()一直是一开始把left 全部遍历的内容。所以就会infinite loop, 永远在左边上下上下。      



---

**15. [Copy List with Random Pointer.java](https://github.com/awangdev/LintCode/blob/master/Java/Copy%20List%20with%20Random%20Pointer.java)**      Level: Medium
      
Basic Implementation, 其中用了一下HashMap:  

遍历head.next .... null.    
每一步都check map里面有没有head。没有？加上。    
每一步都check map里面有没有head.random。没有？加上。



---

**16. [Count of Smaller Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Count%20of%20Smaller%20Number.java)**      Level: Medium
      
和平时的segment tree问题不同。 0 ～ n-1代表实际数字。是造一个based on real value的segment tree.
Modify时，把array里面的value带进去，找到特定的位子（leaf）,然后count+1. 

最终在SegmentTree leaf上面全是array里面实际的数字。

trick:   
在query前，给进去的start和end是： 0 ~ value-1.   
value-1就是说，找比自己所在range小1的range（那么自然而然地就不包括自己了），这样就找到了smaller number.   


[那么其他做过的SegmentTree是怎么样呢？]   
那些构成好的SegmentTree(找min,max,sum)也有一个Array。但是构成Tree时候，随Array的index而构架。   
也就是说，假如有Array[x,y,....]:在leaf,会有[0,0] with value = x. [1,1] with value = y. 

[但是这题]   
构成时，是用actual value.也就是比如Array[x,y,....]会产生leaf:[x,x]with value = ..; [y,y]with value =...    

其实很容易看穿:   
若给出一个固定的array构成 SegmentTree，那估计很简单：按照index从0~array.lengh，leaf上就是[0,0] with value = x.

若题目让构造一个空心SegmentTree, based on value 0 ~ n-1 (n <= 10000), 然后把一个Array的value modify 进去。   
这样八成是另外一种咯。



---

**17. [Delete Digits.java](https://github.com/awangdev/LintCode/blob/master/Java/Delete%20Digits.java)**      Level: Medium
      
数位靠前的，权值更大. 所以硬来把靠前的相对更大的（跟following digit相比）去掉。



---

**18. [Encode and Decode Strings.java](https://github.com/awangdev/LintCode/blob/master/Java/Encode%20and%20Decode%20Strings.java)**      Level: Medium
      
方法1:    
用数字+"#"+string来encode.    
基于我们自己定的规律, 在decode的里面不需要过多地去check error input, assume所有input都是规范的.    
decode就是找"#",然后用"#"前的数字截取后面的string.



Old Solution:    
Cast character into int. 串联起来, seperate by "LINE".   
handle empty list [], or just null: 要把Null特别mark一下为‘NULL’, 这样decode时才能check到。      adminadmin




---

**19. [Fast Power.java](https://github.com/awangdev/LintCode/blob/master/Java/Fast%20Power.java)**      Level: Medium
      
a^n可以被拆解成(a*a*a*a....*a)， 是乘机形式，而%是可以把每一项都mod一下的。所以就拆开来take mod.

这里用个二分的方法，recursively二分下去，直到n/2为0或者1，然后分别对待. 

注意1: 二分后要conquer，乘积可能大于Integer.MAX_VALUE, 所以用个long.

注意2: 要处理n%2==1的情况，二分时候自动省掉了一份，要乘一下。




---

**20. [Find the Connected Component in the Undirected Graph.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20the%20Connected%20Component%20in%20the%20Undirected%20Graph.java)**      Level: Medium
      
BFS遍历，把每个node的neighbor都加进来。    

一定注意要把visit过的node Mark一下。因为curr node也会是别人的neighbor，会无限循环。      

Component的定义：所有Component内的node必须被串联起来via path (反正这里是undirected, 只要链接上就好)     

这道题：其实component在input里面都已经给好了，所有能一口气visit到的，全部加进queue里面，他们就是一个component里面的了。     

而我们这里不需要判断他们是不是Component。   



---

**21. [Find the Weak Connected Component in the Directed Graph.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20the%20Weak%20Connected%20Component%20in%20the%20Directed%20Graph.java)**      Level: Medium
      
Identify这是个union-find问题还挺巧妙。    
看到了weak component的形式： 一个点指向所有，那么所有的点都有一个公共的parent，然后就是要找出这些点。    

为何不能从一个点出发，比如A，直接print它所有的neighbors呢？     
	不行，如果轮到了B点，那因为是directed,它也不知道A的情况，也不知道改如何继续加，或者下手。    

所以，要把所有跟A有关系的点，或者接下去和A的neighbor有关系的点，都放进union-find里面，让这些点有Common parents.     

最后output的想法：    
做一个 map <parent ID, list>。    
之前我们不是给每个num都存好了parent了嘛。    
每个num都有个parent, 然后不同的parent就创造一个不同的list。   
最后，把Map里面所有的list拿出来就好了。    



---

**22. [Flatten 2D Vector.java](https://github.com/awangdev/LintCode/blob/master/Java/Flatten%202D%20Vector.java)**      Level: Medium
      
大概意思就是把2D list里面的element全部遍历一遍。
注意啊，一开始理解题意搞错：我以为是必须要排序正确，所以上来就PriorityQueue+HashMap搞得无比复杂。其实，这个跟一个nxn的matrix遍历，是没区别的拉。
所有来个x,y，把2d list跑一变。



---

**23. [Fraction to Recurring Decimal.java](https://github.com/awangdev/LintCode/blob/master/Java/Fraction%20to%20Recurring%20Decimal.java)**      Level: Medium
      
不难想到处理除法：考虑正负，考虑小数点前后。主要是小数点以后的要着重考虑。
很容易忽略的是integer的益处。


---

**24. [Generate Parentheses.java](https://github.com/awangdev/LintCode/blob/master/Java/Generate%20Parentheses.java)**      Level: Medium
      
递归。
看thought.取或者不取(,  )

Note: 在DFS时, 可以pass object (String) and re-create every time; or pass a reference (StringBuffer) and maintain it



---

**25. [Gray Code.java](https://github.com/awangdev/LintCode/blob/master/Java/Gray%20Code.java)**      Level: Medium
      
题目蛋疼，目前只接受一种结果。

BackTracking + DFS:   
   Recursive helper里每次flip一个 自己/左边/右边. Flip过后还要恢复原样.遍历所有.

曾用法（未仔细验证）：   
基本想法就是从一个点开始往一个方向走，每次flip一个bit, 碰壁的时候就回头走。



---

**26. [H-Index II.java](https://github.com/awangdev/LintCode/blob/master/Java/H-Index%20II.java)**      Level: Medium
      
H-index的一个优化。
binary search


---

**27. [H-Index.java](https://github.com/awangdev/LintCode/blob/master/Java/H-Index.java)**      Level: Medium
      
例子写出来，发现可以sort以后按照定义搜索一遍。 nlogn.
	当然，搜索一遍时候可以优化，用binary search. 但是没意义，因为array.sort已经用了nlogn

o(n)也可以，用bucket. 比较巧妙。




---

**28. [HashWithCustomizedClass(LinkedList).java](https://github.com/awangdev/LintCode/blob/master/Java/HashWithCustomizedClass(LinkedList).java)**      Level: Medium
      
练习HashMap with customized class. 



---

**29. [Heapify.java](https://github.com/awangdev/LintCode/blob/master/Java/Heapify.java)**      Level: Medium
      
Heap用的不多. 得用一下, 才好理解。   
通常default 的PriorityQueue就是给了一个现成的min-heap：所有后面的对应element都比curr element 小。

Heapify里面的siftdown的部分：
	只能从for(i = n/2-1 ~ 0)， 而不能从for(i = 0 ~ n/2 -1): 必须中间开花，向上跑的时候才能确保脚下是符合heap规则的

Heapify/SiftDown做了什么？    
确保在heap datastructure里面curr node下面的两个孩子，以及下面所有的node都遵循一个规律。   
比如在这里，若是min-heap,就是后面的两孩子都要比自己大。若不是，就要swap。    

还是要记一下min-heap的判断规律:for each element A[i], we will get A[i * 2 + 1] >= A[i] and A[i * 2 + 2] >= A[i].

siftdown时：在curr node和两个son里面小的比较。如果的确curr < son, 搞定，break while.   
但若curr 并不比son小，那么就要换位子，而且继续从son的位子往下面盘查。    



---

**30. [Implement Trie (Prefix Tree).java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20Trie%20(Prefix%20Tree).java)**      Level: Medium
      
Trie自己不多用到。
如果是遇到一个一个字查询的题，可以考虑一下。
构建TrieNode的时候要注意：如何找孩子？如果是个map的话，其实就挺好走位的。
而且，每个node里面的 char 或者string有时候用处不大，
可以为空。但是有些题目，比如在结尾要return一些什么String，就可以在end string那边存一个真的String。




---

**31. [Inorder Successor in Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Inorder%20Successor%20in%20Binary%20Search%20Tree.java)**      Level: Medium
      

画inorder图，发现规律.每个node的后继node(successor)有几种情况:   
1. node.right 是个leaf到底了。那么就return.   
2. set rightNode = node.right， 但发现rightNode has a lot left children to leaf.   
3. 比如, node.right == null， 也就是node自己是leaf，要回头看山顶找Inorder traversal规则里的下一个。   
	发现：其实就是每层都把路过的curr node放在stack里，最上面的，就是当下改return的那个successor:) Done.



---

**32. [Interval Minimum Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Interval%20Minimum%20Number.java)**      Level: Medium
      
SegtmentTree, methods: Build, Query. 这题是在SegmentTreeNode里面存min.

类似的有存:max, sum, min





---

**33. [Interval Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Interval%20Sum.java)**      Level: Medium
      
其实是segment tree 每个node上面加个sum。   

记得Segment Tree methods: Build, Query

Note: 存在SegmentTreeNode里面的是sum.  其他题目可能是min,max ... or something else.




---

**34. [Kth Largest Element.java](https://github.com/awangdev/LintCode/blob/master/Java/Kth%20Largest%20Element.java)**      Level: Medium
      
用Quick Sort 里面partion的一部分。     
partion的结果是那个low, 去找 low==nums.size() - k， 也就是倒数第K个。    
没找到继续partion recursively.

sort的过程是排一个从小到大的list. (同样的代码还可以好xth smallest，mid变成x就好)

Quick Sort:   
每个iteration, 找一个pivot,然后从low,和high都和pivot作比较。    
找到一个low>pivot, high<pivot, 也就可以swap了。    
得到的low就是当下的partion point了




---

**35. [Kth Smallest Element in a BST.java](https://github.com/awangdev/LintCode/blob/master/Java/Kth%20Smallest%20Element%20in%20a%20BST.java)**      Level: Medium
      

很容想到Inorder-binary-search-tree Traversal
Recursive 不难，然后稍微优化一下，确保rst.size() == k 时候，就可以return了。
Iterative 稍微难想点：先把最左边的add， pop() stack， 加上右边（如果存在）； 下一个轮回，如果又左孩子，又是一顿加。



---

**36. [Longest Common Prefix.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Common%20Prefix.java)**      Level: Medium
      
Nested loop, 每一次比较所有string 同位是否相等。

相等，append string. 不等，return.



---

**37. [Longest Palindromic Substring.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Palindromic%20Substring.java)**      Level: Medium
      
方法1: 从中间劈开. 遍历i，从n个不同的点劈开：每次劈开都看是否可以从劈开出作为palindromic的中点延伸。   
   Worst case: 整个string都是相同字符，time complexity变成： 1 + 2 +３　＋　．．．　＋n = O(n^2)

方法2: 穷举double for loop. O(n^2)




---

**38. [Lowest Common Ancestor of a Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Lowest%20Common%20Ancestor%20of%20a%20Binary%20Search%20Tree.java)**      Level: Medium
      
方法1: 利用 BST的性质，可以直接搜到target node，而做成两个长度不一定相等的list。然后很简单找到LCA 
方法2: Brutly寻找p和q的common ancestor, 然后recursively drive left/right. 非常巧妙, 但是也比较局限; 稍微变条件, 就很难recursive.



---

**39. [Majority Number II.java](https://github.com/awangdev/LintCode/blob/master/Java/Majority%20Number%20II.java)**      Level: Medium
      
分三份：a b c考虑。若a, countA++, 或b, countB++，或c，countA--,countB--.

最后出现的两个count>0的a和b,自然是potentially大于1/3的。其中有一个大于1/3.

比较a和b哪个大，就return哪一个。



---

**40. [Majority Number III.java](https://github.com/awangdev/LintCode/blob/master/Java/Majority%20Number%20III.java)**      Level: Medium
      
与其他Majority Number一样。

出现次数多余1/k，就要分成k份count occurance.用HashMap。 存在的+1；不存在map里的，分情况:    
若map.size() == k,说明candidate都满了，要在map里把所有现存的都-1；
若map.size() < k, 说明该加新candidate，那么map.put(xxx, 1);

最后在HashMap里找出所留下的occurance最大的那个数。



---

**41. [Merge k Sorted Arrays.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20k%20Sorted%20Arrays.java)**      Level: Medium
      
由Merge k sorted list启发。用PriorityQueue,存那k个首发element。

PriorityQueue需要存储单位。自己建一个Class Node 存val, x,y index.    
因为array里没有 'next' pointer，只能存x,y来推next element



---

**42. [Merge k Sorted Lists.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20k%20Sorted%20Lists.java)**      Level: Medium
      
用Priorityqueue来排列所有list的leading node.

记得k lists 需要是已经sort好的。   

时间：n*O(logk)   
PriorityQueue: logk   

这个题目可以有好几个衍生：   
   比如，如果k很大，一个机器上放不下所有的k list怎么办？ 
   比如，如果Merge起来的很长，一个机器上放不下怎么办？

Note:
1. 不要忘记customized priority需要一个customized new Comparator<T>()
2. Given list 里面也可能有null node, 不要忘记查.



---

**43. [Multiply Strings.java](https://github.com/awangdev/LintCode/blob/master/Java/Multiply%20Strings.java)**      Level: Medium
      
想法不难。turn into int[], 然后每个位子乘积，然后余数carrier移位。

但是做起来有很多坑。适合面试黑。    

1. 数字‘123’， 在数组里面， index == 0 是 ‘1’。 但是我们平时习惯从最小位数开始乘积，就是末尾的'3'开始。
	所以！翻转两个数字先！我去。这个是个大坑。

2. 乘积product，和移动Carrier都很普通。

3. ！！最后不能忘了再翻转。

4. 最后一个看坑。要是乘积是0，就返回‘0’。 但是这个其实可以在开头catch到没必要做到结尾catch。

用到几个StringBuffer的好东西:   
reverse（）；    
sb.deleteCharAt(i)   

找数字，或者26个字母，都可以：    
s.charAt(i) - '0'; //数字    
s.charAt(i) - 'a'; //字母   



---

**44. [Next Permutation.java](https://github.com/awangdev/LintCode/blob/master/Java/Next%20Permutation.java)**      Level: Medium
      
需斟酌。

Permutation的规律:     
1. 从小的数字开始变化因为都是从小的数字开始recursive遍历。    
2. 正因为1的规律，所以找大的断点数字要从末尾开始： 确保swap过后的permutation依然是 前缀固定时 当下最小的。    

steps:    
1. 找到最后一个上升点，k      
2. 从后往前，找到第一个比k大的点, bigIndex      
3. swap k &&　bigIndex     
4. 最后反转 (k+1，end)      




---

**45. [Palindrome Permutation II.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Permutation%20II.java)**      Level: Medium
      
permutation的综合题：    
1. validate Input 是不是可以做palindromic permutation. 这个就是（Palindrome Permutation I）   
2. 顺便存一下permutation string的前半部分和中间的single character(if any)    
3. DFS 做unique permutation: given input有duplicate characters。       



---

**46. [Peeking Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Peeking%20Iterator.java)**      Level: Medium
      

再一次理解错题意. peek() 就是头顶，但是不一定是最大值啊。总是把PEEK想成了最大值，然后用2 STACK做了最大值的cache，练的一手好双stack，可惜错了。

回到原题，其实不难。找一个cache来存next()的值，然后每次next()里面维护这个cache就好。



---

**47. [Permutation Sequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Permutation%20Sequence.java)**      Level: Medium
      
k是permutation的一个数位。而permutation是有规律的。

也就是说，可以根据k的大小来判断每一个数位的字符（从最大数位开始，因为默认factorio从最大数位开始变化）。

于是先求出n!， 然后 k/n!就可以推算出当下这一个数位的字符。然后分别把factorio 和 k减小。

另外, 用一个boolean[] visited来确保每个数字只出现一次。

这个方法比计算出每个permutation要efficient许多。




---

**48. [Permutations.java](https://github.com/awangdev/LintCode/blob/master/Java/Permutations.java)**      Level: Medium
      
Recursive Backtracking: 取，或者不取.
Improvement: maintain list (add/remove elements) instead of 'list.contains'

Iterative: 用个queue，每次poll()出来的list, 把在nums里面能加的挨个加一遍。 However, code is a bit massive.




---

**49. [Rehashing.java](https://github.com/awangdev/LintCode/blob/master/Java/Rehashing.java)**      Level: Medium
      



---

**50. [Reverse Words in a String II.java](https://github.com/awangdev/LintCode/blob/master/Java/Reverse%20Words%20in%20a%20String%20II.java)**      Level: Medium
      
In-place reverse.

reverse用两回. 全局reverse。局部:遇到空格reverse。

注意：结尾点即使没有' '也要给reverse一下最后一个词。




---

**51. [Reverse Words in a String.java](https://github.com/awangdev/LintCode/blob/master/Java/Reverse%20Words%20in%20a%20String.java)**      Level: Medium
      
几种不同的方法flip：   
坑： 1. 结尾不能有空格。 2. 注意，如果Input是 ‘ ’的话，split以后就啥也没有了。check split以后 length == 0

另个题目Reverse Words in String (char[]) 可以in-place，因为条件说char[]里面是没有首尾空格,好做许多哟.



---

**52. [Rotate Image.java](https://github.com/awangdev/LintCode/blob/master/Java/Rotate%20Image.java)**      Level: Medium
      
找到个转角度的规律公式。用一个temp。in place.



---

**53. [Search Range in Binary Search Tree .java](https://github.com/awangdev/LintCode/blob/master/Java/Search%20Range%20in%20Binary%20Search%20Tree%20.java)**      Level: Medium
      

等于遍历了所有k1<= x <= k2的x node。

如果是用Binary Search Tree搜索，那么一般是if (...) else {...}，也就是一条路走到底，直到找到target.

这里, 把 left/right/match的情况全部cover了，然后把k1,k2的边框限制好，中间就全部遍历了。



---

**54. [Segment Tree Build II.java](https://github.com/awangdev/LintCode/blob/master/Java/Segment%20Tree%20Build%20II.java)**      Level: Medium
      

给的是Array。注意找区间内的max, assign给区间。   其余和普通的segment tree build一样   

给了array,但是并不根据array里的内容排位，而是依然根据index in [0, array.length - 1]割开区间，break到底，   
最终start==end。同时assign max=A[start] or A[end]

往上,parent一层的max:就是比较左右孩子,其实都是在两个sub-tree里面比较sub-tree的max。   

这就好做了：   
先分，找到left/right，比较max,在create current node,再append到当前node上面。

实际上是depth-first, 自底向上建立起的。



---

**55. [Segment Tree Build.java](https://github.com/awangdev/LintCode/blob/master/Java/Segment%20Tree%20Build.java)**      Level: Medium
      
按定义：   
左孩子：（A.left, (A.left+A.rigth)/2）   
右孩子：（(A.left+A.rigth)/2＋1， A.right）   



---

**56. [Segment Tree Modify.java](https://github.com/awangdev/LintCode/blob/master/Java/Segment%20Tree%20Modify.java)**      Level: Medium
      
Recursively 在segment tree里面找index, update it with value.   

每个iteration，很可能（要么左手，要么右手）max就变了。所以每次都left.max and right.max compare一下。   
最后轮回到头顶，头顶一下包括头顶，就全部都是max了。   

Divde and Conquer



---

**57. [Segment Tree Query II.java](https://github.com/awangdev/LintCode/blob/master/Java/Segment%20Tree%20Query%20II.java)**      Level: Medium
      
和 Segment Tree Query I 以及其他Segment Tree问题没啥区别。这个就是return个count。

这个题目考了validate input source：input 的start,end可能超出root[start,end]。   
那么第一步就要先clear一下。完全不在range就return 0. 有range重合就规整到root的range.





---

**58. [Segment Tree Query.java](https://github.com/awangdev/LintCode/blob/master/Java/Segment%20Tree%20Query.java)**      Level: Medium
      
给了segment Tree, node里面有Max value, 找[start,end]里面的max

[start,end]跟mid相比，可能：   
全在mid左   
全在mid右   
包含了mid： 这里要特别break into 2 query method   

按定义：   
mid = (root.start + root.end)/2



---

**59. [Strobogrammatic Number II.java](https://github.com/awangdev/LintCode/blob/master/Java/Strobogrammatic%20Number%20II.java)**      Level: Medium
      
耗了一点时间。本以为需要DP一下，把做过的n存一下。后来发现，其实就是剥皮，一层一层，是一个central-depth-first的，钻到底时候，return n=1,或者n=2的case，然后开始backtracking。
难的case先不handle.到底之后来一次O(n) scan.
总共的时间起码是O(n/2) + O(n), 所以还是O(n)


---

**60. [Subarray Sum Closest.java](https://github.com/awangdev/LintCode/blob/master/Java/Subarray%20Sum%20Closest.java)**      Level: Medium
      
?



---

**61. [Subset.java](https://github.com/awangdev/LintCode/blob/master/Java/Subset.java)**      Level: Medium
      
最基本的递归题目。   
坑：记得一开头sort一下 nums。 因为要升序。那么整体就是O(nlogn)

注意：用level/index来track到哪一步。最后一level就add into rst

方法1: subset的概念，取或者不取,backtracking. 当level/index到底，return 一个list.

方法2: 用for loop backtracking. 记得：每个dfs recursive call是一种独特可能，先加进rst。


recap:时间久了忘记dfs的两种路子. for loop dfs/backtracking vs. regular dfs



---

**62. [Subsets II.java](https://github.com/awangdev/LintCode/blob/master/Java/Subsets%20II.java)**      Level: Medium
      
递归：找准需要pass along的几个数据结构。    

和SubsetI类似，先sort input, 然后递归。但是input可能有duplicates. 

Using for loop approach: 每个dfs call是一种可能性，直接add into result.     
为了除去duplicated result, 如果在递归里面用rst.contains(),就是O(n), which makes overall O(n^2). 

这里有个基于sorted array的技巧：    
因为我们有mark index。 一旦for loop里面的i!=index，并且nums[i] == nums[i-1],说明x=nums[i-1]已经用过，不需要再用一次：     
[a,x1,x2]，x1==x2    
i == index -> [a,x1]    
i == index + 1 -> [a,x2]. 我们要skip这一种。

如果需要[a,x1,x2]怎么办？ 其实这一种在index变化时，会在不同的两个dfs call 里面涉及到。


Iterative: 写一写，用个Queue. Not recommended, Again, rst.contains() cost too much.



---

**63. [Top K Frequent Elements.java](https://github.com/awangdev/LintCode/blob/master/Java/Top%20K%20Frequent%20Elements.java)**      Level: Medium
      
题目有提醒: 不能用O(nLog(n)) 也就是说明要Log(n): 首先想到就是PriorityQueue, 并且不能queue.offer on the fly.
那么就先count, O(n); 再priorityQueue, Log(k), k是unique 数字的总量. 



---

**64. [Top K Frequent Words.java](https://github.com/awangdev/LintCode/blob/master/Java/Top%20K%20Frequent%20Words.java)**      Level: Medium
      
方法1：Brutle force用HashMap存frequency, 用ArrayList存lists of words。最后返回从尾部向前数的k个。   
   注意排序时Collection.sort()的cost是O(nLogk)

方法1-1: 还是用HashMap,但create一个Node class, 然后用PriorityQueue.   
PriorityQueue里面用到了 String.compareTo(another String).巧妙。

方法2: Trie && MinHeap屌炸天   
   http://www.geeksforgeeks.org/find-the-k-most-frequent-words-from-a-file/



---

**65. [Topological Sorting.java](https://github.com/awangdev/LintCode/blob/master/Java/Topological%20Sorting.java)**      Level: Medium
      
比较特别的BFS.

几个graph的condition：   
1. 可能有多个root
2. directed node, 可以direct backwards.

Steps:    
Track all neighbors/childrens. 把所有的children都存在map<label, count>里面
先把所有的root加一遍，可能多个root。并且全部加到queue里面。

然后以process queue, do BFS:   
Only when map.get(label) == 0, add into queue && rst.    
这用map track apperance, 确保在后面出现的node, 一定最后process.




---

**66. [Ugly Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Ugly%20Number.java)**      Level: Medium
      
方法1: PriorityQueue排序。用ArrayList check 新的ugly Number是否出现过。

方法1-1：(解释不通，不可取)用PriorityQueue排序。神奇的3，5，7走位：按照题目答案的出发，定了3，5，7以什么规律出现。但是题目并没有特殊表明。

方法2: DP . Not Done yet.




---

**67. [Unique Binary Search Tree II.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Binary%20Search%20Tree%20II.java)**      Level: Medium
      



---

**68. [Word Break.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Break.java)**      Level: Medium
      
DP

方法1:（attempt3 code）
state,rst[i]: 从[0～i] inclusive的string是否可以在dict中break开来找到？      
function: rst[i] = true if (rst[i - j] && set.contains(s.substring(i - j, i))); j in[0~i]     
1. rst[i - j] 记录的是[0, i-j]这一段是否可以break后在dict找到。     
2. 若true，再加上剩下所有[i-j, i]都能在dict找到，那么rst[i] = rst[0, i - j] && rst[i-j, i] == true

优化：找dict里面最长string, 限制j的增大。

(attempt4 code)    
与Word BreakII用同样的DP。
valid[i]: 记录从i到valid array末尾是否valid.



---

**69. [Word Ladder.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Ladder.java)**      Level: Medium
      
BFS Brutle: 在start string基础上，string的每个字母都遍历所有26个字母，换换。

方法2:    
用Trie。 理应更快. However implementation可能有点重复计算的地方，LeetCode timeout. 需要再做做。



---

**70. [Zigzag Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Zigzag%20Iterator.java)**      Level: Medium
      

这个题目相对简单. 做的时候我先考虑起来k条怎么办. 那么用个map把index和每个listmark一下就好了。
每次next(), 相应的list的头拿下来就好。
然后就跑圈呗，每次刷一个list头。不难。只要把几个variable维护清楚就行。


---

**71. [Encode and Decode TinyURL.java](https://github.com/awangdev/LintCode/blob/master/Java/Encode%20and%20Decode%20TinyURL.java)**      Level: Medium
      

其实想到了切入点, 是个可难可简单的题目. 这里的encode就是想办法把url存起来, 然后给个 key.
那么具体怎么做这个key, 简单就可以用一个map, 然后counting. 复杂一点就可以做random letter/number组成key.



---

**72. [Wiggle Sort.java](https://github.com/awangdev/LintCode/blob/master/Java/Wiggle%20Sort.java)**      Level: Medium
      

方法1:
排序, nLog(n). 然后把直线上坡变成层叠山峰, 需要每隔几个(题目中是每隔2位)就做个swap 造成高低不平.
Note: 每隔山峰之间是相互没有关系的, 所以每次只要操心 [i], [i-1]两个位置就好了.

方法2:
O(n)
看好奇数偶数位的规律, 然后根据题目给出的规律, 跑一遍, 每次只关注两个位置: 把不合适的[i], [i-1]调换位置就好了.

方法3:
跟法2一样, 只是更巧妙一点罢了:
第一遍想太多. 其实做一个fall-through就能把问题解决，原因是因为：
这样的fall-through每次在乎两个element，可以一口气搞定，无关乎再之前的elements。
特别的一点：flag来巧妙的掌控山峰和低谷的变化。又是神奇的一幕啊！
这样子的奇观，见过就要知道了，没见过的时候有点摸不着头脑。



---

**73. [Queue Reconstruction by Height.java](https://github.com/awangdev/LintCode/blob/master/Java/Queue%20Reconstruction%20by%20Height.java)**      Level: Medium
      

别无他法, 只能写一遍例子, 找规律,然后greedy. 
需要写一遍发现的规律比如: 从h大的开始排列, 先放入k小的. 写comparator的时候要注意正确性.
如果要sort, 并且灵活insert:用arrayList. 自己做一个object.
最后做那个'matchCount'的地方要思路清晰, 找到最正确的spot, 然后greedy insert.

O(n) space, O(nLog(n)) time, because of sorting.

可能有简化的余地, 代码有点太长.
比如试一试不用额外空间?



---

**74. [2 Sum II - Input array is sorted.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum%20II%20-%20Input%20array%20is%20sorted.java)**      Level: Medium
      

升序array, 找2SUM.

#### 方法1:
- 排序好的array. Two pointer移动start和end，核查sum.
- 注意sum用long.
- O(n) time

#### 方法2: Binary Search, 因为已经排好序了啊
- 定住一个valueA, 然后在剩下的里面 binary serach 找 (target - valueB)
- O(nLogN), 就不写了



---

**75. [2 Sum II.java](https://github.com/awangdev/LintCode/blob/master/Java/2%20Sum%20II.java)**      Level: Medium
      

与 2sum II - input array is sorted类似. 都是sort array, 然后two pointer.

LintCode的题. 注意找的是greater/bigger than target。

由于给定条件允许O(nLogn):   
   sort
   two pointer

while里面two pointer移动。每次如果num[left]+num[right] > target，那么其中所有num[left++]的加上num[right]都>target.   
也就是,num[right]不动，计算加入挪动left能有多少组，那就是: right-left这么多。 全部加到count上去。     
然后right--.换个right去和前面的left部分作比较。



---

**76. [Coin Change.java](https://github.com/awangdev/LintCode/blob/master/Java/Coin%20Change.java)**      Level: Medium
      

给一串不同数额的coins, 和total amount to spent. 求 最少 用多少个coin可以组合到这个amount. 每种coins个数不限量.

#### DP
- 找对方程dp[x], 积累到amount x最少用多少个coin: #coin是value, index是 [0~x].
- 子问题的关系是: 如果用了一个coin, 那么就应该是f[x - coinValue]那个位置的#coins + 1

##### initialization
- 处理边界, 一开始0index的时候, 用value0. 
- 中间利用Integer.MAX_VALUE来作比较, initialize dp[x]
- 注意, 一旦 Integer.MAX_VALUE + 1 就会变成负数. 这种情况会在coin=0的时候发生.

##### Optimization
- 方法1: 直接用Integer.MAX_VALUE
- 方法2: 用-1, 稍微简洁一点, 每次比较dp[i]和 dp[i - coin] + 1, 然后save. 不必要做多次min比较.

#### Memoization
- dp[i] 依然表示: min # of coints to make amount i
- initialize dp[i] = Integer.MAX_VALUE
- 先选最后一步(遍历coins),  然后dfs做同样的操作
- 记录dp[amount] 如果已经给过value, 不要重复计算, 直接return.
- 但是这道题没必要强行做memoization, 普通DP的状态和方程相对来说很好找到



---

**77. [Maximum Product Subarray.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Product%20Subarray.java)**      Level: Medium
      

从一组数列(正负都有)里面找一串连续的子序列, 而达到乘积product最大值.

#### DP
- 求最值, 想到DP. Time/Space O (n)
- 两个特别处: 
- 1. 正负数情况, 需要用两个DP array. 
- 2. continuous prodct 这个条件决定了在Math.min, Math.max的时候, 
- 是跟nums[x]当下值比较的, 如果当下值更适合, 会舍去之前的continous product, 然后重新开始.
- 这也就注定了需要一个global variable 来hold result.

#### Space optimization, rolling array
- maxProduct && minProduct 里面的 index i, 都只能 i - 1相关, 所以可以省去redundant operatoins
- Time: O(n), space: O(1)



---

**78. [3 Sum Closest.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum%20Closest.java)**      Level: Medium
      

3Sum 的一种简单形式, 并且都没有找index, value, 而只是找个sum罢了.

double for loop。 2Sum只能用土办法 left/right 2 pointers。 O(n^2)

注意：check closest时候用long, 以免int不够用



---

**79. [Triangle Count.java](https://github.com/awangdev/LintCode/blob/master/Java/Triangle%20Count.java)**      Level: Medium
      

其实也就是3sum的变形, 或者而说2sum的变形. 主要用2 pointers来做.
注意, 在选index时候每次定好一个 [0 ~ i], 在这里面找点start, end, 然后i 来组成triangle.
Note巧妙点:
在此之中, 如果一种start/end/i 符合, 那么从这个[start~end]中, 大于start的都可以, 所以我们count+= end-start.
反而言之, <end的其他index, 就不一定能符合nums[start] + nums[end] > nums[i]



---

**80. [3 Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum.java)**      Level: Medium
      

方法1:
sort array, for loop + two pointer. O(n)
处理duplicate wthin triplets: 
如果最外圈的移动点i重复, 一直顺到结尾的最后一个再用.
如果是triplet内有重复, 用完start point, 移动到结尾.

Previous notes:
注意:   
   1. 找 value triplets, 多个结果。注意，并非找index。    
   2. 要升序, 第一层for loop 从最后一个元素挑起, 保证了顺序。    
   3. 去掉duplicate: check用过的同样的数字，都跳掉。不需要用同样的数字再计算一边已有结果。

步骤:   
   1. For loop 挑个数字A.    
   2. 2Sum 出一堆2个数字的结果    
   3. Cross match 步骤1里面的A.   

时间 O(n^2), 两个nested loop

另外, 还是可以用HashMap来做2Sum。稍微短点。还是要注意handle duplicates.




---

**81. [4 Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/4%20Sum.java)**      Level: Medium
      

方法1：  
   1. 利用2Sum的原理，把4Sum分为连个2Sum。左一个pair,右一个pair，每个pair里面放2个数字。   
   2. 以一个点，i，作为分界口，也要列举出所有i之前的pair,作为基础。   
   3. 再尝试从所有i+1后面,找合适的2nd pair。   
 
   可以用HashSet<List>, 可以直接比较list里面每一个元素, 保证set不重复.
   Previous Notes: 在造class Pair时候，要做@override的function: hashCode(), equals(Object d). 平时不太想得起来用。
   参见 http://lifexplorer.me/leetcode-3sum-4sum-and-k-sum/    

方法2： 3Sum外面再加一层. 参考3Sum. 时间O(n^3)。 但此方法在k-sum时候，无疑过于费时间. O(n^k)



---

**82. [Longest Increasing Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Increasing%20Subsequence.java)**      Level: Medium
      

无序数组, 找最长的上升(不需要连续)数组 的长度. 先做O(n^2), 然后可否O(nLogN)?

#### DP, double for loop, O(n^2)
- 考虑nums[i]结尾的时候, 在[0, i) 里count有多少小于nums[i]
- 对于所有 i in [0, n), 最常的increasing序列有多少length?
- max需要在全局维护: nums是无序的, nums[i]也可能是一个很小的值, 所以末尾dp[i]并不是全局的max, 而只是对于nums[i]的max.
- 正因此, 每个nums[i]都要和每个nums[j] 作比较, j < i.
- dp[i] = Maht.max(dp[i], dp[j] + 1); j = [0 , i - 1]
- 时间复杂度  O(n^2)


#### O(nLogN)
- 维持一个list of increasing sequence
- 这个list其实是一个base-line, 记录着最低的increasing sequence.
- 当我们go through all nums的时候, 如果刚好都是上升, 直接append
- 如果不上升, 应该去list里面, 找到最小的那个刚好大于new num的数字, 把它换成num
- 这样就完成了baseline. 举个例子, 比如替换的刚好是在list最后一个element, 等于就是把peak下降了, 那么后面其他的数字就可能继续上升.
- '维护baseline就是一个递增的数列' 的证明, 还没有仔细想.



---

**83. [Unique Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Binary%20Search%20Tree.java)**      Level: Medium
      

Not quite clear.
根据左右分割而总结出了原理, 每次分割, 左右两边都会有一定数量的permutation, 总体上的情况数量当然是相乘.
然后每一个不同的分割点都加一遍:
f(n) = f(0)*f(n-1) + f(1)*f(n-2) + ... + f(n-2)*f(1) + f(n-1)*f(0)

然后把数学公式转换成DP的方程, 有点玄学的意思啊! 不好想.



---

**84. [Unique Paths II.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Paths%20II.java)**      Level: Medium
      

跟unique path的grid一样, 目标走到右下角, 但是grid里面可能有obstacle, 不能跨越. 求unique path 的count.

#### 坐标DP
- dp[i][j]: # of paths to reach grid[i][j]
- dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
- 考虑最终结尾需要的状态:如何组成,写出公式.
- 公式中注意处理能跳掉的block, marked as 1. '到不了', 即为 0 path in dp[i][j].



---

**85. [Bomb Enemy.java](https://github.com/awangdev/LintCode/blob/master/Java/Bomb%20Enemy.java)**      Level: Medium
      

2D grid, 每个格子里面可能是 'W' wall, 'E' enemy, 或者是 '0' empty.

一个bomb可以往4个方向炸. 求在grid上面, 最大能炸掉多少个敌人.

#### Corrdinate DP
- Space, Time: O(MN)
- dp[i][j] 就是(i, j)上最多能炸掉的enemy数量
- dp[i][j] 需要从4个方向加起来, 也就是4个方向都要走一遍, 所以分割成 UP/Down/Left/Right 4个 int[][]
- 最后一步的时候求max
- 分方向考虑的方法很容易想到,但是四个方向移动的代码比较繁琐.
- 往上炸: 要从顶向下考虑
- 往下炸: 要从下向上考虑
- 熟练写2D array index 的变换.

似乎还有一个更简洁的方法, 用col count array: http://www.cnblogs.com/grandyang/p/5599289.html



---

**86. [3 Sum Smaller.java](https://github.com/awangdev/LintCode/blob/master/Java/3%20Sum%20Smaller.java)**      Level: Medium
      

一般的O(n3)肯定不行。在此基础上优化。
发现j,k满足条件时候，(k - j)就是所有 sum <target的情况了。
而一旦>target, 又因为j不能后退，只能k--，那么问题就被锁定了. 这样可以做到O(n2)



---

**87. [Update Bits.java](https://github.com/awangdev/LintCode/blob/master/Java/Update%20Bits.java)**      Level: Medium
      

熟悉bits的一些trick:
- ~0 = -1 = 111111...11111111 (32-bit)
- Create mask by shifting right >>>, and shifting left
- Reverse to get 0000...11110000 format mask
- & 0000 = clean up; | ABC = assign ABC



---

**88. [Maximum XOR of Two Numbers in an Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20XOR%20of%20Two%20Numbers%20in%20an%20Array.java)**      Level: Medium
      

比较难想到. 利用到XOR性质A^B=C, then A=B^C.
1. 枚举可能的A, 2. 然后一个个猜.

1. 枚举A: 因为求MAX肯定是找leading-1最多的数字, 那么枚举A从(1000000...000)开始, 
每次多一位取1或者0
2. 因为枚举A的时候是按照每个bit来, 那么B和C也要以同样数位出现.
这里吧B和C变成了prefix的形式, 放在了set里面. 
跟2sum用hashmap的思想类似, 每次用枚举的 A^B=C, 看看结果C是否已经在set里面. 
如果在, 证明枚举的A可能被B^C得出, 那么就找到了一种情况.

还用到一些技巧: 
mask = (1 << i); // i位mask
mask = mask | (1 << i); // prefix mask



---

**89. [Perfect Squares.java](https://github.com/awangdev/LintCode/blob/master/Java/Perfect%20Squares.java)**      Level: Medium
      

给一个数字n, 找到这个数字 最少能用多少个 平方数组成. 

平方数比如: 1, 4, 9, 16 ... etc

#### Partition DP
- 遇到最值, 想到DP.
- 看到分割字眼, 想到分割型 DP. 
- 思考, 如果 j * j = 9, 那么 j = 3 就是最少的一步; 但是如果是10呢? 就会分割成1 + 9 = 1 + j * j 
- 考虑最后的数字: 要是12割个1出来, 剩下11怎么考虑? 割个4出来,剩下8怎么考虑?
- partion的方式: 在考虑dp[i - x]的时候,  x 不是1, 而是 x = j*j.
- 就变成了dp = Min{dp[i - j^2] + 1}

#### 时间复杂度
- 乍一看是O(n*sqrt(n)). 实际也是. 但如何推导?
- 考虑上限: 把小的数字变成大的 推导上限; 考虑下限: 把数字整合归小, 找到下限.
- 考虑sqrt(1) + sqrt(2) + ....sqrt(n):找这个的upper bound and lower bound.
- 最后发现它的两边是 A*n*sqrt(n) <= actual time complexity <= B*n*sqrt(n)
- 那么就是O(n*sqrt(n))啦

#### Previous Notes
- 一开始没clue.看了一下提示
- １.　第一步想到了，从数学角度，可能是从最大的perfect square number开始算起。
- ２.　然后想法到了dp， 假设最后一步用了最大的maxSqrNum, 那么就在剩下的 dp[i - maxSqrNum^2] +１　不就好了？
- ３.　做了，发现有个问题．．．最后一步选不选maxSqrNum?  比如12就是个例子。
- 然后就根据提示，想到BFS。顺的。 把1～maxSqrNum 都试一试。找个最小的。
- 看我把12拆分的那个example. 那很形象的就是BFS了。
- 面试时候，如果拆分到这个阶段不确定，那跟面试官陶瓷一下，说不定也就提示BFS了。



---

**90. [Backpack VI.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20VI.java)**      Level: Medium
      

给一个数组nums, 全正数, 无重复数字; 找: # of 拼出m的方法.

nums 里的数字, 可以重复使用. 不同的order可以算作不同的拼法.

#### Backpack DP
- dp[i] 表示: # of ways to fill weight i
- 1维: dp[w]: fill weigth w 有多少种方法. 前面有多少种可能性, 就sum多少个:
- dp[w] = sum{dp[w - nums[i]]}, i = 0~n

##### 分析
- 拼背包时, 可以有重复item, 所以考虑'最后被放入的哪个unique item' 就没有意义了.
- 背包问题, 永远和weight分不开关系.
- 这里很像coin chagne: 考虑最后被放入的东西的value/weigth, 而不考虑是哪个.






---

**91. [Longest Palindromic Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Palindromic%20Subsequence.java)**      Level: Medium
      

#### Interval DP
- 用[i][j]表示区间的首尾
- 考虑3个情况: 砍头, 砍尾, 砍头并砍尾 (考虑首尾关系)
- Iteration一定是以i ~ j 之间的len来看的. 
- len = j - i + 1; 那么反推, 如果len已知, j = len + i -1;
- 注意考虑len == 1, len == 2是的特殊情况.

#### Memoization
- 同样的方式model dp[i][j]: range [i, j] 之间的  max palindromic length
- 三种情况: 
- 1. 首尾match 继而 dfs[i+1, j-1]
- 2. 首尾不match,dfs[i+1,j] 
- 3. 首尾不match,dfs[i,j-1] 
- 注意: init dp[i][j]=-1, dfs的时候查dp[i][j] 是否算过



---

**92. [Binary Search Tree Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Search%20Tree%20Iterator.java)**      Level: Medium
      

画一下, BST in order traversal. 用stack记录最小值, 放在top. O(h) space.
每次消耗TreeNode, 都看看rightNode(其实就是下一个最小的candidate), 并且一条龙stack叠上rightNode所有的left子孙.

Previous Notes:
用O(h)空间的做法：

理解binary search tree inorder traversal的规律：
   先找left.left.left ....left 到底，这里是加进stack.
   然后考虑parent,然后再right.

例如这题：
   stack里面top，也就是tree最左下角的node先考虑,取名rst.
   其实这个rst拿出来以后, 它也同时是最底层left null的parent，算考虑过了最底层的parent。
   最后就考虑最底层的parent.right, 也就是rst.right.

注意:
   next()其实有个while loop, 很可能是O(h).题目要求average O(1),所以也是okay的.


用O(1)空间的做法：不存stack, 时刻update current为最小值。

找下一个最小值,如果current有right child：   
   和用stack时的iteration类似,那么再找一遍current.right的left-most child,就是最小值了。
   
如果current没有right child:    
    那么就要找current node的右上parent, search in BinarySearchTree from root.

注意：
   一定要确保找到的parent满足parent.left == current.
   反而言之，如果current是parent的 right child, 那么下一轮就会重新process parent。
   但是有错:binary search tree里面parent是小于right child的，也就是在之前一步肯定visit过，如此便会死循环。




---

**93. [Flatten Nested List Iterator.java](https://github.com/awangdev/LintCode/blob/master/Java/Flatten%20Nested%20List%20Iterator.java)**      Level: Medium
      

方法1: 用queue, 把需要的item全部打出来
方法2: 用stack, 把需要的item先存一行, 每次打开子序列时候, 全部加回stack.



---

**94. [Best Time to Buy and Sell Stock with Cooldown.java](https://github.com/awangdev/LintCode/blob/master/Java/Best%20Time%20to%20Buy%20and%20Sell%20Stock%20with%20Cooldown.java)**      Level: Medium
      

Sequence DP
跟StockIII很像. 分析好HaveStock && NoStock的状态, 然后看最后一步.



---

**95. [Find Peak Element.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Peak%20Element.java)**      Level: Medium
      

binary search. 
Goal: find peak, where both sides are descending
最左边, 最右边是Integer.MIN_VALUE时候, 也能构成中间数mid是peak的条件.

Note:
没有必要特别check (mid-1)<0或者(mid+1)>=n.
证明:
1. 最左端: 当start=0, end = 2 => mid = 1, mid-1 = 0;
2. 最右端: 当end = n - 1, start = n - 3; mid = (start+end)/2 = n - 2; 
那么mid + 1 = n - 2 + 1 = n - 1 < n 是理所当然的



---

**96. [Longest Common Subsequence.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Common%20Subsequence.java)**      Level: Medium
      

给两个string, A, B. 找这两个string里面的LCS: 最长公共字符长度 (不需要是continuous substring)

#### Double Sequence DP
- 设定dp长度为(n+1), 因为dp[i]要用来表示前i个(ith)时候的状态, 所以长度需要时i+1才可以在i位置, hold住i.
- 双序列: 两个sequence之间的关系, 都是从末尾字符看起, 分析2种情况:
- 1. A最后字符不在common sequence 或者 B最后字符不在common sequence.
- 2. A/B最后字符都在common sequence. 总体count + 1.



---

**97. [Letter Combinations of a Phone Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Letter%20Combinations%20of%20a%20Phone%20Number.java)**      Level: Medium
      

方法1: Iterative with BFS using queue.

方法2: Recursively adding chars per digit



---

**98. [Pow(x,n).java](https://github.com/awangdev/LintCode/blob/master/Java/Pow(x,n).java)**      Level: Medium
      

傻做就O(n), 要更好就考虑O(logN).
减少重复计算, 一切两半.

注意:
- n/2的奇数偶数
- n的正负
- n == 0的情况, x == 0, x == 1 的情况.


---

**99. [Construct Binary Tree from Inorder and Preorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Construct%20Binary%20Tree%20from%20Inorder%20and%20Preorder%20Traversal.java)**      Level: Medium
      

和Construct from Inorder && Postorder 想法一样。

写出Preorder和Inorder的字母例子，发现Preorder的开头总是这Level的root。依此写helper,注意处理index。



---

**100. [Add Two Numbers.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20Two%20Numbers.java)**      Level: Medium
      

LinkedList都已经反转好了，直接做.
遍历两个l1,l2把carry-on处理好，每次生成一个新node，最后检查carry-on.

跟Add Binary的理解方式一模一样.

注意:
Linked List 没有天然size.
用DummyNode(-1).next来hold住结果.




---

**101. [Add Two Numbers II.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20Two%20Numbers%20II.java)**      Level: Medium
      

Singly-linked list需要reverse, 用stack.
最终结果要恢复成input list 那样的sequence方向, 用stack一个个pop()刚好就可以做到.

加法都一样:
   1. sum = carry
   2. carry = sum / 10
   3. sum = sum % 10;



---

**102. [Balanced Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Balanced%20Binary%20Tree.java)**      Level: Medium
      

1. DFS using depth marker: 每个depth都存一下。然后如果有不符合条件的，存为-1.
   一旦有 <0 或者差值大于1， 就全部返回Integer.MIN_VALUE. Integer.MIN_VALUE比较极端, 确保结果的正确性。
   最后比较返回结果是不是<0. 是<0，那就false.
   Traverse 整个tree, O(n)

2. Only calculate depth using maxDepth function. Same concept as in 1, but cost more traversal efforts.



---

**103. [Populating Next Right Pointers in Each Node.java](https://github.com/awangdev/LintCode/blob/master/Java/Populating%20Next%20Right%20Pointers%20in%20Each%20Node.java)**      Level: Medium
      

方法1：   
题目要求DFS. 想清楚了如何在DFS level把几种情况都考虑了, 写起来很简单.
其实basic implementation, 每次处理next链接:
1. node.left.next = node.right
2. If node.next != null, link node.right.next = node.next.left;

方法2:   
不和题意，用了queue space，与Input成正比。太大。

BFS over Tree。 用Queue 和 queue.size()，老规矩。   
process每层queue时, 注意把next pointer加上去就好. 



---

**104. [Validate Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Validate%20Binary%20Search%20Tree.java)**      Level: Medium
      

查看每个parent-child关系。同时把root level上面传下来max,min界限定住。

Note: min/max需要时long type. 
如果题目真的给node.val = Integer.MAX_VALUE, 我们需要能够与之比较, long就可以.



---

**105. [Convert Sorted List to Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Sorted%20List%20to%20Binary%20Search%20Tree.java)**      Level: Medium
      

Divide and Conquer   
找到mid node

方法1:
用长度来定位mid, 每次找中间点做root, 然后前半段, 后半段分别dfs with length.

方法2: 用快慢pointer
Better: 不用traverse entire linked list

slowPointer = node;
fastPointer = node.next;

然后把root = mid.next     

然后开始sortedListToBST(mid.next.next); //后半段    
mid.next = null;//非常重要，要把后面拍过序的断掉    
sortedListToBST(head); //从头开始的前半段     

最后root.left, root.right merge一下。   



---

**106. [Flatten Binary Tree to Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Flatten%20Binary%20Tree%20to%20Linked%20List.java)**      Level: Medium
      

分析题意后, 按照题意: Flatten it with in-place order
1. reserve right child
2. DFS flatten部分
3. 移花接木
4. flatten 剩下的.



---

**107. [Minimum Size Subarray Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Size%20Subarray%20Sum.java)**      Level: Medium
      

方法1:
2 pointer, O(n). 找subarray, start 或 end pointer，每次一格这样移动.

好的策略: 
1. 先找一个solution, 定住end. 
2. 然后移动start; 记录每个solution if occurs
3. 然后再移动end，往下找。

Note: 虽然一眼看上去是nested loop.但是分析后，发现其实就是按照end pointer移动的Loop。start每次移动一格。总体上，还是O(n)

方法2:
Double for loop, base i 每次只+1, 所以最后O(n^2)

方法3:
Binary Search, O(nLogN)
Not done yet



---

**108. [Clone Graph.java](https://github.com/awangdev/LintCode/blob/master/Java/Clone%20Graph.java)**      Level: Medium
      

给一个graph node, 每个node有list of neighbors. 复制整个graph, return new head node.

思想:
- Use HashMap to mark cloned nodes.    
- 先能复制多少Node复制多少. 然后把neighbor 加上

#### DFS
- copy the node
- Mark 'added' using map(old, new)
- for loop on the each one of the neighbors: map copy, record in map, and further dfs
- once dfs completes, add newNeighbor as neighbor of the new node (get to it via map)
- 主要思想是: 一旦复制过了, 不必要重新复制

#### BFS
_ Copy the root node, then copy all the neighbors. 
_ Mark copied node in map.
_ Use queue to contain the newly added neighbors. Need to work on them in the future.

#### Note
initialize map with (node, newNode)



---

**109. [Longest Substring Without Repeating Characters.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Substring%20Without%20Repeating%20Characters.java)**      Level: Medium
      

方法1:
Two Pointers
双指针: 从start开始遍历, 但是第一步是while loop来推进end; 直到推不动end, 然后start++
巧妙点: 因为end是外围variable, 在start的loop上, end不会重置;[star ~ end] 中间不需要重复计算.
最终可以O(n);

Previous verison of two pointers:
用两个pointer, head和i.
注意：head很可能被退回到很早的地方，比如abbbbbba,当遇到第二个a，head竟然变成了 head = 0+1 = 1.      
当然这是不对的，所以head要确保一直增长，不回溯

方法2:
   HashMap<Char, Integer>: <character, last occurance index>
   一旦有重复, rest map.
   没有重复时候, 不断map.put(), 然后求max值

问题: 每次reset map之后就开始从新从一个最早的index计算, 最坏情况是O(n^2):
'abcdef....xyza'




---

**110. [Remove Nth Node From End of List.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Nth%20Node%20From%20End%20of%20List.java)**      Level: Medium
      

O(n), one pace, no extra space
找到窗口, 然后平移, 最后pre 和 head之间 skip一个node就好.



---

**111. [Longest Substring with At Most K Distinct Characters.java](https://github.com/awangdev/LintCode/blob/master/Java/Longest%20Substring%20with%20At%20Most%20K%20Distinct%20Characters.java)**      Level: Medium
      

大清洗 O(nk)   
map.size一旦>k，要把longest string最开头（marked by pointer:start）的那个char抹掉    
一旦某一个char要被清除，所以在这个char 的1st and last appearance之间的char都要被清洗from map




---

**112. [Linked List Cycle II.java](https://github.com/awangdev/LintCode/blob/master/Java/Linked%20List%20Cycle%20II.java)**      Level: Medium
      

方法1:
快慢指针, O(1)space.

确认有cycle后, 其实是数学问题:
当head == slow.next时候， head就是cycle starting point.
也就是说，当slow 移动到了那个回溯点，slow.next那个点就刚好是head的那个点...

证明:
1. 假设慢指针走t步, 快指针走快一倍, 也就是2t.
2. 我们假设cycle的长度是Y, 而进入cycle之前的长度为X.
3. 假设慢指针走了m圈cycle, 而快指针走了n圈cycle之后, 两个pointer相遇.
4. 最终在Y cycle里面的K点相遇, 也就是两个指针都在这最后一圈里面走了K 步.
=> 
那么:
t = X + mY + K
2t = X + nY + K
整合公式:
X + K = (n - 2m)Y
这里的m和n不过是整数的跑圈数, 也就是说X和K加在一起, 总归是结束cycle. X 和 K 互补
=> 结论: 当slow/fast 指针在K点相遇后, 再走X步, 就到了cycle的起点, 也就是题目要求的起点.

方法2:
HashMap, O(n) space


---

**113. [Kth Smallest Number in Sorted Matrix.java](https://github.com/awangdev/LintCode/blob/master/Java/Kth%20Smallest%20Number%20in%20Sorted%20Matrix.java)**      Level: Medium
      

方法1:
和Merge K sorted Array/ List 类似：使用PriorityQueue。

因为Array的element无法直接找到next,所以用一个class Node 存value, x,y positions.

方法2:
Binary Search
https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/discuss/85182/my-solution-using-binary-search-in-c


变型: Kth Largest in N Arrays


---

**114. [Find Minimum in Rotated Sorted Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20Minimum%20in%20Rotated%20Sorted%20Array.java)**      Level: Medium
      

画图, 最小值被rotate之后, 变成array中间的最低谷.
并且, 左边山坡的最小值, 大于右边山坡的最大值. 
以此来给binary search做判断.

O(nlogn)



---

**115. [Connecting Graph.java](https://github.com/awangdev/LintCode/blob/master/Java/Connecting%20Graph.java)**      Level: Medium
      

没有跑过这个程序, 是一个UnionFind的简单实现.
Document了每个环节的计算原理/思想.



---

**116. [Connecting Graph II.java](https://github.com/awangdev/LintCode/blob/master/Java/Connecting%20Graph%20II.java)**      Level: Medium
      

Lint还不能跑, 全部按照题意和答案document的.



---

**117. [Connecting Graph III.java](https://github.com/awangdev/LintCode/blob/master/Java/Connecting%20Graph%20III.java)**      Level: Medium
      

还是UnionFind的变形, 这次是算有剩下多少个union. 其实非常简单, 维持一个全局变量count:
一开始count=n, 因为全是散装elements;  每次union, count--.



---

**118. [Number of Islands.java](https://github.com/awangdev/LintCode/blob/master/Java/Number%20of%20Islands.java)**      Level: Medium
      

方法1: 两个for loop brutle force。 DFS把每个跟1相关的都Mark一遍.生成一个island.

方法2:
可以用union-find， 就像Number of island II 一样。
只不过这个不Return list, 而只是# of islands
记住UnionFind的模板和几个变化(Connecting Graph I, II, III), 最后归总的代码写起来就比较简单.



---

**119. [Graph Valid Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Graph%20Valid%20Tree.java)**      Level: Medium
      

复习Union-Find的另外一个种形式。   
题目类型：查找2个元素是不是在一个set里面。如果不在，false. 如果在，那就合并成一个set,共享parent.   
存储的关键都是：元素相对的index上存着他的root parent.    

注意: 结尾要检查, 是否只剩下1个union. Tree必须连接到所有给出的node.

另一个union-find， 用hashmap的：http://www.lintcode.com/en/problem/find-the-weak-connected-component-in-the-directed-graph/




---

**120. [Implement Trie.java](https://github.com/awangdev/LintCode/blob/master/Java/Implement%20Trie.java)**      Level: Medium
      

Tire, 也即是 Prefix Tree. 

HashMap构建Trie。 Trie三个Method:　   
1. Inset: 加 word   
2. Search: 找word    
3. StartWith: 找prefix    

只有两条children的是binary tree. 那么多个children就是Trie。 那么没有left/right pointer怎么找孩子？   
用HashMap，以child的label为Key，value就是child node。 HashMap走位   

Note:    
node里的char在这是optional. 只要在每个TrieNode里面用map存储向下分布的children就好了.  
另外有种题目，比如是跟其他种类的search相关，在结尾要return whole string，就可以在node里存一个up-to-this-point的String。





---

**121. [Add and Search Word.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20and%20Search%20Word.java)**      Level: Medium
      

Trie结构, prefix tree的变形： '.'可以代替任何字符，那么就要iterate这个node所有的children.

节点里面有char, isEnd, HashMap<Character, TrieNode>   
Build trie = Insert word:没node就加，有node就移动。   
Search word:没有node就报错. 到结尾return true   

这题因为'.'可以代替任何possible的字符，没一种都是一个新的path，所以recursive做比较好些。    
(iterative就要queue了,麻烦点)



---

**122. [Word Search.java](https://github.com/awangdev/LintCode/blob/master/Java/Word%20Search.java)**      Level: Medium
      

Backtracking:
找到开头的字母, 然后recursively DFS 去把word串到底:
每到一个字母, 朝四个方向走, 之中一个true就可以.

Note:每次到一个字母，mark一下'#'. 4个path recurse回来后，mark it back.

Backtracking方法2:    
用一个boolean visited[][]





---

**123. [Expression Expand.java](https://github.com/awangdev/LintCode/blob/master/Java/Expression%20Expand.java)**      Level: Medium
      


#### DFS
- 与Stack时需要考虑的一些function类似. 特别之处: **检查[ ]的结尾**
- 因为DFS时候, 括号里的substring会被保留着进入下一个level, 所以我们在base level要keep track of substring.
- 用int paren 来track 括号的开合, 当paren再次==0的时候 找到closure ']'

#### Stack
- Stack存 [ ] 里面的内容, detect 括号开头结尾: 结尾时process inner string
- 有很多需要注意的细节才能做对:
- Stack<Object> 也可以用, 每个地方要注意 cast. 存进去的需要是Object: String, Integer
- 几个 type check: instanceof String, Character.isDigit(x), Integer.valueOf(int num)
- 出结果时候, 不能轻易 sb.reverse().toString(): sb.reverse() 翻转了整个连在一起的string, 错.
- 用另一个Stack<String>作为buffer, 先把stack里面的内容倒出来 (pure), 但是每个item里面顺序不变.
- 最后再从buffer里面倒进StringBuffer.




---

**124. [Maximum Binary Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximum%20Binary%20Tree.java)**      Level: Medium
      

给一串数字, 做一个 maximum binary tree: 最顶上的root最大; 左child也是一个max tree, 右child也必须是max tree.

#### Monotonous Stack
- 用到bottom->top递减的stack: 最底下的root维持成最大的element.
- 过程当中, 一旦遇到currNode.val > stack.peek(), 就意味着需要把这个currNode放在 stack的底层位置.
- 也就是说, 遇到这个条件, process, pop()所有 currNode.val > stack.peek(), 最后把currNode加进去.

- maxTree题目本身的要求是: 大的在最中间, 左右两边的subTree也要是maxTree:
- Monotonous Stack在这里帮助 keep/track of max value, 但是left/right tree的logic是MaxTree独有的.
- left/right node的assignment是根据题目要求: 中间最大值分开后, 左边的是左边subTree, 右边的作为右边subTree.

#### Previous notes
- Should memorize MaxTree. 依次类推，会做Min-Tree, Expression Tree
- Stack里，最大的值在下面。利用此性质，有这样几个step:

##### Step1
- 把所有小于curr node的，全Pop出来, while loop, keep it going.    
- 最后pop出的这个小于Curr的node：它同时也是stack里面pop出来小于curr的最大的一个，最接近curr大小。（因为这个stack最大值靠下面）    
- 把这个最大的小于curr的node放在curr.left.    

##### Step2   
- 那么，接下去stack里面的一定是大于curr：   
- 那就变成curr的left parent. set stack.peek().right = curr.

##### Step3   
- 结尾：stack底部一定是最大的那个，也就是max tree的头。





---

**125. [Swap Nodes in Pairs.java](https://github.com/awangdev/LintCode/blob/master/Java/Swap%20Nodes%20in%20Pairs.java)**      Level: Medium
      

#### enumurate 
基本原理, 写出来, 然后连线:
pre -> A -> B -> C -> ...
需要一个虚拟 preNode做起始node, 不然无法把后面的node换到开头.

#### 注意
用dummy = pre作为head前一格.
用 `pre.next == null && pre.next.next` 来check是否为NULL.
pre.next.next 保证了至少有一次swap.



---

**126. [Wood Cut.java](https://github.com/awangdev/LintCode/blob/master/Java/Wood%20Cut.java)**      Level: Medium
      

二分的思想: 判断的是一个 validate() function, 而不是简单的'=='

不需要sort! 为什么呢? 因为我们不是在given array上面二分, 我们是根据最大值在[0, max]上二分.

Overall time: O(nLogM), where M = largest wood length



---

**127. [Find the Duplicate Number.java](https://github.com/awangdev/LintCode/blob/master/Java/Find%20the%20Duplicate%20Number.java)**      Level: Medium
      

- 注意不要思维定式: 以为mid是index
- 这里mid其实是binary search on value [1, n] 的一个value.
- 再次用到validate() function

Time: O(nLogN)



---

**128. [Game of Life.java](https://github.com/awangdev/LintCode/blob/master/Java/Game%20of%20Life.java)**      Level: Medium
      

#### basic
- 简单的implementation, 把count function写清楚就好.
- time: O(mn), extra space: O(mn)
- 注意结尾要一个个board[i][j]copy

#### follow up
unlimited border? 可能需要分割board. 用大框分割, 每次换行的时候, 重复计算2行就好了. see details below.

#### improvement: do it in place!
- time: O(mn), extra space: O(1)
- bit manipulation: 用第二个bit来存previous value.
- 因为我们只考虑 0 和 1 而已, 所以可以这样取巧. 但是并不scalable.
- 如果需要存multiple state, 可能需要移动更多位, 或者用一个 state map
- 注意 bit manipulation 的细节: <<1, >>1, 还有 mast的用法: |, & 




---

**129. [Number of Airplane in the sky.java](https://github.com/awangdev/LintCode/blob/master/Java/Number%20of%20Airplane%20in%20the%20sky.java)**      Level: Medium
      

#### Sweep Line
- 把Interval拆分成数轴上的Point 
- 起飞mark 1   
- 降落mark -1     
- 用PriorityQueue排序， loop through queue, 计算(起飞+降落)值可能有的max。

#### 注意
- 同时起飞和降落，就是 1 - 1 = 0. 所以在while loop里面有第二个while loop，    
- 当坐标x重合时，在这里做完所有x点的加减，然后再比较 max。     
- 这避免了错误多count，或者少count



---

**130. [Meeting Rooms II.java](https://github.com/awangdev/LintCode/blob/master/Java/Meeting%20Rooms%20II.java)**      Level: Medium
      

给一串数字pair, 代表会议的开始/结束时间. 找同时又多少个会议发生(需要多少件房间)

#### 方法1
- PriorityQueue + 一个Class来解决.Ｏ(nlogn)
- 跟 Number of Airpline in the sky是同一道题

#### 方法2: 尝试了一下用一个sorted Array + HashMap
也还行，但是handle edge的时候,HashMap 要小心，因为相同时间start和end的map key 就会重复了。



---

**131. [Unique Path.java](https://github.com/awangdev/LintCode/blob/master/Java/Unique%20Path.java)**      Level: Medium
      

2D array, 算走到最右下角，有多少种方式.

##### DP
- 计数DP.注意方程式前两位置加在一起: 前两种情况没有overlap, 也不会缺情况.
- 注意initialization, 归1.
- 需要initialize的原因是,也是一个reminder: 在方程中会出现-1index
- Of course, row i = 0, or col j = 0, there is only 1 way to access
- time O(mn), space O(mn)

##### 滚动数组
- [i] 只跟 [i - 1] 有关系, 用 curr/prev 建立滚动数组.
- space O(n) 优化空间




---

**132. [Maximal Square.java](https://github.com/awangdev/LintCode/blob/master/Java/Maximal%20Square.java)**      Level: Medium
      

只能往右边,下面走, 找面积最大的 square. 也就是找到变最长的 square.

#### DP
- 正方形, 需要每条边都是一样长度.
- 以右下角为考虑点, 必须满足条件: left/up/diagonal的点都是1
- 并且, 如果三个点分别都衍生向三个方向, 那么最长的 square 边就是他们之中的最短边 (受最短边限制)
- dp[i][j]: max square length when reached at (i, j), from the 3 possible directions
- dp[i][j] = Math.min(Math.min(dp[i - 1][j], dp[i][j - 1]), dp[i - 1][j - 1]) + 1;
- Space, time O(mn)

##### init
每个点都可能是边长1, 如果 matrix[i][j] == '1'

##### 滚动数组
[i] 和 [i - 1] 之间的关系, 想到滚动数组优化 space, O(n) sapce.



---

**133. [Coins in a Line.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line.java)**      Level: Medium
      

拿棋子游戏, 每个人可以拿1个或者2个, 拿走最后一个子儿的输. 问: 根据给的棋子输, 是否能确定先手的输赢?

Game Theory: 如果我要赢, 后手得到的局面一定要'有输的可能'.

#### DP, Game Theory
- 要赢, 必须保证对手拿到棋盘时, 在所有他可走的情况中, '有可能败', 那就足够.
- 设计dp[i]:表示我面对i个coins的局面时是否能赢, 取决于我拿掉1个,或者2个时, 对手是不是会可能输?
- dp[i] = !dp[i - 1] || !dp[i-2]
- 时间: O(n), 空间O(n)
- 博弈问题, 常从'我的第一步'角度分析, 因为此时局面最简单.

#### Rolling Array
空间优化O(1). Rolling array, %2



---

**134. [Coins in a Line II.java](https://github.com/awangdev/LintCode/blob/master/Java/Coins%20in%20a%20Line%20II.java)**      Level: Medium
      

给一串coins, 用values[]表示; 每个coin有自己的value. 先手/后手博弈,
每次只能 按照从左到右的顺序, 拿1个或者2个棋子, 最后看谁拿的总值最大.

MiniMax的思考方法很神奇, 最后写出来的表达式很简单

#### DP, Game Theory 自考过程比较长
- 跟Coins in a line I 不一样: 每个coin的value不同.
- 用到MiniMax的思想, 这里其实是MaxiMin. Reference: http://www.cnblogs.com/grandyang/p/5864323.html
- Goal: 使得player拿到的coins value 最大化.
- 设定dp[i]: 从index i 到 index n的最大值. 所以dp[0]就是我们先手在[0 ~ n]的最大取值 
- 于此同时, 你的对手playerB也想最大化, 而你的选择又不得不被对手的选择所牵制.
- 用MaxiMin的思想, 我们假设一个当下的状态, 假想对手playerB会做什么反应(从对手角度, 如何让我输)
- 在劣势中(对手让我输的目标下)找到最大的coins value sum


##### 推算表达式
- Reference里面详细介绍了表达式如何推到出来, 简而言之:
- 如果我选了i, 那么对手就只能选(i+1), (i+2) 两个位置, 而我在对方掌控时的局面就是min(dp[i+2], dp[i+3])
- 如果我选了i和(i+1), 那么对手就只能选(i+2), (i+3) 两个位置, 而我在对方掌控时的局面就是min(dp[i+3], dp[i+4])
- 大家都是可选1个或者2个coins
- 目标是maximize上面两个最坏情况中的最好结果

##### 简化表达式
- 更加简化一点: 如果我是先手, dp[i]代表我的最大值.
- 取决于我拿了[i], 还是[i] + [i+1], 对手可能是dp[i + 1], 或者是dp[i+2]
- 其实dp[i] = Math.max(sum - dp[i + 1], sum - dp[i + 2]);
- 这里的sum[i] = [i ~ n] 的sum, 减去dp[i+1], 剩下就是dp[i]的值没错了

##### Initialization
- 这个做法是从最后往前推的, 注意initialize dp末尾的值.
- dp = new int[n + 1]; dp[n] = 0; // [n ~ n]啥也不选的时候, 为0.
- sum = new int[n + 1]; sum[n] = 0; // 啥也不选的时候, 自然等于0
- 然后记得initialize (n-1), (n-2)

##### 时间/空间
Time O(n)
Space O(n): dp[], sum[]



---

**135. [Binary Tree Postorder Traversal.java](https://github.com/awangdev/LintCode/blob/master/Java/Binary%20Tree%20Postorder%20Traversal.java)**      Level: Medium
      

如题, POST-ORDER traversal.

LeetCode给了hard, 应该是觉得stack的做法比较难想到.

#### Recursive
trivial, 先加left recursively, 再加right recursively, 然后组成头部.

#### Stack
- 双stack的思想, 需要在图纸上画一画
- 原本需要的顺序是: 先leftChild, rightChild, currNode.
- 营造一个stack, reversely process: 先currNode, 再rightChild, 再leftChild
- 这样出来的结果是reverse的, 那么翻转一下就可以了.
- v1做的时候用了stack1, stack2, 因为根据这个双stack的思想而来
- v2简化, 可以放在一个stack里面, 每次record result 的时候: rst.add(0, item);

##### 利用stack的特点
- 每次加element进stack的时候, 想要在 bottom/后process的, 先加
- 想要下一轮立刻process的, 最后push进stack.

##### 注意
这些binary tree traversal的题目.常常有多个做法:recursive or iterative



---

**136. [Compare Version Numbers.java](https://github.com/awangdev/LintCode/blob/master/Java/Compare%20Version%20Numbers.java)**      Level: Medium
      

给两串version number,  由数字和'.' 组成. 比较先后顺序. 

If version1 > version2 return 1, if version1 < version2 return -1, otherwise return 0.

#### divide and conquer 
- 用 str.split("\\.") 分割string
- Convert成integer, 逐个击破

#### 注意
- '1.0' 和 '0' 是相等的
- 如果可以假设version integer都是valid, 直接Integer.parseInt()就可以了
- 不然的话, 可以compare string



---

**137. [Count Complete Tree Nodes.java](https://github.com/awangdev/LintCode/blob/master/Java/Count%20Complete%20Tree%20Nodes.java)**      Level: Medium
      

Complete Tree就是说, 最后一个level可能是缺node的(不是说最右下角缺node, 别忘了!)

#### DFS + Optimization
- 每次看最左left depth和最右leaf depth 是不是一样, 如果一样, 直接 2 ^ h - 1就好
- 不一样的话, 再DFS

##### Trick
- 直接DFS会timeout, O(n), 其实可以optimize
- to pass the test with O(h^2), 位运算: Math.pow(2, h) = 2 << (h - 1). 神奇!
- 2 << 1就是把所有bits往左移动一位, 也就是 * 2 

#### Iteratively
- See details in comments inline. 要对tree非常理解
- binary tree one child tree nodes # = 2 ^ h - 1; 所以一个child tree + root = 2 ^ h



---

**138. [Course Schedule.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目问是否能把所有的课排了
- input是 numOfCourses, 还有这个prerequisites [[]]

#### Topological Sort
- 给一个graph of nodes
- 目标是根据edge 的 direction, 把这个graph 里面的 node sort 一个list
- 如果有cycle, 这个item就不会被放在最后的list 里面. 
- 比如: 如果两个课互相是dependency, 就变成了cyclic dependency, 这样不好.

#### BFS
- Kahn algorithem:
- 先build一个graph map: <node, list of nodes >
- count in-degree:  inDegree就是每个node上面, 有多少个走进来的edge?
- 那些没有 in-coming-edge的, indegree 其实就 等于 0, 那么他们就应该在final result list里面
- 对这些 indegree == 0 的 nodes BFS
- 模拟visit每个ndoe, 如果visit过了, 这个node上的 indegree--, 然后如果最终 indegree == 0, 这个node就成功进入final list.
- Note: 如果有cycle, indegree是不会变成0的, 它也无法进入最终list.

#### DFS
- 这道题没有要求作出final list, 相对简单, 只要visit每个nodes, 最后确认没有cycle就好了
- 用 visited int[] 来确认是否有cycle. 1 代表 paretNode visited, -1 代表在DFS上一行的标记
- 如果遇到-1, 说明这个node在上一级或者以上的同一个dfs path里面已经走过, 那么证明有cycle, return false.
- 真的topo sort会在DFS的底端, 把record放进一个stack, 最后reverse, 就是真的sort order.

#### Notes:
- 还有 List[] arrayOfList = new ArrayList[]; 这样的操作啊, 代替了map<integer, integerList>

#### Previous notes
有点绕，但是做过一次就明白一点。    
是topological sort的题目。一般都是给有dependency的东西排序。    

最终都会到一个sink node， 再不会有向后的dependency, 在那个点截止。    
我就已这样子的点为map的key, 然后value是以这个node为prerequisite的 list of courses.    

画个图的话，prerequisite都是指向那个sink node， 然后我们在组成map的时候，都是从sink node 发散回来到dependent nodes.    

在DFS里面，我们是反向的， 然后，最先完全visited的那个node, 肯定是最左边的node了，它被mark的seq也是最高的。    

而我们的sink node，当它所有的支线都visit完了，seq肯定都已经减到最小了，也就是0，它就是第一个被visit的。   


最终结果：
每个有pre-requisit的node都trace上去（自底向上），并且都没有发现cycle.也就说明schedule可以用了。



---

**139. [Course Schedule II.java](https://github.com/awangdev/LintCode/blob/master/Java/Course%20Schedule%20II.java)**      Level: Medium
      

- 一堆课用int[2] pair 来表示. [1, 0] 表示要上课1的话, 必须先把课0上了. 
- 每一个数字都是一个ndoe, 题目求这个最后排好的课的list
- 如果排不好, 就给个空就好
- input是 numOfCourses, 还有这个prerequisites [[]]

做法跟Course Schedule I 非常像, 可以参考.

#### BFS
- 每个没有 inDegree==0 node, 都是可以加进 final list里面的. 比如一开始找到的那些 inDegree = 0的 node
- 注意, 如果 prerequisites = [], 那么就是说这些课都independent, 开个int[0 ~ n-1]的数组并赋值就好.
- 如果有cycle, 严格意义上就做不了topological sort, 也无法涵盖所有nodes,  那么return [ ]

#### DFS
- 根据 Course Schedule 里面的DFS 修改
- 维持visited int[]全局变量
- 维持sortedList int[] 全局变量, 注意加进去的时候是 add(0, node) 加在开头这样
- 每次到一个node的children全部DFS走完之后, 就可以把他加进final list里面
- 如果有cycle, 也就是dfs return false的时候, 这个题目判定排课失败, return new int[] { }



---

**140. [Contains Duplicate III.java](https://github.com/awangdev/LintCode/blob/master/Java/Contains%20Duplicate%20III.java)**      Level: Medium
      

给一个unsorted array, 问, 是否有两个element, value相差最大为t,  而两个element的index 相差最大为k.

Note: 虽然题目名字是Contains Duplicate, 但其实要找的两个element不是duplicate, 而是Math.abs(value1 - value2) <= t.

#### TreeSet
- TreeSet还是一个set, 我们用来装已经visit过得item
- 如果window大小超过K, 那么把nums[i - k - 1] 去掉, 并且加上新的element
- 这里有个公式推算: (Math.abs(A-B) <= t) =>>>>> (-t <= A - B <= t) =>>>>>> A >= B - t, A <= B + t
- 也就是说, 如果对于 B = nums[i], 来说, 能找到一个target A, 满足上面的公式, 那么就可以 return true.
- Time O(nLogk), treeSet的大小不会超过k,  而 treeSet.ceiling(), treeSet.add(), treeSet.remove() 都是 O(logK)
- Space O(k)

#### Note
- 与Contains Duplicate II 类似概念. TreeSet有BST 因此可以直接用, 而不用自己构建BST
- 简化题目里面的重要条件 Math.abs(A-B) <= t 而推断出 A >= B - t, A <= B + t
- 并且需要需要用 TreeSet.ceiling(x): return number greater or equal to x. 这个用法要记住吧, 没别的捷径.



---

**141. [One Edit Distance.java](https://github.com/awangdev/LintCode/blob/master/Java/One%20Edit%20Distance.java)**      Level: Medium
      

如果S, T只用一个operation就能变成相等, return true.

#### Edit: 删除，增加，和替换
- 换完之后，理论上换成的String 就应该全等
- for loop, 一旦找到不一样的char, 就判断那三种可能性
- insert/delete 对于2个string来说, 效果是类似的
- O(n)



---

**142. [Jump Game.java](https://github.com/awangdev/LintCode/blob/master/Java/Jump%20Game.java)**      Level: Medium
      

给出步数，看能不能jump to end.

#### DP
- DP[i]: 在i点记录，i点之前的步数是否可以走到i点？ True of false.
- 其实j in [0~i)中间只需要一个能到达i 就好了
- Function: DP[i] = DP[j] && (A[j] >= i - j), for all j in [0 ~ i)
- Return: DP[dp.length - 1];
- It timesout, O(n^2)

#### Greedy
- Keep track of farest can go
- 一旦 farest >= nums.length - 1, 也就是到了头, 就可以停止, return true.
- 一旦 farest <= i, 也就是说, 在i点上, 已经走过了步数, 不能再往前跳, 于是 return false



---

**143. [Coin Change 2.java](https://github.com/awangdev/LintCode/blob/master/Java/Coin%20Change%202.java)**      Level: Medium
      

给串数字, target amount, 求总共多少种方式可以reach the amount.

#### DP
- O(MN): M, total target amount; N: size of coins
- 状态: dp[i]: sum of ways that coins can add up to i.
- Function: dp[j] += dp[j - coins[i]];
- Init: dp[0] = 1 for ease of calculation; other dp[i] = 0 by default
- note: 避免重复count, 所以 j = coins[i] as start
- 注意 coins 可能需要放在for loop 外面, 而主导换coin的流程. 
- 类似于: 网格dp, unique path 里面的2种走法: 从上到下, 从左到右



---

**144. [Decode Ways.java](https://github.com/awangdev/LintCode/blob/master/Java/Decode%20Ways.java)**      Level: Medium
      

给出一串数字, 要翻译(decode)成英文字母. [1 ~ 26] 对应相对的英文字母. 求有多少种方法可以decode.

#### Partition DP
- 确定末尾的2种状态: single letter or combos. 然后计算出单个letter的情况, 和双数的情况
- 定义dp[i] = 前i个digits最多有多少种decode的方法. new dp[n + 1].
- 加法原理: 把不同的情况, single-digit, double-digit 的情况加起来
- note: calculate number from characters, need to - '0' to get the correct integer mapping.
- 注意: check value != '0', 因为'0' 不在条件之中(A-Z)




---

**145. [Minimum Path Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Minimum%20Path%20Sum.java)**      Level: Medium
      

#### DP
- Time, Space O(MN)
- 往右下角走, 计算最短的 path sum. 典型的坐标型.
- 注意: init 第一行的时候, 要accumulate dp[0][j - 1] + grid[i][j], 而不是单纯assign grid[i][j]

#### Rolling Array
- Time O(MN), Space O(1)
- 需要在同一个for loop里面完成initialization, 和使用dp[i][j]
- 原因: dp[i % 2][j] 在被计算出来的时候, 是几乎马上在下一轮是要被用的; 被覆盖前不备用,就白算
- 如果按照第一种方法, 在开始initialize dp, 看起来固然简单, 但是不方便空间优化



---

**146. [Counting Bits.java](https://github.com/awangdev/LintCode/blob/master/Java/Counting%20Bits.java)**      Level: Medium
      

给一个数组, 算里面有多少bit 1. 

#### Bitwise DP
- 对于每一个数字, 其实很简单就能算出来: 每次 >>1, 然后 & 1 就可以count 1s. Time: 一个数字可以 >>1 O(logN) 次
- 现在要对[0 ~ num] 都计算, 也就是N个数字, 时间复杂度: O(nLogN).
- 用DP来优化, 查找过的number的1s count, 存下来在 dp[number]里面.
- 计算你顺序从 0 -> num, count过的数字就可以重复利用.
- Bit题目 用num的数值本身表示DP的状态.
- 这里, dp[i] 并不是和 dp[i-1]有逻辑关系; 而是dp[i] 和dp[i>>1], 从binary representation看出有直接关系.



---

**147. [Continuous Subarray Sum.java](https://github.com/awangdev/LintCode/blob/master/Java/Continuous%20Subarray%20Sum.java)**      Level: Medium
      

给一个非负数的数列和数字k(可正负, 可为0). 找到连续子序列(长度超过2), 使得这个subarray的sum 是 k的倍数. 问: 是否可能?

#### DP
- O(n^2)
- 需要记录在0 ~ i点(包括nums[i], 以nums[i]结尾)的sum, 坐标型动态规划.
- dp[i] = dp[i - 1] + nums[i];
- 最后移动, 作比较

#### 直接算结果
- 从sum = 每次[i ~ j]的所有情况
- 验证



---

**148. [House Robber II.java](https://github.com/awangdev/LintCode/blob/master/Java/House%20Robber%20II.java)**      Level: Medium
      

和House Robber I 类似, 搜刮房子, 相邻不能动. 特点是: 现在nums排成了圈, 首尾相连.

#### Sequence DP
- 根据dp[i-1]是否被rob来讨论dp[i]: dp[i] = Math.max(dp[i-1], dp[i - 2] + nums[i - 1]);
- 特别的是，末尾的last house 和 first house相连. 这里就需要分别讨论两种情况: 第一个房子被搜刮, 或者第一个房子没被搜刮
- be careful with edge case nums = [0], only with 1 element.

#### 两个状态
- 是否搜刮了第一个房子, 分出两个branch, 可以看做两种状态.
- 可以考虑用两个DP array; 也可以加一dp维度, 补充这个状态.
- 连个维度表示的是2种状态(1st house being robbed or not); 这两种状态是平行世界的两种状态, 互不相关.

#### Rolling array
与House Robber I一样, 可以用%2 来操作rolling array



---

**149. [House Robber III.java](https://github.com/awangdev/LintCode/blob/master/Java/House%20Robber%20III.java)**      Level: Medium
      

Houses被arrange成了binary tree, 规则还是一样, 连续相连的房子不能同时抄.

求Binary Tree neighbor max 能抄多少.

#### DFS
- 判断当下的node是否被采用，用一个boolean来表示. 
- 如果curr node被采用，那么下面的child一定不能被采用.
- 如果curr node不被采用，那么下面的children有可能被采用，但也可能略过，所以这里用Math.max() 比较一下两种可能有的dfs结果。
- dfs重复计算:每个root都有4种dive in的可能性, 假设level高度是h, 那么时间O(4^(h)), where h = logN, 也就是O(n^2)

#### DP 
- 并不是单纯的DP, 是在发现DFS很费劲后, 想能不能代替一些重复计算?
- 基本思想是dfs解法一致: 取root找最大值, 或者不取root找最大值
- 在root上DFS, 不在dfs进入前分叉; 每一个level按照状态来存相应的值: dp[0] root not picked, dp[1] root picked.
- Optimization: DP里面, 一口气找leftDP[]会dfs到最底层, 然后自下向上做计算
- 这个过程里面, 因为没有在外面给dfs()分叉, 计算就不会重叠, 再也不用回去visit most-left-leaf了, 算过一遍就完事.
- 然而, 普通没有dp的dfs, 在算完visited的情况下的dfs, 还要重新dfs一遍!visited的情况.
- Space O(h), time O(n), 或者说是O(2^h), where h = log(n)

#### DP 特点
- 不为状态而分叉dfs
- 把不同状态model成dp
- 每一个dfs都return一个based on status的 dp array.
- 等于一次性dfs计算到底, 然后back track, 计算顶部的每一层.
- DP 并不一定要是以n为base的. 也可以是局部的去memorize状态->value.



---

**150. [Palindrome Partitioning.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Partitioning.java)**      Level: Medium
      

#### DFS
- 在遍历str的时候，考虑从每个curr spot 到 str 结尾，是能有多少种palindorme?
- 那就从curr spot当个字符开始算，开始back tracing.
- 如果所选不是palindrome， 那move on.
- 若所选的确是palindrome,　加到path里面，DFS去下个level，等遍历到了结尾，这就产生了一种分割成palindrome的串。
- 每次DFS结尾，要把这一层加的所选palindrome删掉，backtracking嘛

#### Optimization
- 可以再每一个dfs level 算 isPalindrome(S), 但是可以先把 boolean[][] isPalin 算出来, 每次O(1) 来用
- 注意: isPalin[i][j] 是 inclusive的, 所以用的时候要认准坐标
- Overall Space O(n^2): 存 isPlain[][]
- Time O(n!), 每一层的for loop spawn n * (n - 1) * (n - 2)



---

**151. [Permutation in String.java](https://github.com/awangdev/LintCode/blob/master/Java/Permutation%20in%20String.java)**      Level: Medium
      

#### Two Pointer
- 如果做s1的permudation, 时间复杂度是O(n!) 肯定不可以
- 这里用HashTable的做法 (因为26字母, 所以用int[26]简化) 来记录window内的 character count
- 如果window内的character count 相等, 那么就是permudation
- 更进一步优化: 找两个map相互对应, 不如用一个 int[26]: s1对遇到的character做加法, s2对遇到的character做减法
- two pointer 运用在 n1, n2 的把控; 以及 s2.charAt(i - n1) 这一步



---

**152. [Permutations II.java](https://github.com/awangdev/LintCode/blob/master/Java/Permutations%20II.java)**      Level: Medium
      

给一串数组, 找出所有permutation数组. 注意: 给出的nums里面有重复数字, 而permutation的结果需要无重复.

#### Backtracking
- 排序, 
- Mark visited. 通过permutation规律查看是否排出了重复结果
- 并且要检查上一层recursive时有没有略过重复element
- time O(n!)

##### 背景1
- 在recursive call里面有for loop, 每次从i=0开始, 试着在当下list上加上nums里面的每一个。    
- 从i=0开始，所以会依次recursive每一个nums：
- 因此，例如i=2,肯定比i=3先被访问。也就是:取i=2的那个list permutation肯定先排出来。   

##### 背景2
- 重复的例子：给出Input[x, y1, y2], 假设y的值是一样的。那么，{x,y1,y2}和{x,y2,y1}是相同结果。

##### Note
- 综上，y1肯定比y2先被访问,{x,y1,y2}先出。 紧随其后，在另一个recursive循环里，{x,y2...}y2被先访问，跳过了y1。    
- 重点:规律在此，如果跳过y1，也就是visited[y1] == false, 而num[y2] == num[y1]，那么这就是一个重复的结果，没必要做，越过。
- 结果:那么，我们需要input像{x,y1,y2}这样数值放一起，那么必须排序。

#### Non-recursive, manuall swap
- Idea from: https://www.sigmainfy.com/blog/leetcode-permutations-i-and-ii.html
- 用到 sublist sort
- 用 swap function, 在原数组上调节出来新的permutation
- 注意: 每次拿到新的candidate, 都要把没有permutate的数位sort, 然后再开始swap.
- 这是为了确保, [j]和[j-1]在重复时候, 不用重新记录.

#### Queue
- 给一个visited queue
- 和queue在所有的地方一同populate. 
- 然后visited里面存得时visited indexes。 (Not efficient code. check again)



---

**153. [Shuffle an Array.java](https://github.com/awangdev/LintCode/blob/master/Java/Shuffle%20an%20Array.java)**      Level: Medium
      

像shuffle music 一样, 做一套shuffle array的functions: 

shuffle() 给出random的permutation

reset() 给出最初的nums

#### Permutation
- Permutation 实际上就是在list/array/... 上面给元素换位置
- 硬换位置, 每次换的位置不同, 用random来找到要换的index
- 维持同一个random seed
- O(n)

##### Note
- compute all permutations 太慢, 不可行.



---

**154. [Group Anagrams.java](https://github.com/awangdev/LintCode/blob/master/Java/Group%20Anagrams.java)**      Level: Medium
      

给一串string, return list of list, 把anagram 放在一起.

#### Hash Table, key 是 character frequency
- 存anagram
- 用 character frequency 来做unique key
- 用固定长度的char[26] arr 存每个字母的frequency; 然后再 new string(arr).   
- 因为每个位子上的frequency的变化，就能构建一个unique的string
- O(nk), k = max word length


#### Hash Table, key 是 sorted string
- 和check anagram 想法一样：转化并sort char array，用来作为key。
- 把所有anagram 存在一起。注意结尾Collections.sort().
- O(NKlog(K)), N = string[] length, k = longest word length    




---

**155. [Backpack.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack.java)**      Level: Medium
      

给i本书, 每本书有自己的重量 int[] A, 背包有自己的大小M, 看最多能放多少重量的书?

#### Backpack DP 1
- 简单直白的思考 dp[i][m]: 前i本书, 背包大小为M的时候, 最多能装多种的书?
- **注意**: 背包问题, 重量weight一定要是一维.
- dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - A[i - 1]] + A[i - 1]);
- 每一步都track 最大值
- 最后return dp[n][m]
- 时间空间  O(mn)
- Rolling array, 空间O(m)

#### Backpack DP 2
- true/false求解, 稍微曲线救国: 重点是, 最后, 按照weight从大到小遍历, 第一个遇到true的, index就是最大值.  
- 考虑: 用i个item (可跳过地取), 是否能装到weight w?
- 需要从'可能性'的角度考虑, 不要搞成单一的最大值问题.
- 1. 背包可装的物品大小和总承重有关.
- 2. 不要去找dp[i]前i个物品的最大总重, 找的不是这个. 
    dp[i]及时找到可放的最大sum, 但是i+1可能有更好的值, 把dp[i+1]变得更大更合适.

##### 做法
- boolean[][] dp[i][j]表示: 有前i个item, 用他们可否组成size为j的背包? true/false.
- (反过来考虑了，不是想是否超过size j, 而是考虑是否能拼出exact size == j)
- **注意**: 虽然dp里面一直存在i的位置, 实际上考虑的是在i位置的时候, 看前i-1个item.

##### 多项式规律
- 1. picked A[i-1]: 就是A[i-1]被用过, weight j 应该减去A[i-1]. 那么dp[i][j]就取决于dp[i-1][j-A[i-1]]的结果.
- 2. did not pick A[i-1]: 那就是说, 没用过A[i-1], 那么dp[i][j]就取决于上一行d[i-1][j]
- dp[i][j] = dp[i - 1][j] || dp[i - 1][j - A[i - 1]]

##### 结尾
- 跑一遍dp 最下面一个row. 从末尾开始找, 最末尾的一个j (能让dp[i][j] == true)的, 就是最多能装的大小 :)   
- 时间，空间都是：O(mn)




---

**156. [Backpack II.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20II.java)**      Level: Medium
      

给i本书, 每本书有自己的重量 int[] A, 每本书有value int[] V

背包有自己的大小M, 看最多能放多少value的书?

#### Backpack DP
- 做了Backpack I, 这个就如出一辙, 只不过: dp存的不是max weight, 而是 value的最大值.
- 想法还是，选了A[i - 1] 或者没选A[i - 1]时候不同的value值.
- 时间空间O(mn)
- Rolling Array, 空间O(m)

#### Previous DP Solution
- 如果无法达到的w, 应该mark as impossible. 一种简单做法是mark as -1 in dp. 
- 如果有负数value, 就不能这样, 而是要开一个can[i][w]数组, 也就是backpack I 的原型.
- 这样做似乎要多一些代码, 好像并不是非常需要




---

**157. [Backpack V.java](https://github.com/awangdev/LintCode/blob/master/Java/Backpack%20V.java)**      Level: Medium
      

#### Backpack DP
- 与背包1不同: 这里不是check可能性(OR)或者最多能装的size是多少; 而是计算有多少种正好fill的可能性.
- dp[i][w]: 用前i本书, 正好fill到 w weight的可能性.
- 对于末尾, 还是两种情况:
- 1. i-1位置没有加bag
- 2. i-1位置加了bag
- 两种情况可以fill满w的情况加起来, 就是我们要的结果.
- 如常: dp[n + 1][w + 1]
- 重点: dp[0][0] 表示0本书装满weight=0的包, 这里我们必须 dp[0][0] = 1, 给后面的 dp function 做base
- Space, time: O(MN)
- Rolling array, 空间优化, 滚动数组. Space: O(M)

#### 降维打击, 终极优化
- 分析row(i-1)的规律, 发现所有row(i)的值, 都跟row(i-1)的左边element相关, 而右边element是没用的.
- 所以可以被override.
- Space: O(M), 真*一维啊!
- Time: O(MN)



---

**158. [Evaluate Reverse Polish Notation.java](https://github.com/awangdev/LintCode/blob/master/Java/Evaluate%20Reverse%20Polish%20Notation.java)**      Level: Medium
      

给一个 RPN string list, 根据这个list, 计算结果.

#### Stack
- stack 里面 存数字
- 每次遇到operator, 都拿前2个数字计算
- 计算结果存回到stack里面, 方便下一轮使用.
- Time,Space O(n)




---

**159. [Gas Station.java](https://github.com/awangdev/LintCode/blob/master/Java/Gas%20Station.java)**      Level: Medium
      

给一串gas station array, 每个index里面有一定数量gas.

给一串cost array, 每个index有一个值, 是reach下一个gas station的油耗.

array的结尾地方, 再下一个点是开头, 形成一个circle route.

找一个index, 作为starting point: 让车子从这个点, 拿上油, 开出去, 还能开回到这个starting point

#### Greedy
- 不论从哪一个点开始, 都可以记录总油耗, total = {gas[i] - cost[i]}. 最后如果total < 0, 必然不能走回来
- 可以记录每一步的油耗积累, remain = {gas[i] - cost[i]}; 一旦 remain < 0, 说明之前的starting point 不合适, 重设: start = i + 1

#### NOT DP
- 看似有点像 House Robber II, 但是问题要求的是: 一个起始点的index
- 而不是求: 最后点可否走完/最值/计数



---

