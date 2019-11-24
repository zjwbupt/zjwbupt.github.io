The idea is simple, you need to put all 0 in the left, and all 2 on right, and leave 1 in the middle;

So we could do this with one 0-pointer, and one 2-pointer, which in general case, can be called: p_min, p_max;
Ok, we could start iterate the nums, and what we need to do is keep 0 on left and 2 on right;

```java
public void sortColors(int[] nums) {
        int p_min = 0;
        int p_max = nums.length-1;
        int i = 0;
        // continue increase i, when we are not out of boundery;
        while(i<=p_max) {
            if(nums[i] == 0) {
				// if we found min, we just swap it with the current index, and keep going
                swap(nums, i, p_min);
                i++;
                p_min++;
            } else if (nums[i] == 1) {
				// if we found i, just leave it there and continue;
                i++;
            } else {
				// if we found 2, let`s swap it to the end of the array, and update the p_max index smaller( cuz the last position is already the biggest, we need to find next one to swap);
                swap(nums, i, p_max);
                p_max--;
            }
        }
    }
    
	// normal swap procedure
    private void swap(int[] n, int i, int j) {
        int temp = n[i];
        n[i] = n[j];
        n[j] = temp;
    }
}
```