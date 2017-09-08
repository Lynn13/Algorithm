# Course Schedule
- indegree[i] 入度，表示课程i 有多少前置课程
- isPre[i][j] 前置课程的标志位，1表示i是j的前置课程
- 一个queue
- 首先计算出所有课程的入度，把当前入度为0的放进queue
- 遍历queue，把这些课程的后置课程的入度减一
- 如果减一完了这入度变成0了，那就放到queue里面

```
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        int[] indegree = new int[numCourses];
        int[][] isPre = new int[numCourses][numCourses];
        int res = 0;

        for (int i = 0; i < prerequisites.length; i++){
            int lesson = prerequisites[i][0];
            int pre = prerequisites[i][1];
            if (isPre[pre][lesson] == 0)
                indegree[lesson]++;
            isPre[pre][lesson] = 1;
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < indegree.length; i++){
            if (indegree[i] == 0)
                queue.offer(i);
        }

        while (!queue.isEmpty()){
            int course = queue.poll();
            res++;
            for (int i = 0; i < numCourses; i++){
                if (isPre[course][i] != 0){
                    indegree[i] -- ;
                    if (indegree[i] == 0)
                        queue.offer(i);
                }
            }
        }
        
        return res == numCourses;
    }
}
```
