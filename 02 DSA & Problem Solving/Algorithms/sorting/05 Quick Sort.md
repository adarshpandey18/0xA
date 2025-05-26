## Quick Sort : [[18. Quick Sort.pdf]]

```java
public class Main {
	public static void main(String[] args) {
		int[] nums = {5, 4, 3, 2, 1};
		quickSort(nums, 0, nums.length-1);
		System.out.println(Arrays.toString(nums));
	}
	public static void quickSort(int[]nums, int start, int end) {
		if(start >= end) {
			return;
		}

		int s = start;
		int e = end;
		int mid = s + (e - s)/2;
		int pivot = nums[mid];
		
		while(s <= e) {
			while(nums[s] < pivot) s++;
			while(nums[e] > pivot) e--;

			if(s <= e) {
				int temp = nums[s];
				nums[s] = nums[e];
				nums[e] = temp;
				s++;
				e--;
			}
		}
		quickSort(nums, start, e);
		quickSort(nums, s, end);
	}
	
}

```