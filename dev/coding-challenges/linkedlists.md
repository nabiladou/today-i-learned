# Linked Lists in Java – Quick Guide

### What is a Linked List?
A **linked list** is a linear data structure where elements (called **nodes**) are connected using references.

Each node contains:
- **data**
- a reference to the **next node** (and sometimes the previous node)

Unlike arrays, linked list elements are **not stored contiguously in memory**.

-> Linked lists trade fast access for fast insertion and deletion.

---

### Types of Linked Lists

#### 1. Singly Linked List

```
10 → 20 → 30 → null
```

- Each node points to the next node
- Most common type

#### 2. Doubly Linked List

```
null ← 10 ⇄ 20 ⇄ 30 → null
```

- Each node points to both next and previous
- Java’s `LinkedList` uses this internally

#### 3. Circular Linked List


```
10 → 20 → 30
↑ ↓
└────────────┘
```
- Last node points back to the first

---

### Linked List vs Array

| Feature | Array / ArrayList | Linked List |
|------|------------------|------------|
| Memory | Contiguous | Non-contiguous |
| Access by index | O(1) | O(n) |
| Insert/Delete (middle) | O(n) | O(1)* |
| Size | Fixed / Resizable | Dynamic |
| Cache friendly | Yes | No |

\* O(1) if the node reference is already known

---

### Why Use a Linked List?

#### Main Benefits
- Fast **insertion and deletion**
- No shifting of elements
- Dynamic size
- Ideal for queues, stacks, and deques

#### When It Is Useful
- Frequent insertions/deletions
- Implementing:
  - Queues
  - Stacks
  - Browser history
  - Undo/Redo systems
  - LRU Cache (with HashMap)

---

### When NOT to Use a Linked List
- You need fast random access (`get(index)`)
- You mostly read data
- Performance is critical (ArrayList is usually faster)

---

### Java Built-in `LinkedList`
```java
LinkedList<Integer> list = new LinkedList<>();
list.addFirst(10);
list.addLast(20);
list.removeFirst();
```

---

### Reversing a Singly Linked List (Must-Know)

```java
FROM
10 → 20 → 30 → null

TO 
30 → 20 → 10 → null

class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class ReverseLinkedList {

    static Node reverse(Node head) {
        Node prev = null;
        Node curr = head;

        while (curr != null) {
            Node next = curr.next; // save next
            curr.next = prev;      // reverse link
            prev = curr;           // move prev
            curr = next;           // move curr
        }

        return prev; // new head
    }
}



/*
Time & Space Complexity
Traversal: O(n)
Insertion/Deletion: O(1) (if node is known)
Reversal: O(n)
Extra Space: O(1)
*/


```


