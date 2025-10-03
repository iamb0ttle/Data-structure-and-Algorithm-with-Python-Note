# Stack Implementation with Python
- We can implement Stack structure with Python.
- Python doesn't support Stack as primary data structure. So to use Stack, we have to implement code or use primary python features(list append, module, etc.).
- Stack primary operations:
    - `push(e)`: push element(e) in Stack.
    - `pop()`: removal one top element in Stack.
    - `isFull()`: return `True` or `False` depending on whether it is full or not.
    - `isEmpty()`: return `True` or `False` depending on whether it is empty or not.
    - `top()`: return top element of Stack. 
    - `size()` return Stack size.

# Implementation with Code
There is many way to implement Stack by Python code.

### Contiguous Representation - Array(List) based & Procedural

```py
# A constant representing the maximum size of the stack.
MAX_SIZE = 5

# A list to store the elements of the stack.
stack = []

def isFull():
    """
    Check if the stack is full.
    Returns:
        bool: True if the stack has reached its maximum size, False otherwise.
    """
    return len(stack) == MAX_SIZE

def isEmpty():
    """
    Check if the stack is empty.
    Returns:
        bool: True if the stack contains no elements, False otherwise.
    """
    return len(stack) == 0

def push(e):
    """
    Add an element to the top of the stack.
    Args:
        e: The element to be added to the stack.
    """
    if isFull():
        print("Stack is full. Cannot push element.")
    else:
        stack.append(e)
        print(f"Pushed element: {e}")

def pop():
    """
    Remove and return the top element of the stack.
    Returns:
        The element at the top of the stack, or None if the stack is empty.
    """
    if isEmpty():
        print("Stack is empty. Cannot pop element.")
        return None
    else:
        element = stack.pop()
        print(f"Popped element: {element}")
        return element

def top():
    """
    Return the top element of the stack without removing it.
    Returns:
        The element at the top of the stack, or None if the stack is empty.
    """
    if isEmpty():
        print("Stack is empty.")
        return None
    else:
        return stack[-1]

def size():
    """
    Return the number of elements in the stack.
    Returns:
        int: The number of elements in the stack.
    """
    return len(stack)
```

### Non-contiguous Representation - Node based & Objective
```py
# Node class to represent each element in the stack
class Node:
    def __init__(self, data):
        self.data = data  # The data value of the node
        self.next = None  # Reference to the next node in the stack

# A global variable to always point to the top node of the stack.
# Initially, the stack is empty, so it points to None.
top_node = None

def isFull():
    """
    Check if the stack is full.
    In a node-based implementation, the stack is theoretically never full
    unless the system runs out of memory.
    Returns:
        bool: Always returns False.
    """
    return False

def isEmpty():
    """
    Check if the stack is empty.
    Returns:
        bool: True if the top_node is None, False otherwise.
    """
    return top_node is None

def push(e):
    """
    Add an element to the top of the stack.
    Args:
        e: The element to be added to the stack.
    """
    global top_node
    # Create a new node with the given data
    new_node = Node(e)
    # The new node's 'next' points to the current top node
    new_node.next = top_node
    # The new node becomes the new top of the stack
    top_node = new_node
    print(f"Pushed element: {e}")

def pop():
    """
    Remove and return the top element of the stack.
    Returns:
        The data of the top element, or None if the stack is empty.
    """
    global top_node
    if isEmpty():
        print("Stack is empty. Cannot pop element.")
        return None
    else:
        # Get the data from the top node
        popped_data = top_node.data
        # The new top is the next node in the sequence
        top_node = top_node.next
        print(f"Popped element: {popped_data}")
        return popped_data

def top():
    """
    Return the top element of the stack without removing it.
    Returns:
        The data of the top element, or None if the stack is empty.
    """
    if isEmpty():
        print("Stack is empty.")
        return None
    else:
        return top_node.data

def size():
    """
    Return the number of elements in the stack.
    Returns:
        int: The number of elements in the stack.
    """
    count = 0
    current_node = top_node
    # Traverse the linked list from the top and count each node
    while current_node is not None:
        count += 1
        current_node = current_node.next
    return count
```

These two example codes are most use case.  
To implement Stack, you have to choice one in each two options.
1. **Contiguous vs Non-contiguous**: Memory location. Cotiguouse can use **index**. Non-contiguous can use **pointer**.
2. **Procedural vs Objective**: Procedural programming separates data and functions, while object -oriented programming ties two classes to increase data protection and reuse.

In Python, python's array(list) size is variable. But other language's array(C, C++, etc.) is not. So if you want to set your stack size is variable, Non-contiguous implementation will be good choice.

Anyway, whatever you implementation way, stack insertion and removal operate by *O(1)*.

# Use Python Primary Features
For practical purposes, you rarely need to implement a stack from scratch in Python. You can use Python's powerful built-in features directly.

### 1. Using a list as a Stack (Most Common)
Python's `list` type is the simplest and most common way to use a stack. Its methods `append()` and `pop()` function exactly as stack operations.

- `push(e)` ➔ `list.append(e)`
- `pop()` ➔ `list.pop()`
- `top()` ➔ `list[-1]`
- `isEmpty()` ➔ `len(list) == 0 or simply not list`
- `size()` ➔ `len(list)`

### 2. Using `collections.deque` (More Performant)
The deque (double-ended queue) object is designed for fast appends and pops from both ends. While a list is generally fast enough, deque can be more performant for building stacks and queues, especially when dealing with a large number of operations. Its interface for stack operations is identical to a list.
```py
from collections import deque

stack = deque()
stack.append(10)
stack.append(20)
print(f"Current stack: {stack}")

element = stack.pop()
print(f"Popped element: {element}")
```

### 3. Using queue.LifoQueue (For Concurrency)
This is a specialized stack for use in multi-threaded programming. It is thread-safe, meaning multiple threads can push and pop items without corrupting the data.

- `push(e)` ➔ `LifoQueue.put(e)`
- `pop()` ➔ `LifoQueue.get()`

```py
from queue import LifoQueue

# Create a stack with a max size of 5
stack = LifoQueue(maxsize=5)

stack.put(10) # Push 10
stack.put(20) # Push 20

element = stack.get() # Pop 20
print(f"Popped element: {element}")
```