# Queue Implementation with Python
- To use queue in python, we can directly implement by writing code, or use python primary features(like modules).
- Queue has these operations:
    - `enqueue(e)`: insert element from `rear`.
    - `addFront(e)`: insert element from `front`. (If deque.)
    - `dequeue()`: remove element from `front`.
    - `deleteRear()`: remove element from `rear`. (If deque.)
    - `peek()`: return element of top(from `front`).
    - `getRear()`: return element of top(from `rear`). (If deque.)
    - `isFull()`: return True or False depending on whether it is full or not.
    - `isEmpty()`: return True or False depending on whether it is empty or not.
    - `size()`: return size of queue.

## Self implement by writing code.
We can implement queue by wiriting code directly.

### Queue
```py
class ClassicQueue:
    """
    An implementation of a classic, fixed-size queue using a list as a static array.
    This queue uses 'front' and 'rear' indices to manage its elements.
    It demonstrates the classic problem where the queue can become "full"
    even if there are empty slots at the beginning of the array after dequeue operations.
    """

    def __init__(self, capacity):
        """
        Initializes a fixed-size queue.
        Args:
            capacity (int): The maximum number of items the queue can hold.
        """
        self.capacity = capacity
        # Initialize an array of a fixed size with None values.
        self.items = [None] * capacity
        # 'front' points to the position just before the first item.
        self.front = -1
        # 'rear' points to the position of the last item.
        self.rear = -1

    def is_full(self):
        """
        Checks if the queue is full.
        The queue is full when the 'rear' index has reached the last position.
        Returns:
            bool: True if the queue is full, False otherwise.
        """
        return self.rear == self.capacity - 1

    def is_empty(self):
        """
        Checks if the queue is empty.
        The queue is empty when 'front' and 'rear' indices are the same.
        This signifies that all enqueued items have been dequeued.
        Returns:
            bool: True if the queue is empty, False otherwise.
        """
        return self.front == self.rear

    def enqueue(self, item):
        """
        Adds an item to the rear of the queue.
        Fails if the queue is already full (rear is at the end).
        Args:
            item: The item to be added.
        """
        if self.is_full():
            print("Error: Queue is full. Cannot enqueue new item.")
            return
        
        # Move 'rear' forward and then add the item.
        self.rear += 1
        self.items[self.rear] = item
        print(f"Enqueued {item} at index {self.rear}")

    def dequeue(self):
        """
        Removes and returns the item from the front of the queue.
        Returns:
            The item at the front of the queue, or None if the queue is empty.
        """
        if self.is_empty():
            print("Error: Queue is empty. Cannot dequeue.")
            return None
        
        # Move 'front' forward to "remove" the item.
        self.front += 1
        item_to_return = self.items[self.front]
        # Set the dequeued space to None to show it's no longer in the queue.
        self.items[self.front] = None 
        print(f"Dequeued {item_to_return} from index {self.front}")
        return item_to_return

    def peek(self):
        """
        Returns the item at the front of the queue without removing it.
        Returns:
            The item at the front, or None if the queue is empty.
        """
        if self.is_empty():
            print("Error: Queue is empty.")
            return None
        
        # The front item is at the index immediately after 'front'.
        return self.items[self.front + 1]
```

### Circular Queue
```py
class CircularQueue:
    """
    An implementation of a Circular Queue data structure using a fixed-size list.
    This queue overcomes the wasted space problem of a classic linear queue by
    allowing the indices to wrap around the end of the array to the beginning.
    """

    def __init__(self, capacity):
        """
        Initializes a fixed-size circular queue.
        Args:
            capacity (int): The maximum number of items the queue can hold.
        """
        self.capacity = capacity
        # Initialize an array of a fixed size with None values.
        self.items = [None] * capacity
        # 'front' points to the index of the first item.
        self.front = 0
        # 'rear' points to the index of the last item.
        self.rear = -1
        # 'size' tracks the current number of items in the queue.
        self.size = 0

    def is_empty(self):
        """
        Checks if the queue is empty.
        Returns:
            bool: True if the queue is empty, False otherwise.
        """
        return self.size == 0

    def is_full(self):
        """
        Checks if the queue is full.
        Returns:
            bool: True if the queue is full, False otherwise.
        """
        return self.size == self.capacity

    def enqueue(self, item):
        """
        Adds an item to the rear of the queue.
        If the rear reaches the end of the list, it wraps around to the beginning.
        Args:
            item: The item to be added.
        """
        if self.is_full():
            print("Error: Queue is full. Cannot enqueue new item.")
            return

        # Calculate the new rear index using the modulo operator for wrap-around.
        self.rear = (self.rear + 1) % self.capacity
        self.items[self.rear] = item
        self.size += 1
        print(f"Enqueued {item} at index {self.rear}")

    def dequeue(self):
        """
        Removes and returns the item from the front of the queue.
        If the front reaches the end of the list, it wraps around.
        Returns:
            The item at the front of the queue, or None if the queue is empty.
        """
        if self.is_empty():
            print("Error: Queue is empty. Cannot dequeue.")
            return None

        # Get the item from the front of the queue.
        item_to_return = self.items[self.front]
        # Set the dequeued space to None for clarity.
        self.items[self.front] = None
        
        # Calculate the new front index using the modulo operator.
        self.front = (self.front + 1) % self.capacity
        self.size -= 1
        print(f"Dequeued {item_to_return}")
        return item_to_return

    def peek(self):
        """
        Returns the item at the front of the queue without removing it.
        Returns:
            The item at the front, or None if the queue is empty.
        """
        if self.is_empty():
            print("Error: Queue is empty.")
            return None
        
        return self.items[self.front]
```

### Deque
Deque is implemented by extending Circular Queue. We don't have to implement all of features.
```py
class Deque(CircularQueue):
    """
    A Deque implementation that inherits from the CircularQueue class.
    It reuses the circular array logic and adds functionality to add/remove
    from the front and rear of the queue.
    """

    def __init__(self, capacity):
        """
        Initializes the Deque by calling the parent's constructor.
        """
        super().__init__(capacity)

    # --- Methods for the Rear End (Inherited and Renamed) ---
    def add_rear(self, item):
        """
        Adds an item to the rear of the deque. This is an alias for enqueue.
        """
        # We can directly call the parent's enqueue method.
        super().enqueue(item)

    def remove_rear(self):
        """
        Removes and returns an item from the rear of the deque. (New method)
        """
        if self.is_empty():
            print("Error: Deque is empty. Cannot remove item.")
            return None
        
        item_to_return = self.items[self.rear]
        self.items[self.rear] = None
        # Move the rear pointer backwards, wrapping around if necessary.
        self.rear = (self.rear - 1 + self.capacity) % self.capacity
        self.size -= 1
        
        # If we removed the last item, reset pointers to initial empty state for consistency.
        if self.is_empty():
            self.front = 0
            self.rear = -1

        print(f"Removed {item_to_return} from rear")
        return item_to_return

    def peek_rear(self):
        """
        Returns the item at the rear of the deque without removing it. (New method)
        """
        if self.is_empty():
            print("Error: Deque is empty.")
            return None
        return self.items[self.rear]

    # --- Methods for the Front End (Inherited and New) ---
    def add_front(self, item):
        """
        Adds an item to the front of the deque. (New method)
        """
        if self.is_full():
            print("Error: Deque is full. Cannot add new item.")
            return

        # On first insert, rear needs to be set as well.
        if self.is_empty():
            # front is already 0, just need to set rear
            self.rear = 0
        else:
            # Move the front pointer backwards, wrapping around if necessary.
            self.front = (self.front - 1 + self.capacity) % self.capacity
        
        self.items[self.front] = item
        self.size += 1
        print(f"Added {item} at index {self.front}")

    # For clarity, we can give aliases to the inherited methods.
    remove_front = CircularQueue.dequeue
    peek_front = CircularQueue.peek
```

Of course. Here is the queue version of your example in Markdown format, written in English.

## Use Python Primary Features for Queues

For practical purposes, you rarely need to implement a queue from scratch in Python. The standard library provides highly optimized and easy-to-use queue implementations. A queue follows the **FIFO (First-In, First-Out)** principle.

### 1\. Using `collections.deque` (Most Common & Performant)

The `collections.deque` (double-ended queue) is the preferred way to implement a general-purpose queue in Python. It is designed for fast, O(1) appends and pops from both ends. Using a standard `list` is inefficient for queues because removing an item from the beginning of a list (`list.pop(0)`) is an O(n) operation.

  - `enqueue(e)` ➔ `deque.append(e)`
  - `dequeue()` ➔ `deque.popleft()`
  - `front()` or `peek()` ➔ `deque[0]`
  - `isEmpty()` ➔ `len(deque) == 0` or simply `not deque`
  - `size()` ➔ `len(deque)`

```py
from collections import deque

# Create an empty queue
queue = deque()

# Enqueue elements
queue.append(10)
queue.append(20)
queue.append(30)
print(f"Current queue: {queue}")
print(f"Front element is: {queue[0]}")

# Dequeue an element
element = queue.popleft()
print(f"Dequeued element: {element}")
print(f"Queue after dequeue: {queue}")
```

### 2\. Using `queue.Queue` (For Concurrency)

This is a specialized queue for use in multi-threaded programming. It is thread-safe, meaning multiple threads can safely add (`put`) and remove (`get`) items without data corruption. It is essential for managing tasks or communication between threads.

  - `enqueue(e)` ➔ `Queue.put(e)`
  - `dequeue()` ➔ `Queue.get()`
  - `isEmpty()` ➔ `Queue.empty()`
  - `size()` ➔ `Queue.qsize()`

The `get()` method will block by default until an item is available in the queue.

```py
from queue import Queue

# Create a queue with a max size of 5
queue = Queue(maxsize=5)

# Enqueue (put) items
queue.put('A')
queue.put('B')
print(f"Current queue size: {queue.qsize()}")

# Dequeue (get) an item
element = queue.get()
print(f"Dequeued element: {element}")
print(f"Queue size after get: {queue.qsize()}")
```
