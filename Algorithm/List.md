# List
> A list is a common ADT for holding ordered data, having operations like append a data item, remove a data item, search whether a data item exists, and print the list.
>
> Here's a two types of List.
 1. Singly-Linked List
 2. Doubly-Linked List

What is difference between Singly vs Doubly?

Answer = Doubly has previous pointer.

Solve way: Search, Insert(Append, Prepend, and InsertAfter), and Remove.

### Basic Setup

##### Singly Linked List
> Class Definition
```
class Node {
   public int data;
   public Node next;
    
   public Node(int initialData) {
      data = initialData;
      next = null;
   }
}

class LinkedList {
   private Node head;
   private Node tail;
    
   public LinkedList() {
      head = null;
      tail = null;
   }
}
```
Insert: (Append, Prepend, and InsertAfter)
> Append() Method Definition
```
public void append(Node newNode) {
   if (head == null) {
      head = newNode;
      tail = newNode;
   }
   else {
      tail.next = newNode;
      tail = newNode;
   }
}
```

> Prepend() Method Definition
```
public void prepend(Node newNode) {
   if (head == null) {
      head = newNode;
      tail = newNode;
   }
   else {
      newNode.next = head;
      head = newNode;
   }
}
```

> InsertAfter() Method Definition
```
public void insertAfter(Node currentNode, Node newNode) {
   if (head == null) {
      head = newNode;
      tail = newNode;
   }
   else if (currentNode == tail) {
      tail.next = newNode;
      tail = newNode;
   }
   else {
      newNode.next = currentNode.next;
      currentNode.next = newNode;
   }
}
```

>RemoveAfter() Method Definition
```
public void removeAfter(Node currentNode) {
   if (currentNode == null && head != null) {
      // Special case: remove head
      Node succeedingNode = head.next;
      head = succeedingNode;
      if (succeedingNode == null) {
          // Last item was removed
          tail = null;
      }
   }
   else if (currentNode.next != null) {
      Node succeedingNode = currentNode.next.next;
      currentNode.next = succeedingNode;
      if (succeedingNode == null) {
         // Remove tail
         tail = currentNode;
      }
   }
}
```



##### Doubly Linked List
> Class Definition
```
class Node {
   public int data;
   public Node next;
   public Node previous;

   public Node(int initialData) {
      data = initialData;
      next = null;
      previous = null;
   }
}

class LinkedList {
   private Node head;
   private Node tail;
    
   public LinkedList() {
      head = null;
      tail = null;
   }
}
```

> Append() Method Definition
```
public void append(Node newNode) {
   if (head == null) {
      head = newNode;
      tail = newNode;
   }
   else {
      tail.next = newNode;
      newNode.previous = tail;
      tail = newNode;
   }
}
```

> Prepend() Method Definition
```
public void prepend(Node newNode) {
   if (head == null) {
      head = newNode;
      tail = newNode;
   }
   else {
      newNode.next = head;
      head.previous = newNode;
      head = newNode;
   }
}
```

> InsertAfter() Method Definition
```
public void insertAfter(Node currentNode, Node newNode) {
   if (head == null) {
      head = newNode;
      tail = newNode;
   }
   else if (currentNode == tail) {
      tail.next = newNode;
      newNode.previous = tail;
      tail = newNode;
   }
   else {
      Node successor = currentNode.next;
      newNode.next = successor;
      newNode.previous = currentNode;
      currentNode.next = newNode;
      successor.previous = newNode;
   }
}
```

> Remove() Method Definition
```
public void remove(Node currentNode) {
   Node successor = currentNode.next;
   Node predecessor = currentNode.previous;
      
   if (successor != null)
      successor.previous = predecessor;
         
   if (predecessor != null)
      predecessor.next = successor;
         
   if (currentNode == head)
      head = successor;
         
   if (currentNode == tail)
      tail = predecessor;
}
```



