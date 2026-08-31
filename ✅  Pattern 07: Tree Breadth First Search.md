# Pattern 7: Tree Breadth First Search

This pattern is based on the <b>Breadth First Search (BFS)</b> technique to traverse a tree.

Any problem involving the traversal of a tree in a level-by-level order can be efficiently solved using this approach. We will use a <b>Queue</b> to keep track of all the nodes of a level before we jump onto the next level. This also means that the space complexity of the algorithm will be `O(W)`, where `W` is the maximum number of nodes on any level.


## Binary Tree Level Order Traversal (easy)
https://leetcode.com/problems/binary-tree-level-order-traversal/

> Given a binary tree, populate an array to represent its level-by-level traversal. You should populate the values of all <b>nodes of each level from left to right</b> in separate sub-arrays.

Since we need to traverse all nodes of each level before moving onto the next level, we can use the <b>Breadth First Search (BFS)</b> technique to solve this problem.

We can use a <b>Queue</b> to efficiently traverse in <b>BFS</b> fashion. Here are the steps of our algorithm:
1. Start by pushing the `root` node to the queue.
2. Keep iterating until the <b>queue</b> is empty.
3. In each iteration, first count the elements in the <b>queue</b> (let’s call it `levelSize`). We will have these many nodes in the current level.
4. Next, remove `levelSize` nodes from the <b>queue</b> and push their `value` in an array to represent the current level.
5. After removing each node from the queue, insert both of its children into the queue.
6. If the <b>queue</b> is not empty, repeat from <i>step 3</i> for the next level.

### Java
```java
class Deque {
    constructor() {
        this.front = this.back = undefined;
    }
    addFront(value) {
        if (!this.front) this.front = this.back = { value };
        else this.front = this.front.next = { value, prev: this.front };
    }
    removeFront() {
        value = this.peekFront();
        if (this.front === this.back) this.front = this.back = undefined;
        else (this.front = this.front.prev).next = undefined;
        return value;
    }
    peekFront() { 
        return this.front && this.front.value;
    }
    addBack(value) {
        if (!this.front) this.front = this.back = { value };
        else this.back = this.back.prev = { value, next: this.back };
    }
    removeBack() {
        value = this.peekBack();
        if (this.front === this.back) this.front = this.back = undefined;
        else (this.back = this.back.next).back = undefined;
        return value;
    }
    peekBack() { 
        return this.back && this.back.value;
    }
}

class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null; 
  }
};


public static Object traverse (root) {
  result = [];
  if(root === null ) {
    return result
  }
  
  queue = new Deque()
  //Start by pushing the root node to the queue.
  queue.addFront(root)
  //Keep iterating until the queue is empty.
  currentLevel = []
  while (queue.length > 0) {
    levelSize = queue.length
    //In each iteration, first count the elements in the queue (let’s call it levelSize). We will have these many nodes in the current level.
     
    for(i = 0; i < levelSize; i++) {
      TreeNode = queue.removeFront()
      //add the node to the current level
      currentLevel.add(TreeNode.val)
      //insert the children of current node in the queue
      if(TreeNode.left !== null) {
        queue.addBack(TreeNode.left)
      }
    }
    if(TreeNode.right !== null) {
      queue.addBack(TreeNode.right)
    }
  }
  
  result.add(currentLevel)
  
  //Next, remove levelSize nodes from the queue and push their value in an array to represent the current level.
  //After removing each node from the queue, insert both of its children into the queue.
  //If the queue is not empty, repeat from step 3 for the next level.
  return result;
};



root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
System.out.println(`Level order traversal: ${traverse(root)}`);
```

### Python
```python
class Deque:
    constructor():
        this.front = this.back = None
    addFront(value):
        if !this.front:this.front = this.back = { value }
        else this.front = this.front.next = { value, prev: this.front }
    removeFront():
        value = this.peekFront()
        if this.front === this.back:this.front = this.back = None
        else (this.front = this.front.prev).next = None
        return value
    peekFront():
        return this.front && this.front.value
    addBack(value):
        if !this.front:this.front = this.back = { value }
        else this.back = this.back.prev = { value, next: this.back }
    removeBack():
        value = this.peekBack()
        if this.front === this.back:this.front = this.back = None
        else (this.back = this.back.next).back = None
        return value
    peekBack():
        return this.back && this.back.value

class TreeNode:
    constructor(value):
        this.value = value
        this.left = None
        this.right = None


def traverse(root):
    result = []
    if root === None :
        return result

    queue = new Deque()
    #Start by pushing the root node to the queue.
    queue.addFront(root)
    #Keep iterating until the queue is empty.
    currentLevel = []
    while len(queue) > 0:
        levelSize = len(queue)
        #In each iteration, first count the elements in the queue (let’s call it levelSize). We will have these many nodes in the current level.

        for i in range(levelSize):
            TreeNode = queue.removeFront()
            #add the node to the current level
            currentLevel.append(TreeNode.val)
            #insert the children of current node in the queue
            if TreeNode.left !== None:
                queue.addBack(TreeNode.left)
        if TreeNode.right !== None:
            queue.addBack(TreeNode.right)

    result.append(currentLevel)

    #Next, remove levelSize nodes from the queue and push their value in an array to represent the current level.
    #After removing each node from the queue, insert both of its children into the queue.
    #If the queue is not empty, repeat from step 3 for the next level.
    return result



root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.left.left = new TreeNode(9)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)
print(`Level order traversal: ${traverse(root)}`)
```

### C++
```cpp
class Deque {
    constructor() {
        this.front = this.back = undefined;
    }
    addFront(value) {
        if (!this.front) this.front = this.back = { value };
        else this.front = this.front.next = { value, prev: this.front };
    }
    removeFront() {
        auto value = this.peekFront();
        if (this.front === this.back) this.front = this.back = undefined;
        else (this.front = this.front.prev).next = undefined;
        return value;
    }
    peekFront() { 
        return this.front && this.front.value;
    }
    addBack(value) {
        if (!this.front) this.front = this.back = { value };
        else this.back = this.back.prev = { value, next: this.back };
    }
    removeBack() {
        auto value = this.peekBack();
        if (this.front === this.back) this.front = this.back = undefined;
        else (this.back = this.back.next).back = undefined;
        return value;
    }
    peekBack() { 
        return this.back && this.back.value;
    }
}

class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = nullptr;
    this.right = nullptr; 
  }
};


auto traverse (root) {
  result = [];
  if(root === nullptr ) {
    return result
  }
  
  auto queue = new Deque()
  //Start by pushing the root node to the queue.
  queue.addFront(root)
  //Keep iterating until the queue is empty.
  auto currentLevel = []
  while (queue.size() > 0) {
    auto levelSize = queue.size()
    //In each iteration, first count the elements in the queue (let’s call it levelSize). We will have these many nodes in the current level.
     
    for(i = 0; i < levelSize; i++) {
      TreeNode = queue.removeFront()
      //add the node to the current level
      currentLevel.push_back(TreeNode.val)
      //insert the children of current node in the queue
      if(TreeNode.left !== nullptr) {
        queue.addBack(TreeNode.left)
      }
    }
    if(TreeNode.right !== nullptr) {
      queue.addBack(TreeNode.right)
    }
  }
  
  result.push_back(currentLevel)
  
  //Next, remove levelSize nodes from the queue and push their value in an array to represent the current level.
  //After removing each node from the queue, insert both of its children into the queue.
  //If the queue is not empty, repeat from step 3 for the next level.
  return result;
};



auto root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
std::cout << `Level order traversal: ${traverse(root)}`);
```

- The time complexity of the above algorithm is `O(N)`, where `N` is the total number of nodes in the tree. This is due to the fact that we traverse each node once.
- The space complexity of the above algorithm will be `O(N)` as we need to return a list containing the level order traversal. We will also need `O(N)` space for the queue. Since we can have a maximum of `N/2` nodes at any level (this could happen only at the lowest level), therefore we will need `O(N)` space to store them in the queue.

### Easier to understand solution w/o `Deque()`
### Java
```java
class TreeNode {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

public static Object levelOrder(root) {
  //If root is null return an empty array
  if (!root) return [];

  //initialize the queue with root
  queue = [root];

  //declare output array
  levels = [];

  while (queue.length !== 0) {
    //get the length prior to deque
    queueLength = queue.length;

    //declare this level
    currLevel = [];

    //loop through to exhuast all options and only to include nodes at currLevel
    for (i = 0; i < queueLength; i++) {
      //get next node
      currNode = queue.shift();

      if (currNode.left) {
        queue.add(currNode.left);
      }
      if (currNode.right) {
        queue.add(currNode.right);
      }
      //after we add left and right for current, we add to currLevel
      currLevel.add(currNode.value);
    }
    //Level has been finished. Push into output array
    levels.add(currLevel);
  }

  return levels;
}

root = new TreeNode(3);
root.left = new TreeNode(9);
root.right = new TreeNode(20);
root.right.left = new TreeNode(15);
root.right.right = new TreeNode(7);
levelOrder(root);
//[[3],[9,20],[15,7]]

root = new TreeNode(1);
levelOrder(root);
//[[1]]

root = new TreeNode();
levelOrder(root);
//[]
```

### Python
```python
class TreeNode:
    constructor(value, left = None, right = None):
        this.value = value
        this.left = left
        this.right = right

def levelOrder(root):
    #If root is null return an empty array
    if !root:return []

    #initialize the queue with root
    queue = [root]

    #declare output array
    levels = []

    while len(queue) !== 0:
        #get the length prior to deque
        queueLength = len(queue)

        #declare this level
        currLevel = []

        #loop through to exhuast all options and only to include nodes at currLevel
        for i in range(queueLength):
            #get next node
            currNode = queue.shift()

            if currNode.left:
                queue.append(currNode.left)
            if currNode.right:
                queue.append(currNode.right)
            #after we add left and right for current, we add to currLevel
            currLevel.append(currNode.value)
        #Level has been finished. Push into output array
        levels.append(currLevel)

    return levels

root = new TreeNode(3)
root.left = new TreeNode(9)
root.right = new TreeNode(20)
root.right.left = new TreeNode(15)
root.right.right = new TreeNode(7)
levelOrder(root)
#[[3],[9,20],[15,7]]

root = new TreeNode(1)
levelOrder(root)
#[[1]]

root = new TreeNode()
levelOrder(root)
#[]
```

### C++
```cpp
class TreeNode {
  constructor(value, left = nullptr, right = nullptr) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

auto levelOrder(root) {
  //If root is nullptr return an empty array
  if (!root) return [];

  //initialize the queue with root
  auto queue = [root];

  //declare output array
  auto levels = [];

  while (queue.size() !== 0) {
    //get the length prior to deque
    auto queueLength = queue.size();

    //declare this level
    auto currLevel = [];

    //loop through to exhuast all options and only to include nodes at currLevel
    for (auto i = 0; i < queueLength; i++) {
      //get next node
      auto currNode = queue.shift();

      if (currNode.left) {
        queue.push_back(currNode.left);
      }
      if (currNode.right) {
        queue.push_back(currNode.right);
      }
      //after we add left and right for current, we add to currLevel
      currLevel.push_back(currNode.value);
    }
    //Level has been finished. Push into output array
    levels.push_back(currLevel);
  }

  return levels;
}

auto root = new TreeNode(3);
root.left = new TreeNode(9);
root.right = new TreeNode(20);
root.right.left = new TreeNode(15);
root.right.right = new TreeNode(7);
levelOrder(root);
//[[3],[9,20],[15,7]]

root = new TreeNode(1);
levelOrder(root);
//[[1]]

root = new TreeNode();
levelOrder(root);
//[]
```

## Reverse Level Order Traversal (easy)
https://leetcode.com/problems/binary-tree-level-order-traversal-ii/
> Given a binary tree, populate an array to represent its level-by-level traversal in reverse order, i.e., <b>the lowest level comes first</b>. You should populate the values of all nodes in each level from left to right in separate sub-arrays.

This problem follows the <b>Binary Tree Level Order Traversal</b> pattern. We can follow the same <b>BFS</b> approach. The only difference will be that instead of appending the current level at the end, we will append the current level at the beginning of the result list.
### Java
```java
class TreeNode {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

public static Object reverseLevelOrder(root) {
  //If root is null return an empty array
  if (!root) return [];

  //initialize the queue with root
  queue = [root];

  //declare output array
  levels = [];

  while (queue.length !== 0) {
    //get the length prior to deque
    queueLength = queue.length;

    //declare this level
    currLevel = [];

    //loop through to exhuast all options and only to include nodes at currLevel
    for (i = 0; i < queueLength; i++) {
      //get next node
      currNode = queue.shift();

      if (currNode.left) {
        queue.add(currNode.left);
      }
      if (currNode.right) {
        queue.add(currNode.right);
      }
      //after we add left and right for current, we add to currLevel
      currLevel.add(currNode.value);
    }
    //Level has been finished. Push into output array in reverse order
    levels.unshift(currLevel);
  }

  return levels;
}

root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.left.right = new TreeNode(10);
root.right.right = new TreeNode(5);
reverseLevelOrder(root);
// [[9, 10, 5], [7, 1], [12]];
```

### Python
```python
class TreeNode:
    constructor(value, left = None, right = None):
        this.value = value
        this.left = left
        this.right = right

def reverseLevelOrder(root):
    #If root is null return an empty array
    if !root:return []

    #initialize the queue with root
    queue = [root]

    #declare output array
    levels = []

    while len(queue) !== 0:
        #get the length prior to deque
        queueLength = len(queue)

        #declare this level
        currLevel = []

        #loop through to exhuast all options and only to include nodes at currLevel
        for i in range(queueLength):
            #get next node
            currNode = queue.shift()

            if currNode.left:
                queue.append(currNode.left)
            if currNode.right:
                queue.append(currNode.right)
            #after we add left and right for current, we add to currLevel
            currLevel.append(currNode.value)
        #Level has been finished. Push into output array in reverse order
        levels.unshift(currLevel)

    return levels

root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.left.left = new TreeNode(9)
root.left.right = new TreeNode(10)
root.right.right = new TreeNode(5)
reverseLevelOrder(root)
# [[9, 10, 5], [7, 1], [12]];
```

### C++
```cpp
class TreeNode {
  constructor(value, left = nullptr, right = nullptr) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

auto reverseLevelOrder(root) {
  //If root is nullptr return an empty array
  if (!root) return [];

  //initialize the queue with root
  auto queue = [root];

  //declare output array
  auto levels = [];

  while (queue.size() !== 0) {
    //get the length prior to deque
    auto queueLength = queue.size();

    //declare this level
    auto currLevel = [];

    //loop through to exhuast all options and only to include nodes at currLevel
    for (auto i = 0; i < queueLength; i++) {
      //get next node
      auto currNode = queue.shift();

      if (currNode.left) {
        queue.push_back(currNode.left);
      }
      if (currNode.right) {
        queue.push_back(currNode.right);
      }
      //after we add left and right for current, we add to currLevel
      currLevel.push_back(currNode.value);
    }
    //Level has been finished. Push into output array in reverse order
    levels.unshift(currLevel);
  }

  return levels;
}

auto root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.left.right = new TreeNode(10);
root.right.right = new TreeNode(5);
reverseLevelOrder(root);
// [[9, 10, 5], [7, 1], [12]];
```
- The time complexity of the above algorithm is `O(N)`, where `N` is the total number of nodes in the tree. This is due to the fact that we traverse each node once.
- The space complexity of the above algorithm will be `O(N)` as we need to return a list containing the level order traversal. We will also need `O(N)` space for the queue. Since we can have a maximum of `N/2` nodes at any level (this could happen only at the lowest level), therefore we will need `O(N)` space to store them in the queue.

## 🌴 Zigzag Traversal (medium)
https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/

> Given a binary tree, populate an array to represent its zigzag level order traversal. You should populate the values of all <b>nodes of the first level from left to right</b>, then <b>right to left for the next level</b> and keep alternating in the same manner for the following levels.

This problem follows the <b>Binary Tree Level Order Traversal</b> pattern. We can follow the same <b>BFS</b> approach. The only additional step we have to keep in mind is to alternate the level order traversal, which means that for every other level, we will traverse similar to <b>[Reverse Level Order Traversal](#reverse-level-order-traversal-easy)</b>.


### Java
```java
class TreeNode {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

public static Object zigzagLevelOrder(root) {
  //If root is null return an empty array
  if (!root) return [];

  //initialize the queue with root
  queue = [root];

  //declare output array
  levels = [];
  leftToRight = true;

  while (queue.length !== 0) {
    //get the length prior to deque
    queueLength = queue.length;

    //declare this level
    currLevel = [];

    //loop through to exhuast all options and only to include nodes at currLevel
    for (i = 0; i < queueLength; i++) {
      //get next node
      currNode = queue.shift();

      //add the node to the current level based on the traverse direction

      if (leftToRight) {
        currLevel.add(currNode.value);
      } else {
        currLevel.unshift(currNode.value);
      }

      //insert the children of current node in the queue
      if (currNode.left !== null) {
        queue.add(currNode.left);
      }
      if (currNode.right !== null) {
        queue.add(currNode.right);
      }
    }
    //Level has been finished. Push into output array
    levels.add(currLevel);

    //reverse the traversal direction
    leftToRight = !leftToRight;
  }
  return levels;
}

root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);
root.right.left = new TreeNode(6);
root.right.right = new TreeNode(7);
zigzagLevelOrder(root);
// [[1], [3, 2], [4, 5, 6, 7]];

root = new TreeNode(3);
root.left = new TreeNode(9);
root.right = new TreeNode(20);
root.right.left = new TreeNode(15);
root.right.right = new TreeNode(7);
zigzagLevelOrder(root);
// [[3], [20, 9], [15, 7]];

root = new TreeNode(1);
zigzagLevelOrder(root);
// [[1]];

root = new TreeNode();
zigzagLevelOrder(root);
// [[]];
```

### Python
```python
class TreeNode:
    constructor(value, left = None, right = None):
        this.value = value
        this.left = left
        this.right = right

def zigzagLevelOrder(root):
    #If root is null return an empty array
    if !root:return []

    #initialize the queue with root
    queue = [root]

    #declare output array
    levels = []
    leftToRight = True

    while len(queue) !== 0:
        #get the length prior to deque
        queueLength = len(queue)

        #declare this level
        currLevel = []

        #loop through to exhuast all options and only to include nodes at currLevel
        for i in range(queueLength):
            #get next node
            currNode = queue.shift()

            #add the node to the current level based on the traverse direction

            if leftToRight:
                currLevel.append(currNode.value)
                else:
                    currLevel.unshift(currNode.value)

                #insert the children of current node in the queue
                if currNode.left !== None:
                    queue.append(currNode.left)
                if currNode.right !== None:
                    queue.append(currNode.right)
            #Level has been finished. Push into output array
            levels.append(currLevel)

            #reverse the traversal direction
            leftToRight = !leftToRight
        return levels

    root = new TreeNode(1)
    root.left = new TreeNode(2)
    root.right = new TreeNode(3)
    root.left.left = new TreeNode(4)
    root.left.right = new TreeNode(5)
    root.right.left = new TreeNode(6)
    root.right.right = new TreeNode(7)
    zigzagLevelOrder(root)
    # [[1], [3, 2], [4, 5, 6, 7]];

    root = new TreeNode(3)
    root.left = new TreeNode(9)
    root.right = new TreeNode(20)
    root.right.left = new TreeNode(15)
    root.right.right = new TreeNode(7)
    zigzagLevelOrder(root)
    # [[3], [20, 9], [15, 7]];

    root = new TreeNode(1)
    zigzagLevelOrder(root)
    # [[1]];

    root = new TreeNode()
    zigzagLevelOrder(root)
    # [[]];
```

### C++
```cpp
class TreeNode {
  constructor(value, left = nullptr, right = nullptr) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

auto zigzagLevelOrder(root) {
  //If root is nullptr return an empty array
  if (!root) return [];

  //initialize the queue with root
  auto queue = [root];

  //declare output array
  auto levels = [];
  auto leftToRight = true;

  while (queue.size() !== 0) {
    //get the length prior to deque
    auto queueLength = queue.size();

    //declare this level
    auto currLevel = [];

    //loop through to exhuast all options and only to include nodes at currLevel
    for (auto i = 0; i < queueLength; i++) {
      //get next node
      auto currNode = queue.shift();

      //add the node to the current level based on the traverse direction

      if (leftToRight) {
        currLevel.push_back(currNode.value);
      } else {
        currLevel.unshift(currNode.value);
      }

      //insert the children of current node in the queue
      if (currNode.left !== nullptr) {
        queue.push_back(currNode.left);
      }
      if (currNode.right !== nullptr) {
        queue.push_back(currNode.right);
      }
    }
    //Level has been finished. Push into output array
    levels.push_back(currLevel);

    //reverse the traversal direction
    leftToRight = !leftToRight;
  }
  return levels;
}

auto root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);
root.right.left = new TreeNode(6);
root.right.right = new TreeNode(7);
zigzagLevelOrder(root);
// [[1], [3, 2], [4, 5, 6, 7]];

root = new TreeNode(3);
root.left = new TreeNode(9);
root.right = new TreeNode(20);
root.right.left = new TreeNode(15);
root.right.right = new TreeNode(7);
zigzagLevelOrder(root);
// [[3], [20, 9], [15, 7]];

root = new TreeNode(1);
zigzagLevelOrder(root);
// [[1]];

root = new TreeNode();
zigzagLevelOrder(root);
// [[]];
```
- The time complexity of the above algorithm is `O(N)`, where `N` is the total number of nodes in the tree. This is due to the fact that we traverse each node once.
- The space complexity of the above algorithm will be `O(N)` as we need to return a list containing the level order traversal. We will also need `O(N)` space for the queue. Since we can have a maximum of `N/2` nodes at any level (this could happen only at the lowest level), therefore we will need `O(N)` space to store them in the queue.

## Level Averages in a Binary Tree (easy)
https://leetcode.com/problems/average-of-levels-in-binary-tree/

> Given a binary tree, populate an array to represent the <b>averages of all of its levels</b>

This problem follows the <b>Binary Tree Level Order Traversal</b> pattern. We can follow the same <b>BFS</b> approach. The only difference will be that instead of keeping track of all nodes of a level, we will only track the running sum of the values of all nodes in each level. In the end, we will append the average of the current level to the result array.

### Java
```java
class TreeNode {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

public static Object findLevelAverages(root) {
  //If root is null return an empty array
  if (!root) return [];

  //declare output array
  result = [];

  //initialize the queue with root
  queue = [root];

  while (queue.length > 0) {
    levelSize = queue.length;
    levelSum = 0;

    for (i = 0; i < levelSize; i++) {
      //get next node
      currNode = queue.shift();

      //add the node's value to the running sum
      levelSum += currNode.value;

      //insert the children of current node in the queue
      if (currNode.left !== null) {
        queue.add(currNode.left);
      }
      if (currNode.right !== null) {
        queue.add(currNode.right);
      }
    }
    //append the current level's average to the result array
    result.add(levelSum / levelSize);
  }
  return result;
}

root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.left.right = new TreeNode(2);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
System.out.println(`Level averages are: ${findLevelAverages(root)}`)
// [[12], [4], [6.5]];
```

### Python
```python
class TreeNode:
    constructor(value, left = None, right = None):
        this.value = value
        this.left = left
        this.right = right

def findLevelAverages(root):
    #If root is null return an empty array
    if !root:return []

    #declare output array
    result = []

    #initialize the queue with root
    queue = [root]

    while len(queue) > 0:
        levelSize = len(queue)
        levelSum = 0

        for i in range(levelSize):
            #get next node
            currNode = queue.shift()

            #add the node's value to the running sum
            levelSum += currNode.value

            #insert the children of current node in the queue
            if currNode.left !== None:
                queue.append(currNode.left)
            if currNode.right !== None:
                queue.append(currNode.right)
        #append the current level's average to the result array
        result.append(levelSum / levelSize)
    return result

root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.left.left = new TreeNode(9)
root.left.right = new TreeNode(2)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)
print(`Level averages are: ${findLevelAverages(root)}`)
# [[12], [4], [6.5]];
```

### C++
```cpp
class TreeNode {
  constructor(value, left = nullptr, right = nullptr) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

auto findLevelAverages(root) {
  //If root is nullptr return an empty array
  if (!root) return [];

  //declare output array
  auto result = [];

  //initialize the queue with root
  auto queue = [root];

  while (queue.size() > 0) {
    auto levelSize = queue.size();
    auto levelSum = 0;

    for (auto i = 0; i < levelSize; i++) {
      //get next node
      auto currNode = queue.shift();

      //add the node's value to the running sum
      levelSum += currNode.value;

      //insert the children of current node in the queue
      if (currNode.left !== nullptr) {
        queue.push_back(currNode.left);
      }
      if (currNode.right !== nullptr) {
        queue.push_back(currNode.right);
      }
    }
    //append the current level's average to the result array
    result.push_back(levelSum / levelSize);
  }
  return result;
}

auto root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.left.right = new TreeNode(2);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
std::cout << `Level averages are: ${findLevelAverages(root)}`)
// [[12], [4], [6.5]];
```
- The time complexity of the above algorithm is `O(N)`, where `N` is the total number of nodes in the tree. This is due to the fact that we traverse each node once.
- The space complexity of the above algorithm will be `O(N)` which is required for the queue. Since we can have a maximum of `N/2` nodes at any level (this could happen only at the lowest level), therefore we will need `O(N)` space to store them in the queue

### Level Maximum in a Binary Tree 
https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/
> 🌟  Find the largest value on each level of a binary tree.

We will follow a similar approach, but instead of having a running sum we will track the maximum value of each level.

`maxValue = Math.max(maxValue, currentNode.val)`

### Java
```java
class TreeNode {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

public static Object largestValue(root) {
  //If root is null return an empty array
  if (!root) return [];

  //declare output array
  result = [];

  //initialize the queue with root
  queue = [root];

  while (queue.length > 0) {
    levelSize = queue.length;
    maxValue = 0;

    for (i = 0; i < levelSize; i++) {
      //get next node
      currNode = queue.shift();

      maxValue = Math.max(maxValue, currNode.value);

      //insert the children of current node in the queue
      if (currNode.left !== null) {
        queue.add(currNode.left);
      }
      if (currNode.right !== null) {
        queue.add(currNode.right);
      }
    }
    //append the current level's average to the result array
    result.add(maxValue);
    maxValue = 0;
  }
  return result;
}

root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.left.right = new TreeNode(2);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);

System.out.println(`Max value's for each level are: ${largestValue(root)}`);
// [[12], [7], [10]];
```

### Python
```python
class TreeNode:
    constructor(value, left = None, right = None):
        this.value = value
        this.left = left
        this.right = right

def largestValue(root):
    #If root is null return an empty array
    if !root:return []

    #declare output array
    result = []

    #initialize the queue with root
    queue = [root]

    while len(queue) > 0:
        levelSize = len(queue)
        maxValue = 0

        for i in range(levelSize):
            #get next node
            currNode = queue.shift()

            maxValue = max(maxValue, currNode.value)

            #insert the children of current node in the queue
            if currNode.left !== None:
                queue.append(currNode.left)
            if currNode.right !== None:
                queue.append(currNode.right)
        #append the current level's average to the result array
        result.append(maxValue)
        maxValue = 0
    return result

root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.left.left = new TreeNode(9)
root.left.right = new TreeNode(2)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)

print(`Max value's for each level are: ${largestValue(root)}`)
# [[12], [7], [10]];
```

### C++
```cpp
class TreeNode {
  constructor(value, left = nullptr, right = nullptr) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

auto largestValue(root) {
  //If root is nullptr return an empty array
  if (!root) return [];

  //declare output array
  auto result = [];

  //initialize the queue with root
  auto queue = [root];

  while (queue.size() > 0) {
    auto levelSize = queue.size();
    auto maxValue = 0;

    for (auto i = 0; i < levelSize; i++) {
      //get next node
      auto currNode = queue.shift();

      maxValue = std::max(maxValue, currNode.value);

      //insert the children of current node in the queue
      if (currNode.left !== nullptr) {
        queue.push_back(currNode.left);
      }
      if (currNode.right !== nullptr) {
        queue.push_back(currNode.right);
      }
    }
    //append the current level's average to the result array
    result.push_back(maxValue);
    maxValue = 0;
  }
  return result;
}

auto root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.left.right = new TreeNode(2);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);

std::cout << `Max value's for each level are: ${largestValue(root)}`);
// [[12], [7], [10]];
```

## Minimum Depth of a Binary Tree (easy)
https://leetcode.com/problems/minimum-depth-of-binary-tree/

> Find the minimum depth of a binary tree. The minimum depth is the number of nodes along the <b>shortest path from the root node to the nearest leaf node</b>.

This problem follows the <b>Binary Tree Level Order Traversal</b> pattern. We can follow the same <b>BFS</b> approach. The only difference will be, instead of keeping track of all the nodes in a level, we will only track the depth of the tree. As soon as we find our first leaf node, that level will represent the minimum depth of the tree.

### Java
```java
class TreeNode {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

public static Object findMinimumDepth(root) {
  if (!root) return 0;

  //initialize the queue with root
  queue = [root];

  minimumTreeDepth = 0;

  while (queue.length > 0) {
    minimumTreeDepth++;
    levelSize = queue.length;

    for (i = 0; i < levelSize; i++) {
      //get next node
      currNode = queue.shift();

      //check if this is a leaf node
      if (currNode.left === null && currNode.right === null) {
        return minimumTreeDepth;
      }

      //insert the children of current node in the queue
      if (currNode.left !== null) {
        queue.add(currNode.left);
      }
      if (currNode.right !== null) {
        queue.add(currNode.right);
      }
    }
  }
}

root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
System.out.println(`Tree Minimum Depth: ${findMinimumDepth(root)}`);
root.left.left = new TreeNode(9);
root.right.left.left = new TreeNode(11);
System.out.println(`Tree Minimum Depth: ${findMinimumDepth(root)}`);
```

### Python
```python
class TreeNode:
    constructor(value, left = None, right = None):
        this.value = value
        this.left = left
        this.right = right

def findMinimumDepth(root):
    if !root:return 0

    #initialize the queue with root
    queue = [root]

    minimumTreeDepth = 0

    while len(queue) > 0:
        minimumTreeDepth++
        levelSize = len(queue)

        for i in range(levelSize):
            #get next node
            currNode = queue.shift()

            #check if this is a leaf node
            if currNode.left === None && currNode.right === None:
                return minimumTreeDepth

            #insert the children of current node in the queue
            if currNode.left !== None:
                queue.append(currNode.left)
            if currNode.right !== None:
                queue.append(currNode.right)

root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)
print(`Tree Minimum Depth: ${findMinimumDepth(root)}`)
root.left.left = new TreeNode(9)
root.right.left.left = new TreeNode(11)
print(`Tree Minimum Depth: ${findMinimumDepth(root)}`)
```

### C++
```cpp
class TreeNode {
  constructor(value, left = nullptr, right = nullptr) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

auto findMinimumDepth(root) {
  if (!root) return 0;

  //initialize the queue with root
  auto queue = [root];

  auto minimumTreeDepth = 0;

  while (queue.size() > 0) {
    minimumTreeDepth++;
    auto levelSize = queue.size();

    for (auto i = 0; i < levelSize; i++) {
      //get next node
      auto currNode = queue.shift();

      //check if this is a leaf node
      if (currNode.left === nullptr && currNode.right === nullptr) {
        return minimumTreeDepth;
      }

      //insert the children of current node in the queue
      if (currNode.left !== nullptr) {
        queue.push_back(currNode.left);
      }
      if (currNode.right !== nullptr) {
        queue.push_back(currNode.right);
      }
    }
  }
}

auto root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
std::cout << `Tree Minimum Depth: ${findMinimumDepth(root)}`);
root.left.left = new TreeNode(9);
root.right.left.left = new TreeNode(11);
std::cout << `Tree Minimum Depth: ${findMinimumDepth(root)}`);
```
- The time complexity of the above algorithm is `O(N)`, where `N` is the total number of nodes in the tree. This is due to the fact that we traverse each node once.
- The space complexity of the above algorithm will be `O(N)` which is required for the queue. Since we can have a maximum of `N/2` nodes at any level (this could happen only at the lowest level), therefore we will need `O(N)` space to store them in the queue.

### Maximum Depth of a Binary Tree
https://leetcode.com/problems/maximum-depth-of-binary-tree/
> Given a binary tree, find its maximum depth (or height).

We will follow a similar approach. Instead of returning as soon as we find a leaf node, we will keep traversing for all the levels, incrementing `maximumDepth` each time we complete a level. 
### Java
```java
class TreeNode {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

public static Object findMaximumDepth(root) {
  if (!root) return 0;

  //initialize the queue with root
  queue = [root];

  maximumTreeDepth = 0;

  while (queue.length > 0) {
    maximumTreeDepth++;
    levelSize = queue.length;

    for (i = 0; i < levelSize; i++) {
      //get next node
      currNode = queue.shift();

    

      //insert the children of current node in the queue
      if (currNode.left !== null) {
        queue.add(currNode.left);
      }
      if (currNode.right !== null) {
        queue.add(currNode.right);
      }
    }
  }
  return maximumTreeDepth
}

root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
System.out.println(`Tree Maximum Depth: ${findMaximumDepth(root)}`);
root.left.left = new TreeNode(9);
root.right.left.left = new TreeNode(11);
System.out.println(`Tree Maximum Depth: ${findMaximumDepth(root)}`);
```

### Python
```python
class TreeNode:
    constructor(value, left = None, right = None):
        this.value = value
        this.left = left
        this.right = right

def findMaximumDepth(root):
    if !root:return 0

    #initialize the queue with root
    queue = [root]

    maximumTreeDepth = 0

    while len(queue) > 0:
        maximumTreeDepth++
        levelSize = len(queue)

        for i in range(levelSize):
            #get next node
            currNode = queue.shift()



            #insert the children of current node in the queue
            if currNode.left !== None:
                queue.append(currNode.left)
            if currNode.right !== None:
                queue.append(currNode.right)
    return maximumTreeDepth

root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)
print(`Tree Maximum Depth: ${findMaximumDepth(root)}`)
root.left.left = new TreeNode(9)
root.right.left.left = new TreeNode(11)
print(`Tree Maximum Depth: ${findMaximumDepth(root)}`)
```

### C++
```cpp
class TreeNode {
  constructor(value, left = nullptr, right = nullptr) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

auto findMaximumDepth(root) {
  if (!root) return 0;

  //initialize the queue with root
  auto queue = [root];

  auto maximumTreeDepth = 0;

  while (queue.size() > 0) {
    maximumTreeDepth++;
    auto levelSize = queue.size();

    for (auto i = 0; i < levelSize; i++) {
      //get next node
      auto currNode = queue.shift();

    

      //insert the children of current node in the queue
      if (currNode.left !== nullptr) {
        queue.push_back(currNode.left);
      }
      if (currNode.right !== nullptr) {
        queue.push_back(currNode.right);
      }
    }
  }
  return maximumTreeDepth
}

auto root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
std::cout << `Tree Maximum Depth: ${findMaximumDepth(root)}`);
root.left.left = new TreeNode(9);
root.right.left.left = new TreeNode(11);
std::cout << `Tree Maximum Depth: ${findMaximumDepth(root)}`);
```
## Level Order Successor (easy) 
> Given a binary tree and a node, find the level order successor of the given node in the tree. The level order successor is the node that appears right after the given node in the level order traversal.

This problem follows the <b>Binary Tree Level Order Traversal</b> pattern. We can follow the same <b>BFS</b> approach. The only difference will be that we will not keep track of all the levels. Instead we will keep inserting child nodes to the queue. As soon as we find the given node, we will return the next node from the <b>queue</b> as the level order successor.

### Java
```java
class TreeNode {
  constructor(value, left = null, right = null) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

public static Object findSuccessor(root, key) {
  if (root == null) return null;

  //initialize the queue with root
  queue = [root];

  while (queue.length > 0) {
    //get next node
    currNode = queue.shift();

    //insert the children of current node in the queue
    if (currNode.left !== null) {
      queue.add(currNode.left);
    }
    if (currNode.right !== null) {
      queue.add(currNode.right);
    }

    // break if we have found the key
    if (currNode.value === key) break;
  }
  if (queue.length > 0) return queue.shift();

  return null;
}

root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);

result = findSuccessor(root, 12);
if (result != null) System.out.println(result.value);

result = findSuccessor(root, 9);
if (result != null) System.out.println(result.value);
```

### Python
```python
class TreeNode:
    constructor(value, left = None, right = None):
        this.value = value
        this.left = left
        this.right = right

def findSuccessor(root, key):
    if root == None:return None

    #initialize the queue with root
    queue = [root]

    while len(queue) > 0:
        #get next node
        currNode = queue.shift()

        #insert the children of current node in the queue
        if currNode.left !== None:
            queue.append(currNode.left)
        if currNode.right !== None:
            queue.append(currNode.right)

        # break if we have found the key
        if currNode.value === key:break
    if len(queue) > 0:return queue.shift()

    return None

root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.left.left = new TreeNode(9)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)

result = findSuccessor(root, 12)
if result != None:print(result.value)

result = findSuccessor(root, 9)
if result != None:print(result.value)
```

### C++
```cpp
class TreeNode {
  constructor(value, left = nullptr, right = nullptr) {
    this.value = value;
    this.left = left;
    this.right = right;
  }
}

auto findSuccessor(root, key) {
  if (root == nullptr) return nullptr;

  //initialize the queue with root
  auto queue = [root];

  while (queue.size() > 0) {
    //get next node
    auto currNode = queue.shift();

    //insert the children of current node in the queue
    if (currNode.left !== nullptr) {
      queue.push_back(currNode.left);
    }
    if (currNode.right !== nullptr) {
      queue.push_back(currNode.right);
    }

    // break if we have found the key
    if (currNode.value === key) break;
  }
  if (queue.size() > 0) return queue.shift();

  return nullptr;
}

auto root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);

result = findSuccessor(root, 12);
if (result != nullptr) std::cout << result.value);

result = findSuccessor(root, 9);
if (result != nullptr) std::cout << result.value);
```

- The time complexity of the above algorithm is `O(N)`, where `N` is the total number of nodes in the tree. This is due to the fact that we traverse each node once.
- The space complexity of the above algorithm will be `O(N)` which is required for the queue. Since we can have a maximum of `N/2` nodes at any level (this could happen only at the lowest level), therefore we will need `O(N)` space to store them in the queue.

## 😕 Connect Level Order Siblings (medium)
https://leetcode.com/problems/populating-next-right-pointers-in-each-node/
> Given a binary tree, connect each node with its level order successor. The last node of each level should point to a `null` node.

This problem follows the <b>Binary Tree Level Order Traversal</b> pattern. We can follow the same <b>BFS</b> approach. The only difference is that while traversing a level we will remember the previous node to connect it with the current node.
### Java
```java
class TreeNode {
  constructor(val) {
    this.val = val
    this.left = null
    this.right = null
    this.next = null
  }
}

  // level order traversal using 'next' pointer
 public static Object printLevelOrder() {
    System.out.println("Level order traversal using 'next' pointer: ");
    nextLevelRoot = this;
    while (nextLevelRoot !== null) {
      currentNode = nextLevelRoot;
      nextLevelRoot = null;
      while (currentNode != null) {
        process.stdout.write(`${currentNode.val} `);
        if (nextLevelRoot === null) {
          if (currentNode.left !== null) {
            nextLevelRoot = currentNode.left;
          } else if (currentNode.right !== null) {
            nextLevelRoot = currentNode.right;
          }
        }
        currentNode = currentNode.next;
      }
      System.out.println();
    }
  }


public static Object connectLevelOrderSiblings(root) {
  //if root is null return an empty array
  if(!root) return []
  
  //initilize the queue with root
  queue = [root]
  
  // //declare output array
  // levels = []
  
  while(queue.length > 0) {
    previousNode = null
    
    //get length prior to dequeue
    levelSize = queue.length
    
    // //declare this level
    // currLevel = []
    
    //connect all nodes of this level
    for(i = 0; i < levelSize; i++) {
      //get the next node
      currentNode = queue.shift()
      if(previousNode !== null) {
        previousNode.next = currentNode
      }
      previousNode = currentNode
      
      //insert the children of currentNode in the queue
      if(currentNode.left !== null) {
        queue.add(currentNode.left)
      }
      if(currentNode.right !== null) {
        queue.add(currentNode.right)
      }
      
    //   //after we add left and right for current, we add to currLevel
    //   currLevel.add(current.val)
    }
    
    // //level has been finished. Push into output array
    // levels.add(currLevel)
  }
  // return levels
}

root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
connectLevelOrderSiblings(root);

printLevelOrder(root)
```

### Python
```python
class TreeNode:
    constructor(val):
        this.val = val
        this.left = None
        this.right = None
        this.next = None

# level order traversal using 'next' pointer
def printLevelOrder():
    print("Level order traversal using 'next' pointer: ")
    nextLevelRoot = this
    while nextLevelRoot !== None:
        currentNode = nextLevelRoot
        nextLevelRoot = None
        while currentNode != None:
            process.stdout.write(`${currentNode.val} `)
            if nextLevelRoot === None:
                if currentNode.left !== None:
                    nextLevelRoot = currentNode.left
                    else:if currentNode.right !== None:
                        nextLevelRoot = currentNode.right
                currentNode = currentNode.next
            print()


    def connectLevelOrderSiblings(root):
        #if root is null return an empty array
        if !root:return []

        #initilize the queue with root
        queue = [root]

        # //declare output array
        # const levels = []

        while len(queue) > 0:
            previousNode = None

            #get length prior to dequeue
            levelSize = len(queue)

            # //declare this level
            # const currLevel = []

            #connect all nodes of this level
            for i in range(levelSize):
                #get the next node
                currentNode = queue.shift()
                if previousNode !== None:
                    previousNode.next = currentNode
                previousNode = currentNode

                #insert the children of currentNode in the queue
                if currentNode.left !== None:
                    queue.append(currentNode.left)
                if currentNode.right !== None:
                    queue.append(currentNode.right)

                #   //after we add left and right for current, we add to currLevel
                #   currLevel.push(current.val)

            # //level has been finished. Push into output array
            # levels.push(currLevel)
        # return levels

    root = new TreeNode(12)
    root.left = new TreeNode(7)
    root.right = new TreeNode(1)
    root.left.left = new TreeNode(9)
    root.right.left = new TreeNode(10)
    root.right.right = new TreeNode(5)
    connectLevelOrderSiblings(root)

    printLevelOrder(root)
```

### C++
```cpp
class TreeNode {
  constructor(val) {
    this.val = val
    this.left = nullptr
    this.right = nullptr
    this.next = nullptr
  }
}

  // level order traversal using 'next' pointer
 auto printLevelOrder() {
    std::cout << "Level order traversal using 'next' pointer: ");
    auto nextLevelRoot = this;
    while (nextLevelRoot !== nullptr) {
      auto currentNode = nextLevelRoot;
      nextLevelRoot = nullptr;
      while (currentNode != nullptr) {
        process.stdout.write(`${currentNode.val} `);
        if (nextLevelRoot === nullptr) {
          if (currentNode.left !== nullptr) {
            nextLevelRoot = currentNode.left;
          } else if (currentNode.right !== nullptr) {
            nextLevelRoot = currentNode.right;
          }
        }
        currentNode = currentNode.next;
      }
      std::cout << );
    }
  }


auto connectLevelOrderSiblings(root) {
  //if root is nullptr return an empty array
  if(!root) return []
  
  //initilize the queue with root
  auto queue = [root]
  
  // //declare output array
  // auto levels = []
  
  while(queue.size() > 0) {
    auto previousNode = nullptr
    
    //get length prior to dequeue
    auto levelSize = queue.size()
    
    // //declare this level
    // auto currLevel = []
    
    //connect all nodes of this level
    for(auto i = 0; i < levelSize; i++) {
      //get the next node
      auto currentNode = queue.shift()
      if(previousNode !== nullptr) {
        previousNode.next = currentNode
      }
      previousNode = currentNode
      
      //insert the children of currentNode in the queue
      if(currentNode.left !== nullptr) {
        queue.push_back(currentNode.left)
      }
      if(currentNode.right !== nullptr) {
        queue.push_back(currentNode.right)
      }
      
    //   //after we add left and right for current, we add to currLevel
    //   currLevel.push_back(current.val)
    }
    
    // //level has been finished. Push into output array
    // levels.push_back(currLevel)
  }
  // return levels
}

auto root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
connectLevelOrderSiblings(root);

printLevelOrder(root)
```
- The time complexity of the above algorithm is `O(N)`, where `N` is the total number of nodes in the tree. This is due to the fact that we traverse each node once.
- The space complexity of the above algorithm will be `O(N)`, which is required for the queue. Since we can have a maximum of `N/2`nodes at any level (this could happen only at the lowest level), therefore we will need `O(N)` space to store them in the queue.

## 🌟 Connect All Level Order Siblings (medium) 
> Given a binary tree, connect each node with its level order successor. The last node of each level should point to the first node of the next level.

This problem follows the <b>Binary Tree Level Order Traversal</b> pattern. We can follow the same <b>BFS</b> approach. The only difference will be that while traversing we will remember (irrespective of the level) the previous node to connect it with the current node.

### Java
```java
class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null; 
  }
  
  // tree traversal using 'next' pointer
  printTree() {
    result = "Traversal using 'next' pointer: ";
    current = this;
    while (current != null) {
      result += current.value + " ";
      current = current.next;
    }
    System.out.println(result);
  }
};

public static Object connectAllSiblings(root) {
  if(root === null) {
    return
  }
  
  queue = [root]
  currentNode = null
  previousNode = null
  
  while(queue.length > 0) {
    currentNode = queue.shift()
    
    if(previousNode !== null) {
      previousNode.next = currentNode
    }
    
    previousNode = currentNode
    
    //insert the children of the currentNode into the queue
    if(currentNode.left !== null) {
      queue.add(currentNode.left)
    }
    if(currentNode.right !== null) {
      queue.add(currentNode.right)
    }
  }
};


root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.left.left = new TreeNode(9)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)
connectAllSiblings(root)
root.printTree()
```

### Python
```python
class TreeNode:
    constructor(value):
        this.value = value
        this.left = None
        this.right = None

    # tree traversal using 'next' pointer
    printTree():
        result = "Traversal using 'next' pointer: "
        current = this
        while current != None:
            result += current.value + " "
            current = current.next
        print(result)

def connectAllSiblings(root):
    if root === None:
        return

    queue = [root]
    currentNode = None
    previousNode = None

    while len(queue) > 0:
        currentNode = queue.shift()

        if previousNode !== None:
            previousNode.next = currentNode

        previousNode = currentNode

        #insert the children of the currentNode into the queue
        if currentNode.left !== None:
            queue.append(currentNode.left)
        if currentNode.right !== None:
            queue.append(currentNode.right)


root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.left.left = new TreeNode(9)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)
connectAllSiblings(root)
root.printTree()
```

### C++
```cpp
class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = nullptr;
    this.right = nullptr; 
  }
  
  // tree traversal using 'next' pointer
  printTree() {
    auto result = "Traversal using 'next' pointer: ";
    auto current = this;
    while (current != nullptr) {
      result += current.value + " ";
      current = current.next;
    }
    std::cout << result);
  }
};

auto connectAllSiblings(root) {
  if(root === nullptr) {
    return
  }
  
  auto queue = [root]
  auto currentNode = nullptr
  auto previousNode = nullptr
  
  while(queue.size() > 0) {
    currentNode = queue.shift()
    
    if(previousNode !== nullptr) {
      previousNode.next = currentNode
    }
    
    previousNode = currentNode
    
    //insert the children of the currentNode into the queue
    if(currentNode.left !== nullptr) {
      queue.push_back(currentNode.left)
    }
    if(currentNode.right !== nullptr) {
      queue.push_back(currentNode.right)
    }
  }
};


auto root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.left.left = new TreeNode(9)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)
connectAllSiblings(root)
root.printTree()
```

- The time complexity of the above algorithm is `O(N)`, where `N` is the total number of nodes in the tree. This is due to the fact that we traverse each node once.
- The space complexity of the above algorithm will be `O(N)` which is required for the queue. Since we can have a maximum of `N/2` nodes at any level (this could happen only at the lowest level), therefore we will need `O(N)` space to store them in the queue.
## 🌟 Right View of a Binary Tree (easy) 
https://leetcode.com/problems/binary-tree-right-side-view/

> Given a binary tree, return an array containing nodes in its right view. The right view of a binary tree is the set of <b>nodes visible when the tree is seen from the right side</b>.

### Java
```java
class TreeNode {
  constructor(value) {
    this.value = value
    this.left = null
    this.right = null
  }
}

public static Object treeRightView(root) {
  result = [];
  
  if(root === null) {
    return result
  }
  
  queue = [root]
  
  while(queue.length > 0) {
    levelSize = queue.length
    
    for(i = 0; i < levelSize; i++) {
      currentNode = queue.shift()
      
      //if it is the last node of this level,
      //add it to the result
      if(i === levelSize - 1){
        result.add(currentNode.value)
      }
      //insert the children of current node in the queue
      if(currentNode.left !== null) {
        queue.add(currentNode.left)
      }
      if(currentNode.right !== null) {
        queue.add(currentNode.right)
      }
    }
  }

  return result;
};

root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
root.left.left.left = new TreeNode(3);
System.out.println("Tree right view: " + treeRightView(root))
```

### Python
```python
class TreeNode:
    constructor(value):
        this.value = value
        this.left = None
        this.right = None

def treeRightView(root):
    result = []

    if root === None:
        return result

    queue = [root]

    while len(queue) > 0:
        levelSize = len(queue)

        for i in range(levelSize):
            currentNode = queue.shift()

            #if it is the last node of this level,
            #add it to the result
            if i === levelSize - 1:
                result.append(currentNode.value)
            #insert the children of current node in the queue
            if currentNode.left !== None:
                queue.append(currentNode.left)
            if currentNode.right !== None:
                queue.append(currentNode.right)

    return result

root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.left.left = new TreeNode(9)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)
root.left.left.left = new TreeNode(3)
print("Tree right view: " + treeRightView(root))
```

### C++
```cpp
class TreeNode {
  constructor(value) {
    this.value = value
    this.left = nullptr
    this.right = nullptr
  }
}

auto treeRightView(root) {
  auto result = [];
  
  if(root === nullptr) {
    return result
  }
  
  auto queue = [root]
  
  while(queue.size() > 0) {
    auto levelSize = queue.size()
    
    for(auto i = 0; i < levelSize; i++) {
      auto currentNode = queue.shift()
      
      //if it is the last node of this level,
      //add it to the result
      if(i === levelSize - 1){
        result.push_back(currentNode.value)
      }
      //insert the children of current node in the queue
      if(currentNode.left !== nullptr) {
        queue.push_back(currentNode.left)
      }
      if(currentNode.right !== nullptr) {
        queue.push_back(currentNode.right)
      }
    }
  }

  return result;
};

auto root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
root.left.left.left = new TreeNode(3);
std::cout << "Tree right view: " + treeRightView(root))
```
- The time complexity of the above algorithm is `O(N)`, where `N` is the total number of nodes in the tree. This is due to the fact that we traverse each node once
- The space complexity of the above algorithm will be `O(N)` as we need to return a list containing the level order traversal. We will also need `O(N)` space for the queue. Since we can have a maximum of `N/2` nodes at any level (this could happen only at the lowest level), therefore we will need `O(N)` space to store them in the queue.

### Similar Questions
> Given a binary tree, return an array containing nodes in its left view. The left view of a binary tree is the set of nodes visible when the tree is seen from the left side.

We will be following a similar approach, but instead of appending the last element of each level, we will be appending the first element of each level to the output array.

### Java
```java
class TreeNode {
  constructor(value) {
    this.value = value
    this.left = null
    this.right = null
  }
}

public static Object treeRightView(root) {
  result = [];
  
  if(root === null) {
    return result
  }
  
  queue = [root]
  
  while(queue.length > 0) {
    levelSize = queue.length
    
    for(i = 0; i < levelSize; i++) {
      currentNode = queue.shift()
      
      //if it is the first node of this level,
      //add it to the result
      if(i === 0){
        result.add(currentNode.value)
      }
      //insert the children of current node in the queue
      if(currentNode.left !== null) {
        queue.add(currentNode.left)
      }
      if(currentNode.right !== null) {
        queue.add(currentNode.right)
      }
    }
  }

  return result;
};

root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
root.left.left.left = new TreeNode(3);
System.out.println("Tree right view: " + treeRightView(root))
```

### Python
```python
class TreeNode:
    constructor(value):
        this.value = value
        this.left = None
        this.right = None

def treeRightView(root):
    result = []

    if root === None:
        return result

    queue = [root]

    while len(queue) > 0:
        levelSize = len(queue)

        for i in range(levelSize):
            currentNode = queue.shift()

            #if it is the first node of this level,
            #add it to the result
            if i === 0:
                result.append(currentNode.value)
            #insert the children of current node in the queue
            if currentNode.left !== None:
                queue.append(currentNode.left)
            if currentNode.right !== None:
                queue.append(currentNode.right)

    return result

root = new TreeNode(12)
root.left = new TreeNode(7)
root.right = new TreeNode(1)
root.left.left = new TreeNode(9)
root.right.left = new TreeNode(10)
root.right.right = new TreeNode(5)
root.left.left.left = new TreeNode(3)
print("Tree right view: " + treeRightView(root))
```

### C++
```cpp
class TreeNode {
  constructor(value) {
    this.value = value
    this.left = nullptr
    this.right = nullptr
  }
}

auto treeRightView(root) {
  auto result = [];
  
  if(root === nullptr) {
    return result
  }
  
  auto queue = [root]
  
  while(queue.size() > 0) {
    auto levelSize = queue.size()
    
    for(auto i = 0; i < levelSize; i++) {
      auto currentNode = queue.shift()
      
      //if it is the first node of this level,
      //add it to the result
      if(i === 0){
        result.push_back(currentNode.value)
      }
      //insert the children of current node in the queue
      if(currentNode.left !== nullptr) {
        queue.push_back(currentNode.left)
      }
      if(currentNode.right !== nullptr) {
        queue.push_back(currentNode.right)
      }
    }
  }

  return result;
};

auto root = new TreeNode(12);
root.left = new TreeNode(7);
root.right = new TreeNode(1);
root.left.left = new TreeNode(9);
root.right.left = new TreeNode(10);
root.right.right = new TreeNode(5);
root.left.left.left = new TreeNode(3);
std::cout << "Tree right view: " + treeRightView(root))
```
