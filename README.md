# Data Structures 

Topics:
 * Queues
 * Stacks
 * Doubly Linked Lists
 * LRU Caches

## Tasks
* Part 1 In Class:  `doubly_linked_list`
* Part 1 Homework:  `queue_and_stack`
* Part 2 In Class:  No Starter.  Interview problems described below.
* Part 2 Homework:  `lru_cache`

 > NOTE: The quickest and easiest way to reliably import a file in Python is to just copy and paste the file you want to import into the same directory as the file that wants to import. This obviously isn't considered best practice, but it is the most reliable way to do it across all platforms.  If the import isn't working, feel free to try this method.

### Queues
 * Should have the methods: `enqueue`, `dequeue`, and `len`.
   * `enqueue` should add an item to the back of the queue.
   * `dequeue` should remove and return an item from the front of the queue.
   * `len` returns the number of items in the queue.
 
![Image of Queue](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/600px-Data_Queue.svg.png)

### Doubly Linked Lists
 * The `ListNode` class, which represents a single node in the doubly-linked list, has already been implemented for you. Inspect this code and try to understand what it is doing to the best of your ability.
 * The `DoublyLinkedList` class itself should have the methods: `add_to_head`, `add_to_tail`, `remove_from_head`, `remove_from_tail`, `move_to_front`, `move_to_end`, `delete`, and `get_max`.
   * `add_to_head` replaces the head of the list with a new value that is passed in.
   * `add_to_tail` replaces the tail of the list with a new value that is passed in.
   * `remove_from_head` removes the head node and returns the value stored in it.
   * `remove_from_tail` removes the tail node and returns the value stored in it.
   * `move_to_front` takes a reference to a node in the list and moves it to the front of the list, shifting all other list nodes down. 
   * `move_to_end` takes a reference to a node in the list and moves it to the end of the list, shifting all other list nodes up. 
   * `delete` takes a reference to a node in the list and removes it from the list. The deleted node's `previous` and `next` pointers should point to each afterwards.
   * `get_max` returns the maximum value in the list. 
 * The `head` property is a reference to the first node and the `tail` property is a reference to the last node.
 
![Image of Doubly Linked List](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Doubly-linked-list.svg/610px-Doubly-linked-list.svg.png)

### LRU Cache
An LRU (Least Recently Used) cache is an in-memory storage structure that adheres to the [Least Recently Used](https://en.wikipedia.org/wiki/Cache_replacement_policies#Least_recently_used_(LRU)) caching strategy. 

In essence, you can think of an LRU cache as a data structure that keeps track of the order in which elements (which take the form of key-value pairs) it holds are added and updated. The cache also has a max number of entries it can hold. This is important because once the cache is holding the max number of entries, if a new entry is to be inserted, another pre-existing entry needs to be evicted from the cache. Because the cache is using a least-recently used strategy, the oldest entry (the one that was added/updated the longest time ago) is removed to make space for the new entry. 

So what operations will we need on our cache? We'll certainly need some sort of `set` operation to add key-value pairs to the cache. Newly-set pairs will get moved up the priority order such that every other pair in the cache is now one spot lower in the priority order that the cache maintains. The lowest-priority pair will get removed from the cache if the cache is already at its maximal capacity. Additionally, in the case that the key already exists in the cache, we simply want to overwrite the old value associated with the key with the newly-specified value. 

We'll also need a `get` operation that fetches a value given a key. When a key-value pair is fetched from the cache, we'll go through the same priority-increase dance that also happens when a new pair is added to the cache.

Note that the only way for entries to be removed from the cache is when one needs to be evicted to make room for a new one. Thus, there is no explicit `remove` method. 

Given the above spec, try to get a working implementation that passes the tests. What data structure(s) might be good candidates with which to build our cache on top of? Hint: Since our cache is going to be storing key-value pairs, we might want to use a structure that is adept at handling those. 

---

Once you've gotten the tests passing, it's time to analyze the runtime complexity of your `get` and `set` operations. There's a way to get both operations down to sub-linear time. In fact, we can get them each down to constant time by picking the right data structures to use. 

Here are you some things to think about with regards to optimizing your implementation: If you opted to use a dictionary to work with key-value pairs, we know that dictionaries give us constant access time, which is great. It's cheap and efficient to fetch pairs. A problem arises though from the fact that dictionaries don't have any way of remembering the order in which key-value pairs are added. But we definitely need something to remember the order in which pairs are added. Can you think of some ways to get around this constraint?
