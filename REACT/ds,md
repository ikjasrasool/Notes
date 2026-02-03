# 🎯 COMPLETE DSA GUIDE FOR CODETANTRA EXAM

---

## **TOPIC 1: ARRAYS**

### 1️⃣ ALL POSSIBLE CODETANTRA QUESTIONS

**MCQs:**
- What is the time complexity of finding max element in unsorted array?
- Which traversal is needed to find second largest element?
- What happens when you access arr[n] in array of size n?
- Best case time complexity for separating positive/negative numbers?
- Space complexity of finding min/max in array?

**Output Prediction:**
```c
int arr[] = {3, 5, 1, 8, 2};
int max = arr[0];
for(int i=1; i<5; i++)
    if(arr[i] > max) max = arr[i];
printf("%d", max);
```

**Fill in the Blank:**
```c
// Find minimum element
int min = arr[___];
for(int i=___; i<n; i++)
    if(arr[i] ___ min) min = arr[i];
```

**Debugging:**
```c
// Find second largest (spot the error)
int first = arr[0], second = arr[0];
for(int i=0; i<n; i++) {
    if(arr[i] > first) {
        second = first;
        first = arr[i];
    }
}
```

**Coding Questions:**
1. Write a program to find max and min in single traversal
2. Find second largest element (handle duplicates)
3. Separate positive and negative numbers maintaining order
4. Rearrange array: negatives on left, positives on right
5. Find kth largest/smallest element

---

### 2️⃣ CORE CONCEPTS

**Finding Min/Max:**
- Initialize with first element (NOT with 0 or infinity in exams)
- Single pass: O(n) time, O(1) space
- Compare each element with current min/max

**Second Largest:**
- **Method 1:** Sort array, take arr[n-2] → O(n log n)
- **Method 2:** Two variables (first, second) → O(n) ✅ Best for exams
- **Key Logic:** If element > first, update both. If element > second (but < first), update only second

**Separate Positive/Negative:**
- **Method 1:** Two-pointer approach (Dutch National Flag variant)
- **Method 2:** Use auxiliary array (easier to code)
- **Exam Trick:** They often ask to maintain relative order

---

### 3️⃣ SOLVED EXAMPLES

#### **EASY: Find Min and Max**

**Problem:** Array = {12, 5, 23, 1, 18, 9}

**Step-by-Step:**
```
Step 1: Initialize min=12, max=12
Step 2: Compare 5  → min=5, max=12
Step 3: Compare 23 → min=5, max=23
Step 4: Compare 1  → min=1, max=23
Step 5: Compare 18 → min=1, max=23
Step 6: Compare 9  → min=1, max=23

Answer: Min=1, Max=23
```

**Code:**
```c
int min = arr[0], max = arr[0];
for(int i=1; i<n; i++) {
    if(arr[i] < min) min = arr[i];
    if(arr[i] > max) max = arr[i];
}
```

---

#### **MODERATE: Second Largest Element**

**Problem:** Array = {10, 5, 10, 8, 3}

**Step-by-Step:**
```
Initialize: first = -∞, second = -∞

i=0: arr[0]=10 > first → second=-∞, first=10
i=1: arr[1]=5 < first, 5 > second → second=5
i=2: arr[2]=10 == first → skip (duplicate)
i=3: arr[3]=8 < first, 8 > second → second=8
i=4: arr[4]=3 < second → no change

Answer: Second Largest = 8
```

**Code:**
```c
int first = INT_MIN, second = INT_MIN;
for(int i=0; i<n; i++) {
    if(arr[i] > first) {
        second = first;
        first = arr[i];
    } else if(arr[i] > second && arr[i] != first) {
        second = arr[i];
    }
}
```

---

#### **HARD: Separate Positive/Negative (Maintain Order)**

**Problem:** Array = {-3, 5, -1, 7, -8, 2}

**Expected Output:** {-3, -1, -8, 5, 7, 2}

**Step-by-Step:**
```
Step 1: Create two arrays: neg[], pos[]
Step 2: Traverse and separate
   neg[] = {-3, -1, -8}
   pos[] = {5, 7, 2}
Step 3: Copy neg[] to arr[0...2]
Step 4: Copy pos[] to arr[3...5]
```

**Code:**
```c
int neg[100], pos[100], ni=0, pi=0;
for(int i=0; i<n; i++) {
    if(arr[i] < 0) neg[ni++] = arr[i];
    else pos[pi++] = arr[i];
}
int k=0;
for(int i=0; i<ni; i++) arr[k++] = neg[i];
for(int i=0; i<pi; i++) arr[k++] = pos[i];
```

---

### 4️⃣ SHORTCUTS / SMART LOGIC

✅ **For Min/Max:**
- Don't initialize with 0 (fails if all elements are negative)
- Use arr[0] as initial value

✅ **For Second Largest:**
- **Quick Check:** If n < 2, no second largest exists
- Handle duplicates: Use `arr[i] != first` condition
- **Pattern:** Update second BEFORE first when arr[i] > first

✅ **For Separation:**
- If order doesn't matter → Two-pointer swap (O(1) space)
- If order matters → Use auxiliary array (O(n) space)

✅ **Exam Trick:**
- Read question carefully: "second largest DISTINCT" vs "second largest"

---

### 5️⃣ PRACTICE QUESTIONS

**Q1 (MCQ):** Time complexity of finding second largest in unsorted array?
- A) O(n²)
- B) O(n log n)
- C) O(n)
- D) O(1)

**Q2 (Output):** What is the output?
```c
int arr[] = {4, 2, 4, 1, 4};
int first = arr[0], second = -1;
for(int i=1; i<5; i++) {
    if(arr[i] > first) {
        second = first;
        first = arr[i];
    }
}
printf("%d", second);
```

**Q3 (Coding):** Write a program to find third largest element in array {10, 20, 4, 45, 99, 99, 45}

**Q4 (Debugging):** Find and fix the error:
```c
int max = 0;
for(int i=0; i<n; i++)
    if(arr[i] > max) max = arr[i];
```

**Q5 (MCQ):** For array {-5, -2, -8, -1}, what will be max?
- A) 0
- B) -1
- C) -8
- D) Error

**Q6 (Coding):** Rearrange array so that negative numbers come first (order doesn't matter). Input: {3, -1, 5, -2, 7}

**Q7 (Fill in Blank):**
```c
// Separate even and odd
int even[100], odd[100], ei=___, oi=___;
for(int i=0; i<n; i++) {
    if(arr[i] % 2 == ___) even[ei++] = arr[i];
    else odd[oi++] = arr[i];
}
```

---

### 6️⃣ COMMON MISTAKES

❌ **Initializing min/max with 0:**
- Fails for negative numbers
- **Fix:** Use arr[0] or INT_MIN/INT_MAX

❌ **Not handling duplicates in second largest:**
```c
// WRONG
if(arr[i] > second && arr[i] < first)
// RIGHT
if(arr[i] > second && arr[i] != first)
```

❌ **Array out of bounds:**
```c
// WRONG: accessing arr[n]
for(int i=0; i<=n; i++)
// RIGHT
for(int i=0; i<n; i++)
```

❌ **Forgetting edge cases:**
- Empty array (n=0)
- Single element (n=1)
- All elements same

❌ **Using sorted array logic on unsorted:**
- Don't assume arr[n-1] is max without sorting

---

### 7️⃣ EXAM TIPS

🎯 **Time Management:**
- Array questions: 3-5 minutes max
- If asked to code, write function (not full program) to save time

🎯 **CodeTantra Specifics:**
- They love testing edge cases (empty array, single element)
- Output questions often have tricky loop conditions
- Debugging questions hide errors in initialization or loop bounds

🎯 **Approach Strategy:**
1. Read twice, understand what's asked
2. Check for edge cases first
3. Write algorithm in comments before coding
4. Use meaningful variable names (first, second NOT a, b)

🎯 **Common Traps:**
- "Largest" vs "Second Largest DISTINCT"
- "Maintain order" vs "Any order"
- "Positive numbers" (>0) vs "Non-negative" (≥0)

---

## **TOPIC 2: SINGLY LINKED LIST**

### 1️⃣ ALL POSSIBLE CODETANTRA QUESTIONS

**MCQs:**
- Time complexity of inserting at beginning vs end?
- What is stored in the last node's next pointer?
- Which operation is O(1) in linked list?
- How to detect if linked list is empty?
- Memory allocation function used for new node?

**Output Prediction:**
```c
struct Node {
    int data;
    struct Node* next;
};
// List: 10->20->30->NULL
Node* temp = head;
while(temp->next != NULL) {
    printf("%d ", temp->data);
    temp = temp->next;
}
```

**Fill in the Blank:**
```c
// Insert at beginning
Node* newNode = (Node*)malloc(___);
newNode->data = value;
newNode->___ = head;
___ = newNode;
```

**Debugging:**
```c
// Delete first node (spot the error)
void deleteFirst() {
    Node* temp = head;
    head = head->next;
    // Missing: free(temp);
}
```

**Coding Questions:**
1. Insert at end of linked list
2. Delete node at given position
3. Search for an element
4. Reverse the linked list
5. Print nodes at odd positions
6. Reverse every K nodes
7. Find middle element
8. Detect loop in linked list

---

### 2️⃣ CORE CONCEPTS

**Node Structure:**
```c
struct Node {
    int data;           // Stores value
    struct Node* next;  // Points to next node
};
```

**Key Operations Time Complexity:**
- Insert at beginning: O(1)
- Insert at end: O(n) [need to traverse]
- Insert at end with tail pointer: O(1)
- Delete at beginning: O(1)
- Delete at end: O(n)
- Search: O(n)
- Access nth element: O(n)

**Important Pointers:**
- `head`: Points to first node
- `NULL`: Marks end of list
- `temp`: Used for traversal
- `prev`: Used for deletion/reversal

**Reversal Logic:**
```
Original: 10->20->30->NULL
After:    30->20->10->NULL

Change direction of arrows!
```

---

### 3️⃣ SOLVED EXAMPLES

#### **EASY: Insert at Beginning**

**Problem:** List = 20→30→NULL, Insert 10 at beginning

**Step-by-Step:**
```
Step 1: Create newNode with data=10
   newNode: [10|?]

Step 2: Point newNode->next to current head
   newNode: [10|●]→[20|●]→[30|NULL]

Step 3: Update head to newNode
   head→[10|●]→[20|●]→[30|NULL]

Final: 10→20→30→NULL
```

**Code:**
```c
void insertAtBeginning(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = value;
    newNode->next = head;
    head = newNode;
}
```

---

#### **MODERATE: Delete Node at Position**

**Problem:** List = 10→20→30→40→NULL, Delete position 2 (20)

**Step-by-Step:**
```
Position 2 means second node (index starts from 1)

Step 1: Traverse to position-1 (i.e., position 1)
   prev → [10|●]→[20|●]→[30|●]→[40|NULL]
                  ↑temp

Step 2: prev->next = temp->next
   [10|●]─────────→[30|●]→[40|NULL]
          [20|●] (isolated)

Step 3: free(temp)

Final: 10→30→40→NULL
```

**Code:**
```c
void deleteAtPosition(int pos) {
    if(pos == 1) {
        Node* temp = head;
        head = head->next;
        free(temp);
        return;
    }
    
    Node* prev = head;
    for(int i=1; i<pos-1 && prev!=NULL; i++) {
        prev = prev->next;
    }
    
    if(prev == NULL || prev->next == NULL) return;
    
    Node* temp = prev->next;
    prev->next = temp->next;
    free(temp);
}
```

---

#### **HARD: Reverse Linked List**

**Problem:** List = 10→20→30→NULL

**Step-by-Step:**
```
Initial: 10→20→30→NULL

Use 3 pointers: prev, curr, next

Step 1: prev=NULL, curr=10, next=20
        NULL  10→20→30→NULL
              ↑curr

Step 2: Reverse arrow
        NULL←10  20→30→NULL
        ↑prev ↑curr

Step 3: Move pointers
        NULL←10  20→30→NULL
             ↑prev ↑curr

Step 4: Reverse arrow
        NULL←10←20  30→NULL

Step 5: Move pointers
        NULL←10←20  30→NULL
                ↑prev ↑curr

Step 6: Reverse arrow
        NULL←10←20←30

Step 7: Update head = curr (30)

Final: 30→20→10→NULL
```

**Code:**
```c
void reverseList() {
    Node* prev = NULL;
    Node* curr = head;
    Node* next = NULL;
    
    while(curr != NULL) {
        next = curr->next;  // Save next
        curr->next = prev;  // Reverse arrow
        prev = curr;        // Move prev
        curr = next;        // Move curr
    }
    
    head = prev;
}
```

---

#### **MODERATE: Print Odd Position Nodes**

**Problem:** List = 10→20→30→40→50→NULL

**Expected Output:** 10 30 50 (positions 1, 3, 5)

**Step-by-Step:**
```
Position counter starts from 1

Position 1: 10 ✓ (odd)
Position 2: 20 ✗ (even)
Position 3: 30 ✓ (odd)
Position 4: 40 ✗ (even)
Position 5: 50 ✓ (odd)
```

**Code:**
```c
void printOddPosition() {
    Node* temp = head;
    int pos = 1;
    
    while(temp != NULL) {
        if(pos % 2 == 1) {
            printf("%d ", temp->data);
        }
        temp = temp->next;
        pos++;
    }
}
```

---

#### **HARD: Reverse Every K Nodes**

**Problem:** List = 10→20→30→40→50→60→NULL, K=3

**Expected:** 30→20→10→60→50→40→NULL

**Step-by-Step:**
```
Group 1: 10→20→30  → Reverse → 30→20→10
Group 2: 40→50→60  → Reverse → 60→50→40

Connect: 30→20→10→60→50→40→NULL
```

**Logic:**
```c
void reverseKNodes(int k) {
    Node* curr = head;
    Node* prev = NULL;
    Node* next = NULL;
    int count = 0;
    
    // Reverse first K nodes
    while(curr != NULL && count < k) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
        count++;
    }
    
    // head now points to kth node
    // Recursively reverse remaining
    if(next != NULL) {
        head->next = reverseKNodes(next, k);
    }
    
    return prev; // New head
}
```

---

### 4️⃣ SHORTCUTS / SMART LOGIC

✅ **Insert at Beginning:**
- **3 steps:** Create→Link→Update head
- Fastest operation: O(1)

✅ **Insert at End:**
- **Without tail:** Traverse to last node (O(n))
- **With tail:** Direct insertion (O(1))
- **Exam shortcut:** If they give tail pointer, mention O(1)

✅ **Deletion:**
- **At beginning:** Move head, free old head
- **At position:** Need `prev` pointer (traverse to pos-1)
- **Key:** Always check if position exists

✅ **Reversal:**
- **Pattern:** 3 pointers (prev, curr, next)
- **Loop:** Save next → Reverse arrow → Move pointers
- **Remember:** Update head at end

✅ **Searching:**
- **Linear search only:** No random access
- **Return:** Node pointer or data or position

✅ **Odd/Even Positions:**
- **Counter method:** Start counter at 1, check pos%2
- **Alternate method:** Print, skip, print, skip...

---

### 5️⃣ PRACTICE QUESTIONS

**Q1 (MCQ):** Which operation is fastest in linked list?
- A) Insert at end
- B) Insert at beginning
- C) Search
- D) Access 5th element

**Q2 (Output):** What is printed?
```c
Node* head = createNode(5);
head->next = createNode(10);
head->next->next = createNode(15);

Node* temp = head;
int count = 0;
while(temp != NULL) {
    count++;
    temp = temp->next;
}
printf("%d", count);
```

**Q3 (Coding):** Write function to insert at end of linked list.

**Q4 (Debugging):** Find error in search function:
```c
int search(int key) {
    Node* temp = head;
    while(temp->next != NULL) {
        if(temp->data == key) return 1;
        temp = temp->next;
    }
    return 0;
}
```

**Q5 (MCQ):** After reversing 1→2→3→NULL, what is the list?
- A) 1→2→3→NULL
- B) 3→2→1→NULL
- C) NULL←1←2←3
- D) Error

**Q6 (Coding):** Write function to print nodes at even positions.

**Q7 (Fill in Blank):**
```c
void deleteFirst() {
    if(head == ___) return;
    Node* temp = ___;
    head = head->___;
    ___(temp);
}
```

**Q8 (MCQ):** Time complexity of deleting last node?
- A) O(1)
- B) O(n)
- C) O(log n)
- D) O(n²)

**Q9 (Coding):** Find middle element of linked list in one pass.

**Q10 (Output):** What happens?
```c
Node* temp = head;
while(temp != NULL) {
    printf("%d ", temp->data);
    temp = temp->next->next;
}
// List: 1→2→3→4→5→NULL
```

---

### 6️⃣ COMMON MISTAKES

❌ **Memory Leak:**
```c
// WRONG: Deleting without free
head = head->next;

// RIGHT
Node* temp = head;
head = head->next;
free(temp);
```

❌ **NULL Pointer Access:**
```c
// WRONG: Not checking NULL
while(temp->next != NULL)  // Crashes if temp is NULL

// RIGHT
while(temp != NULL && temp->next != NULL)
```

❌ **Losing Head Pointer:**
```c
// WRONG: Moving head for traversal
while(head != NULL) {
    printf("%d", head->data);
    head = head->next;  // Lost original list!
}

// RIGHT: Use temp pointer
Node* temp = head;
while(temp != NULL) {
    printf("%d", temp->data);
    temp = temp->next;
}
```

❌ **Off-by-One in Position:**
```c
// Position 1 is FIRST node, not position 0
// CodeTantra usually uses 1-based indexing
```

❌ **Reversal Errors:**
```c
// WRONG: Not saving next
curr->next = prev;
curr = curr->next;  // Lost reference!

// RIGHT: Save next first
next = curr->next;
curr->next = prev;
curr = next;
```

❌ **Insert at End Without Traversing:**
```c
// WRONG: Assuming one node
head->next = newNode;

// RIGHT: Traverse to last
Node* temp = head;
while(temp->next != NULL) temp = temp->next;
temp->next = newNode;
```

---

### 7️⃣ EXAM TIPS

🎯 **Memory Management:**
- Always `malloc()` for new nodes
- Always `free()` deleted nodes
- Check if `malloc()` succeeded (not always needed in exams)

🎯 **NULL Checks:**
- Before accessing `temp->data`, check `temp != NULL`
- Before accessing `temp->next`, check if `temp` exists

🎯 **Drawing Diagrams:**
- Pointer questions? Draw the list!
- Mark arrows, show changes step-by-step
- Helps avoid logical errors

🎯 **Common Patterns:**
- **Two pointers:** Fast/slow for middle element
- **Three pointers:** prev/curr/next for reversal
- **Counter:** For position-based operations

🎯 **CodeTantra Traps:**
- They test empty list (head == NULL)
- They test single node list
- Deletion at position > list length
- Accessing data after free()

🎯 **Quick Checks:**
1. Does it handle empty list?
2. Does it handle single node?
3. Is memory freed?
4. Is NULL checked before dereferencing?

---

## **TOPIC 3: DOUBLY LINKED LIST**

### 1️⃣ ALL POSSIBLE CODETANTRA QUESTIONS

**MCQs:**
- How many pointers in a doubly linked list node?
- Advantage of DLL over singly linked list?
- Time complexity of inserting at end with tail pointer?
- How to traverse backward in DLL?
- What does `prev` of first node point to?

**Output Prediction:**
```c
struct Node {
    int data;
    struct Node *prev, *next;
};
// List: NULL←10⇄20⇄30→NULL
Node* temp = head;
while(temp->next != NULL)
    temp = temp->next;
while(temp != NULL) {
    printf("%d ", temp->data);
    temp = temp->prev;
}
```

**Fill in the Blank:**
```c
// Insert at beginning
newNode->next = ___;
newNode->___ = NULL;
if(head != NULL)
    head->___ = newNode;
head = ___;
```

**Debugging:**
```c
// Delete a node (spot errors)
void deleteNode(Node* node) {
    node->prev->next = node->next;
    node->next->prev = node->prev;
    free(node);
}
```

**Coding Questions:**
1. Insert at beginning
2. Insert at end
3. Insert after given node
4. Delete first node
5. Delete last node
6. Delete node at position
7. Forward and backward traversal
8. Search for element

---

### 2️⃣ CORE CONCEPTS

**Node Structure:**
```c
struct Node {
    int data;
    struct Node* prev;  // Points to previous node
    struct Node* next;  // Points to next node
};
```

**Visual Representation:**
```
NULL ← [10] ⇄ [20] ⇄ [30] → NULL
      ↑head              ↑tail
```

**Key Differences from Singly Linked List:**
| Feature | Singly LL | Doubly LL |
|---------|-----------|-----------|
| Pointers per node | 1 (next) | 2 (prev, next) |
| Backward traversal | ✗ | ✓ |
| Deletion (given node) | O(n) | O(1) |
| Memory | Less | More |

**Important Points:**
- First node's `prev` = NULL
- Last node's `next` = NULL
- Can traverse both directions
- Insertion/deletion updates TWO links

---

### 3️⃣ SOLVED EXAMPLES

#### **EASY: Insert at Beginning**

**Problem:** List = 20⇄30→NULL, Insert 10

**Step-by-Step:**
```
Initial: NULL←[20]⇄[30]→NULL

Step 1: Create newNode [10|NULL|?]

Step 2: newNode->next = head
        [10|NULL|●]→[20]⇄[30]→NULL

Step 3: newNode->prev = NULL
        [10|NULL|●]→[20]⇄[30]→NULL

Step 4: head->prev = newNode
        NULL←[10]⇄[20]⇄[30]→NULL

Step 5: head = newNode
        head↑

Final: NULL←[10]⇄[20]⇄[30]→NULL
```

**Code:**
```c
void insertAtBeginning(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = value;
    newNode->next = head;
    newNode->prev = NULL;
    
    if(head != NULL)
        head->prev = newNode;
    
    head = newNode;
}
```

---

#### **MODERATE: Insert at End**

**Problem:** List = 10⇄20→NULL, Insert 30

**Step-by-Step:**
```
Step 1: Create newNode [30|?|NULL]

Step 2: If list is empty
        head = newNode; return;

Step 3: Traverse to last node
        temp → [20]
        
Step 4: temp->next = newNode
        [10]⇄[20]→[30]

Step 5: newNode->prev = temp
        [10]⇄[20]⇄[30]

Step 6: newNode->next = NULL (already done)

Final: NULL←[10]⇄[20]⇄[30]→NULL
```

**Code:**
```c
void insertAtEnd(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = value;
    newNode->next = NULL;
    
    if(head == NULL) {
        newNode->prev = NULL;
        head = newNode;
        return;
    }
    
    Node* temp = head;
    while(temp->next != NULL)
        temp = temp->next;
    
    temp->next = newNode;
    newNode->prev = temp;
}
```

---

#### **HARD: Delete Node at Position**

**Problem:** List = 10⇄20⇄30⇄40→NULL, Delete position 3 (30)

**Step-by-Step:**
```
Position 3 = node with data 30

Step 1: Traverse to position 3
        [10]⇄[20]⇄[30]⇄[40]
                   ↑temp

Step 2: temp->prev->next = temp->next
        [10]⇄[20]────→[40]
             [30] isolated

Step 3: temp->next->prev = temp->prev
        [10]⇄[20]⇄[40]
        [30] fully isolated

Step 4: free(temp)

Final: NULL←[10]⇄[20]⇄[40]→NULL
```

**Code:**
```c
void deleteAtPosition(int pos) {
    if(head == NULL) return;
    
    Node* temp = head;
    
    // Special case: delete first node
    if(pos == 1) {
        head = head->next;
        if(head != NULL)
            head->prev = NULL;
        free(temp);
        return;
    }
    
    // Traverse to position
    for(int i=1; i<pos && temp!=NULL; i++)
        temp = temp->next;
    
    if(temp == NULL) return;
    
    // Update links
    if(temp->prev != NULL)
        temp->prev->next = temp->next;
    
    if(temp->next != NULL)
        temp->next->prev = temp->prev;
    
    free(temp);
}
```

---

#### **MODERATE: Forward and Backward Traversal**

**Problem:** List = 10⇄20⇄30→NULL

**Forward:** 10 20 30
**Backward:** 30 20 10

**Code:**
```c
void forwardTraversal() {
    Node* temp = head;
    printf("Forward: ");
    while(temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}

void backwardTraversal() {
    if(head == NULL) return;
    
    // Go to last node
    Node* temp = head;
    while(temp->next != NULL)
        temp = temp->next;
    
    // Traverse backward
    printf("Backward: ");
    while(temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->prev;
    }
    printf("\n");
}
```

---

### 4️⃣ SHORTCUTS / SMART LOGIC

✅ **Insert at Beginning:**
- **4 steps:** Create → Link next → Link prev → Update head
- **Remember:** Check if list is empty (head == NULL)

✅ **Insert at End:**
- **With tail pointer:** O(1) - Direct insertion
- **Without tail:** O(n) - Traverse to last
- **Key:** Set both prev and next of newNode

✅ **Deletion:**
- **First node:** Update head, set new head's prev = NULL
- **Last node:** Traverse to last, update prev node's next
- **Middle:** Update BOTH prev and next pointers
- **Edge cases:** Single node, position out of bounds

✅ **Traversal:**
- **Forward:** Use next pointer (like singly LL)
- **Backward:** Go to last, use prev pointer
- **Advantage:** No need to reverse list

✅ **Memory:**
- Each node uses MORE memory (2 pointers vs 1)
- Trade-off: Space for flexibility

---

### 5️⃣ PRACTICE QUESTIONS

**Q1 (MCQ):** Main advantage of doubly linked list?
- A) Less memory
- B) Backward traversal
- C) Faster insertion
- D) No pointers needed

**Q2 (Output):** What is printed?
```c
Node* head = createDLL();  // 5⇄10⇄15→NULL
Node* temp = head->next;
printf("%d %d", temp->prev->data, temp->next->data);
```

**Q3 (Fill in Blank):**
```c
void insertAfter(Node* prevNode, int value) {
    if(prevNode == ___) return;
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = ___;
    newNode->next = prevNode->___;
    newNode->___ = prevNode;
    prevNode->next = ___;
    if(newNode->next != NULL)
        newNode->next->___ = newNode;
}
```

**Q4 (Coding):** Write function to delete last node of DLL.

**Q5 (Debugging):** Fix the error:
```c
void deleteFirst() {
    Node* temp = head;
    head = head->next;
    free(temp);
}
```

**Q6 (MCQ):** Time complexity of deleting a node when pointer to node is given?
- A) O(1)
- B) O(n)
- C) O(log n)
- D) Not possible

**Q7 (Coding):** Search for an element and return position (1-based).

**Q8 (Output):** What happens?
```c
// List: 1⇄2⇄3→NULL
Node* temp = head;
while(temp->next != NULL)
    temp = temp->next;
printf("%d", temp->prev->data);
```

---

### 6️⃣ COMMON MISTAKES

❌ **Forgetting to Update Both Pointers:**
```c
// WRONG: Only updating next
newNode->next = head;
head = newNode;

// RIGHT: Update both next and prev
newNode->next = head;
newNode->prev = NULL;
if(head != NULL)
    head->prev = newNode;
head = newNode;
```

❌ **Not Checking NULL Before Accessing:**
```c
// WRONG: Crashes if node is NULL
node->prev->next = node->next;

// RIGHT
if(node->prev != NULL)
    node->prev->next = node->next;
```

❌ **Deleting First Node Without Updating Prev:**
```c
// WRONG
head = head->next;

// RIGHT
head = head->next;
if(head != NULL)
    head->prev = NULL;
```

❌ **Memory Leak in Deletion:**
```c
// WRONG: Not freeing node
temp->prev->next = temp->next;
temp->next->prev = temp->prev;

// RIGHT: Free the node
free(temp);
```

❌ **Order of Operations in Deletion:**
```c
// WRONG: Losing reference
free(temp);
temp->prev->next = temp->next;  // Accessing freed memory!

// RIGHT: Update links first, then free
temp->prev->next = temp->next;
temp->next->prev = temp->prev;
free(temp);
```

---

### 7️⃣ EXAM TIPS

🎯 **Drawing DLL:**
- Always draw arrows in BOTH directions
- Mark NULL at both ends
- Helps visualize pointer updates

🎯 **Insertion Checklist:**
1. Create new node ✓
2. Update newNode->next ✓
3. Update newNode->prev ✓
4. Update adjacent node's pointers ✓

🎯 **Deletion Checklist:**
1. Check if node exists ✓
2. Update prev node's next ✓
3. Update next node's prev ✓
4. Free the node ✓

🎯 **Edge Cases to Remember:**
- Empty list (head == NULL)
- Single node
- Deleting first node
- Deleting last node

🎯 **CodeTantra Patterns:**
- Love to test backward traversal
- Often give code with missing prev updates
- Test NULL pointer scenarios

🎯 **Quick Debug:**
- If crash → Check NULL before dereferencing
- If memory leak → Check free() calls
- If broken links → Check both prev and next updates

---

## **TOPIC 4: STACK USING LINKED LIST**

### 1️⃣ ALL POSSIBLE CODETANTRA QUESTIONS

**MCQs:**
- Which end is used as top in stack using linked list?
- Time complexity of push operation?
- What happens on pop when stack is empty?
- Difference between peek and pop?
- LIFO stands for?

**Output Prediction:**
```c
push(10); push(20); push(30);
pop();
push(40);
printf("%d", peek());
```

**Fill in the Blank:**
```c
void push(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = ___;
    newNode->next = ___;
    ___ = newNode;
}
```

**Debugging:**
```c
int pop() {
    int value = top->data;
    top = top->next;
    return value;
}
```

**Coding Questions:**
1. Implement push operation
2. Implement pop operation
3. Implement peek operation
4. Display all elements
5. Check if stack is empty
6. Get size of stack
7. Reverse a string using stack
8. Check balanced parentheses

---

### 2️⃣ CORE CONCEPTS

**Stack Principle:**
- **LIFO:** Last In First Out
- Like a stack of plates
- Operations only at top

**Why Linked List for Stack?**
- Dynamic size (no overflow like array)
- Efficient O(1) operations
- No wasted space

**Node Structure:**
```c
struct Node {
    int data;
    struct Node* next;
};
Node* top = NULL;  // Points to top element
```

**Visual:**
```
top → [30] → [20] → [10] → NULL
      ↑      ↑      ↑
     3rd    2nd    1st
   (pushed last)
```

**Operations:**
- **Push:** Insert at beginning (top)
- **Pop:** Delete from beginning (top)
- **Peek:** View top element without removing
- **isEmpty:** Check if top == NULL
- **Display:** Traverse from top to bottom

**Time Complexities:**
- Push: O(1)
- Pop: O(1)
- Peek: O(1)
- Display: O(n)
- isEmpty: O(1)

---

### 3️⃣ SOLVED EXAMPLES

#### **EASY: Push Operation**

**Problem:** Empty stack, push 10, 20, 30

**Step-by-Step:**
```
Initial: top = NULL

Push 10:
  newNode [10|NULL]
  top → [10|NULL]

Push 20:
  newNode [20|?]
  newNode->next = top
  top → [20] → [10] → NULL

Push 30:
  newNode [30|?]
  newNode->next = top
  top → [30] → [20] → [10] → NULL

Stack (top to bottom): 30, 20, 10
```

**Code:**
```c
void push(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = value;
    newNode->next = top;
    top = newNode;
    printf("%d pushed\n", value);
}
```

---

#### **EASY: Pop Operation**

**Problem:** Stack = 30→20→10→NULL, Pop twice

**Step-by-Step:**
```
Initial: top → [30] → [20] → [10] → NULL

Pop 1:
  Save value = 30
  temp = top
  top = top->next
  free(temp)
  Result: top → [20] → [10] → NULL
  Returned: 30

Pop 2:
  Save value = 20
  temp = top
  top = top->next
  free(temp)
  Result: top → [10] → NULL
  Returned: 20

Final Stack: 10
```

**Code:**
```c
int pop() {
    if(top == NULL) {
        printf("Stack Underflow\n");
        return -1;
    }
    
    Node* temp = top;
    int value = temp->data;
    top = top->next;
    free(temp);
    return value;
}
```

---

#### **MODERATE: Display Stack**

**Problem:** Stack = 40→30→20→10→NULL

**Expected Output:** 40 30 20 10

**Code:**
```c
void display() {
    if(top == NULL) {
        printf("Stack is empty\n");
        return;
    }
    
    Node* temp = top;
    printf("Stack: ");
    while(temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}
```

---

#### **HARD: Check Balanced Parentheses**

**Problem:** Input = "{[()]}"
**Expected:** Balanced

**Step-by-Step:**
```
String: { [ ( ) ] }

Process '{'  → Push
Stack: {

Process '['  → Push
Stack: { [

Process '('  → Push
Stack: { [ (

Process ')'  → Pop '(' → Match ✓
Stack: { [

Process ']'  → Pop '[' → Match ✓
Stack: {

Process '}'  → Pop '{' → Match ✓
Stack: Empty

Result: Balanced
```

**Logic:**
1. Push opening brackets: `{`, `[`, `(`
2. For closing brackets: `)`, `]`, `}`
   - Pop from stack
   - Check if it matches
3. At end, stack should be empty

**Code:**
```c
int isBalanced(char* expr) {
    for(int i=0; expr[i]!='\0'; i++) {
        char ch = expr[i];
        
        // Opening brackets
        if(ch=='(' || ch=='[' || ch=='{') {
            push(ch);
        }
        // Closing brackets
        else if(ch==')' || ch==']' || ch=='}') {
            if(isEmpty()) return 0;  // No match
            
            char top_ch = pop();
            if((ch==')' && top_ch!='(') ||
               (ch==']' && top_ch!='[') ||
               (ch=='}' && top_ch!='{')) {
                return 0;  // Mismatch
            }
        }
    }
    
    return isEmpty();  // Should be empty
}
```

---

### 4️⃣ SHORTCUTS / SMART LOGIC

✅ **Push = Insert at Beginning:**
- Exactly same as linked list insert at beginning
- Top is just another name for head

✅ **Pop = Delete from Beginning:**
- Remember to free() memory
- Check underflow (top == NULL)

✅ **Peek vs Pop:**
- **Peek:** Just return top->data (don't remove)
- **Pop:** Return value AND remove node

✅ **Stack Empty Check:**
```c
int isEmpty() {
    return top == NULL;
}
```

✅ **Balanced Parentheses Pattern:**
- Opening → Push
- Closing → Pop and match
- Empty at end → Balanced

✅ **Common Use Cases:**
- Function call stack
- Undo/Redo operations
- Expression evaluation
- Backtracking algorithms

---

### 5️⃣ PRACTICE QUESTIONS

**Q1 (MCQ):** Which operation removes element from stack?
- A) Push
- B) Pop
- C) Peek
- D) Display

**Q2 (Output):** What is printed?
```c
push(5); push(10); push(15);
printf("%d ", pop());
printf("%d ", peek());
push(20);
printf("%d", pop());
```

**Q3 (Coding):** Write function to get size of stack.

**Q4 (Fill in Blank):**
```c
int peek() {
    if(top == ___) {
        printf("Stack is empty\n");
        return ___;
    }
    return top->___;
}
```

**Q5 (MCQ):** After push(1), push(2), push(3), pop(), what is at top?
- A) 1
- B) 2
- C) 3
- D) Stack is empty

**Q6 (Debugging):** Fix the error:
```c
void push(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = value;
    top = newNode;
    newNode->next = top;
}
```

**Q7 (Coding):** Check if expression "((a+b)" is balanced.

**Q8 (MCQ):** Stack using linked list vs array?
- A) Linked list has fixed size
- B) Array has dynamic size
- C) Linked list has dynamic size
- D) Both are same

**Q9 (Output):** What happens?
```c
// Empty stack
int x = pop();
printf("%d", x);
```

**Q10 (Coding):** Reverse a string "HELLO" using stack.

---

### 6️⃣ COMMON MISTAKES

❌ **Not Checking Underflow:**
```c
// WRONG
int pop() {
    int value = top->data;  // Crashes if top is NULL
    top = top->next;
    return value;
}

// RIGHT
int pop() {
    if(top == NULL) {
        printf("Stack Underflow\n");
        return -1;
    }
    // ... rest of code
}
```

❌ **Memory Leak in Pop:**
```c
// WRONG: Not freeing node
int pop() {
    int value = top->data;
    top = top->next;
    return value;  // Memory leak!
}

// RIGHT
int pop() {
    Node* temp = top;
    int value = temp->data;
    top = top->next;
    free(temp);
    return value;
}
```

❌ **Wrong Push Order:**
```c
// WRONG
newNode->next = top;
top = newNode;
newNode->next = top;  // Creates self-loop!

// RIGHT
newNode->next = top;
top = newNode;
```

❌ **Peek Modifying Stack:**
```c
// WRONG: peek should NOT remove
int peek() {
    return pop();  // This removes element!
}

// RIGHT
int peek() {
    if(top == NULL) return -1;
    return top->data;
}
```

❌ **Balanced Parentheses Edge Cases:**
