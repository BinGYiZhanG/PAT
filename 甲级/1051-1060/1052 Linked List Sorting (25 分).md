### 题意：
* Now given a linked list, you are supposed to sort the structures according to their key values in increasing order.

### 思路：
* 1,在于对链表的排序，此题```address```与```key```是绑定的，而```next```根据排完序之后再赋值
* 2,初始表可能不是相连的（```next_```的结点可能不存在），得先把链表建立
* 3,代码中始终有一个点没想通，就是排序问题
  * 解释：排序是针对点的值进行排序，而点有两个属性--序号和值，排序会重新分配点的序号，对于本题而言，```address```既相当于序号，又相当于值，
  所以要单独存储（否则，排序完之后，```address```会改变），而```key```就是要排序的内容,与```address```一一对应


```

```
