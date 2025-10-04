# Binary Tree Traversal
- Binary Tree Traversal mean visiting every nodes in the tree.
- Depending what order visit nodes, traversal type is divided.
- Mainly Binary Tree Traversal is divided **preorder**, **inorder**, **postorder**.
- Depending situation, using traversal is changed. For instance, We can't know entire folder size, if we don't know sub-folder size.

## Preorder Traversal
- Preorder Traversal is visiting node from middle to the left to the right.
- V(Root) ➔ L(Left) ➔ R(Right)
- Example
    - ![Source: https://medium.com/@GeneHFang/algorithm-talk-day-4-depth-first-tree-traversal-572f6c88475b](https://miro.medium.com/v2/resize:fit:720/format:webp/1*kjSfOuibHa-iZ_czyjT14g.png)
    

## Inorder Traversal
- Inorder Traversal is vsiting node from left to the middle to the right.
- L(Left) ➔ V(Root) ➔ R(Right)
- Example
    - ![Source: https://medium.com/@GeneHFang/algorithm-talk-day-4-depth-first-tree-traversal-572f6c88475b](https://miro.medium.com/v2/resize:fit:720/format:webp/1*YwlYJeCQ1-_bfX0kKOlDag.png)

## Postorder Traversal
- Postorder Traversal is visiting node from left to the right to the middle.
- L(Left) ➔ R(Right) ➔ V(Root)
- Example
    - ![Source: https://medium.com/@GeneHFang/algorithm-talk-day-4-depth-first-tree-traversal-572f6c88475b](https://miro.medium.com/v2/resize:fit:720/format:webp/1*O1xtjU8FRbMfAPTLl7wDfA.png)

## Level Traversal (BFS)
- Level Traversal is a little special.
- Level Traversal is known as BFS(Breadth-first search) to people.
- Level Traversal is visiting node from top level's left and then continue according level.
- To do Level Traversal, implement by using queue.
- Example
    - ![Source: https://inarizuuuushi.hatenablog.com/entry/2022/10/31/090000](https://cdn-ak.f.st-hatena.com/images/fotolife/i/inarizuuuushi/20220904/20220904210200.png)