# Binary Tree
- Binary Tree is Tree data structure that is restricted every nodes to has only two children nodes.
- Every nodes degree is less than 2.
- Also Binary Tree exist many form according its principle. 
- Representative Binary Tree: Full Binary Tree, Complete Binary Tree, Height-Balanced Binary Tree, Skewed Binary Tree.

## Full Binary Tree & Complete Binary Tree
![Source: https://comsciguide.blogspot.com/2015/08/differences-between-complete-balanced.html](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj3IeOA38U6WckHLREIH3uC9Yyahf9DDxM3AQ64Hj6eT9E_AAUMphgiq-fpz-8ea2bzfEgBnj6eKrJ6kG30d-GfwFd7ZMimfTwPbck4eIfdp9DHVnnch_Jeh6UC6dmBrwqAwdAV71anSzs/s640/types-of-binary-tree.jpg)

- **Full Binary Tree**
    - Full Binary Tree is Binary Tree that filled maximum nodes in every level.
    - If tree's height is *k*,  the total number of nodes is 2^*k* - 1.
- **Complete Binary Tree**
    - Complete Binary Tree is Binary Tree that filled maximum nodes until *k*-1 level, and *k* level nodes are filled from left.
    - Full Binary Tree is Complete Binary Tree, but Complete Binary Tree is not Full binary Tree.

## Height-Balanced Binary Tree & Skewed Binary Tree
![Source: https://codepumpkin.com/binary-tree-types-introduction/](https://codepumpkin.com/wp-content/uploads/2018/08/Balanced_Binary_Tree.jpg)

- **Height-Balanced Binary Tree**
    - Height-Balanced Binary Tree is Binary Tree that left and right sub tree's degree difference is less than 1 in every nodes.
    - If tree left and right sub tree's degree difference is over than 1, we can't call that tree is Height-Balanced Binary Tree.

![Source: https://findtodaysnotes.wordpress.com/binary-tree/](https://www.gatevidyalay.com/wp-content/uploads/2018/07/Skewed-Binary-Tree-Example.png)

- **Skewed Binary Tree**
    - Skewed Binary Tree is Binary Tree that only has child node on only one direction.
    - If nodes only exist right, we call Right-Skewed Binary Tree.