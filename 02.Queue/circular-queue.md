# Circular Queue
- Circular Queue is theory that queues front and rear have been connected.
- If we implement queue generally, we will meet problem that can't insert element despite queue has space. Because general queue insert only rear with fixed index, we can't insert element despite queue has space that was deleted element.
- So, to use queue's remaining space, appeared 'circular queue theory'.
- Circular Queue's rear is moved to front's behind, if queue is not full. So, we can insert element if there is space to insert element.
- We can implement **Circular buffer**(delete first oldest element) with Circular Queue.

![Source: http://xn--simpllearn-372b.com/tutorials/data-structure-tutorial/circular-queue-in-data-structure](https://www.simplilearn.com/ice9/free_resources_article_thumb/Circular_incrementation_in_Circular_queue.png)