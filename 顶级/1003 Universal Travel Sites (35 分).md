* 在完成环球旅行后，CYLL现在正在计划一个环球旅游网站开发项目。
* 经过仔细的调查，她掌握了所有卫星运输站的运力清单。
* 为了估算预算，她必须知道行星空间站必须保证每艘太空飞船在到达时都能停靠并下载乘客的最低容量。


### 输入：
* 第一行，源点星球名字，目的地星球名字，正整数N
* 接下来N行，
  * 每行格式:```source[i] destination[i] capacity[i]```,
    * ```source[i]```,```destination[i]```,是卫星名字，和所涉及的两个星球的名字，
    * ```capacity[i]```,是从```source[i]```到```destination```所能运输的最大游客数
    * 每个名字是一个3个大写字母的字符串，
    
* 请注意，卫星运输站没有为乘客提供住宿设施。
* 因此没有一个乘客可以留下来。
* 这样的空间站将不允许载有超过自身容量的太空飞船进入。
* 保证列表既不包含到达源行星的道路，也不包含从目标行星出发的道路。

### 输出：

* 对于每个测试用例，只需在一行中打印行星站必须保证每艘太空飞船能够停靠并在到达时下载乘客的最低容量。
