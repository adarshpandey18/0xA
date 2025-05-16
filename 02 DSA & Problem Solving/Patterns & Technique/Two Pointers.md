Two pointers are variables that point to different positions in a data structure (usually arrays or strings). You move them in a controlled way to explore the data efficiently, often reducing time complexity from $\mathcal{O}(n²)$ to $\mathcal{O}(n)$ or $\mathcal{O}(n \log{}n)$.

---
## When to use 2 Pointer - Pattern Recognition

- You're working with **sorted arrays or strings** (especially for sum or match problems).
- You want to **find pairs or triplets** with a specific property (like a sum).
- You want to **reverse**, **partition**, or **merge** parts of arrays.
- You're asked to **remove duplicates**, or **move certain elements** (like zeroes or negatives).
- You need to **slide a window** to calculate something (sometimes overlaps with sliding window).
---
##  Common Two Pointer Scenarios 

### 1. **Finding a Pair with a Target Sum in a Sorted Array**

```java
int[] nums = {1, 2, 4, 7, 11, 15};
int target = 15;

int left = 0, right = nums.length - 1;
while (left < right) {
    int sum = nums[left] + nums[right];
    if (sum == target) {
        System.out.println(nums[left] + ", " + nums[right]);
        break;
    } else if (sum < target) {
        left++; // Need a bigger number
    } else {
        right--; // Need a smaller number
    }
}
```

✅ **Pattern**: Array is sorted, look for pairs.  
🧠 **Trick**: Move the pointer that will bring you closer to the target.

---

### 2. **3Sum**

**Goal**: Find triplets that sum to zero.

```java
// Sort -> Fix one -> Two-pointer on rest
Arrays.sort(nums);
for (int i = 0; i < nums.length - 2; i++) {
    if (i > 0 && nums[i] == nums[i - 1]) continue; // Skip duplicates

    int left = i + 1, right = nums.length - 1;
    while (left < right) {
        int sum = nums[i] + nums[left] + nums[right];
        if (sum == 0) {
            // Found a triplet
            result.add(Arrays.asList(nums[i], nums[left], nums[right]));
            left++;
            right--;
            while (left < right && nums[left] == nums[left - 1]) left++;
            while (left < right && nums[right] == nums[right + 1]) right--;
        } else if (sum < 0) {
            left++;
        } else {
            right--;
        }
    }
}
```

✅ **Pattern**: Fix one number, apply two-pointer to the rest.  
🧠 **Tip**: Always sort first for consistency and to handle duplicates.

---

### 3. **Reverse an Array or String**

```java
int[] nums = {1, 2, 3, 4, 5};
int left = 0, right = nums.length - 1;
while (left < right) {
    int temp = nums[left];
    nums[left] = nums[right];
    nums[right] = temp;
    left++;
    right--;
}
```

✅ **Pattern**: Symmetric work from both ends.  
🧠 **Trick**: Stop when the pointers meet.

---

### 4. **Remove Duplicates from Sorted Array**

```java
int[] nums = {1, 1, 2, 2, 3};
int slow = 1;
for (int fast = 1; fast < nums.length; fast++) {
    if (nums[fast] != nums[fast - 1]) {
        nums[slow++] = nums[fast];
    }
}
System.out.println(Arrays.copyOf(nums, slow)); // Unique part
```

✅ **Pattern**: Fast scans ahead, slow updates position.  
🧠 **Trick**: Think of `slow` as the position to fill next unique element.

---

### 5. **Move Zeroes to the End**

```java
int[] nums = {0, 1, 0, 3, 12};
int slow = 0;
for (int fast = 0; fast < nums.length; fast++) {
    if (nums[fast] != 0) {
        int temp = nums[fast];
        nums[fast] = nums[slow];
        nums[slow++] = temp;
    }
}
```

✅ **Pattern**: Partition the array based on some condition.  
🧠 **Trick**: Don't overthink it — just move the valid stuff first.

---

## How to Recognize Two-Pointer Problems

**Ask yourself:**
- Is the array or string sorted?
- Do I need to compare elements from both ends?
- Am I asked to find a pair/triplet/subarray that satisfies a condition?
- Is there a clear need to reduce time from $\mathcal{O}(n²)$ to $\mathcal{O}(n)$ ?
- Does the problem involve removing/partitioning/swapping?

If yes → two-pointer is a strong candidate.

---

##  Tips & Tricks

| Tip                                 | Description                                                             |
| ----------------------------------- | ----------------------------------------------------------------------- |
| **Always sort first if not sorted** | Sorting makes it easier to control duplicate logic and pointer movement |
| **Avoid duplicates**                | After finding a match (like in 3Sum), skip over repeated values         |
| **Watch for index safety**          | Don’t access `nums[j - 1]` unless you’re sure `j > 0`                   |
| **Name pointers meaningfully**      | `left`, `right`, `slow`, `fast` help you think clearly                  |
| **Dry-run small inputs**            | Trace with pen & paper to understand pointer motion                     |
|                                     |                                                                         |

---

## 🧪 Practice Problems (LeetCode)

- [Two Sum II - Input Array is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
- [3Sum](https://leetcode.com/problems/3sum/)
- [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
- [Move Zeroes](https://leetcode.com/problems/move-zeroes/)
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

---
