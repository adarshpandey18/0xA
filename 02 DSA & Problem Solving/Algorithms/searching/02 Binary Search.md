## Read :  [[08. Binary Search.pdf]]

```java
public static int binarySearch(int[]nums, int target) {
	int start = 0;
	int end = nums.length - 1;
		
	while(start <= end) {
		int mid = start + (end - start)/2;
		if(nums[mid] == target) {
			return mid;
		} else if(nums[mid] < target) {
			start = mid + 1;
		} else {
			end = mid -1;
		}
	}
		
	return -1;
}

```

## Time Complexity
Worst Case - $\mathcal{O}(\log{}n)$ 