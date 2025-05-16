## Read : [[07. Linear Search.pdf]]

```java
public static int linearSearch(int[]nums, int target) {
	for(int i = 0; i < nums.length; i++) {
		if(nums[i] == target) {
			return i;
		}		
	}
	return -1;
}
```

## Time Complexity
Worst case - $\mathcal{O}(n)$