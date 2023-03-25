---
title: DFS——深度优先（Depth First Search）
date: 2023-03-25 22:19:35
tags:
categories: 算法
---

## DFS——深度优先（Depth First Search）

### 思想：

属于图算法的一种，也是对一个连通图进行遍历的算法。从一个顶点v开始，沿着一条路线一直走到底，如果发现不能到达目标，那就返回到走不通节点的上一个节点，然后尝试从另一条路开始走到底，每个节点只可以访问一次。这种尽量往深处走的概念就是DFS的概念

### 基本思路：

（1）访问顶点v

（2）依次从v的未被访问的邻接点出发，对图进行深度优先遍历；直至图中和v有路径相通的顶点都被访问

（3）若此时图中尚有顶点未被访问，则从一个未被访问的顶点出发，重新进行深度优先遍历，直到图中所有顶点均被访问过为止

### DFS特点以及和BFS的比较

DFS可以用递归来写，也可以用栈来写。

DFS在回溯时要取消原先的标记，而BFS不存在回溯也就不存在取消标记这一问题。(即避免节点出现在别的搜索路径中)

DFS难以寻找最优解，仅仅只能寻找有解。其优点就是相比BFS内存消耗小


### 题目

#### 第一题
#### [剑指 Offer 12. 矩阵中的路径](https://leetcode.cn/problems/ju-zhen-zhong-de-lu-jing-lcof/)

给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 

例如，在下面的 3×4 的矩阵中包含单词 "ABCCED"（单词中的字母已标出）。

![img](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

示例 1：

输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
示例 2：

输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false

```js
/**
 * @param {character[][]} board
 * @param {string} word
 * @return {boolean}
 */
const exist = (board, word) => {
      let m = board.length
      let n = board[0].length
    const dfs = (i, j, index) => {
        // 越界、或者字符不匹配
        if (i < 0 || i >= m || j < 0 || j >= n || board[i][j] !== word[index]) return false;
        // 索引等于单词长度-1，说明全匹配上了
        if (index === word.length - 1) return true;
        // 保存当前字符
        const temp = board[i][j];
        // 将当前字符设置为空，防止四个方向dfs再次遍历到
        board[i][j] = '';
        // 四个方向遍历
        const res =
            dfs(i + 1, j, index + 1) ||
            dfs(i, j + 1, index + 1) ||
            dfs(i - 1, j, index + 1) ||
            dfs(i, j - 1, index + 1);
        // 恢复当前字符
        board[i][j] = temp;
        return res;
    };

    // 从第一个匹配的字符处开始dfs
    for (let i = 0; i < m; i++) {
        for (let j = 0; j < n; j++) {
            if (dfs(i, j, 0)) return true;
        }
    }

    return false;
};

```


#### 第二题

#### 面试题13. 机器人的运动范围[https://leetcode.cn/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/]

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

 

示例 1：

输入：m = 2, n = 3, k = 1
输出：3
示例 2：

输入：m = 3, n = 1, k = 0
输出：1
提示：

1 <= n,m <= 100
0 <= k <= 20

```js
/**
 * @param {number} m
 * @param {number} n
 * @param {number} k
 * @return {number}
 */

var movingCount = function (m, n, k) {
    function dfs(i, j, m, n, k, visited) {
        // 基本判断 + 判断是否走过这条路
        if (i >= m || i < 0 || j >= n || j < 0 || visited[i][j]) {
            return false;
        }

        // 没有走过，先标记，在判断是否符合题意
        visited[i][j] = true;

        // 求和
        let sum = i % 10 + j % 10 + Math.floor(i / 10) + Math.floor(j / 10);
        if (sum > k) return false;

        // 符合题意数量+1
        res++;

        // 直接大范围撒网
        dfs(i + 1, j, m, n, k, visited);
        dfs(i, j + 1, m, n, k, visited);
    }

    let res = 0;
    // 用来做标记的数组
    let visited = new Array(m).fill(0).map(() => new Array(n));
    dfs(0, 0, m, n, k, visited);

    return res;
};


```
