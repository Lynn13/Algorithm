# Largest Divisible Subset

- leetcode 386

- 这题没那么复杂没那么难，不要想太多

- `count[i]`表示以`num[i]`结束时，结果的长度

- `preIndex[i]`表示结果中能被`num[i]`除开的上一个num 的index

- 如果`nums[i]%nums[j]==0`，并且比上一次更新`count[i]`要大，则`count[i]=count[j]+1`

- 用一个变量来记录最长结果的最后一个index，最后就用这个变量和preindex[]即可遍历整个结果

  ```
  import java.util.ArrayList;
  import java.util.Arrays;
  import java.util.List;

  class Solution {
  public List<Integer> largestDivisibleSubset(int[] nums) {
      List<Integer> result = new ArrayList<>();
      if (nums.length == 0)
          return result;
      if (nums.length == 1){
          result.add(nums[0]);
          return result;
      }

      Arrays.sort(nums);
      int[] count = new int[nums.length];
      int[] preIndex = new int[nums.length];
      count[0] = 1;
      preIndex[0] = -1;
      int maxCount = 1;
      int maxIndex = 0;
      for (int i = 1; i < nums.length; i++){
          count[i] = 1;
          preIndex[i] = -1;
          for (int j = 0; j < i; j++){
              if (nums[i] % nums[j] == 0 && count[j] + 1 > count[i]){
                  count[i] = count[j] + 1;
                  preIndex[i] = j;
                  if (count[i] > maxCount){
                      maxCount = count[i];
                      maxIndex = i;
                  }
              }
             
          }
      }

      while (maxIndex != -1){
          result.add(0, nums[maxIndex]);
          maxIndex = preIndex[maxIndex];
      }
      return result;
  }
  }
  ```

