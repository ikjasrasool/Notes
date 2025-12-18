# Striver's SDE Sheet - Top Coding Interview Problems

## Day 1: Arrays

### 1. Set Matrix Zeroes
**Problem:** Given a matrix, if an element is 0, set its entire row and column to 0.

**Solution:** Use first row and column as markers. Iterate through matrix, mark rows/columns to be zeroed using first row/col, then set zeros.

```java
void setZeroes(int[][] matrix) {
    boolean firstRow = false, firstCol = false;
    
    // Check if first row/col needs to be zero
    for(int i = 0; i < matrix.length; i++) {
        if(matrix[i][0] == 0) firstCol = true;
    }
    for(int j = 0; j < matrix[0].length; j++) {
        if(matrix[0][j] == 0) firstRow = true;
    }
    
    // Mark rows and columns using first row/col
    for(int i = 1; i < matrix.length; i++) {
        for(int j = 1; j < matrix[0].length; j++) {
            if(matrix[i][j] == 0) {
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }
    
    // Set zeros based on marks
    for(int i = 1; i < matrix.length; i++) {
        for(int j = 1; j < matrix[0].length; j++) {
            if(matrix[i][0] == 0 || matrix[0][j] == 0) {
                matrix[i][j] = 0;
            }
        }
    }
    
    // Handle first row and column
    if(firstRow) {
        for(int j = 0; j < matrix[0].length; j++) matrix[0][j] = 0;
    }
    if(firstCol) {
        for(int i = 0; i < matrix.length; i++) matrix[i][0] = 0;
    }
}
```

---

### 2. Pascal's Triangle
**Problem:** Generate Pascal's Triangle up to n rows.

**Solution:** Each element is sum of two elements above it. First and last elements are 1.

```java
List<List<Integer>> generate(int numRows) {
    List<List<Integer>> result = new ArrayList<>();
    for(int i = 0; i < numRows; i++) {
        List<Integer> row = new ArrayList<>();
        for(int j = 0; j <= i; j++) {
            if(j == 0 || j == i) row.add(1);
            else row.add(result.get(i-1).get(j-1) + result.get(i-1).get(j));
        }
        result.add(row);
    }
    return result;
}
```

---

### 3. Next Permutation
**Problem:** Find the next lexicographically greater permutation.

**Solution:** 
1. Find first decreasing element from right (pivot)
2. Find smallest element greater than pivot from right
3. Swap them
4. Reverse elements after pivot

```java
void nextPermutation(int[] nums) {
    int i = nums.length - 2;
    while(i >= 0 && nums[i] >= nums[i+1]) i--;
    
    if(i >= 0) {
        int j = nums.length - 1;
        while(nums[j] <= nums[i]) j--;
        swap(nums, i, j);
    }
    reverse(nums, i+1, nums.length-1);
}
```

---

### 4. Maximum Subarray (Kadane's Algorithm)
**Problem:** Find contiguous subarray with maximum sum.

**Solution:** Keep track of current sum and max sum. Reset current sum if it becomes negative.

```java
int maxSubArray(int[] nums) {
    int maxSum = nums[0], currentSum = nums[0];
    for(int i = 1; i < nums.length; i++) {
        currentSum = Math.max(nums[i], currentSum + nums[i]);
        maxSum = Math.max(maxSum, currentSum);
    }
    return maxSum;
}
```

---

### 5. Sort Colors (Dutch National Flag)
**Problem:** Sort array containing only 0s, 1s, and 2s.

**Solution:** Three pointers - low, mid, high. Partition array in one pass.

```java
void sortColors(int[] nums) {
    int low = 0, mid = 0, high = nums.length - 1;
    while(mid <= high) {
        if(nums[mid] == 0) swap(nums, low++, mid++);
        else if(nums[mid] == 1) mid++;
        else swap(nums, mid, high--);
    }
}
```

---

### 6. Best Time to Buy and Sell Stock
**Problem:** Find maximum profit from one transaction.

**Solution:** Track minimum price so far and maximum profit.

```java
int maxProfit(int[] prices) {
    int minPrice = Integer.MAX_VALUE;
    int maxProfit = 0;
    for(int price : prices) {
        minPrice = Math.min(minPrice, price);
        maxProfit = Math.max(maxProfit, price - minPrice);
    }
    return maxProfit;
}
```

---

## Day 2: Arrays Part II

### 7. Rotate Matrix (90 degrees)
**Problem:** Rotate matrix 90 degrees clockwise.

**Solution:** Transpose matrix, then reverse each row.

```java
void rotate(int[][] matrix) {
    int n = matrix.length;
    // Transpose
    for(int i = 0; i < n; i++) {
        for(int j = i; j < n; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }
    // Reverse each row
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n/2; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[i][n-1-j];
            matrix[i][n-1-j] = temp;
        }
    }
}
```

---

### 8. Merge Overlapping Intervals
**Problem:** Merge all overlapping intervals.

**Solution:** Sort intervals by start time, then merge overlapping ones.

```java
int[][] merge(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    List<int[]> result = new ArrayList<>();
    int[] current = intervals[0];
    
    for(int i = 1; i < intervals.length; i++) {
        if(intervals[i][0] <= current[1]) {
            current[1] = Math.max(current[1], intervals[i][1]);
        } else {
            result.add(current);
            current = intervals[i];
        }
    }
    result.add(current);
    return result.toArray(new int[result.size()][]);
}
```

---

### 9. Merge Two Sorted Arrays
**Problem:** Merge two sorted arrays without extra space.

**Solution:** Use gap method or two pointers from end.

```java
void merge(int[] nums1, int m, int[] nums2, int n) {
    int i = m - 1, j = n - 1, k = m + n - 1;
    while(j >= 0) {
        if(i >= 0 && nums1[i] > nums2[j]) {
            nums1[k--] = nums1[i--];
        } else {
            nums1[k--] = nums2[j--];
        }
    }
}
```

---

### 10. Find Duplicate Number
**Problem:** Find the duplicate number in array of n+1 integers where each is between 1 and n.

**Solution:** Floyd's Cycle Detection (Tortoise and Hare).

```java
int findDuplicate(int[] nums) {
    int slow = nums[0], fast = nums[0];
    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while(slow != fast);
    
    slow = nums[0];
    while(slow != fast) {
        slow = nums[slow];
        fast = nums[fast];
    }
    return slow;
}
```

---

### 11. Repeat and Missing Number
**Problem:** Find the repeating and missing number in array 1 to N.

**Solution:** Use mathematical equations or XOR.

```java
int[] findMissingRepeating(int[] arr) {
    long n = arr.length;
    long sumN = n * (n + 1) / 2;
    long sumN2 = n * (n + 1) * (2 * n + 1) / 6;
    
    long sum = 0, sum2 = 0;
    for(int num : arr) {
        sum += num;
        sum2 += (long)num * num;
    }
    
    long diff = sum - sumN; // X - Y
    long sumDiff = sum2 - sumN2; // X^2 - Y^2
    long add = sumDiff / diff; // X + Y
    
    int repeat = (int)(diff + add) / 2;
    int missing = (int)(add - repeat);
    return new int[]{repeat, missing};
}
```

---

### 12. Inversion Count
**Problem:** Count pairs (i, j) where i < j and arr[i] > arr[j].

**Solution:** Use merge sort and count inversions during merge.

```java
int inversionCount(int[] arr) {
    return mergeSort(arr, 0, arr.length - 1);
}

int mergeSort(int[] arr, int left, int right) {
    int count = 0;
    if(left < right) {
        int mid = left + (right - left) / 2;
        count += mergeSort(arr, left, mid);
        count += mergeSort(arr, mid + 1, right);
        count += merge(arr, left, mid, right);
    }
    return count;
}
```

---

## Day 3: Arrays Part III

### 13. Search in 2D Matrix
**Problem:** Search target in row-wise and column-wise sorted matrix.

**Solution:** Treat as 1D sorted array and apply binary search.

```java
boolean searchMatrix(int[][] matrix, int target) {
    int m = matrix.length, n = matrix[0].length;
    int left = 0, right = m * n - 1;
    
    while(left <= right) {
        int mid = left + (right - left) / 2;
        int midVal = matrix[mid / n][mid % n];
        
        if(midVal == target) return true;
        else if(midVal < target) left = mid + 1;
        else right = mid - 1;
    }
    return false;
}
```

---

### 14. Pow(x, n)
**Problem:** Calculate x raised to power n.

**Solution:** Binary exponentiation - reduce power by half each time.

```java
double myPow(double x, int n) {
    if(n == 0) return 1;
    if(n < 0) {
        x = 1 / x;
        n = -(n + 1); // Handle overflow
        return x * myPow(x, n);
    }
    
    double half = myPow(x, n / 2);
    if(n % 2 == 0) return half * half;
    else return half * half * x;
}
```

---

### 15. Majority Element (>N/2)
**Problem:** Find element appearing more than n/2 times.

**Solution:** Boyer-Moore Voting Algorithm.

```java
int majorityElement(int[] nums) {
    int candidate = nums[0], count = 1;
    for(int i = 1; i < nums.length; i++) {
        if(count == 0) {
            candidate = nums[i];
            count = 1;
        } else if(nums[i] == candidate) {
            count++;
        } else {
            count--;
        }
    }
    return candidate;
}
```

---

### 16. Majority Element (>N/3)
**Problem:** Find all elements appearing more than n/3 times.

**Solution:** Extended Boyer-Moore (at most 2 such elements).

```java
List<Integer> majorityElement(int[] nums) {
    int candidate1 = 0, candidate2 = 0, count1 = 0, count2 = 0;
    
    for(int num : nums) {
        if(num == candidate1) count1++;
        else if(num == candidate2) count2++;
        else if(count1 == 0) { candidate1 = num; count1 = 1; }
        else if(count2 == 0) { candidate2 = num; count2 = 1; }
        else { count1--; count2--; }
    }
    
    List<Integer> result = new ArrayList<>();
    count1 = count2 = 0;
    for(int num : nums) {
        if(num == candidate1) count1++;
        else if(num == candidate2) count2++;
    }
    
    if(count1 > nums.length / 3) result.add(candidate1);
    if(count2 > nums.length / 3) result.add(candidate2);
    return result;
}
```

---

### 17. Grid Unique Paths
**Problem:** Find number of unique paths from top-left to bottom-right (only right/down moves).

**Solution:** Combinatorics: C(m+n-2, m-1) or DP.

```java
int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];
    for(int i = 0; i < m; i++) dp[i][0] = 1;
    for(int j = 0; j < n; j++) dp[0][j] = 1;
    
    for(int i = 1; i < m; i++) {
        for(int j = 1; j < n; j++) {
            dp[i][j] = dp[i-1][j] + dp[i][j-1];
        }
    }
    return dp[m-1][n-1];
}
```

---

### 18. Reverse Pairs
**Problem:** Count pairs (i, j) where i < j and arr[i] > 2 * arr[j].

**Solution:** Modified merge sort.

```java
int reversePairs(int[] nums) {
    return mergeSort(nums, 0, nums.length - 1);
}

int mergeSort(int[] nums, int left, int right) {
    if(left >= right) return 0;
    int mid = left + (right - left) / 2;
    int count = mergeSort(nums, left, mid) + mergeSort(nums, mid + 1, right);
    
    // Count reverse pairs
    int j = mid + 1;
    for(int i = left; i <= mid; i++) {
        while(j <= right && nums[i] > 2L * nums[j]) j++;
        count += j - (mid + 1);
    }
    
    merge(nums, left, mid, right);
    return count;
}
```

---

## Day 4: Arrays Part IV

### 19. Two Sum
**Problem:** Find two numbers that add up to target.

**Solution:** Use HashMap to store complement.

```java
int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for(int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if(map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{};
}
```

---

### 20. Four Sum
**Problem:** Find all unique quadruplets that sum to target.

**Solution:** Sort array, use two pointers for inner two elements.

```java
List<List<Integer>> fourSum(int[] nums, int target) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();
    
    for(int i = 0; i < nums.length - 3; i++) {
        if(i > 0 && nums[i] == nums[i-1]) continue;
        for(int j = i + 1; j < nums.length - 2; j++) {
            if(j > i + 1 && nums[j] == nums[j-1]) continue;
            
            int left = j + 1, right = nums.length - 1;
            while(left < right) {
                long sum = (long)nums[i] + nums[j] + nums[left] + nums[right];
                if(sum == target) {
                    result.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
                    while(left < right && nums[left] == nums[left+1]) left++;
                    while(left < right && nums[right] == nums[right-1]) right--;
                    left++;
                    right--;
                } else if(sum < target) left++;
                else right--;
            }
        }
    }
    return result;
}
```

---

### 21. Longest Consecutive Sequence
**Problem:** Find length of longest consecutive elements sequence.

**Solution:** Use HashSet, for each number check if it's start of sequence.

```java
int longestConsecutive(int[] nums) {
    Set<Integer> set = new HashSet<>();
    for(int num : nums) set.add(num);
    
    int maxLen = 0;
    for(int num : set) {
        if(!set.contains(num - 1)) { // Start of sequence
            int currentNum = num;
            int currentLen = 1;
            
            while(set.contains(currentNum + 1)) {
                currentNum++;
                currentLen++;
            }
            maxLen = Math.max(maxLen, currentLen);
        }
    }
    return maxLen;
}
```

---

### 22. Largest Subarray with 0 Sum
**Problem:** Find length of largest subarray with sum 0.

**Solution:** Use HashMap to store cumulative sum and index.

```java
int maxLen(int[] arr) {
    Map<Integer, Integer> map = new HashMap<>();
    int sum = 0, maxLen = 0;
    
    for(int i = 0; i < arr.length; i++) {
        sum += arr[i];
        
        if(sum == 0) maxLen = i + 1;
        else if(map.containsKey(sum)) {
            maxLen = Math.max(maxLen, i - map.get(sum));
        } else {
            map.put(sum, i);
        }
    }
    return maxLen;
}
```

---

### 23. Count Subarrays with Given XOR
**Problem:** Count subarrays with XOR equal to K.

**Solution:** Use HashMap to store XOR prefix.

```java
int subarraysWithXorK(int[] arr, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    int xor = 0, count = 0;
    map.put(0, 1);
    
    for(int num : arr) {
        xor ^= num;
        if(map.containsKey(xor ^ k)) {
            count += map.get(xor ^ k);
        }
        map.put(xor, map.getOrDefault(xor, 0) + 1);
    }
    return count;
}
```

---

### 24. Longest Substring Without Repeating Characters
**Problem:** Find length of longest substring without repeating characters.

**Solution:** Sliding window with HashSet or HashMap.

```java
int lengthOfLongestSubstring(String s) {
    Set<Character> set = new HashSet<>();
    int left = 0, maxLen = 0;
    
    for(int right = 0; right < s.length(); right++) {
        while(set.contains(s.charAt(right))) {
            set.remove(s.charAt(left++));
        }
        set.add(s.charAt(right));
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

---

## Day 5: Linked List

### 25. Reverse Linked List
**Problem:** Reverse a singly linked list.

**Solution:** Iterative or recursive approach with three pointers.

```java
ListNode reverseList(ListNode head) {
    ListNode prev = null, curr = head;
    while(curr != null) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

---

### 26. Find Middle of Linked List
**Problem:** Find middle node of linked list.

**Solution:** Slow and fast pointer (tortoise and hare).

```java
ListNode middleNode(ListNode head) {
    ListNode slow = head, fast = head;
    while(fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```

---

### 27. Merge Two Sorted Lists
**Problem:** Merge two sorted linked lists.

**Solution:** Two pointers, compare and attach smaller node.

```java
ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;
    
    while(l1 != null && l2 != null) {
        if(l1.val < l2.val) {
            curr.next = l1;
            l1 = l1.next;
        } else {
            curr.next = l2;
            l2 = l2.next;
        }
        curr = curr.next;
    }
    curr.next = (l1 != null) ? l1 : l2;
    return dummy.next;
}
```

---

### 28. Remove Nth Node From End
**Problem:** Remove nth node from end of list.

**Solution:** Two pointers with gap of n.

```java
ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode first = dummy, second = dummy;
    
    for(int i = 0; i <= n; i++) {
        first = first.next;
    }
    
    while(first != null) {
        first = first.next;
        second = second.next;
    }
    
    second.next = second.next.next;
    return dummy.next;
}
```

---

### 29. Delete Node in Linked List
**Problem:** Delete a node (not tail) given only access to that node.

**Solution:** Copy next node's value and delete next node.

```java
void deleteNode(ListNode node) {
    node.val = node.next.val;
    node.next = node.next.next;
}
```

---

### 30. Add Two Numbers (Linked Lists)
**Problem:** Add two numbers represented as linked lists.

**Solution:** Simulate addition with carry.

```java
ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;
    int carry = 0;
    
    while(l1 != null || l2 != null || carry != 0) {
        int sum = carry;
        if(l1 != null) { sum += l1.val; l1 = l1.next; }
        if(l2 != null) { sum += l2.val; l2 = l2.next; }
        
        carry = sum / 10;
        curr.next = new ListNode(sum % 10);
        curr = curr.next;
    }
    return dummy.next;
}
```

---

## Day 6: Linked List Part II

### 31. Detect Cycle in Linked List
**Problem:** Detect if linked list has a cycle.

**Solution:** Floyd's Cycle Detection (slow and fast pointer).

```java
boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while(fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if(slow == fast) return true;
    }
    return false;
}
```

---

### 32. Reverse Nodes in K-Group
**Problem:** Reverse nodes in groups of k.

**Solution:** Reverse k nodes at a time, keep track of connections.

```java
ListNode reverseKGroup(ListNode head, int k) {
    ListNode curr = head;
    int count = 0;
    
    while(curr != null && count < k) {
        curr = curr.next;
        count++;
    }
    
    if(count == k) {
        curr = reverseKGroup(curr, k);
        while(count-- > 0) {
            ListNode next = head.next;
            head.next = curr;
            curr = head;
            head = next;
        }
        head = curr;
    }
    return head;
}
```

---

### 33. Palindrome Linked List
**Problem:** Check if linked list is palindrome.

**Solution:** Find middle, reverse second half, compare.

```java
boolean isPalindrome(ListNode head) {
    if(head == null || head.next == null) return true;
    
    // Find middle
    ListNode slow = head, fast = head;
    while(fast.next != null && fast.next.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    
    // Reverse second half
    ListNode secondHalf = reverse(slow.next);
    
    // Compare
    ListNode p1 = head, p2 = secondHalf;
    while(p2 != null) {
        if(p1.val != p2.val) return false;
        p1 = p1.next;
        p2 = p2.next;
    }
    return true;
}
```

---

### 34. Linked List Cycle II (Starting Point)
**Problem:** Find the node where cycle begins.

**Solution:** Floyd's algorithm, then move one pointer to start.

```java
ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;
    
    while(fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if(slow == fast) {
            slow = head;
            while(slow != fast) {
                slow = slow.next;
                fast = fast.next;
            }
            return slow;
        }
    }
    return null;
}
```

---

### 35. Flattening a Linked List
**Problem:** Flatten a multi-level linked list with down pointers.

**Solution:** Merge lists level by level like merge sort.

```java
Node flatten(Node root) {
    if(root == null || root.next == null) return root;
    
    root.next = flatten(root.next);
    root = merge(root, root.next);
    return root;
}

Node merge(Node a, Node b) {
    if(a == null) return b;
    if(b == null) return a;
    
    if(a.data < b.data) {
        a.bottom = merge(a.bottom, b);
        return a;
    } else {
        b.bottom = merge(a, b.bottom);
        return b;
    }
}
```

---

### 36. Rotate List
**Problem:** Rotate list to the right by k places.

**Solution:** Make circular, find new tail, break circle.

```java
ListNode rotateRight(ListNode head, int k) {
    if(head == null || k == 0) return head;
    
    // Find length and make circular
    ListNode curr = head;
    int len = 1;
    while(curr.next != null) {
        curr = curr.next;
        len++;
    }
    curr.next = head;
    
    // Find new tail
    k = k % len;
    int stepsToNewHead = len - k;
    ListNode newTail = head;
    for(int i = 1; i < stepsToNewHead; i++) {
        newTail = newTail.next;
    }
    
    ListNode newHead = newTail.next;
    newTail.next = null;
    return newHead;
}
```

---

## Day 7: 2-Pointer & Linked List

### 37. Clone Linked List with Random Pointer
**Problem:** Deep copy linked list with random pointer.

**Solution:** Create copy nodes next to originals, set random, separate lists.

```java
Node copyRandomList(Node head) {
    if(head == null) return null;
    
    // Create copy nodes
    Node curr = head;
    while(curr != null) {
        Node copy = new Node(curr.val);
        copy.next = curr.next;
        curr.next = copy;
        curr = copy.next;
    }
    
    // Set random pointers
    curr = head;
    while(curr != null) {
        if(curr.random != null) {
            curr.next.random = curr.random.next;
        }
        curr = curr.next.next;
    }
    
    // Separate lists
    Node dummy = new Node(0);
    Node copyCurr = dummy;
    curr = head;
    while(curr != null) {
        copyCurr.next = curr.next;
        curr.next = curr.next.next;
        curr = curr.next;
        copyCurr = copyCurr.next;
    }
    return dummy.next;
}
```

---

### 38. 3 Sum
**Problem:** Find all unique triplets that sum to zero.

**Solution:** Sort array, fix one element, use two pointers for remaining.

```java
List<List<Integer>> threeSum(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();
    
    for(int i = 0; i < nums.length - 2; i++) {
        if(i > 0 && nums[i] == nums[i-1]) continue;
        
        int left = i + 1, right = nums.length - 1;
        while(left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            if(sum == 0) {
                result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                while(left < right && nums[left] == nums[left+1]) left++;
                while(left < right && nums[right] == nums[right-1]) right--;
                left++;
                right--;
            } else if(sum < 0) left++;
            else right--;
        }
    }
    return result;
}
```

---

### 39. Trapping Rain Water
**Problem:** Calculate how much water can be trapped.

**Solution:** Two pointers or precompute max heights.

```java
int trap(int[] height) {
    int left = 0, right = height.length - 1;
    int leftMax = 0, rightMax = 0, water = 0;
    
    while(left < right) {
        if(height[left] < height[right]) {
            if(height[left] >= leftMax) leftMax = height[left];
            else water += leftMax - height[left];
            left++;
        } else {
            if(height[right] >= rightMax) rightMax = height[right];
            else water += rightMax - height[right];
            right--;
        }
    }
    return water;
}
```

---

### 40. Remove Duplicates from Sorted Array
**Problem:** Remove duplicates in-place from sorted array.

**Solution:** Two pointers - one for unique position, one for scanning.

```java
int removeDuplicates(int[] nums) {
    if(nums.length == 0) return 0;
    int i = 0;
    for(int j = 1; j < nums.length; j++) {
        if(nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }
    return i + 1;
}
```

---

### 41. Max Consecutive Ones
**Problem:** Find maximum consecutive 1s in binary array.

**Solution:** Count consecutive ones, track maximum.

```java
int findMaxConsecutiveOnes(int[] nums) {
    int maxCount = 0, currentCount = 0;
    for(int num : nums) {
        if(num == 1) {
            currentCount++;
            maxCount = Math.max(maxCount, currentCount);
        } else {
            currentCount = 0;
        }
    }
    return maxCount;
}
```

---

## Day 8: Greedy Algorithm

### 42. N Meetings in One Room
**Problem:** Maximum meetings that can be performed in one room.

**Solution:** Sort by end time, greedily select non-overlapping meetings.

```java
int maxMeetings(int[] start, int[] end, int n) {
    int[][] meetings = new int[n][2];
    for(int i = 0; i < n; i++) {
        meetings[i][0] = start[i];
        meetings[i][1] = end[i];
    }
    Arrays.sort(meetings, (a, b) -> a[1] - b[1]);
    
    int count = 1, lastEnd = meetings[0][1];
    for(int i = 1; i < n; i++) {
        if(meetings[i][0] > lastEnd) {
            count++;
            lastEnd = meetings[i][1];
        }
    }
    return count;
}
```

---

### 43. Minimum Platforms
**Problem:** Minimum platforms needed for train schedule.

**Solution:** Sort arrival and departure, use two pointers.

```java
int findPlatform(int[] arr, int[] dep, int n) {
    Arrays.sort(arr);
    Arrays.sort(dep);
    
    int platforms = 1, maxPlatforms = 1;
    int i = 1, j = 0;
    
    while(i < n && j < n) {
        if(arr[i] <= dep[j]) {
            platforms++;
            i++;
        } else {
            platforms--;
            j++;
        }
        maxPlatforms = Math.max(maxPlatforms, platforms);
    }
    return maxPlatforms;
}
```

---

### 44. Job Sequencing Problem
**Problem:** Schedule jobs to maximize profit with deadlines.

**Solution:** Sort by profit, use greedy approach with deadline slots.

```java
int[] JobScheduling(Job[] jobs, int n) {
    Arrays.sort(jobs, (a, b) -> b.profit - a.profit);
    
    int maxDeadline = 0;
    for(Job job : jobs) maxDeadline = Math.max(maxDeadline, job.deadline);
    
    int[] slot = new int[maxDeadline + 1];
    Arrays.fill(slot, -1);
    
    int countJobs = 0, maxProfit = 0;
    for(Job job : jobs) {
        for(int j = job.deadline; j > 0; j--) {
            if(slot[j] == -1) {
                slot[j] = job.id;
                countJobs++;
                maxProfit += job.profit;
                break;
            }
        }
    }
    return new int[]{countJobs, maxProfit};
}
```

---

### 45. Fractional Knapsack
**Problem:** Maximize value with fractional items allowed.

**Solution:** Sort by value/weight ratio, take greedily.

```java
double fractionalKnapsack(int W, Item[] items, int n) {
    Arrays.sort(items, (a, b) -> 
        Double.compare((double)b.value/b.weight, (double)a.value/a.weight));
    
    double totalValue = 0;
    for(Item item : items) {
        if(W >= item.weight) {
            totalValue += item.value;
            W -= item.weight;
        } else {
            totalValue += (double)item.value * W / item.weight;
            break;
        }
    }
    return totalValue;
}
```

---

### 46. Minimum Coins (Greedy - for Indian currency)
**Problem:** Find minimum coins needed for amount.

**Solution:** Greedy approach (works for canonical coin systems).

```java
int minCoins(int[] coins, int amount) {
    Arrays.sort(coins);
    int count = 0;
    
    for(int i = coins.length - 1; i >= 0; i--) {
        while(amount >= coins[i]) {
            amount -= coins[i];
            count++;
        }
    }
    return amount == 0 ? count : -1;
}
```

---

## Day 9: Recursion

### 47. Subset Sums
**Problem:** Find sum of all subsets.

**Solution:** Recursion - include or exclude each element.

```java
ArrayList<Integer> subsetSums(ArrayList<Integer> arr, int n) {
    ArrayList<Integer> result = new ArrayList<>();
    generateSubsets(arr, 0, 0, result);
    Collections.sort(result);
    return result;
}

void generateSubsets(ArrayList<Integer> arr, int index, int sum, ArrayList<Integer> result) {
    if(index == arr.size()) {
        result.add(sum);
        return;
    }
    generateSubsets(arr, index + 1, sum + arr.get(index), result);
    generateSubsets(arr, index + 1, sum, result);
}
```

---

### 48. Subsets II (with duplicates)
**Problem:** Find all unique subsets with duplicates in array.

**Solution:** Sort and skip duplicates during recursion.

```java
List<List<Integer>> subsetsWithDup(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, 0, new ArrayList<>(), result);
    return result;
}

void backtrack(int[] nums, int start, List<Integer> current, List<List<Integer>> result) {
    result.add(new ArrayList<>(current));
    for(int i = start; i < nums.length; i++) {
        if(i > start && nums[i] == nums[i-1]) continue;
        current.add(nums[i]);
        backtrack(nums, i + 1, current, result);
        current.remove(current.size() - 1);
    }
}
```

---

### 49. Combination Sum
**Problem:** Find combinations that sum to target (elements can be reused).

**Solution:** Backtracking with same index allowed.

```java
List<List<Integer>> combinationSum(int[] candidates, int target) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(candidates, target, 0, new ArrayList<>(), result);
    return result;
}

void backtrack(int[] candidates, int remain, int start, List<Integer> current, List<List<Integer>> result) {
    if(remain < 0) return;
    if(remain == 0) {
        result.add(new ArrayList<>(current));
        return;
    }
    for(int i = start; i < candidates.length; i++) {
        current.add(candidates[i]);
        backtrack(candidates, remain - candidates[i], i, current, result);
        current.remove(current.size() - 1);
    }
}
```

---

### 50. Combination Sum II (no reuse)
**Problem:** Find combinations that sum to target (each element used once).

**Solution:** Sort and skip duplicates, move to next index.

```java
List<List<Integer>> combinationSum2(int[] candidates, int target) {
    Arrays.sort(candidates);
    List<List<Integer>> result = new ArrayList<>();
    backtrack(candidates, target, 0, new ArrayList<>(), result);
    return result;
}

void backtrack(int[] candidates, int remain, int start, List<Integer> current, List<List<Integer>> result) {
    if(remain < 0) return;
    if(remain == 0) {
        result.add(new ArrayList<>(current));
        return;
    }
    for(int i = start; i < candidates.length; i++) {
        if(i > start && candidates[i] == candidates[i-1]) continue;
        current.add(candidates[i]);
        backtrack(candidates, remain - candidates[i], i + 1, current, result);
        current.remove(current.size() - 1);
    }
}
```

---

### 51. Palindrome Partitioning
**Problem:** Partition string into all possible palindrome substrings.

**Solution:** Backtracking, check palindrome for each substring.

```java
List<List<String>> partition(String s) {
    List<List<String>> result = new ArrayList<>();
    backtrack(s, 0, new ArrayList<>(), result);
    return result;
}

void backtrack(String s, int start, List<String> current, List<List<String>> result) {
    if(start == s.length()) {
        result.add(new ArrayList<>(current));
        return;
    }
    for(int i = start; i < s.length(); i++) {
        if(isPalindrome(s, start, i)) {
            current.add(s.substring(start, i + 1));
            backtrack(s, i + 1, current, result);
            current.remove(current.size() - 1);
        }
    }
}

boolean isPalindrome(String s, int left, int right) {
    while(left < right) {
        if(s.charAt(left++) != s.charAt(right--)) return false;
    }
    return true;
}
```

---

### 52. K-th Permutation Sequence
**Problem:** Find kth permutation of numbers 1 to n.

**Solution:** Mathematical approach using factorial.

```java
String getPermutation(int n, int k) {
    List<Integer> numbers = new ArrayList<>();
    int factorial = 1;
    for(int i = 1; i <= n; i++) {
        factorial *= i;
        numbers.add(i);
    }
    
    k--; // 0-indexed
    StringBuilder result = new StringBuilder();
    
    for(int i = 0; i < n; i++) {
        factorial /= (n - i);
        int index = k / factorial;
        result.append(numbers.get(index));
        numbers.remove(index);
        k %= factorial;
    }
    return result.toString();
}
```

---

## Day 10: Recursion and Backtracking

### 53. Print All Permutations
**Problem:** Generate all permutations of array.

**Solution:** Backtracking with swapping or using visited array.

```java
List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, 0, result);
    return result;
}

void backtrack(int[] nums, int start, List<List<Integer>> result) {
    if(start == nums.length) {
        List<Integer> perm = new ArrayList<>();
        for(int num : nums) perm.add(num);
        result.add(perm);
        return;
    }
    for(int i = start; i < nums.length; i++) {
        swap(nums, i, start);
        backtrack(nums, start + 1, result);
        swap(nums, i, start);
    }
}
```

---

### 54. N Queens
**Problem:** Place N queens on NxN board so no two attack each other.

**Solution:** Backtracking with column, diagonal checks.

```java
List<List<String>> solveNQueens(int n) {
    List<List<String>> result = new ArrayList<>();
    char[][] board = new char[n][n];
    for(int i = 0; i < n; i++) Arrays.fill(board[i], '.');
    
    backtrack(board, 0, result);
    return result;
}

void backtrack(char[][] board, int row, List<List<String>> result) {
    if(row == board.length) {
        result.add(construct(board));
        return;
    }
    for(int col = 0; col < board.length; col++) {
        if(isValid(board, row, col)) {
            board[row][col] = 'Q';
            backtrack(board, row + 1, result);
            board[row][col] = '.';
        }
    }
}

boolean isValid(char[][] board, int row, int col) {
    // Check column
    for(int i = 0; i < row; i++) {
        if(board[i][col] == 'Q') return false;
    }
    // Check diagonal
    for(int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
        if(board[i][j] == 'Q') return false;
    }
    for(int i = row - 1, j = col + 1; i >= 0 && j < board.length; i--, j++) {
        if(board[i][j] == 'Q') return false;
    }
    return true;
}
```

---

### 55. Sudoku Solver
**Problem:** Solve a 9x9 Sudoku puzzle.

**Solution:** Backtracking, try 1-9 for each empty cell.

```java
void solveSudoku(char[][] board) {
    solve(board);
}

boolean solve(char[][] board) {
    for(int i = 0; i < 9; i++) {
        for(int j = 0; j < 9; j++) {
            if(board[i][j] == '.') {
                for(char c = '1'; c <= '9'; c++) {
                    if(isValid(board, i, j, c)) {
                        board[i][j] = c;
                        if(solve(board)) return true;
                        board[i][j] = '.';
                    }
                }
                return false;
            }
        }
    }
    return true;
}

boolean isValid(char[][] board, int row, int col, char c) {
    for(int i = 0; i < 9; i++) {
        if(board[row][i] == c || board[i][col] == c ||
           board[3*(row/3) + i/3][3*(col/3) + i%3] == c) return false;
    }
    return true;
}
```

---

### 56. M Coloring Problem
**Problem:** Color graph with m colors so no adjacent nodes have same color.

**Solution:** Backtracking, try each color for each node.

```java
boolean graphColoring(boolean[][] graph, int m, int n) {
    int[] color = new int[n];
    return solve(graph, m, color, 0, n);
}

boolean solve(boolean[][] graph, int m, int[] color, int node, int n) {
    if(node == n) return true;
    
    for(int c = 1; c <= m; c++) {
        if(isSafe(graph, color, node, c, n)) {
            color[node] = c;
            if(solve(graph, m, color, node + 1, n)) return true;
            color[node] = 0;
        }
    }
    return false;
}

boolean isSafe(boolean[][] graph, int[] color, int node, int c, int n) {
    for(int i = 0; i < n; i++) {
        if(graph[node][i] && color[i] == c) return false;
    }
    return true;
}
```

---

### 57. Rat in a Maze
**Problem:** Find all paths from top-left to bottom-right in maze.

**Solution:** Backtracking with 4 directions (D, L, R, U).

```java
ArrayList<String> findPath(int[][] m, int n) {
    ArrayList<String> result = new ArrayList<>();
    if(m[0][0] == 0) return result;
    
    boolean[][] visited = new boolean[n][n];
    solve(m, 0, 0, n, "", result, visited);
    return result;
}

void solve(int[][] m, int i, int j, int n, String path, ArrayList<String> result, boolean[][] visited) {
    if(i == n-1 && j == n-1) {
        result.add(path);
        return;
    }
    
    visited[i][j] = true;
    
    // Down
    if(i+1 < n && m[i+1][j] == 1 && !visited[i+1][j]) 
        solve(m, i+1, j, n, path + "D", result, visited);
    // Left
    if(j-1 >= 0 && m[i][j-1] == 1 && !visited[i][j-1])
        solve(m, i, j-1, n, path + "L", result, visited);
    // Right
    if(j+1 < n && m[i][j+1] == 1 && !visited[i][j+1])
        solve(m, i, j+1, n, path + "R", result, visited);
    // Up
    if(i-1 >= 0 && m[i-1][j] == 1 && !visited[i-1][j])
        solve(m, i-1, j, n, path + "U", result, visited);
    
    visited[i][j] = false;
}
```

---

### 58. Word Break (Print all ways)
**Problem:** Split string into dictionary words in all possible ways.

**Solution:** Backtracking, check prefix in dictionary.

```java
List<String> wordBreak(String s, List<String> wordDict) {
    Set<String> dict = new HashSet<>(wordDict);
    List<String> result = new ArrayList<>();
    backtrack(s, dict, 0, new ArrayList<>(), result);
    return result;
}

void backtrack(String s, Set<String> dict, int start, List<String> current, List<String> result) {
    if(start == s.length()) {
        result.add(String.join(" ", current));
        return;
    }
    for(int end = start + 1; end <= s.length(); end++) {
        String word = s.substring(start, end);
        if(dict.contains(word)) {
            current.add(word);
            backtrack(s, dict, end, current, result);
            current.remove(current.size() - 1);
        }
    }
}
```

---

## Day 11: Binary Search

### 59. Nth Root of M
**Problem:** Find nth root of m (return -1 if not perfect root).

**Solution:** Binary search on answer.

```java
int NthRoot(int n, int m) {
    int low = 1, high = m;
    while(low <= high) {
        int mid = low + (high - low) / 2;
        long val = (long)Math.pow(mid, n);
        
        if(val == m) return mid;
        else if(val < m) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```

---

### 60. Matrix Median
**Problem:** Find median of row-wise sorted matrix.

**Solution:** Binary search on value range, count elements <= mid.

```java
int findMedian(int[][] matrix) {
    int r = matrix.length, c = matrix[0].length;
    int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;
    
    for(int i = 0; i < r; i++) {
        min = Math.min(min, matrix[i][0]);
        max = Math.max(max, matrix[i][c-1]);
    }
    
    int desired = (r * c + 1) / 2;
    while(min < max) {
        int mid = min + (max - min) / 2;
        int count = 0;
        
        for(int i = 0; i < r; i++) {
            count += countLessEqual(matrix[i], mid);
        }
        
        if(count < desired) min = mid + 1;
        else max = mid;
    }
    return min;
}

int countLessEqual(int[] row, int target) {
    int left = 0, right = row.length - 1;
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if(row[mid] <= target) left = mid + 1;
        else right = mid - 1;
    }
    return left;
}
```

---

### 61. Single Element in Sorted Array
**Problem:** Find element that appears once in sorted array (others appear twice).

**Solution:** Binary search, check parity of index.

```java
int singleNonDuplicate(int[] nums) {
    int left = 0, right = nums.length - 1;
    
    while(left < right) {
        int mid = left + (right - left) / 2;
        if(mid % 2 == 1) mid--;
        
        if(nums[mid] == nums[mid + 1]) left = mid + 2;
        else right = mid;
    }
    return nums[left];
}
```

---

### 62. Search in Rotated Sorted Array
**Problem:** Search in rotated sorted array.

**Solution:** Binary search, determine which half is sorted.

```java
int search(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if(nums[mid] == target) return mid;
        
        if(nums[left] <= nums[mid]) {
            if(target >= nums[left] && target < nums[mid]) right = mid - 1;
            else left = mid + 1;
        } else {
            if(target > nums[mid] && target <= nums[right]) left = mid + 1;
            else right = mid - 1;
        }
    }
    return -1;
}
```

---

### 63. Median of Two Sorted Arrays
**Problem:** Find median of two sorted arrays.

**Solution:** Binary search on smaller array, partition both arrays.

```java
double findMedianSortedArrays(int[] nums1, int[] nums2) {
    if(nums1.length > nums2.length) return findMedianSortedArrays(nums2, nums1);
    
    int m = nums1.length, n = nums2.length;
    int low = 0, high = m;
    
    while(low <= high) {
        int partition1 = (low + high) / 2;
        int partition2 = (m + n + 1) / 2 - partition1;
        
        int maxLeft1 = (partition1 == 0) ? Integer.MIN_VALUE : nums1[partition1 - 1];
        int minRight1 = (partition1 == m) ? Integer.MAX_VALUE : nums1[partition1];
        int maxLeft2 = (partition2 == 0) ? Integer.MIN_VALUE : nums2[partition2 - 1];
        int minRight2 = (partition2 == n) ? Integer.MAX_VALUE : nums2[partition2];
        
        if(maxLeft1 <= minRight2 && maxLeft2 <= minRight1) {
            if((m + n) % 2 == 0) {
                return (Math.max(maxLeft1, maxLeft2) + Math.min(minRight1, minRight2)) / 2.0;
            } else {
                return Math.max(maxLeft1, maxLeft2);
            }
        } else if(maxLeft1 > minRight2) {
            high = partition1 - 1;
        } else {
            low = partition1 + 1;
        }
    }
    return 0.0;
}
```

---

### 64. Kth Element of Two Sorted Arrays
**Problem:** Find kth element in union of two sorted arrays.

**Solution:** Binary search similar to median problem.

```java
int kthElement(int[] arr1, int[] arr2, int k) {
    int m = arr1.length, n = arr2.length;
    if(m > n) return kthElement(arr2, arr1, k);
    
    int low = Math.max(0, k - n), high = Math.min(k, m);
    
    while(low <= high) {
        int cut1 = (low + high) / 2;
        int cut2 = k - cut1;
        
        int left1 = (cut1 == 0) ? Integer.MIN_VALUE : arr1[cut1 - 1];
        int left2 = (cut2 == 0) ? Integer.MIN_VALUE : arr2[cut2 - 1];
        int right1 = (cut1 == m) ? Integer.MAX_VALUE : arr1[cut1];
        int right2 = (cut2 == n) ? Integer.MAX_VALUE : arr2[cut2];
        
        if(left1 <= right2 && left2 <= right1) {
            return Math.max(left1, left2);
        } else if(left1 > right2) {
            high = cut1 - 1;
        } else {
            low = cut1 + 1;
        }
    }
    return -1;
}
```

---

### 65. Allocate Minimum Number of Pages
**Problem:** Allocate books to students to minimize maximum pages.

**Solution:** Binary search on answer (max pages a student reads).

```java
int findPages(int[] arr, int n, int m) {
    if(m > n) return -1;
    
    int low = arr[0], high = 0;
    for(int pages : arr) {
        low = Math.max(low, pages);
        high += pages;
    }
    
    int result = -1;
    while(low <= high) {
        int mid = low + (high - low) / 2;
        if(isPossible(arr, n, m, mid)) {
            result = mid;
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    return result;
}

boolean isPossible(int[] arr, int n, int m, int maxPages) {
    int students = 1, currentPages = 0;
    for(int pages : arr) {
        if(currentPages + pages > maxPages) {
            students++;
            currentPages = pages;
            if(students > m) return false;
        } else {
            currentPages += pages;
        }
    }
    return true;
}
```

---

### 66. Aggressive Cows
**Problem:** Place cows in stalls to maximize minimum distance.

**Solution:** Binary search on minimum distance.

```java
int aggressiveCows(int[] stalls, int k) {
    Arrays.sort(stalls);
    int low = 1, high = stalls[stalls.length - 1] - stalls[0];
    int result = 0;
    
    while(low <= high) {
        int mid = low + (high - low) / 2;
        if(canPlace(stalls, k, mid)) {
            result = mid;
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return result;
}

boolean canPlace(int[] stalls, int cows, int minDist) {
    int count = 1, lastPos = stalls[0];
    for(int i = 1; i < stalls.length; i++) {
        if(stalls[i] - lastPos >= minDist) {
            count++;
            lastPos = stalls[i];
            if(count == cows) return true;
        }
    }
    return false;
}
```

---

## Day 12: Heaps

### 67. Max Heap / Min Heap Implementation
**Problem:** Implement heap data structure.

**Solution:** Use array, maintain heap property with heapify.

```java
class MaxHeap {
    private int[] heap;
    private int size;
    private int capacity;
    
    public MaxHeap(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        this.heap = new int[capacity];
    }
    
    private int parent(int i) { return (i - 1) / 2; }
    private int left(int i) { return 2 * i + 1; }
    private int right(int i) { return 2 * i + 2; }
    
    public void insert(int key) {
        if(size == capacity) return;
        
        heap[size] = key;
        int i = size;
        size++;
        
        while(i != 0 && heap[parent(i)] < heap[i]) {
            swap(i, parent(i));
            i = parent(i);
        }
    }
    
    public int extractMax() {
        if(size == 0) return Integer.MIN_VALUE;
        if(size == 1) { size--; return heap[0]; }
        
        int root = heap[0];
        heap[0] = heap[size - 1];
        size--;
        heapify(0);
        return root;
    }
    
    private void heapify(int i) {
        int l = left(i), r = right(i), largest = i;
        
        if(l < size && heap[l] > heap[largest]) largest = l;
        if(r < size && heap[r] > heap[largest]) largest = r;
        
        if(largest != i) {
            swap(i, largest);
            heapify(largest);
        }
    }
    
    private void swap(int i, int j) {
        int temp = heap[i];
        heap[i] = heap[j];
        heap[j] = temp;
    }
}
```

---

### 68. Kth Largest Element
**Problem:** Find kth largest element in array.

**Solution:** Min heap of size k or quickselect.

```java
int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    
    for(int num : nums) {
        minHeap.offer(num);
        if(minHeap.size() > k) {
            minHeap.poll();
        }
    }
    return minHeap.peek();
}
```

---

### 69. Maximum Sum Combination
**Problem:** Find k maximum sum combinations from two arrays.

**Solution:** Max heap with pairs, track visited combinations.

```java
List<Integer> maxCombinations(int[] A, int[] B, int k) {
    Arrays.sort(A);
    Arrays.sort(B);
    int n = A.length;
    
    PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> b[0] - a[0]);
    Set<String> visited = new HashSet<>();
    
    maxHeap.offer(new int[]{A[n-1] + B[n-1], n-1, n-1});
    visited.add((n-1) + "," + (n-1));
    
    List<Integer> result = new ArrayList<>();
    while(k-- > 0 && !maxHeap.isEmpty()) {
        int[] curr = maxHeap.poll();
        result.add(curr[0]);
        
        int i = curr[1], j = curr[2];
        if(i > 0 && !visited.contains((i-1) + "," + j)) {
            maxHeap.offer(new int[]{A[i-1] + B[j], i-1, j});
            visited.add((i-1) + "," + j);
        }
        if(j > 0 && !visited.contains(i + "," + (j-1))) {
            maxHeap.offer(new int[]{A[i] + B[j-1], i, j-1});
            visited.add(i + "," + (j-1));
        }
    }
    return result;
}
```

---

### 70. Find Median from Data Stream
**Problem:** Design structure to find median from stream of integers.

**Solution:** Two heaps - max heap for lower half, min heap for upper half.

```java
class MedianFinder {
    PriorityQueue<Integer> maxHeap; // Lower half
    PriorityQueue<Integer> minHeap; // Upper half
    
    public MedianFinder() {
        maxHeap = new PriorityQueue<>((a, b) -> b - a);
        minHeap = new PriorityQueue<>();
    }
    
    public void addNum(int num) {
        if(maxHeap.isEmpty() || num <= maxHeap.peek()) {
            maxHeap.offer(num);
        } else {
            minHeap.offer(num);
        }
        
        // Balance heaps
        if(maxHeap.size() > minHeap.size() + 1) {
            minHeap.offer(maxHeap.poll());
        } else if(minHeap.size() > maxHeap.size()) {
            maxHeap.offer(minHeap.poll());
        }
    }
    
    public double findMedian() {
        if(maxHeap.size() == minHeap.size()) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        }
        return maxHeap.peek();
    }
}
```

---

### 71. Merge K Sorted Arrays
**Problem:** Merge k sorted arrays into one sorted array.

**Solution:** Min heap to track smallest elements from each array.

```java
int[] mergeKArrays(int[][] arr, int k) {
    PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);
    int totalSize = 0;
    
    for(int i = 0; i < k; i++) {
        if(arr[i].length > 0) {
            minHeap.offer(new int[]{arr[i][0], i, 0});
            totalSize += arr[i].length;
        }
    }
    
    int[] result = new int[totalSize];
    int idx = 0;
    
    while(!minHeap.isEmpty()) {
        int[] curr = minHeap.poll();
        result[idx++] = curr[0];
        
        int arrayIdx = curr[1], elementIdx = curr[2];
        if(elementIdx + 1 < arr[arrayIdx].length) {
            minHeap.offer(new int[]{arr[arrayIdx][elementIdx + 1], arrayIdx, elementIdx + 1});
        }
    }
    return result;
}
```

---

### 72. Top K Frequent Elements
**Problem:** Find k most frequent elements.

**Solution:** HashMap for frequency, min heap of size k.

```java
int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for(int num : nums) {
        freq.put(num, freq.getOrDefault(num, 0) + 1);
    }
    
    PriorityQueue<int[]> minHeap = new PriorityQueue<>((a, b) -> a[1] - b[1]);
    
    for(Map.Entry<Integer, Integer> entry : freq.entrySet()) {
        minHeap.offer(new int[]{entry.getKey(), entry.getValue()});
        if(minHeap.size() > k) minHeap.poll();
    }
    
    int[] result = new int[k];
    for(int i = 0; i < k; i++) {
        result[i] = minHeap.poll()[0];
    }
    return result;
}
```

---

## Day 13: Stack and Queue

### 73. Implement Stack using Arrays
**Problem:** Implement stack using array.

**Solution:** Use array with top pointer.

```java
class Stack {
    private int[] arr;
    private int top;
    private int capacity;
    
    public Stack(int size) {
        arr = new int[size];
        capacity = size;
        top = -1;
    }
    
    public void push(int x) {
        if(top == capacity - 1) throw new RuntimeException("Stack Overflow");
        arr[++top] = x;
    }
    
    public int pop() {
        if(top == -1) throw new RuntimeException("Stack Underflow");
        return arr[top--];
    }
    
    public int peek() {
        if(top == -1) throw new RuntimeException("Stack is empty");
        return arr[top];
    }
    
    public boolean isEmpty() {
        return top == -1;
    }
    
    public int size() {
        return top + 1;
    }
}
```

---

### 74. Implement Queue using Arrays
**Problem:** Implement queue using array.

**Solution:** Circular array with front and rear pointers.

```java
class Queue {
    private int[] arr;
    private int front, rear, size, capacity;
    
    public Queue(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }
    
    public void enqueue(int x) {
        if(size == capacity) throw new RuntimeException("Queue is full");
        rear = (rear + 1) % capacity;
        arr[rear] = x;
        size++;
    }
    
    public int dequeue() {
        if(size == 0) throw new RuntimeException("Queue is empty");
        int item = arr[front];
        front = (front + 1) % capacity;
        size--;
        return item;
    }
    
    public int peek() {
        if(size == 0) throw new RuntimeException("Queue is empty");
        return arr[front];
    }
    
    public boolean isEmpty() {
        return size == 0;
    }
}
```

---

### 75. Implement Stack using Queue
**Problem:** Implement stack using queue(s).

**Solution:** Use one queue, rotate on push or pop.

```java
class MyStack {
    Queue<Integer> queue;
    
    public MyStack() {
        queue = new LinkedList<>();
    }
    
    public void push(int x) {
        queue.offer(x);
        int size = queue.size();
        while(size > 1) {
            queue.offer(queue.poll());
            size--;
        }
    }
    
    public int pop() {
        return queue.poll();
    }
    
    public int top() {
        return queue.peek();
    }
    
    public boolean empty() {
        return queue.isEmpty();
    }
}
```

---

### 76. Implement Queue using Stack
**Problem:** Implement queue using stack(s).

**Solution:** Use two stacks - input and output.

```java
class MyQueue {
    Stack<Integer> input, output;
    
    public MyQueue() {
        input = new Stack<>();
        output = new Stack<>();
    }
    
    public void push(int x) {
        input.push(x);
    }
    
    public int pop() {
        if(output.isEmpty()) {
            while(!input.isEmpty()) {
                output.push(input.pop());
            }
        }
        return output.pop();
    }
    
    public int peek() {
        if(output.isEmpty()) {
            while(!input.isEmpty()) {
                output.push(input.pop());
            }
        }
        return output.peek();
    }
    
    public boolean empty() {
        return input.isEmpty() && output.isEmpty();
    }
}
```

---

### 77. Valid Parentheses
**Problem:** Check if string has valid parentheses.

**Solution:** Stack to match opening and closing brackets.

```java
boolean isValid(String s) {
    Stack<Character> stack = new Stack<>();
    Map<Character, Character> map = new HashMap<>();
    map.put(')', '(');
    map.put('}', '{');
    map.put(']', '[');
    
    for(char c : s.toCharArray()) {
        if(map.containsKey(c)) {
            if(stack.isEmpty() || stack.pop() != map.get(c)) return false;
        } else {
            stack.push(c);
        }
    }
    return stack.isEmpty();
}
```

---

### 78. Next Greater Element
**Problem:** Find next greater element for each element in array.

**Solution:** Stack to track indices in decreasing order.

```java
int[] nextGreaterElement(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    Arrays.fill(result, -1);
    Stack<Integer> stack = new Stack<>();
    
    for(int i = 0; i < n; i++) {
        while(!stack.isEmpty() && nums[stack.peek()] < nums[i]) {
            result[stack.pop()] = nums[i];
        }
        stack.push(i);
    }
    return result;
}
```

---

### 79. Sort a Stack
**Problem:** Sort a stack using recursion.

**Solution:** Pop all elements, insert in sorted order.

```java
void sortStack(Stack<Integer> stack) {
    if(stack.isEmpty()) return;
    
    int top = stack.pop();
    sortStack(stack);
    sortedInsert(stack, top);
}

void sortedInsert(Stack<Integer> stack, int element) {
    if(stack.isEmpty() || stack.peek() <= element) {
        stack.push(element);
        return;
    }
    
    int top = stack.pop();
    sortedInsert(stack, element);
    stack.push(top);
}
```

---

## Day 14: Stack and Queue Part II

### 80. Next Smaller Element
**Problem:** Find next smaller element for each element.

**Solution:** Stack similar to next greater element.

```java
int[] nextSmallerElement(int[] arr) {
    int n = arr.length;
    int[] result = new int[n];
    Arrays.fill(result, -1);
    Stack<Integer> stack = new Stack<>();
    
    for(int i = 0; i < n; i++) {
        while(!stack.isEmpty() && arr[stack.peek()] > arr[i]) {
            result[stack.pop()] = arr[i];
        }
        stack.push(i);
    }
    return result;
}
```

---

### 81. LRU Cache
**Problem:** Design LRU (Least Recently Used) cache.

**Solution:** HashMap + Doubly Linked List.

```java
class LRUCache {
    class Node {
        int key, value;
        Node prev, next;
        Node(int k, int v) { key = k; value = v; }
    }
    
    private Map<Integer, Node> map;
    private Node head, tail;
    private int capacity;
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<>();
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        if(!map.containsKey(key)) return -1;
        Node node = map.get(key);
        remove(node);
        insert(node);
        return node.value;
    }
    
    public void put(int key, int value) {
        if(map.containsKey(key)) {
            remove(map.get(key));
        }
        if(map.size() == capacity) {
            remove(tail.prev);
        }
        insert(new Node(key, value));
    }
    
    private void remove(Node node) {
        map.remove(node.key);
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    
    private void insert(Node node) {
        map.put(node.key, node);
        node.next = head.next;
        node.next.prev = node;
        head.next = node;
        node.prev = head;
    }
}
```

---

### 82. LFU Cache
**Problem:** Design LFU (Least Frequently Used) cache.

**Solution:** HashMap + frequency map with doubly linked lists.

```java
class LFUCache {
    class Node {
        int key, value, freq;
        Node prev, next;
        Node(int k, int v) { key = k; value = v; freq = 1; }
    }
    
    private Map<Integer, Node> cache;
    private Map<Integer, Node> freqMap; // freq -> dummy head
    private int capacity, minFreq;
    
    public LFUCache(int capacity) {
        this.capacity = capacity;
        cache = new HashMap<>();
        freqMap = new HashMap<>();
        minFreq = 0;
    }
    
    public int get(int key) {
        if(!cache.containsKey(key)) return -1;
        Node node = cache.get(key);
        updateFreq(node);
        return node.value;
    }
    
    public void put(int key, int value) {
        if(capacity == 0) return;
        
        if(cache.containsKey(key)) {
            Node node = cache.get(key);
            node.value = value;
            updateFreq(node);
        } else {
            if(cache.size() == capacity) {
                Node head = freqMap.get(minFreq);
                Node toRemove = head.prev;
                remove(toRemove);
                cache.remove(toRemove.key);
            }
            Node node = new Node(key, value);
            cache.put(key, node);
            minFreq = 1;
            addToFreqList(node);
        }
    }
    
    private void updateFreq(Node node) {
        remove(node);
        node.freq++;
        addToFreqList(node);
        
        if(!freqMap.containsKey(node.freq - 1) && minFreq == node.freq - 1) {
            minFreq++;
        }
    }
    
    private void addToFreqList(Node node) {
        if(!freqMap.containsKey(node.freq)) {
            Node head = new Node(0, 0);
            Node tail = new Node(0, 0);
            head.next = tail;
            tail.prev = head;
            freqMap.put(node.freq, head);
        }
        Node head = freqMap.get(node.freq);
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
        node.prev = head;
    }
    
    private void remove(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
}
```

---

### 83. Largest Rectangle in Histogram
**Problem:** Find largest rectangle area in histogram.

**Solution:** Stack to find next/previous smaller elements.

```java
int largestRectangleArea(int[] heights) {
    Stack<Integer> stack = new Stack<>();
    int maxArea = 0;
    int n = heights.length;
    
    for(int i = 0; i <= n; i++) {
        int h = (i == n) ? 0 : heights[i];
        
        while(!stack.isEmpty() && h < heights[stack.peek()]) {
            int height = heights[stack.pop()];
            int width = stack.isEmpty() ? i : i - stack.peek() - 1;
            maxArea = Math.max(maxArea, height * width);
        }
        stack.push(i);
    }
    return maxArea;
}
```

---

### 84. Sliding Window Maximum
**Problem:** Find maximum in each sliding window of size k.

**Solution:** Deque to maintain decreasing order of indices.

```java
int[] maxSlidingWindow(int[] nums, int k) {
    Deque<Integer> deque = new ArrayDeque<>();
    int n = nums.length;
    int[] result = new int[n - k + 1];
    int idx = 0;
    
    for(int i = 0; i < n; i++) {
        // Remove elements outside window
        while(!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
            deque.pollFirst();
        }
        
        // Remove smaller elements
        while(!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
            deque.pollLast();
        }
        
        deque.offerLast(i);
        
        if(i >= k - 1) {
            result[idx++] = nums[deque.peekFirst()];
        }
    }
    return result;
}
```

---

### 85. Min Stack
**Problem:** Design stack with O(1) min operation.

**Solution:** Store pairs (value, current_min) or use two stacks.

```java
class MinStack {
    Stack<Long> stack;
    long min;
    
    public MinStack() {
        stack = new Stack<>();
    }
    
    public void push(int val) {
        if(stack.isEmpty()) {
            stack.push(0L);
            min = val;
        } else {
            stack.push(val - min);
            if(val < min) min = val;
        }
    }
    
    public void pop() {
        if(stack.isEmpty()) return;
        long pop = stack.pop();
        if(pop < 0) min = min - pop;
    }
    
    public int top() {
        long top = stack.peek();
        if(top > 0) return (int)(top + min);
        return (int)min;
    }
    
    public int getMin() {
        return (int)min;
    }
}
```

---

### 86. Rotten Oranges
**Problem:** Find minimum time to rot all oranges (BFS problem, often in Stack/Queue section).

**Solution:** Multi-source BFS.

```java
int orangesRotting(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    Queue<int[]> queue = new LinkedList<>();
    int fresh = 0;
    
    for(int i = 0; i < m; i++) {
        for(int j = 0; j < n; j++) {
            if(grid[i][j] == 2) queue.offer(new int[]{i, j});
            else if(grid[i][j] == 1) fresh++;
        }
    }
    
    if(fresh == 0) return 0;
    
    int[][] dirs = {{-1,0}, {1,0}, {0,-1}, {0,1}};
    int minutes = 0;
    
    while(!queue.isEmpty()) {
        int size = queue.size();
        boolean rotted = false;
        
        for(int i = 0; i < size; i++) {
            int[] curr = queue.poll();
            
            for(int[] dir : dirs) {
                int x = curr[0] + dir[0];
                int y = curr[1] + dir[1];
                
                if(x >= 0 && x < m && y >= 0 && y < n && grid[x][y] == 1) {
                    grid[x][y] = 2;
                    queue.offer(new int[]{x, y});
                    fresh--;
                    rotted = true;
                }
            }
        }
        if(rotted) minutes++;
    }
    return fresh == 0 ? minutes : -1;
}
```

---

## Day 15: String

### 87. Reverse Words in a String
**Problem:** Reverse the order of words in a string.

**Solution:** Split by spaces, reverse order.

```java
String reverseWords(String s) {
    String[] words = s.trim().split("\\s+");
    StringBuilder result = new StringBuilder();
    
    for(int i = words.length - 1; i >= 0; i--) {
        result.append(words[i]);
        if(i > 0) result.append(" ");
    }
    return result.toString();
}
```

---

### 88. Longest Palindromic Substring
**Problem:** Find longest palindromic substring.

**Solution:** Expand around center or DP.

```java
String longestPalindrome(String s) {
    if(s.length() < 2) return s;
    
    int start = 0, maxLen = 1;
    
    for(int i = 0; i < s.length(); i++) {
        // Odd length palindrome
        int len1 = expandAroundCenter(s, i, i);
        // Even length palindrome
        int len2 = expandAroundCenter(s, i, i + 1);
        
        int len = Math.max(len1, len2);
        if(len > maxLen) {
            start = i - (len - 1) / 2;
            maxLen = len;
        }
    }
    return s.substring(start, start + maxLen);
}

int expandAroundCenter(String s, int left, int right) {
    while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
        left--;
        right++;
    }
    return right - left - 1;
}
```

---

### 89. Roman to Integer
**Problem:** Convert Roman numeral to integer.

**Solution:** Map symbols, subtract if smaller before larger.

```java
int romanToInt(String s) {
    Map<Character, Integer> map = new HashMap<>();
    map.put('I', 1); map.put('V', 5); map.put('X', 10);
    map.put('L', 50); map.put('C', 100); map.put('D', 500); map.put('M', 1000);
    
    int result = 0;
    for(int i = 0; i < s.length(); i++) {
        int curr = map.get(s.charAt(i));
        if(i + 1 < s.length() && curr < map.get(s.charAt(i + 1))) {
            result -= curr;
        } else {
            result += curr;
        }
    }
    return result;
}
```

---

### 90. Implement ATOI/STRTOI
**Problem:** Convert string to integer with overflow handling.

**Solution:** Parse character by character, handle edge cases.

```java
int myAtoi(String s) {
    if(s == null || s.length() == 0) return 0;
    
    int i = 0, n = s.length();
    // Skip whitespace
    while(i < n && s.charAt(i) == ' ') i++;
    
    if(i == n) return 0;
    
    // Check sign
    int sign = 1;
    if(s.charAt(i) == '+' || s.charAt(i) == '-') {
        sign = (s.charAt(i) == '-') ? -1 : 1;
        i++;
    }
    
    // Convert digits
    long result = 0;
    while(i < n && Character.isDigit(s.charAt(i))) {
        result = result * 10 + (s.charAt(i) - '0');
        
        // Check overflow
        if(result * sign > Integer.MAX_VALUE) return Integer.MAX_VALUE;
        if(result * sign < Integer.MIN_VALUE) return Integer.MIN_VALUE;
        
        i++;
    }
    return (int)(result * sign);
}
```

---

### 91. Longest Common Prefix
**Problem:** Find longest common prefix among array of strings.

**Solution:** Compare character by character or divide and conquer.

```java
String longestCommonPrefix(String[] strs) {
    if(strs.length == 0) return "";
    
    String prefix = strs[0];
    for(int i = 1; i < strs.length; i++) {
        while(strs[i].indexOf(prefix) != 0) {
            prefix = prefix.substring(0, prefix.length() - 1);
            if(prefix.isEmpty()) return "";
        }
    }
    return prefix;
}
```

---

### 92. Rabin Karp Algorithm (String Matching)
**Problem:** Find pattern in text using rolling hash.

**Solution:** Use polynomial rolling hash.

```java
int rabinKarp(String text, String pattern) {
    int n = text.length(), m = pattern.length();
    if(m > n) return -1;
    
    int prime = 101;
    long patternHash = 0, textHash = 0, h = 1;
    
    // h = pow(256, m-1) % prime
    for(int i = 0; i < m - 1; i++) h = (h * 256) % prime;
    
    // Calculate initial hashes
    for(int i = 0; i < m; i++) {
        patternHash = (256 * patternHash + pattern.charAt(i)) % prime;
        textHash = (256 * textHash + text.charAt(i)) % prime;
    }
    
    // Slide pattern
    for(int i = 0; i <= n - m; i++) {
        if(patternHash == textHash) {
            boolean match = true;
            for(int j = 0; j < m; j++) {
                if(text.charAt(i + j) != pattern.charAt(j)) {
                    match = false;
                    break;
                }
            }
            if(match) return i;
        }
        
        if(i < n - m) {
            textHash = (256 * (textHash - text.charAt(i) * h) + text.charAt(i + m)) % prime;
            if(textHash < 0) textHash += prime;
        }
    }
    return -1;
}
```

---

### 93. KMP Algorithm (Pattern Matching)
**Problem:** Find pattern in text efficiently.

**Solution:** Build LPS (Longest Proper Prefix which is also Suffix) array.

```java
int KMP(String text, String pattern) {
    int n = text.length(), m = pattern.length();
    int[] lps = computeLPS(pattern);
    
    int i = 0, j = 0;
    while(i < n) {
        if(text.charAt(i) == pattern.charAt(j)) {
            i++;
            j++;
        }
        
        if(j == m) return i - j;
        else if(i < n && text.charAt(i) != pattern.charAt(j)) {
            if(j != 0) j = lps[j - 1];
            else i++;
        }
    }
    return -1;
}

int[] computeLPS(String pattern) {
    int m = pattern.length();
    int[] lps = new int[m];
    int len = 0, i = 1;
    
    while(i < m) {
        if(pattern.charAt(i) == pattern.charAt(len)) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if(len != 0) len = lps[len - 1];
            else { lps[i] = 0; i++; }
        }
    }
    return lps;
}
```

---

### 94. Minimum Characters to Make String Palindrome
**Problem:** Find minimum insertions at front to make palindrome.

**Solution:** Use KMP on string + reverse.

```java
int minCharsToAddFront(String s) {
    String rev = new StringBuilder(s).reverse().toString();
    String combined = s + "#" + rev;
    
    int[] lps = computeLPS(combined);
    return s.length() - lps[combined.length() - 1];
}
```

---

### 95. Check for Anagrams
**Problem:** Check if two strings are anagrams.

**Solution:** Count character frequencies.

```java
boolean isAnagram(String s, String t) {
    if(s.length() != t.length()) return false;
    
    int[] count = new int[26];
    for(int i = 0; i < s.length(); i++) {
        count[s.charAt(i) - 'a']++;
        count[t.charAt(i) - 'a']--;
    }
    
    for(int c : count) {
        if(c != 0) return false;
    }
    return true;
}
```

---

### 96. Count and Say
**Problem:** Generate nth term of count-and-say sequence.

**Solution:** Iteratively build sequence.

```java
String countAndSay(int n) {
    String s = "1";
    
    for(int i = 1; i < n; i++) {
        StringBuilder next = new StringBuilder();
        int count = 1;
        char current = s.charAt(0);
        
        for(int j = 1; j < s.length(); j++) {
            if(s.charAt(j) == current) {
                count++;
            } else {
                next.append(count).append(current);
                current = s.charAt(j);
                count = 1;
            }
        }
        next.append(count).append(current);
        s = next.toString();
    }
    return s;
}
```

---

### 97. Compare Version Numbers
**Problem:** Compare two version strings.

**Solution:** Split by '.', compare numbers.

```java
int compareVersion(String version1, String version2) {
    String[] v1 = version1.split("\\.");
    String[] v2 = version2.split("\\.");
    
    int len = Math.max(v1.length, v2.length);
    
    for(int i = 0; i < len; i++) {
        int num1 = (i < v1.length) ? Integer.parseInt(v1[i]) : 0;
        int num2 = (i < v2.length) ? Integer.parseInt(v2[i]) : 0;
        
        if(num1 < num2) return -1;
        if(num1 > num2) return 1;
    }
    return 0;
}
```

---

## Day 16: String Part II

### 98. Z-Algorithm (Pattern Matching)
**Problem:** Find all occurrences of pattern in text.

**Solution:** Build Z-array for pattern + text.

```java
List<Integer> zAlgorithm(String text, String pattern) {
    String combined = pattern + "$" + text;
    int[] z = buildZArray(combined);
    
    List<Integer> result = new ArrayList<>();
    for(int i = pattern.length() + 1; i < combined.length(); i++) {
        if(z[i] == pattern.length()) {
            result.add(i - pattern.length() - 1);
        }
    }
    return result;
}

int[] buildZArray(String s) {
    int n = s.length();
    int[] z = new int[n];
    int l = 0, r = 0;
    
    for(int i = 1; i < n; i++) {
        if(i > r) {
            l = r = i;
            while(r < n && s.charAt(r - l) == s.charAt(r)) r++;
            z[i] = r - l;
            r--;
        } else {
            int k = i - l;
            if(z[k] < r - i + 1) {
                z[i] = z[k];
            } else {
                l = i;
                while(r < n && s.charAt(r - l) == s.charAt(r)) r++;
                z[i] = r - l;
                r--;
            }
        }
    }
    return z;
}
```

---

## Day 17: Binary Tree

### 99. Inorder Traversal
**Problem:** Traverse tree in inorder (Left-Root-Right).

**Solution:** Recursive or iterative with stack.

```java
List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    Stack<TreeNode> stack = new Stack<>();
    TreeNode curr = root;
    
    while(curr != null || !stack.isEmpty()) {
        while(curr != null) {
            stack.push(curr);
            curr = curr.left;
        }
        curr = stack.pop();
        result.add(curr.val);
        curr = curr.right;
    }
    return result;
}
```

---

### 100. Preorder Traversal
**Problem:** Traverse tree in preorder (Root-Left-Right).

**Solution:** Recursive or iterative with stack.

```java
List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if(root == null) return result;
    
    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);
    
    while(!stack.isEmpty()) {
        TreeNode node = stack.pop();
        result.add(node.val);
        
        if(node.right != null) stack.push(node.right);
        if(node.left != null) stack.push(node.left);
    }
    return result;
}
```

---

### 101. Postorder Traversal
**Problem:** Traverse tree in postorder (Left-Right-Root).

**Solution:** Recursive or two stacks.

```java
List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if(root == null) return result;
    
    Stack<TreeNode> s1 = new Stack<>();
    Stack<TreeNode> s2 = new Stack<>();
    s1.push(root);
    
    while(!s1.isEmpty()) {
        TreeNode node = s1.pop();
        s2.push(node);
        
        if(node.left != null) s1.push(node.left);
        if(node.right != null) s1.push(node.right);
    }
    
    while(!s2.isEmpty()) {
        result.add(s2.pop().val);
    }
    return result;
}
```

---

### 102. Level Order Traversal
**Problem:** Traverse tree level by level.

**Solution:** BFS using queue.

```java
List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if(root == null) return result;
    
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    
    while(!queue.isEmpty()) {
        int size = queue.size();
        List<Integer> level = new ArrayList<>();
        
        for(int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            level.add(node.val);
            
            if(node.left != null) queue.offer(node.left);
            if(node.right != null) queue.offer(node.right);
        }
        result.add(level);
    }
    return result;
}
```

---

### 103. Maximum Depth of Binary Tree
**Problem:** Find height of binary tree.

**Solution:** Recursive or BFS.

```java
int maxDepth(TreeNode root) {
    if(root == null) return 0;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

---

### 104. Diameter of Binary Tree
**Problem:** Find longest path between any two nodes.

**Solution:** At each node, find max path through it.

```java
int diameter = 0;

int diameterOfBinaryTree(TreeNode root) {
    height(root);
    return diameter;
}

int height(TreeNode node) {
    if(node == null) return 0;
    
    int left = height(node.left);
    int right = height(node.right);
    
    diameter = Math.max(diameter, left + right);
    return 1 + Math.max(left, right);
}
```

---

### 105. Balanced Binary Tree
**Problem:** Check if tree is height-balanced.

**Solution:** Check height difference at each node.

```java
boolean isBalanced(TreeNode root) {
    return checkHeight(root) != -1;
}

int checkHeight(TreeNode node) {
    if(node == null) return 0;
    
    int left = checkHeight(node.left);
    if(left == -1) return -1;
    
    int right = checkHeight(node.right);
    if(right == -1) return -1;
    
    if(Math.abs(left - right) > 1) return -1;
    return 1 + Math.max(left, right);
}
```

---

### 106. Lowest Common Ancestor (LCA)
**Problem:** Find LCA of two nodes.

**Solution:** Recursive approach.

```java
TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if(root == null || root == p || root == q) return root;
    
    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    
    if(left != null && right != null) return root;
    return (left != null) ? left : right;
}
```

---

## Day 18: Binary Tree Part II

### 107. Identical Trees
**Problem:** Check if two trees are identical.

**Solution:** Recursive comparison.

```java
boolean isSameTree(TreeNode p, TreeNode q) {
    if(p == null && q == null) return true;
    if(p == null || q == null) return false;
    
    return p.val == q.val && 
           isSameTree(p.left, q.left) && 
           isSameTree(p.right, q.right);
}
```

---

### 108. Zigzag Level Order Traversal
**Problem:** Traverse tree in zigzag pattern.

**Solution:** BFS with alternating direction flag.

```java
List<List<Integer>> zigzagLevelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if(root == null) return result;
    
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    boolean leftToRight = true;
    
    while(!queue.isEmpty()) {
        int size = queue.size();
        List<Integer> level = new ArrayList<>();
        
        for(int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            level.add(node.val);
            
            if(node.left != null) queue.offer(node.left);
            if(node.right != null) queue.offer(node.right);
        }
        
        if(!leftToRight) Collections.reverse(level);
        result.add(level);
        leftToRight = !leftToRight;
    }
    return result;
}
```

---

### 109. Boundary Traversal
**Problem:** Print boundary of binary tree.

**Solution:** Left boundary + leaves + right boundary (reverse).

```java
List<Integer> boundaryOfBinaryTree(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if(root == null) return result;
    
    if(!isLeaf(root)) result.add(root.val);
    
    addLeftBoundary(root.left, result);
    addLeaves(root, result);
    addRightBoundary(root.right, result);
    
    return result;
}

void addLeftBoundary(TreeNode node, List<Integer> result) {
    while(node != null) {
        if(!isLeaf(node)) result.add(node.val);
        node = (node.left != null) ? node.left : node.right;
    }
}

void addRightBoundary(TreeNode node, List<Integer> result) {
    List<Integer> temp = new ArrayList<>();
    while(node != null) {
        if(!isLeaf(node)) temp.add(node.val);
        node = (node.right != null) ? node.right : node.left;
    }
    Collections.reverse(temp);
    result.addAll(temp);
}

void addLeaves(TreeNode node, List<Integer> result) {
    if(node == null) return;
    if(isLeaf(node)) result.add(node.val);
    addLeaves(node.left, result);
    addLeaves(node.right, result);
}

boolean isLeaf(TreeNode node) {
    return node.left == null && node.right == null;
}
```

---

### 110. Vertical Order Traversal
**Problem:** Print nodes in vertical order.

**Solution:** Map with column index, BFS/DFS.

```java
List<List<Integer>> verticalTraversal(TreeNode root) {
    TreeMap<Integer, TreeMap<Integer, PriorityQueue<Integer>>> map = new TreeMap<>();
    dfs(root, 0, 0, map);
    
    List<List<Integer>> result = new ArrayList<>();
    for(TreeMap<Integer, PriorityQueue<Integer>> colMap : map.values()) {
        List<Integer> col = new ArrayList<>();
        for(PriorityQueue<Integer> pq : colMap.values()) {
            while(!pq.isEmpty()) col.add(pq.poll());
        }
        result.add(col);
    }
    return result;
}

void dfs(TreeNode node, int row, int col, TreeMap<Integer, TreeMap<Integer, PriorityQueue<Integer>>> map) {
    if(node == null) return;
    
    map.putIfAbsent(col, new TreeMap<>());
    map.get(col).putIfAbsent(row, new PriorityQueue<>());
    map.get(col).get(row).offer(node.val);
    
    dfs(node.left, row + 1, col - 1, map);
    dfs(node.right, row + 1, col + 1, map);
}
```

---

### 111. Top View of Binary Tree
**Problem:** Print top view of tree.

**Solution:** Level order with first node at each column.

```java
List<Integer> topView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if(root == null) return result;
    
    TreeMap<Integer, Integer> map = new TreeMap<>();
    Queue<Pair<TreeNode, Integer>> queue = new LinkedList<>();
    queue.offer(new Pair<>(root, 0));
    
    while(!queue.isEmpty()) {
        Pair<TreeNode, Integer> pair = queue.poll();
        TreeNode node = pair.getKey();
        int col = pair.getValue();
        
        map.putIfAbsent(col, node.val);
        
        if(node.left != null) queue.offer(new Pair<>(node.left, col - 1));
        if(node.right != null) queue.offer(new Pair<>(node.right, col + 1));
    }
    
    return new ArrayList<>(map.values());
}
```

---

### 112. Bottom View of Binary Tree
**Problem:** Print bottom view of tree.

**Solution:** Level order, update last node at each column.

```java
List<Integer> bottomView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if(root == null) return result;
    
    TreeMap<Integer, Integer> map = new TreeMap<>();
    Queue<Pair<TreeNode, Integer>> queue = new LinkedList<>();
    queue.offer(new Pair<>(root, 0));
    
    while(!queue.isEmpty()) {
        Pair<TreeNode, Integer> pair = queue.poll();
        TreeNode node = pair.getKey();
        int col = pair.getValue();
        
        map.put(col, node.val);
        
        if(node.left != null) queue.offer(new Pair<>(node.left, col - 1));
        if(node.right != null) queue.offer(new Pair<>(node.right, col + 1));
    }
    
    return new ArrayList<>(map.values());
}
```

---

### 113. Left/Right View of Binary Tree
**Problem:** Print left or right view of tree.

**Solution:** Level order, take first/last node at each level.

```java
List<Integer> rightSideView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if(root == null) return result;
    
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    
    while(!queue.isEmpty()) {
        int size = queue.size();
        
        for(int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            
            if(i == size - 1) result.add(node.val); // Rightmost
            
            if(node.left != null) queue.offer(node.left);
            if(node.right != null) queue.offer(node.right);
        }
    }
    return result;
}
```

---

## Day 19: Binary Tree Part III

### 114. Symmetric Tree
**Problem:** Check if tree is mirror of itself.

**Solution:** Compare left and right subtrees.

```java
boolean isSymmetric(TreeNode root) {
    return root == null || isMirror(root.left, root.right);
}

boolean isMirror(TreeNode left, TreeNode right) {
    if(left == null && right == null) return true;
    if(left == null || right == null) return false;
    
    return left.val == right.val && 
           isMirror(left.left, right.right) && 
           isMirror(left.right, right.left);
}
```

---

### 115. Root to Leaf Paths
**Problem:** Print all root to leaf paths.

**Solution:** DFS with path tracking.

```java
List<String> binaryTreePaths(TreeNode root) {
    List<String> result = new ArrayList<>();
    if(root != null) dfs(root, "", result);
    return result;
}

void dfs(TreeNode node, String path, List<String> result) {
    if(node.left == null && node.right == null) {
        result.add(path + node.val);
        return;
    }
    
    if(node.left != null) dfs(node.left, path + node.val + "->", result);
    if(node.right != null) dfs(node.right, path + node.val + "->", result);
}
```

---

### 116. Maximum Path Sum
**Problem:** Find maximum path sum between any two nodes.

**Solution:** At each node, calculate max path through it.

```java
int maxSum = Integer.MIN_VALUE;

int maxPathSum(TreeNode root) {
    maxGain(root);
    return maxSum;
}

int maxGain(TreeNode node) {
    if(node == null) return 0;
    
    int left = Math.max(maxGain(node.left), 0);
    int right = Math.max(maxGain(node.right), 0);
    
    int pathSum = node.val + left + right;
    maxSum = Math.max(maxSum, pathSum);
    
    return node.val + Math.max(left, right);
}
```

---

### 117. Construct Binary Tree from Inorder and Preorder
**Problem:** Build tree from inorder and preorder traversals.

**Solution:** Use preorder for root, inorder to split subtrees.

```java
int preIndex = 0;
Map<Integer, Integer> inMap = new HashMap<>();

TreeNode buildTree(int[] preorder, int[] inorder) {
    for(int i = 0; i < inorder.length; i++) {
        inMap.put(inorder[i], i);
    }
    return build(preorder, 0, inorder.length - 1);
}

TreeNode build(int[] preorder, int inStart, int inEnd) {
    if(inStart > inEnd) return null;
    
    int rootVal = preorder[preIndex++];
    TreeNode root = new TreeNode(rootVal);
    
    int inIndex = inMap.get(rootVal);
    root.left = build(preorder, inStart, inIndex - 1);
    root.right = build(preorder, inIndex + 1, inEnd);
    
    return root;
}
```

---

### 118. Construct Binary Tree from Inorder and Postorder
**Problem:** Build tree from inorder and postorder traversals.

**Solution:** Use postorder for root (from end), inorder to split.

```java
int postIndex;
Map<Integer, Integer> inMap = new HashMap<>();

TreeNode buildTree(int[] inorder, int[] postorder) {
    postIndex = postorder.length - 1;
    for(int i = 0; i < inorder.length; i++) {
        inMap.put(inorder[i], i);
    }
    return build(postorder, 0, inorder.length - 1);
}

TreeNode build(int[] postorder, int inStart, int inEnd) {
    if(inStart > inEnd) return null;
    
    int rootVal = postorder[postIndex--];
    TreeNode root = new TreeNode(rootVal);
    
    int inIndex = inMap.get(rootVal);
    root.right = build(postorder, inIndex + 1, inEnd);
    root.left = build(postorder, inStart, inIndex - 1);
    
    return root;
}
```

---

### 119. Serialize and Deserialize Binary Tree
**Problem:** Convert tree to string and back.

**Solution:** Use preorder with markers for null.

```java
// Serialize
String serialize(TreeNode root) {
    if(root == null) return "null,";
    return root.val + "," + serialize(root.left) + serialize(root.right);
}

// Deserialize
TreeNode deserialize(String data) {
    Queue<String> queue = new LinkedList<>(Arrays.asList(data.split(",")));
    return buildTree(queue);
}

TreeNode buildTree(Queue<String> queue) {
    String val = queue.poll();
    if(val.equals("null")) return null;
    
    TreeNode root = new TreeNode(Integer.parseInt(val));
    root.left = buildTree(queue);
    root.right = buildTree(queue);
    return root;
}
```

---

### 120. Flatten Binary Tree to Linked List
**Problem:** Flatten tree to linked list (preorder).

**Solution:** Reverse postorder or Morris traversal.

```java
void flatten(TreeNode root) {
    if(root == null) return;
    
    flatten(root.left);
    flatten(root.right);
    
    TreeNode temp = root.right;
    root.right = root.left;
    root.left = null;
    
    while(root.right != null) root = root.right;
    root.right = temp;
}
```

---

## Day 20: Binary Search Tree

### 121. Search in BST
**Problem:** Search for value in BST.

**Solution:** Compare with root, go left or right.

```java
TreeNode searchBST(TreeNode root, int val) {
    if(root == null || root.val == val) return root;
    
    if(val < root.val) return searchBST(root.left, val);
    return searchBST(root.right, val);
}
```

---

### 122. Convert Sorted Array to BST
**Problem:** Convert sorted array to balanced BST.

**Solution:** Middle element as root, recurse on halves.

```java
TreeNode sortedArrayToBST(int[] nums) {
    return build(nums, 0, nums.length - 1);
}

TreeNode build(int[] nums, int left, int right) {
    if(left > right) return null;
    
    int mid = left + (right - left) / 2;
    TreeNode root = new TreeNode(nums[mid]);
    root.left = build(nums, left, mid - 1);
    root.right = build(nums, mid + 1, right);
    return root;
}
```

---

### 123. Validate BST
**Problem:** Check if tree is valid BST.

**Solution:** Inorder should be sorted, or use range.

```java
boolean isValidBST(TreeNode root) {
    return validate(root, null, null);
}

boolean validate(TreeNode node, Integer min, Integer max) {
    if(node == null) return true;
    
    if((min != null && node.val <= min) || (max != null && node.val >= max)) {
        return false;
    }
    
    return validate(node.left, min, node.val) && 
           validate(node.right, node.val, max);
}
```

---

### 124. LCA in BST
**Problem:** Find LCA in BST.

**Solution:** Use BST property for efficient search.

```java
TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if(root.val > p.val && root.val > q.val) {
        return lowestCommonAncestor(root.left, p, q);
    }
    if(root.val < p.val && root.val < q.val) {
        return lowestCommonAncestor(root.right, p, q);
    }
    return root;
}
```

---

### 125. Inorder Predecessor/Successor in BST
**Problem:** Find inorder predecessor and successor.

**Solution:** Use BST properties.

```java
TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
    TreeNode successor = null;
    
    while(root != null) {
        if(p.val < root.val) {
            successor = root;
            root = root.left;
        } else {
            root = root.right;
        }
    }
    return successor;
}

TreeNode inorderPredecessor(TreeNode root, TreeNode p) {
    TreeNode predecessor = null;
    
    while(root != null) {
        if(p.val > root.val) {
            predecessor = root;
            root = root.right;
        } else {
            root = root.left;
        }
    }
    return predecessor;
}
```

---

### 126. Kth Smallest Element in BST
**Problem:** Find kth smallest element in BST.

**Solution:** Inorder traversal (iterative or recursive).

```java
int kthSmallest(TreeNode root, int k) {
    Stack<TreeNode> stack = new Stack<>();
    TreeNode curr = root;
    
    while(true) {
        while(curr != null) {
            stack.push(curr);
            curr = curr.left;
        }
        curr = stack.pop();
        if(--k == 0) return curr.val;
        curr = curr.right;
    }
}
```

---

### 127. Kth Largest Element in BST
**Problem:** Find kth largest element in BST.

**Solution:** Reverse inorder traversal.

```java
int count = 0;
int result = 0;

int kthLargest(TreeNode root, int k) {
    count = k;
    reverseInorder(root);
    return result;
}

void reverseInorder(TreeNode node) {
    if(node == null) return;
    
    reverseInorder(node.right);
    count--;
    if(count == 0) {
        result = node.val;
        return;
    }
    reverseInorder(node.left);
}
```

---

## Day 21: Binary Search Tree Part II

### 128. Floor in BST
**Problem:** Find floor (largest element ≤ key) in BST.

**Solution:** Track last left turn.

```java
int floor(TreeNode root, int key) {
    int floor = -1;
    
    while(root != null) {
        if(root.val == key) return root.val;
        
        if(root.val < key) {
            floor = root.val;
            root = root.right;
        } else {
            root = root.left;
        }
    }
    return floor;
}
```

---

### 129. Ceil in BST
**Problem:** Find ceil (smallest element ≥ key) in BST.

**Solution:** Track last right turn.

```java
int ceil(TreeNode root, int key) {
    int ceil = -1;
    
    while(root != null) {
        if(root.val == key) return root.val;
        
        if(root.val > key) {
            ceil = root.val;
            root = root.left;
        } else {
            root = root.right;
        }
    }
    return ceil;
}
```

---

### 130. BST Iterator
**Problem:** Implement iterator for BST (inorder).

**Solution:** Use stack for controlled inorder traversal.

```java
class BSTIterator {
    Stack<TreeNode> stack;
    
    public BSTIterator(TreeNode root) {
        stack = new Stack<>();
        pushAll(root);
    }
    
    public int next() {
        TreeNode node = stack.pop();
        pushAll(node.right);
        return node.val;
    }
    
    public boolean hasNext() {
        return !stack.isEmpty();
    }
    
    void pushAll(TreeNode node) {
        while(node != null) {
            stack.push(node);
            node = node.left;
        }
    }
}
```

---

### 131. Two Sum in BST
**Problem:** Find if two elements sum to target in BST.

**Solution:** Two iterators (forward and backward).

```java
boolean findTarget(TreeNode root, int k) {
    Stack<TreeNode> leftStack = new Stack<>();
    Stack<TreeNode> rightStack = new Stack<>();
    
    pushLeft(leftStack, root);
    pushRight(rightStack, root);
    
    TreeNode left = getNext(leftStack, true);
    TreeNode right = getNext(rightStack, false);
    
    while(left.val < right.val) {
        int sum = left.val + right.val;
        if(sum == k) return true;
        
        if(sum < k) left = getNext(leftStack, true);
        else right = getNext(rightStack, false);
    }
    return false;
}

void pushLeft(Stack<TreeNode> stack, TreeNode node) {
    while(node != null) {
        stack.push(node);
        node = node.left;
    }
}

void pushRight(Stack<TreeNode> stack, TreeNode node) {
    while(node != null) {
        stack.push(node);
        node = node.right;
    }
}

TreeNode getNext(Stack<TreeNode> stack, boolean isLeft) {
    TreeNode node = stack.pop();
    if(isLeft) pushLeft(stack, node.right);
    else pushRight(stack, node.left);
    return node;
}
```

---

### 132. Recover BST (Two nodes swapped)
**Problem:** Fix BST where two nodes are swapped.

**Solution:** Find violations in inorder traversal.

```java
TreeNode first, second, prev;

void recoverTree(TreeNode root) {
    first = second = prev = null;
    inorder(root);
    
    int temp = first.val;
    first.val = second.val;
    second.val = temp;
}

void inorder(TreeNode node) {
    if(node == null) return;
    
    inorder(node.left);
    
    if(prev != null && node.val < prev.val) {
        if(first == null) first = prev;
        second = node;
    }
    prev = node;
    
    inorder(node.right);
}
```

---

### 133. Largest BST in Binary Tree
**Problem:** Find size of largest BST subtree.

**Solution:** Post-order traversal with BST validation.

```java
class NodeInfo {
    boolean isBST;
    int size, min, max;
    
    NodeInfo(boolean isBST, int size, int min, int max) {
        this.isBST = isBST;
        this.size = size;
        this.min = min;
        this.max = max;
    }
}

int maxBSTSize = 0;

int largestBSTSubtree(TreeNode root) {
    postorder(root);
    return maxBSTSize;
}

NodeInfo postorder(TreeNode node) {
    if(node == null) {
        return new NodeInfo(true, 0, Integer.MAX_VALUE, Integer.MIN_VALUE);
    }
    
    NodeInfo left = postorder(node.left);
    NodeInfo right = postorder(node.right);
    
    if(left.isBST && right.isBST && node.val > left.max && node.val < right.min) {
        int size = left.size + right.size + 1;
        maxBSTSize = Math.max(maxBSTSize, size);
        return new NodeInfo(true, size, 
                           Math.min(node.val, left.min), 
                           Math.max(node.val, right.max));
    }
    
    return new NodeInfo(false, 0, 0, 0);
}
```

---

This completes a comprehensive overview of Striver's SDE Sheet with 133+ problems covering Arrays, Linked Lists, Stacks, Queues, Strings, Binary Trees, BST, Recursion, Backtracking, Greedy, Heaps, and Binary Search!

Each solution includes the optimal approach with code. For interview preparation, practice implementing these solutions and understand the time/space complexity of each approach.
