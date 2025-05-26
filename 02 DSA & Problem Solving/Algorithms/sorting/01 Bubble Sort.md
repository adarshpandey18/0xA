## Read : [[09. Bubble Sort.pdf]]

```java
public class Main {
	public static void main(String[] args) {
		int[] nums = {5, 4, 3, 2, 1};
		bubbleSort(nums);
		System.out.println(Arrays.toString(nums));
	}
	public static void bubbleSort(int[]nums) {
		for(int i = 0; i < nums.length; i++) {
			for(int j = 1; j < nums.length-i; j++) {
				if(nums[j] < nums[j-1]) {
					swap(nums, j, j-1);
				}
			}
		}
	}
	public static void swap(int[]nums, int i, int j) {
		int temp = nums[i];
		nums[i] = nums[j];
		nums[j] = temp;
	}
}

```

Time Complexity : $\mathcal{O}({N}^{2})$
