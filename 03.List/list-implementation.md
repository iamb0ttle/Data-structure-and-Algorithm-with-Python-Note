# List implementation with Python
- In Python, List can be implemented by many way. The things that we will implement are Singly-Linked List and Doubly-Linked List.These Lists can be implemented with Array, but it has many restrictions and problems. So we only deal ways that implemented by non-contiguous.
- List operations:
    - `append(e)`: Adds a single element `e` to the end of the list.
    - `extend(lst)`: Adds all elements from another list `lst` to the end of the list.
    - `count(e)`: Returns the number of times element `e` appears in the list.
    - `index(e, [start], [end])`: Returns the index of the first occurrence of element `e`. You can optionally specify a `start` and `end` index to search within a slice.
    - `insert(pos, e)`: Inserts an element `e` at a specific position `pos`.
    - `pop(pos)`: Removes and returns the element at a specific position `pos`.
    - `pop()`: Removes and returns the last element of the list.
    - `remove(e)`: Removes the first occurrence of element `e` from the list.
    - `reverse()`: Reverses the order of the elements in the list in-place.
    - `sort([key], [reverse])`: Sorts the elements of the list in-place. You can optionally specify a `key` function for custom sorting and set `reverse=True` for descending order.

## Self implement by writing code.
We can implement List by wiriting code directly.

### Singly-Linked List
```py
# Step 1: Define the Node class
class Node:
    """
    A helper class representing a single node in a singly-linked list.
    """
    def __init__(self, data=None):
        """
        Initializes a Node.
        :param data: The data or element to be stored in the node.
        """
        self.data = data
        self.next = None

# Step 2: Define the SinglyLinkedList class
class SinglyLinkedList:
    """
    A class implementing a Singly-Linked List data structure with
    various list-like operations.
    """
    def __init__(self, data=None):
        """
        Initializes the SinglyLinkedList.
        :param data: An optional iterable to populate the list with initial data.
        """
        self.head = None
        self.tail = None
        self.size = 0
        if data is not None:
            for item in data:
                self.append(item)

    def __len__(self):
        """Returns the number of elements in the list."""
        return self.size

    def __str__(self):
        """Returns a string representation of the list."""
        elements = []
        current = self.head
        while current:
            elements.append(repr(current.data))
            current = current.next
        return f"[{', '.join(elements)}]"

    def __repr__(self):
        """Returns the official string representation of the list."""
        return f"SinglyLinkedList({self.__str__()})"

    def __iter__(self):
        """Allows iteration over the list's elements."""
        current = self.head
        while current:
            yield current.data
            current = current.next

    def _get_node(self, index):
        """Private helper to get the node at a specific index."""
        if not 0 <= index < self.size:
            raise IndexError("list index out of range")
        current = self.head
        for _ in range(index):
            current = current.next
        return current

    def append(self, e):
        """Adds a single element `e` to the end of the list."""
        new_node = Node(e)
        if self.head is None: # If the list is empty
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node
            self.tail = new_node
        self.size += 1

    def extend(self, lst):
        """Adds all elements from an iterable `lst` to the end of the list."""
        for item in lst:
            self.append(item)

    def count(self, e):
        """Returns the number of times element `e` appears in the list."""
        count = 0
        current = self.head
        while current:
            if current.data == e:
                count += 1
            current = current.next
        return count

    def index(self, e, start=0, end=None):
        """
        Returns the index of the first occurrence of element `e`.
        Raises ValueError if e is not in the list.
        """
        if end is None:
            end = self.size
        
        # Handle negative slicing like Python's list
        if start < 0:
            start = max(0, self.size + start)
        if end < 0:
            end = max(0, self.size + end)

        current = self.head
        for i in range(self.size):
            if i >= start and i < end:
                if current.data == e:
                    return i
            if i >= end:
                break
            current = current.next
        
        raise ValueError(f"{e} is not in list")

    def insert(self, pos, e):
        """Inserts an element `e` at a specific position `pos`."""
        if pos <= 0:
            new_node = Node(e)
            new_node.next = self.head
            self.head = new_node
            if self.size == 0: # If list was empty, new node is also the tail
                self.tail = new_node
        elif pos >= self.size:
            self.append(e)
            return # append already increments size
        else:
            prev_node = self._get_node(pos - 1)
            new_node = Node(e)
            new_node.next = prev_node.next
            prev_node.next = new_node
        
        self.size += 1

    def pop(self, pos=None):
        """
        Removes and returns the element at a specific position `pos`.
        If pos is not specified, removes and returns the last element.
        """
        if self.size == 0:
            raise IndexError("pop from empty list")
        
        if pos is None:
            pos = self.size - 1

        if not 0 <= pos < self.size:
            raise IndexError("list index out of range")

        if pos == 0:
            popped_data = self.head.data
            self.head = self.head.next
            if self.size == 1: # If list becomes empty
                self.tail = None
        else:
            prev_node = self._get_node(pos - 1)
            node_to_pop = prev_node.next
            popped_data = node_to_pop.data
            prev_node.next = node_to_pop.next
            if pos == self.size - 1: # If we are popping the tail
                self.tail = prev_node
        
        self.size -= 1
        return popped_data

    def remove(self, e):
        """Removes the first occurrence of element `e` from the list."""
        if self.size == 0:
            raise ValueError(f"{e} not in list")

        if self.head.data == e:
            self.pop(0)
            return

        prev_node = self.head
        current_node = self.head.next
        while current_node:
            if current_node.data == e:
                prev_node.next = current_node.next
                if current_node == self.tail: # Update tail if last element is removed
                    self.tail = prev_node
                self.size -= 1
                return
            prev_node = current_node
            current_node = current_node.next
            
        raise ValueError(f"{e} not in list")

    def reverse(self):
        """Reverses the order of the elements in the list in-place."""
        if self.size <= 1:
            return
            
        prev_node = None
        current_node = self.head
        self.tail = self.head # The old head becomes the new tail
        
        while current_node:
            next_node = current_node.next # Store next node
            current_node.next = prev_node # Reverse the link
            
            # Move pointers one position ahead
            prev_node = current_node
            current_node = next_node
        
        self.head = prev_node # The old last node becomes the new head

    def sort(self, key=None, reverse=False):
        """
        Sorts the elements of the list in-place.
        Note: This implementation is not the most efficient for a linked list.
        It converts to a Python list, sorts it, and then rebuilds the data.
        """
        if self.size <= 1:
            return
            
        # 1. Extract all data into a standard Python list
        elements = list(self)
        
        # 2. Use Python's built-in sort
        elements.sort(key=key, reverse=reverse)
        
        # 3. Re-populate the linked list with the sorted data
        current = self.head
        for elem in elements:
            current.data = elem
            current = current.next
```

### Doubly-Linked List
```py
# Step 1: Define the Node class for a Doubly-Linked List
class Node:
    """
    A helper class representing a single node in a doubly-linked list.
    """
    def __init__(self, data=None):
        """
        Initializes a Node.
        :param data: The data or element to be stored in the node.
        """
        self.data = data
        self.next = None
        self.prev = None

# Step 2: Define the DoublyLinkedList class
class DoublyLinkedList:
    """
    A class implementing a Doubly-Linked List data structure with
    various list-like operations.
    """
    def __init__(self, data=None):
        """
        Initializes the DoublyLinkedList.
        :param data: An optional iterable to populate the list with initial data.
        """
        self.head = None
        self.tail = None
        self.size = 0
        if data is not None:
            for item in data:
                self.append(item)

    def __len__(self):
        """Returns the number of elements in the list."""
        return self.size

    def __str__(self):
        """Returns a string representation of the list."""
        elements = []
        current = self.head
        while current:
            elements.append(repr(current.data))
            current = current.next
        return f"[{', '.join(elements)}]"

    def __repr__(self):
        """Returns the official string representation of the list."""
        return f"DoublyLinkedList({self.__str__()})"

    def __iter__(self):
        """Allows forward iteration over the list's elements."""
        current = self.head
        while current:
            yield current.data
            current = current.next

    def __reversed__(self):
        """Allows reverse iteration over the list's elements."""
        current = self.tail
        while current:
            yield current.data
            current = current.prev

    def _get_node(self, index):
        """
        Private helper to get the node at a specific index.
        Optimized to traverse from the nearest end (head or tail).
        """
        if not 0 <= index < self.size:
            raise IndexError("list index out of range")
        
        # Optimization: if index is in the second half, start from the tail
        if index > self.size // 2:
            current = self.tail
            for _ in range(self.size - 1, index, -1):
                current = current.prev
        else:
            current = self.head
            for _ in range(index):
                current = current.next
        return current

    def append(self, e):
        """Adds a single element `e` to the end of the list."""
        new_node = Node(e)
        if self.head is None:  # If the list is empty
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node
            new_node.prev = self.tail
            self.tail = new_node
        self.size += 1

    def extend(self, lst):
        """Adds all elements from an iterable `lst` to the end of the list."""
        for item in lst:
            self.append(item)

    def count(self, e):
        """Returns the number of times element `e` appears in the list."""
        count = 0
        for item in self:  # Using the iterator is clean here
            if item == e:
                count += 1
        return count

    def index(self, e, start=0, end=None):
        """
        Returns the index of the first occurrence of element `e`.
        Raises ValueError if e is not in the list.
        """
        if end is None:
            end = self.size
        
        if start < 0: start = max(0, self.size + start)
        if end < 0: end = max(0, self.size + end)

        current = self.head
        for i in range(self.size):
            if i >= start and i < end:
                if current.data == e:
                    return i
            if i >= end:
                break
            current = current.next
        
        raise ValueError(f"{e} is not in list")

    def insert(self, pos, e):
        """Inserts an element `e` at a specific position `pos`."""
        if pos <= 0: # Insert at the beginning
            new_node = Node(e)
            if self.head:
                new_node.next = self.head
                self.head.prev = new_node
            else: # list was empty
                self.tail = new_node
            self.head = new_node
            self.size += 1
        elif pos >= self.size: # Insert at the end
            self.append(e)
        else: # Insert in the middle
            next_node = self._get_node(pos)
            prev_node = next_node.prev
            new_node = Node(e)
            
            # Link new_node with its neighbors
            new_node.prev = prev_node
            new_node.next = next_node
            
            # Update neighbors to point to new_node
            prev_node.next = new_node
            next_node.prev = new_node
            self.size += 1

    def pop(self, pos=None):
        """
        Removes and returns the element at `pos`.
        If pos is not specified, removes and returns the last element.
        """
        if self.size == 0:
            raise IndexError("pop from empty list")
        
        if pos is None:
            pos = self.size - 1

        if not 0 <= pos < self.size:
            raise IndexError("list index out of range")
        
        node_to_pop = self._get_node(pos)
        popped_data = node_to_pop.data

        if self.size == 1:
            self.head = None
            self.tail = None
        elif node_to_pop == self.head:
            self.head = self.head.next
            self.head.prev = None
        elif node_to_pop == self.tail:
            self.tail = self.tail.prev
            self.tail.next = None
        else:
            prev_node = node_to_pop.prev
            next_node = node_to_pop.next
            prev_node.next = next_node
            next_node.prev = prev_node
        
        self.size -= 1
        return popped_data

    def remove(self, e):
        """Removes the first occurrence of element `e` from the list."""
        current = self.head
        while current:
            if current.data == e:
                # Found the node to remove, now handle pointer updates
                if current == self.head:
                    self.pop(0)
                elif current == self.tail:
                    self.pop()
                else:
                    current.prev.next = current.next
                    current.next.prev = current.prev
                    self.size -= 1
                return
            current = current.next
        
        raise ValueError(f"{e} not in list")

    def reverse(self):
        """Reverses the order of the elements in the list in-place."""
        if self.size <= 1:
            return

        current = self.head
        while current:
            # Swap the prev and next pointers of the current node
            current.prev, current.next = current.next, current.prev
            # Move to the next node in the original list (which is now current.prev)
            current = current.prev
        
        # Swap the head and tail pointers for the entire list
        self.head, self.tail = self.tail, self.head


    def sort(self, key=None, reverse=False):
        """
        Sorts the elements of the list in-place.
        This method converts to a Python list, sorts it, then rebuilds the data.
        """
        if self.size <= 1:
            return
            
        elements = list(self)
        elements.sort(key=key, reverse=reverse)
        
        current = self.head
        for elem in elements:
            current.data = elem
            current = current.next
```

## Use Python Primary Features for List
Python data structure docs: [docs.python.org](https://docs.python.org/3/tutorial/datastructures.html)
- `list`: most useful and powerful list class of python. 
- `deque`: deque is implemented by doubly-linked list internally. 