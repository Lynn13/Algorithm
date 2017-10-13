# Perfect Rectangle

### 解法1
- 条件1：方块们拼起来之后用斜两个角计算的面积，和原来的面积和一样
- 条件2：最终拼的方块只有四个角，也就是只有四个点且唯一，每次遍历一个小方块，就把所有的点放进set里，重复的点删除
```
import java.util.HashMap;
import java.util.HashSet;

class Solution {
    public boolean isRectangleCover(int[][] rectangles) {
        if (rectangles.length == 0)
            return false;

        int x1 = Integer.MAX_VALUE;
        int x2 = Integer.MIN_VALUE;
        int y1 = Integer.MAX_VALUE;
        int y2 = Integer.MIN_VALUE;

        int oldArea = 0;
        HashSet<String> hashSet = new HashSet<>();
        for (int[] rect : rectangles){
            x1 = Math.min(x1, rect[0]);
            x2 = Math.max(x2, rect[2]);
            y1 = Math.min(y1, rect[1]);
            y2 = Math.max(y2, rect[3]);

            oldArea += (rect[2] - rect[0]) * (rect[3] - rect[1]);

            String s1 = rect[0] + "," + rect[1];
            String s2 = rect[0] + "," + rect[3];
            String s3 = rect[2] + "," + rect[3];
            String s4 = rect[2] + "," + rect[1];

            if (!hashSet.add(s1))
                hashSet.remove(s1);
                
            if (!hashSet.add(s2))
                hashSet.remove(s2);
            if (!hashSet.add(s3))
                hashSet.remove(s3);
            if (!hashSet.add(s4))
                hashSet.remove(s4);


        }

        if (!hashSet.contains(x1 + "," + y1) ||!hashSet.contains(x1 + "," + y2) ||!hashSet.contains(x2 + "," + y1) ||!hashSet.contains(x2 + "," + y2) || hashSet.size() != 4)
            return false;

        System.out.println(hashSet.size());
        return oldArea == (x2 - x1) * (y2 - y1);
    }
}
```
