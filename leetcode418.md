# The Skyline Problem
- 详细的解法说明 https://briangordon.github.io/2014/08/the-skyline-problem.html
- 根据上面链接的最后一个动图，我们可以这样：
- 从左到右遍历矩形的上方顶点
- 用最大堆存储当前需要的高度，矩形左顶点被遍历时，放入矩形的高度，矩形右顶点被遍历时，从最大堆中去除本矩形高度
- 这样就可以每次记录下矩形的左上角的值，而不影响右上角

```
public List<int[]> getSkyline(int[][] buildings) {
    List<int[]> result = new ArrayList<>();
    List<int[]> height = new ArrayList<>();
    //用正负来判断左上还是右上
    for(int[] b:buildings) {
        height.add(new int[]{b[0], -b[2]});
        height.add(new int[]{b[1], b[2]});
    }
    Collections.sort(height, (a, b) -> {
            if(a[0] != b[0]) 
                return a[0] - b[0];
            return a[1] - b[1];
    });
    Queue<Integer> pq = new PriorityQueue<>((a, b) -> (b - a));
    pq.offer(0);
    int prev = 0;
    for(int[] h:height) {
        if(h[1] < 0) {
            pq.offer(-h[1]);
        } else {
            pq.remove(h[1]);
        }
        int cur = pq.peek();
        if(prev != cur) {
            result.add(new int[]{h[0], cur});
            prev = cur;
        }
    }
    return result;
}
```
