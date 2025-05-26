## Read : [[11. Insertion Sort.pdf]]

```java
public class Main {
	public static void main(String[] args) {
		int[] nums = {5, 4, 3, 2, 1};
		selectionSort(nums);
		System.out.println(Arrays.toString(nums));
	}
	public static void selectionSort(int[]nums) {
		for(int i = 0; i < nums.length; i++) {
			int minIndex = findMin(nums, i);
			if(minIndex != i) {
				swap(nums, i, minIndex);
			}
		}
	}
	public static int findMin(int[]nums, int start) {
		int ans = start;
		for(int i = start+1; i < nums.length; i++) {
			if(nums[i] < nums[ans]) {
				ans = i;
			}
		}

		return ans;
	}
	public static void swap(int[]nums, int i, int j) {
		int temp = nums[i];
		nums[i] = nums[j];
		nums[j] = temp;
	}
}

```

Time Complexity : $\mathcal{O}({N}^{2})$
