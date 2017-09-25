```
import java.util.PriorityQueue;

class Solution {
    public void wiggleSort(int[] nums) {
        // 时间o(n),空间o(n)
        // 1 找到中位数，O(n)
        // 2 把小于中位数的元素放在左边，大于的放在右边，O(n)
        // 3 中位数左边拿一个，右边拿一个，这样就ok
        //
        // 改善为空间o(1)：
        // 公式：(1 + 2*index) % (n | 1)
        // 这是什么鬼公式我也不知道，看了半天solution没看明白为什么要这么算下一个的位置
        // 放弃~

        int mid = findKthLargest(nums, (nums.length+1)/2);
        int[] newNums = new int[nums.length];
        int odd = 1;
        int even=nums.length%2==0?nums.length-2:nums.length-1;

        for (int i = 0; i < nums.length; i++){
            if (nums[i] > mid){
                newNums[odd] = nums[i];
                odd += 2;
                continue;
            }
            if (nums[i] < mid){
                newNums[even] = nums[i];
                even -= 2;
                continue;
            }
        }

        while (odd < nums.length){
            newNums[odd] = mid;
            odd += 2;
        }
        while (even >= 0){
            newNums[even] = mid;
            even -= 2;
        }
        
        for (int i = 0; i < nums.length; i++)
            nums[i] = newNums[i];

    }

    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int i = 0; i < nums.length; i++){
            pq.offer(nums[i]);
            if (pq.size() > k)
                pq.poll();
        }
        return pq.peek();
    }
}
```
