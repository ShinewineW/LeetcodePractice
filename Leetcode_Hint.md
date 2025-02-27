# Leetcode 算法题解思路

以下是一些 Leetcode 题目的简单思路提示。具体的解题过程和详细分析，请查看 [Notion 页面](https://zmwjz.notion.site/0af4c8fa7b4c4fd38188ad085e419b3b)。

## 题目 141
两种方法：
- 一种是使用哈希表记录，如果下一个 `next` 的结点在哈希表中存在，直接返回 `true`。
- 另一种是赛马法，把链表想象成一个赛道，有环的说明这个赛道是圆形赛道，可以套圈，所以指派两个指针，一个 `fast` 一个 `slow`，一个一次位移两个，一个一次位移一个，控制好结束判断，只要 `fast == slow` 那么返回 `true`。

## 题目 142
两种方法：
- 一种同上，使用哈希表，只需要这次返回哈希表中记录的地址即可。
- 另一种方法和赛马法一样，唯一的区别在于 `slow` 和 `fast` 循环过程中，如果使用一个 `time_clock` 来计数，随后循环结束时的 `time_clock` 值就是这个圆环的长度，那么对于每一个从头开始的结点，往后延伸 `time_clock` 的长度，能够回到自身的就是碰撞点。更进一步的想，在 `slow` 和 `fast` 循环结束时，`fast/slow` 的位置其实就是开头距离 `time_clock` 的位置，直接维护好 `fast`，每一次和开头一起 `->Next` 那么如果相等，就是碰撞点。

## 题目 143
两种方法：
- 一种使用 `deque` 数据结构，最大限度地利用 `deque` 特性，将整个链表转移到 `deque` 中，然后一头一尾进行操作。
- 另一种使用前两题中的 `two point` 法，使用 `fast`，`slow` 指针得到这个链表的中间节点，然后顺带在遍历过程中将 `slow` 经过的节点入栈，然后一个一个 `pop` 出来进行处理，但是要分奇偶。原则上此方法没取巧，时间比上面更快一些。

## 题目 144
两种方法：
- 一种直接递归，很简单的先序遍历操作。
- 另一种使用栈数据结构，后进先出，首先对于根节点，（将其所有的左节点全部入栈，然后对每一个 `pop` 出来的 `temp` 节点，将 `temp` 更新为他的右节点，然后重复括号内循环）这样就完成了对于每个右节点的左节点入栈并记录，得到结果。

## 题目 145
两种方法：
- 一种直接递归，很简单的后序遍历操作。
- 另一种使用栈数据结构，由于正常的后序遍历按照左，右，根的顺序进行，因此我们按照根，右，左的顺序将数据在堆栈中放置，同时压入 `res` 中，最后将 `res` 取反可以得到最终结果。

## 题目 146
两种方法：
- 一种首先使用 `hashmap` 来存储 `key` 和 `value`，同时，使用 `list` 链表结构来维护操作序列，`list` 的首元素，一定满足这个条件：在容量满了之后，每次操作之后的首元素一定是可以删除的元素，因此在每次 `put` 和 `get` 操作完成以后，都需要对满足条件的 `key` 值进行维护，维护在 `list` 链表中。
- 另一种是上一种方法的改进版本，方法一种最浪费时间的就是维护 `List` 操作，因此直接在每次插入新元素时，将地址和 `key` 值一同存放在 `hashmap` 中，然后 `maintain` 操作可以在 `O(1)` 时间内完成。

## 题目 147
一种方法，设计思路，首先构建一个值为 `INT_MIN` 的人造表头，将表头连接至 `head`，所有循环都从人造表头开始，在插入排序过程中，使用如下变量 `InsertIre` 为插入排序迭代器，`InsertEnd` 为插入排序停止位，每次外部循环需要维护好 `null` 指针的位置，`InsertNode` 为当前待插入的节点位置，`temp` 为每次外部循环找到的，下一个需要插入排序的位置。使用两个 `while` 完成插入排序。

## 题目 148
两种方法：
- 一种使用归并排序，具体参考已提交的某人的答案，非常完美和工整。
- 另一种使用快速排序，但是这里有一个 `tricky point`。就是一般的基于数组的快排只划归 2 个子类，即小于和大于等于，这里应该划归 3 个子类，即小于，等于和大于，原因在于链表没有办法像数组一样，获得非常随机的 `povit value`。

## 题目 149
一种方法，直接锚定基点，计算斜率，遍历迭代循环，得到结果，`ez` 问题，不属于 `hard` 难度。忠告，不要乱用 `abs`！

## 题目 150
一种方法，直接使用栈，然后按照规律 `push` 和 `pop` 即可得到结果。

## 题目 151
两种方法：
- 一种直接使用 `stack` 数据结构，将分离好的 `word` 直接写入 `stack` 中，然后挨个弹出生成即可。
- 另一种使用 `ssstream`，时间和空间都非常高，所以不推荐使用。

## 题目 152
两种方法：
- 一种使用自底向上的 `DP` 法，思路在于对于每一个新加入的元素，将这个元素累乘之前的每个元素，然后和 `DP` 比较，找到最大的赋值给这个新的 `DP[i]`，得到结果，但是时间复杂度会非常糟糕，面对输入序列含有大量 `1`，`-1` 的情况。
- 另一种针对题干条件，是一个整数的输入序列，这意味着唯一影响最终结果的元素只可能是负号，只要输入的是正数，那么最大值结果一定是乘上这个正数，但是如果输入的是负数，那么最大值结果就变成之前的最小值乘上这个负数，所以考虑到这里，在原有基础上维护两个 `int` 变量即可，`pre_max` 用于存储之前存在的最大值，`pre_min` 用于存储之前存在的最小值，然后每次更新就可以得到最终结果。

## 题目 153
一种方法，二分查找而已，唯一 `tricky` 的点在于我比较的是 `start+1<end`，这样最后出循环只需要比较 `start` 和 `end` 中的较大者即可。

## 题目 154
一种方法，二分查找，同上方法，但是由于存在了重复数，因此在每次做二分查找之前，先确认中间点是否是重复的，有重复的就一直往两边搜索，直到找到不重复的，如果搜索到了尽头都还是重复，那么就相应的改编 `start` 和 `end` 的值。这道题的查找核心其实不在于 `min`，而在于转折点，最小值一定存在于转折点，首位置，末位置这三者中。

## 题目 155
两种方法：
- 一种直接使用 `list+哈希表` 模式，每次稳定存储最小值，同时进行维护，但是忽略了本题是堆栈的特征，复杂度糟糕。
- 另一种根据堆栈特征我们可以知道，对于每一次输入，我们都可以判定一次最小值，然后将最小值放入新的 `min_store` 堆栈中，这样哪怕是重复弹出相等的元素，或者该最小值被弹出，同样可以根据 `min_store` 找到次级最大值。

## 题目 160
一种方法，赛马法进阶版，没有圆，但是我们可以创造圆，将尾部和 `headB` 连接起来，本题就等效于 142 号题目。

## 题目 162
两种方法：
- 一种线性扫描，直接从头扫描到尾巴。
- 另一种二分查找，具体看题目 `solution` 中的解答，二分查找可以找一个数组中的峰值也是我没想到的。