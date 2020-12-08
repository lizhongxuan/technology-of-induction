# 数据结构

## 树

### 二叉树

每个节点最多有两个叶子节点。
*  [《二叉树》](https://blog.csdn.net/cai2016/article/details/52589952)

### 完全二叉树
* [《完全二叉树》](https://baike.baidu.com/item/%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91/7773232?fr=aladdin)
	* 叶节点只能出现在最下层和次下层，并且最下面一层的结点都集中在该层最左边的若干位置的二叉树。

### 平衡二叉树
左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。
* [《浅谈数据结构-平衡二叉树》](http://www.cnblogs.com/polly333/p/4798944.html)
* [《浅谈算法和数据结构: 八 平衡查找树之2-3树》](http://www.cnblogs.com/yangecnu/p/Introduce-2-3-Search-Tree.html)

### 二叉查找树（BST）
二叉查找树（Binary Search Tree），也称有序二叉树（ordered binary tree）,排序二叉树（sorted binary tree）。

* [《浅谈算法和数据结构: 七 二叉查找树》](http://www.cnblogs.com/yangecnu/p/Introduce-Binary-Search-Tree.html)


### 红黑树
* [《最容易懂得红黑树》](https://blog.csdn.net/sun_tttt/article/details/65445754)
	* 添加阶段后，左旋或者右旋从而再次达到平衡。 
* [《浅谈算法和数据结构: 九 平衡查找树之红黑树》](http://www.cnblogs.com/yangecnu/p/Introduce-Red-Black-Tree.html)

### B，B+，B*树
MySQL是基于B+树聚集索引组织表

* [《B-树，B+树，B\*树详解》](https://blog.csdn.net/aqzwss/article/details/53074186)
* [《B-树，B+树与B\*树的优缺点比较》](https://blog.csdn.net/bigtree_3721/article/details/73632405)
	* B+树的叶子节点链表结构相比于 B-树便于扫库，和范围检索。
### LSM 树

LSM（Log-Structured Merge-Trees）和 B+ 树相比，是牺牲了部分读的性能来换取写的性能(通过批量写入)，实现读写之间的平衡。
Hbase、LevelDB、Tair（Long DB）、nessDB 采用 LSM 树的结构。LSM可以快速建立索引。

* [《LSM树 VS B+树》](https://blog.csdn.net/dbanote/article/details/8897599)
	* B+ 树读性能好，但由于需要有序结构，当key比较分散时，磁盘寻道频繁，造成写性能较差。
	* LSM 是将一个大树拆分成N棵小树，先写到内存（无寻道问题，性能高），在内存中构建一颗有序小树（有序树），随着小树越来越大，内存的小树会flush到磁盘上。当读时，由于不知道数据在哪棵小树上，因此必须遍历（二分查找）所有的小树，但在每颗小树内部数据是有序的。
	
* [《LSM树（Log-Structured Merge Tree）存储引擎》](https://blog.csdn.net/u014774781/article/details/52105708)
	* 极端的说，基于LSM树实现的HBase的写性能比MySQL高了一个数量级，读性能低了一个数量级。
	* 优化方式：Bloom filter 替代二分查找；compact 小数位大树，提高查询性能。
	* Hbase 中，内存中达到一定阈值后，整体flush到磁盘上、形成一个文件（B+数），HDFS不支持update操作，所以Hbase做整体flush而不是merge update。flush到磁盘上的小树，定期会合并成一个大树。

### 前缀树
又称单词查找树,字典树，Trie树，是一种树形结构，是一种哈希树的变种。
它的优点是：利用字符串的公共前缀来减少查询时间，最大限度地减少无谓的字符串比较，查询效率比哈希树高。

* [《字典树(前缀树)》](https://blog.csdn.net/weixin_39778570/article/details/81990417)

## BitSet

经常用于大规模数据的排重检查。

* [《Java Bitset类》](http://www.runoob.com/java/java-bitset-class.html)
* [《Java BitSet（位集）》](https://blog.csdn.net/caiandyong/article/details/51581160)
