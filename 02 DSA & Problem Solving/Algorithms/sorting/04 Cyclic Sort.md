## Read : [[12. Cyclic Sort.pdf]]

```java
public class Main {
	public static void main(String[] args) {
		int[] nums = {5, 4, 3, 2, 1};
		cyclicSort(nums);
		System.out.println(Arrays.toString(nums));
	}
	public static void cyclicSort(int[]nums) {
		int index = 0;
		while(index != nums.length) {
			int rightIndex = nums[index] - 1;
			if(nums[rightIndex] != nums[index]) {
				swap(nums, rightIndex, index);
			} else {
				index++;
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