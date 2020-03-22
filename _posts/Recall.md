---
title: 回溯算法
description: 数据结构
date: 2020-01-01 00:00:00 +08:00
tags: 数据结构
category: 数据结构
---

# 回溯算法
复杂度较高, 指数级, 适合用递归来解决

### 算法应用
深度优先搜索、八皇后、0-1 背包问题、图的着色、旅行商问题、数独、全排列、正则表达式匹配等。

### 八皇后
``` java
//全局或成员变量,下标表示行,值表示queen存储在哪一列
int[] result = new int[8];

public void cal8queens(int row) { 
    // 8个棋子都放置好了, 打印结果
    if (row == 8) { 
        printQueens(result);
        return; // 8行棋子都放好了, 结束
    }

    // 每一行都有8中放法
    for (int column = 0; column < 8; ++column) { 
        if (isOk(row, column)) 
        { 
            // 有些放法不满足要求
            // 第row行的棋子放到了column列
            result[row] = column; 
            // 考察下一行
            cal8queens(row+1); 
        }
    }
}

//判断row行column列放置是否合适
private boolean isOk(int row, int column) {
    int leftup = column - 1, rightup = column + 1;

    // 逐行往上考察每一行
    for (int i = row-1; i >= 0; --i) 
    { 
        // 第i行的column列有棋子吗？
        if (result[i] == column) return false; 
        // 考察左上对角线：第i行leftup列有棋子吗？
        if (leftup >= 0) 
        { 
            if (result[i] == leftup) return false;
        }

        // 考察右上对角线：第i行rightup列有棋子吗？
        if (rightup < 8) 
        { 
            if (result[i] == rightup) return false;
        }
        
        --leftup; ++rightup;
    }

    return true;
}

// 输出二维矩阵
private void printQueens(int[] result) { 
    for (int row = 0; row < 8; ++row) 
    {
        for (int column = 0; column < 8; ++column) 
        {
            if (result[row] == column) 
                System.out.print("Q ");
            else 
                System.out.print("* ");
        }
        System.out.println();
    }
    System.out.println();
}
```

判断是否在一条斜线上还有更加简便的做法，就是如果行互减的绝对值等于列互减的绝对值，那么就是在一条斜线上的。
``` java
if (Math.abs(row - i) == Math.abs(column - result[i])) 
{
    return false;
}
```