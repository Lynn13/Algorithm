# Maximum Gap
- 给一堆乱序的数，得出排序后相邻的数的最大差值

### 解法1 快排
- 复杂度 o(n * logn)

### 解法2 基数排序
- 复杂度 o(k * n)
- 想了半天才想起来，基数排序就是按照个位数、十位数、百位数依次排序，很垃圾，只能对整数进行

### 解法3 基于鸽巢原理的bucket sort 
- 复杂度 o(n)
- 一共有n个数，按照大小范围，放进n-1个容器中，那么至少有一个容器有2个或以上的数
- 如果排序后两个相邻的数差值最大，那么这两个数一定分别在两个容器里，并且肯定是容器的边界值
- 所以只需要放好后，遍历相邻容器的最大最小值就OK
```
public class Solution {
public int maximumGap(int[] num) {
    if (num == null || num.length < 2)
        return 0;
    // get the max and min value of the array
    int min = num[0];
    int max = num[0];
    for (int i:num) {
        min = Math.min(min, i);
        max = Math.max(max, i);
    }
    // the minimum possibale gap, ceiling of the integer division
    int gap = (int)Math.ceil((double)(max - min)/(num.length - 1));
    int[] bucketsMIN = new int[num.length - 1]; // store the min value in that bucket
    int[] bucketsMAX = new int[num.length - 1]; // store the max value in that bucket
    Arrays.fill(bucketsMIN, Integer.MAX_VALUE);
    Arrays.fill(bucketsMAX, Integer.MIN_VALUE);
    // put numbers into buckets
    for (int i:num) {
        if (i == min || i == max)
            continue;
        int idx = (i - min) / gap; // index of the right position in the buckets
        bucketsMIN[idx] = Math.min(i, bucketsMIN[idx]);
        bucketsMAX[idx] = Math.max(i, bucketsMAX[idx]);
    }
    // scan the buckets for the max gap
    int maxGap = Integer.MIN_VALUE;
    int previous = min;
    for (int i = 0; i < num.length - 1; i++) {
        if (bucketsMIN[i] == Integer.MAX_VALUE && bucketsMAX[i] == Integer.MIN_VALUE)
            // empty bucket
            continue;
        // min value minus the previous value is the current gap
        maxGap = Math.max(maxGap, bucketsMIN[i] - previous);
        // update previous bucket value
        previous = bucketsMAX[i];
    }
    maxGap = Math.max(maxGap, max - previous); // updata the final max value gap
    return maxGap;
}
```
