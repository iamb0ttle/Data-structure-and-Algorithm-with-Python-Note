# Tree Implementation
- Because Tree is very abstract structure, Tree exist very many form and style by its components.
- So, to implement tree, we have to know tree's constraints and principle.
- In this document, we deal most generally form tree, **General Tree**(Tree that doesn't have constraints about child node counts). 

![https://www.chegg.com/homework-help/questions-and-answers/represent-type-n-array-tree-using-left-child-right-sibling-lcrs-trees-node-m-lcrs-tree-sto-q102266642](https://media.cheggcdn.com/media/0f4/0f4f9713-4013-4674-8a6b-ff62f92ae0c1/phpBKFoqI)

## N-Link
- This is a way that allows a node with N child nodes to have N links.
- It is very simple way, but every node's link counts can different. 

## Left-Child, Right-Sibling 
- This is a way that make node's right link as child pointer and node's left link as sibling pointer. 
- It has advantage that every node's linke count is same.
- It has disadvantage that we may visit many node than *N-Link* way to find specific node.