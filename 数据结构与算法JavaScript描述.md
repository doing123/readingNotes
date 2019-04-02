## 第一章 JavaScript的编程环境和模型
JavaScript 中，函数的参数传递方式都是按值传递，没有按引用传递的参数。但是 JavaScript中有保存引用的对象，比如数组，它们是按引用传递的。

## 第二章 数组
JavaScript中的数组是一种特殊的对象，用来表示偏移量的索引是该对象的属性。这些数字索引在内部被转换为字符串类型，这是因为JavaScript对象中的属性名必须是字符串。

在调用 Array 的构造函数时，可以只传入一个参数，用来指定数组的长度

sort() 方法是按照字典顺序对元素进行排序的，因此它假定元素都是字符串类型，即使元素是数字类型，也被认为是字符串类型。

## 第三章 列表
抽象数据类型：ADT

3.1 列表的抽象数据类型定义
listSize(属性)pos(属性)length(属性)clear(方法)toString(方法)getElement(方法)insert(方法)append(方法)remove(方法)front(方法)end(方法)prev(方法)next(方法)currPos(方法)moveTo(方法)

3.3 使用迭代器访问列表
for(names.front(); names.currPos() < names.length(); names.next()) {
    print(names.getElement());
}

## 第四章 栈
栈是一种特殊的列表

clear()：清除时不清楚dataStore数组的值？？？

    使用：
        数制间的相互转换
        回文
        递归：使用 JavaScript 讲解递归工作原理的网页(http://bit.ly/lenDGE3)

## 第五章 队列
使用队列：
* 方块舞的舞伴分配问题
* 使用队列对数据进行排序，基数排序（0-99，先个位，再十位）
* 优先队列：急诊室

## 第六章 链表
6.2 定义链表
链表是由一组节点组成的集合。每个节点都使用一个对象的引用指向它的后继。指向另一 个节点的引用叫做链

数组元素靠它们的位置进行引用，链表元素则是靠相互之间的关系进行引用

头节点、null、前驱节点、后继节点

6.3 设计一个基于对象的链表

    function LList() {
        this.head = new Node("head"); 
        this.find = find;
        this.insert = insert; 
        this.display = display; 
        this.findPrevious = findPrevious; 
        this.remove = remove;
    }

6.4 双向链表

    function Node(element) {
        this.element = element;
        this.next = null;
        this.previous = null;

    }

    function LList() {
        this.head = new Node("head"); 
        this.find = find;
        this.insert = insert; 
        this.display = display; 
        this.remove = remove; 
        this.findLast = findLast; 
        this.dispReverse = dispReverse;
    }

6.5 循环链表

链表的尾节点指向头节点：theLastNode.next = head

6.6 链表的其他方法

    advance(n)
    back(n)
    show()

## 第七章 字典
字典是一种以键-值对形式存储数据的数据结构

7.1 Dictionary 类

Dictionay 类的基础是 Array 类，而不是 Object 类。本章稍后将提到，我们想对字典中的 键排序，而 JavaScript 中是不能对对象的属性进行排序的。但是也不要忘记，JavaScript 中 一切皆对象，数组也是对象。

    delete this.datastore[kay]

    function Dictionary() {
        this.add = add;
        this.datastore = new Array(); 
        this.find = find;
        this.remove = remove;
        this.showAll = showAll;
    }

7.2 Dictionary 类的辅助方法

为什么不使用 length 属性?这是因为当键的类型为字符串时，length 属性 就不管用了。

7.3 为 Dictionary 类添加排序功能

    function showAll() {
        for(var key in Object.keys(this.datastore).sort()) {
            print(key + " -> " + this.datastore[key]);
        }
    }

## 第八章 散列
散列使用的数据结构叫做散列表

使用散列表存储数据时，通过一个散列函数将键映射为一个数字，这个数字的范围是 0 到散列表的长度。

理想情况下，散列函数会将每个键值映射为一个唯一的数组索引。然而，键的数量是无限 的，数组的长度是有限的(理论上，在 JavaScript 中是这样)，一个更现实的目标是让散列 函数尽量将键均匀地映射到数组中。

即使使用一个高效的散列函数，仍然存在将两个键映射成同一个值的可能，这种现象称为碰撞(collision)，当碰撞发生时，我们需要有方案去解决。

散列表中的数组究竟应该有多大?这是编写散列函数时必须要 考虑的。对数组大小常见的限制是:数组长度应该是一个质数。

ASCII（American Standard Code for Information Interchange:美国信息交换标准代码）

8.2 HashTable 类

来表示散列表

    function HashTable() {
        this.table = new Array(137);
        this.simpleHash = simpleHash;
        this.showDistro = showDistro;
        this.put = put;
        // this.get = get;
    }

8.2.1 选择一个散列函数

除留余数法

将字符串中每个字符的 ASCII 码值相加似乎是一个不错的散列函数。这样散列值
就是 ASCII 码值的和除以数组长度的余数

8.2.2 一个更好的散列函数

霍纳算法，在此算法中，新 的散列函数仍然先计算字符串中各字符的 ASCII 码值，不过求和时每次要乘以一个质数。 大多数算法书建议使用一个较小的质数，比如 31，但是对于我们的数据集，31 不起作用， 我们使用 37，这样刚好不会产生碰撞

8.2.3 散列化整型键

学生成绩

8.2.4 对散列表排序、从散列表中取值

    function get(key) {
        return this.table[this.betterHash(key)];
    }

8.3 碰撞处理

8.3.1 开链法

开链法是指实现散列表的底层数组中，每个数组 元素又是一个新的数据结构，比如另一个数组，这样就能存储多个键了

8.3.2 线性探测法

开放寻址散列

如果数组的大小是待存储数据个数的 1.5 倍， 那么使用开链法;如果数组的大小是待存储数据的两倍及两倍以上时，那么使用线性探 测法。

为了说明线性探测法的工作原理，可以重写 put() 和 get() 方法。为了实现一个真实的 数据存取系统，需要为 HashTable 类增加一个新的数组，用来存储数据。数组 table 和values 并行工作，当将一个键值保存到数组 table 中时，将数据存入数组 values 中相应的 位置上。？？？

## 第九章 集合 set
首先，集合中的成员是无序的;其次，集合中不允许相同成员存在。

* 不包含任何成员的集合称为空集，全集则是包含一切可能成员的集合。
* 如果两个集合的成员完全相同，则称两个集合相等。
* 如果一个集合中所有的成员都属于另外一个集合，则前一集合称为后一集合的子集。

并集、交集、补集

9.2 Set 类的实现

    function Set() {
        this.dataStore = [];
        this.add = add;
        this.remove = remove;
        this.size = size;
        this.union = union;
        this.intersect = intersect;
        this.subset = subset;
        this.difference = difference;
        this.show = show;
    }

    ES6 Set WeakSet Map WeakMap

第十章 二叉树和二叉查找树

树由一组以边连接的节点组成

根节点、父节点、子节点、叶子节点

以某种特定顺序 访问树中所有的节点称为树的遍历。

定义树的层数就是树的深度。

每个节点都有一个与之相关的值，该值有时被称为键。

二叉树是一种特殊的树，它的子节点个数不超过两个。

二叉查找树是一种 特殊的二叉树，相对较小的值保存在左节点中，较大的值保存在右节点中

实现二叉查找树，Binary Sort Tree， BST

    function Node(data, left, right) {
        this.data = data;
        this.left = left;
        this.right = right;
        this.show = show;
    }

10.2.2 遍历二叉查找树

有三种遍历 BST 的方式:中序、先序和后序。

中序遍历按照节点上的键值，以升序访问BST 上的所有节点。先序遍历先访问根节点，然后以同样方式访问左子树和右子树。后序 遍历先访问叶子节点，从左子树到右子树，再到根节点。

    function inOrder(node) { // 中序遍历
        if (!(node == null)) {
            inOrder(node.left);
            putstr(node.show() + " ");
            inOrder(node.right);
        }
    }

    function preOrder(node) { // 先序
        if (!(node == null)) {
            putstr(node.show() + " ");
            preOrder(node.left);
            preOrder(node.right);
        }
    }

    function postOrder(node) { // 后序
        if (!(node == null)) {
            postOrder(node.left);
            postOrder(node.right);
            putstr(node.show() + " ");
        }
    }

10.3 在二叉查找树上进行查找

给定值、最大值、最小值

10.4 从二叉查找树上删除节点

    function remove(data) {
        root = removeNode(this.root, data);
    }

    function removeNode(node, data) { // 两个子节点：要么查找待删除节点左子树 上的最大值，要么查找其右子树上的最小值
        if (node == null) {
            return null;
        }
        if (data == node.data) {
            // 没有子节点的节点
            if (node.left == null && node.right == null) {
                return null;
            }
            // 没有左子节点的节点
            if (node.left == null) {
                return node.right;
            }
            // 没有右子节点的节点
            if (node.right == null) {
                return node.left;
            }
            // 有两个子节点的节点
            var tempNode = getSmallest(node.right);
            node.data = tempNode.data;
            node.right = removeNode(node.right, tempNode.data); 
            return node;
        } else if (data < node.data) {
            node.left = removeNode(node.left, data);
            return node;
        } else {
            node.right = removeNode(node.right, data);
            return node;
        }
    }

10.5 计数

## 第十一章 图和图算法
11.1 图的定义

图由边的集合及顶点的集合组成

有向图、无序图、顶点、路径、简单圈、平凡圈、强连通

11.2 用图对现实中的系统建模

11.3 图类

表示顶点：Vertex

表示边：邻接表或者邻接表数组、邻接矩阵

构建图

    function Graph(v) {
        this.vertices = v;
        this.edges = 0;
            this.adj = [];
        for (var i = 0; I < this.vertices; ++i) {
            this.adj[i] = [];
            this.adj[i].push("");
        }
        this.addEdge = addEdge;
        this.toString = toString;
        this.showGraph = showGraph
    }

11.4 搜索图

深度优先搜索

    function dfs(v) {
        this.marked[v] = true;
        if (this.adj[v] != undefined) {
            print("Visited vertex:  " + v);
        }
        for each(var w in this.adj[v]) {
            if (!this.marked[w]) {
                 this.dfs(w);
            }
        }
    }

广度优先搜索

    function bfs(s) {
        var queue = []; 
        this.marked[s] = true; 
        queue.push(s); // 添加到队尾
        while (queue.length > 0) {
            var v = queue.shift(); // 从队首移除
            if (v !== undefined) {
                print("Visisted vertex:  " + v);
            }
            for each(var w in this.adj[v]) {
                if (!this.marked[w]) {
                    this.edgeTo[w] = v; // ???
                    this.marked[w] = true;
                    queue.push(w);
                } 
            }
        } 
    }

11.5 查找最短路径

广度优先搜索对应的最短路径

11.6 拓扑排序

优先级约束调度

11.6.2 实现拓扑排序算法 // ？？？

与深度优先搜索类似

topSort、sopSortHelper函数

## 第十二章 排序算法
排序和检索

12.1 数组测试平台

12.2 基本排序算法

* 冒泡排序：最慢的排序算法之一，但也是一种最容易实现的排序算法

假设正在将一组数字按照升序排列，较大的值会浮动到数组的右侧，而较小 的值则会浮动到数组的左侧。

* 选择排序：选择排序从数组的开头开始，将第一个元素和其他元 素进行比较。检查完所有元素后，最小的元素会被放到数组的第一个位置，然后算法会从 第二个位置继续。这个过程一直进行，当进行到数组的倒数第二个位置时，所有的数据便 完成了排序。

* 插入排序：

* 基本排序算法的计时比较：

12.3 高级排序算法：处理大型数据集的最高效排序算法

希尔排序：首先比较距离较远的元素，而非相邻的元素。通过定义一个间隔序列来表示在排序过程中进行比较的元素之 间有多远的间隔。

间隔序列=1，此时是标准的插入排序

这种方案可以使离正确位置很远的元素更快地回到合适的位置。当开始用这个算法遍历 数据集时，所有元素之间的距离会不断减小，直到处理到数据集的末尾，这时算法比较的 就是相邻元素了。

计算动态间隔序列：Sedgewick

    var N = this.dataStore.length;
    var h = 1;
    while (h < N/3) {
        h = 3 * h + 1; 
    }

归并排序：把一系列排好序的子序列合并成一个大的完整有序序列。

自顶向下的归并排序（js中这种方法不太可行）

自底向上的归并排序：这个算法首先将数据集分解 为一组只有一个元素的数组。然后通过创建一组左右子数组将它们慢慢合并起来，每次合 并都保存一部分排好序的数据，直到最后剩下的这个数组所有的数据都已完美排序。

快速排序：是处理大数据集最快的排序算法之一

是一种分而治之的算法，通过递归的方 式将数据依次分解为包含较小元素和较大元素的不同子序列。

基准值（pivot）

## 第十三章 检索算法
在列表中查找数据有两种方式:顺序（线性）查找和二分查找。顺序查找适用于元素随机排列的列 表;二分查找适用于元素已排序的列表。二分查找效率更高，但是你必须在进行查找之前 花费额外的时间将列表中的元素排序。

13.1 顺序查找

* 查找最小值和最大值
* 使用自组织数据
* 通过将频繁查找到的元素置于数据集的起始位置来最小化查找次数
* 数据的位置并非由程 序员在程序执行之前就组织好，而是在程序运行过程中由程序自动组织的。
* 80-20原则；帕累托分布

13.2 二分查找算法：有序数据

计算重复次数

13.3 查找文本数据

seqSearch()、binSearch()、insertionsort()

## 第十四章 高级算法

动态规划：从底部开始解决问题，将所有小问题解决掉，然后合并成一个 整体解决方案，从而解决掉整个大问题。

贪心算法：是一种以寻找“优质解”为手段从而达成整体解决方案的算法。优质解、局部最优解、全局最优解

14.1 动态规划

14.1.1 实例：计算斐波那契数列 

在我们计算 fib(20) 及更大的数字时，动态规划的解决方案要比递归的解决方案 更加高效。

    function recurFib(n) {
        if (n < 2) {
            return n; 
        } else {
            return recurFib(n-1) + recurFib(n-2);
        }
    }

    function dynFib(n) {
        var val = [];
        for (var i = 0; i <= n; ++i) {
            val[i] = 0; 
        }
        if (n == 1 || n == 2) {
            return 1;
        } else {
            val[1] = 1;
            val[2] = 2;
            for (var i = 3; i <= n; ++i) {
                val[i] = val[i-1] + val[i-2];
            }
            return val[n-1];
        }
    }

    function iterFib(n) { // 使用迭代的方案计算斐波那契数列时，是可以不使用数组的
        var last = 1;
        var nextLast = 1;
        var result = 1;
        for (var i = 2; i < n; ++i) {
            result = last + nextLast;
            nextLast = last;
            last = result;
        }
        return result;
    }

14.1.2 寻找最长公共子串

    if (word1[i - 1] == word2[j - 1]) { // todo：如何理解
        lcsarr[i][j] = lcsarr[i - 1][j - 1] + 1;
    } else {
        lcsarr[i][j] = 0;
    }

14.1.3 背包问题：递归解决方案

// todo：待理解

14.1.4 背包问题：动态规划方案

使用递归方案能解决的问题，都能够使用动态规划技巧来解决，而且还能够提高程序的执 行效率。背包问题绝对可以用动态规划的方式来重写，要做的只是使用一个数组来保存临 时解，直到获得最终的解为止

14.2 贪心算法

第一个贪心算法案例：找零问题

背包问题的贪心算法解决方案


