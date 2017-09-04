# Maximum XOR of Two Numbers in an Array
- leetcode 421
- XOR的性质，a^b = c, 则有 a^c = b，且 b^c = a
- mask：每次从高位开始，到第i位为止，所能获得的最大的数
- max:  当前能够生成的最大值
- 每一次将mask和其他的num相与得到的值加入hashset
- 到当前位为止，期望生成的最大值 wantMAX = max | (1 << i)
- 如果真的能生成，即a ^ b = wantMAX，那么a和b肯定都在hashset里面

```
class Solution {
    public int findMaximumXOR(int[] nums) {
        int max = 0;
        int mask = 0;
        for (int i = 31; i >= 0; i--){
            mask = mask | (1 << i);
            HashSet<Integer> set = new HashSet<>();
            for (int num : nums){
                set.add(mask & num);
            }

            int wantMax = max | (1 << i);
            for (int num : set){
                if (set.contains(wantMax ^ num)){
                    max = wantMax;
                    break;
                }
            }
        }
        return max;
    }
}
```