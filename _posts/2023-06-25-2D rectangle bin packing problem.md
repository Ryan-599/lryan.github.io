---
layout: default
title:  "论文-A Thousand Ways to Pack the Bin"
date:   2023-06-24 23:38:00 +0800
categories: paper
---
<head>
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
</head>

<script> 
MathJax = {
  tex: {
    inlineMath: [['$', '$']],
    processEscapes: true
  }
};
</script>

# 目录

1. 二维装箱问题简介
2. 经典算法
   - Shelf算法
   - Guillotine算法
   - 最优矩形算法
   - Skyline算法
3. 其他问题

# 正文

1. 二维装箱问题简介  
   二维装箱问题是一个经典的组合优化问题。该问题需要求解将一个矩形序列$(R_1,R_2,...,R_n)$中的每个$R_i$尽可能地、互不重叠地放入一个长宽固定的二维矩形箱中。该问题被证明是一个NP-hard问题。
2. 经典算法
   - Shelf算法  
      Shelf算法是一种简单的装箱方法。首先将整个二维矩形箱从下到上分割成一层一层的货架（Shelf），在每一层上从左到右地放置矩形。由于是从下到上进行分割，所以最顶层往往是未使用的，可以对最顶层进行再次分割。而除了最顶层外，其他层的高度是固定的，这些层是封闭的，不能再进行改变。  
      在对一个矩形进行装箱时，Shelf算法将这个矩形放到哪一层，哪一层的哪个位置上依据于其自身的启发性函数。常见的Shelf启发性函数有：
      - Next Fit：对一个矩形进行装箱时，尝试将该矩形放入当前货架上，如果不能放入，则向上开辟新一层的货架。如果不能开辟新的货架，那么算法终止。
      - First Fit：对一个矩形进行装箱时，从下到上扫描一遍所有货架，选择第一个能装入该矩形的货架将其放入。
      - Best Width Fit：对一个矩形进行装箱时，从下到上扫描一遍所有货架，选择能装入该矩形的货架中，剩余可用宽度最小的那一个。
      - Best Height Fit：对一个矩形进行装箱时，从下到上扫描一遍所有货架，选择能装入该矩形的货架中，高度最小的那一个。
      - Best Area Fit：对一个矩形进行装箱时，从下到上扫描一遍所有货架，选择能装入该矩形的货架中，可用面积最小的那一个。
      - Worst Width Fit

      Waste-Map改善：使用Shelf算法进行装箱时，每一个货架上半部分的空间往往是空闲的。使用Guillotine算法记录并追踪每一层的空闲空间，对一个矩形进行装箱时，优先使用Guillotine算法将该矩形装入这些空闲空间中。如果不能装入空闲空间，则照常使用Shelf算法。

   - Guillotine算法  
      Guillotine算法是一种剪切的方法。它的基本原理是将一个空闲的矩形逐步分解成多个空闲的小矩形。分解的方法是先将空闲的矩形直接截去一个角，然后沿着截去的角的边，以垂直或水平的方法将剩余空间截成两个较小的空闲矩形。如下图所示：

      ![picture 1](..\_site\assets\images\d940acc30d06878a7cfece2248d7be4be01aa0b169597b10b0653d7c5601c7d1.png)  

      Guillotine算法维护一个空闲矩形列表${F_1,...,F_n}$，该列表实际上就是对箱中剩余空间的一个划分。初始时，该列表只有一个空闲矩形块，即箱本身。在对一个矩形进行装箱时，从列表中选取一个能装入该矩形的空闲矩形$F_i$并将该矩形放在$F_i$的左下角，进行上述的剪切操作，得到两个新的空闲矩形$F_i'$和$F_i''$并加入到列表中。

   - 最优矩形算法
   - Skyline算法
3. 