# Binary Tree implementation
- Binary Tree can be implemented by two major way.
- One is using Array, the other is using Node(Class).

## Using Array
- With array, we can implement binary tree easily.
- Because binary tree that is implemented by array has some rule like this:
    - The root of the tree is stored at index `0`.
    - For any node at index `i`:
    - Its left child is at index `2 * i + 1`.
    - Its right child is at index `2 * i + 2`.
    - We will use None to indicate that a node does not exist at a particular position in the array.
- So array implementation is very easy, but it has some disadvantages. For instance, if our tree has many empty node each level, our tree will waste memory.

```py
class ArrayBinaryTree:
    """
    A class to represent a binary tree using a Python list (array).
    """

    def __init__(self, size):
        """
        Initializes the binary tree.
        The tree is represented as a list of a given size, filled with None.
        
        :param size: The maximum number of nodes the tree can hold.
        """
        # Create a list of 'size' elements, all initialized to None.
        # This list will store the tree nodes.
        self.tree = [None] * size
        # Store the maximum size for boundary checks.
        self.size = size

    def set_root(self, value):
        """
        Sets the value of the root node.
        The root is always at index 0.

        :param value: The value to be stored in the root node.
        """
        # Check if the tree is not empty.
        if self.size > 0:
            # Set the first element of the list as the root.
            self.tree[0] = value
        else:
            print("Error: Tree size is 0. Cannot set root.")

    def set_left(self, parent_index, value):
        """
        Adds a left child to a given parent node.

        :param parent_index: The index of the parent node.
        :param value: The value of the left child to be added.
        """
        # Calculate the index for the left child.
        left_child_index = 2 * parent_index + 1
        
        # Check if the calculated index is within the bounds of the list.
        if left_child_index < self.size:
            # Check if the parent node exists.
            if self.tree[parent_index] is not None:
                # Set the value for the left child.
                self.tree[left_child_index] = value
            else:
                print(f"Error: Cannot set left child because parent at index {parent_index} is None.")
        else:
            print(f"Error: Left child index {left_child_index} is out of bounds.")

    def set_right(self, parent_index, value):
        """
        Adds a right child to a given parent node.

        :param parent_index: The index of the parent node.
        :param value: The value of the right child to be added.
        """
        # Calculate the index for the right child.
        right_child_index = 2 * parent_index + 2

        # Check if the calculated index is within the bounds of the list.
        if right_child_index < self.size:
            # Check if the parent node exists.
            if self.tree[parent_index] is not None:
                # Set the value for the right child.
                self.tree[right_child_index] = value
            else:
                print(f"Error: Cannot set right child because parent at index {parent_index} is None.")
        else:
            print(f"Error: Right child index {right_child_index} is out of bounds.")
            
    def get_parent_index(self, child_index):
        """
        Returns the index of the parent of a node at a given index.

        :param child_index: The index of the child node.
        :return: The index of the parent node, or None if it's the root or index is invalid.
        """
        if child_index > 0 and child_index < self.size:
            return (child_index - 1) // 2
        return None

    def get_left_child_value(self, parent_index):
        """
        Returns the value of the left child of a node.

        :param parent_index: The index of the parent node.
        :return: The value of the left child, or None if it doesn't exist.
        """
        left_child_index = 2 * parent_index + 1
        if left_child_index < self.size:
            return self.tree[left_child_index]
        return None

    def get_right_child_value(self, parent_index):
        """
        Returns the value of the right child of a node.

        :param parent_index: The index of the parent node.
        :return: The value of the right child, or None if it doesn't exist.
        """
        right_child_index = 2 * parent_index + 2
        if right_child_index < self.size:
            return self.tree[right_child_index]
        return None

    def print_tree(self):
        """
        Prints the array representation of the tree.
        """
        # Loop through the list and print each element with its index.
        for i in range(self.size):
            if self.tree[i] is not None:
                print(f"Node at index {i}: {self.tree[i]}")
            else:
                print(f"Node at index {i}: None")
```

## Using Node(Class)
- With node class, we can solve the memory wasting problem when happens using array.
```py
class Node:
    """
    A class to represent a single node in a binary tree.
    """
    def __init__(self, value):
        """
        Initializes a new node.

        :param value: The data to be stored in the node.
        """
        self.value = value  # The value or data of the node
        self.left = None    # Reference to the left child node
        self.right = None   # Reference to the right child node

class BinaryTree:
    """
    A class to represent a binary tree structure using nodes.
    """
    def __init__(self, root_value=None):
        """
        Initializes the binary tree.
        
        :param root_value: The value of the root node. If provided, a root node is created.
        """
        # The root of the tree. It is None for an empty tree.
        if root_value is not None:
            self.root = Node(root_value)
        else:
            self.root = None

    # --- Traversal Methods ---
    # Traversal is the process of visiting (e.g., printing) each node in the tree.

    def print_preorder(self):
        """Public method to start pre-order traversal and print the result."""
        result = self._preorder_recursive(self.root, [])
        print("Pre-order Traversal:", " -> ".join(map(str, result)))

    def _preorder_recursive(self, node, traversal_list):
        """
        Helper method for pre-order traversal (Root -> Left -> Right).
        
        :param node: The current node to visit.
        :param traversal_list: A list to store the visited node values.
        :return: The list of visited node values.
        """
        if node:
            traversal_list.append(node.value)
            self._preorder_recursive(node.left, traversal_list)
            self._preorder_recursive(node.right, traversal_list)
        return traversal_list

    def print_inorder(self):
        """Public method to start in-order traversal and print the result."""
        result = self._inorder_recursive(self.root, [])
        print("In-order Traversal: ", " -> ".join(map(str, result)))

    def _inorder_recursive(self, node, traversal_list):
        """
        Helper method for in-order traversal (Left -> Root -> Right).
        
        :param node: The current node to visit.
        :param traversal_list: A list to store the visited node values.
        :return: The list of visited node values.
        """
        if node:
            self._inorder_recursive(node.left, traversal_list)
            traversal_list.append(node.value)
            self._inorder_recursive(node.right, traversal_list)
        return traversal_list

    def print_postorder(self):
        """Public method to start post-order traversal and print the result."""
        result = self._postorder_recursive(self.root, [])
        print("Post-order Traversal:", " -> ".join(map(str, result)))

    def _postorder_recursive(self, node, traversal_list):
        """
        Helper method for post-order traversal (Left -> Right -> Root).

        :param node: The current node to visit.
        :param traversal_list: A list to store the visited node values.
        :return: The list of visited node values.
        """
        if node:
            self._postorder_recursive(node.left, traversal_list)
            self._postorder_recursive(node.right, traversal_list)
            traversal_list.append(node.value)
        return traversal_list
```