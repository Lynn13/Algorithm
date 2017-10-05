### Sliding Window Maximum
- 维护一个索引队列，使队列内依次降序，queue.peek是最大的索引 
- 使用deque是为了左右两边都可以poll出
- 例子：[1,3,-1,-3,5,3,6,7]   3
- DEQUE：0 （1）
- DEQUE：1 （3）
- DEQUE：1 2（3 -1）
- DEQUE：1 2 3（3 -1 -3）
- DEQUE：4（5）
- DEQUE：4 5（5 3）
- ···
```
class Solution {
    public int[] maxSlidingWindow(int[] a, int k) {		
		if (a == null || k <= 0) {
			return new int[0];
		}
		int n = a.length;
		int[] r = new int[n-k+1];
		int ri = 0;
        
		Deque<Integer> q = new ArrayDeque<>();
		for (int i = 0; i < a.length; i++) {
      
			while (!q.isEmpty() && q.peek() < i - k + 1) {
                q.poll();
			}
            
			while (!q.isEmpty() && a[q.peekLast()] < a[i]) {
                q.pollLast();
			}
            
			q.offer(i);
			if (i >= k - 1) {
				r[ri++] = a[q.peek()];
                
			}
		}
		return r;
	}
}
```
