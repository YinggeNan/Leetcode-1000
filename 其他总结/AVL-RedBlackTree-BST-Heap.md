### AVL树
平衡二叉查找树，AVL也是BST：插入、删除都是log(n)，查找log(n)  
### RedBlackTree
TreeMap底层红黑树  
红黑树的每一条从根到叶子的路径不过比任何一条其他的从根到叶子的路径长两倍，所以红黑树也近似为AVL  
插入、删除、查找log(n)
### Heap
PriorityQueue  
建堆的时间复杂度，自底向上为O(N)    
堆调整（插入/删除）：logN   
堆排序：O(N)+O(N*logN)=O(NlogN)  
AVL、RedBlack：
### BST
查找最坏O(N)，平均O(logN)  
插入和删除都是基于查找，所以时间复杂度同查找
### 构建BST、AVL、RedBlackTree、Heap
BST、AVL、RedBlackTree都是基于查找  
构建BST: 最坏O(N*N)，平均O(Nlogn)     
构建AVL、RedBlackTree: O(NlogN)  
构建Heap: O(N)，自底向上  