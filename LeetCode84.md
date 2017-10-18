```
import java.util.Stack;

class Solution {
    public int largestRectangleArea(int[] heights) {
        
        Stack<Integer> stack = new Stack<>();
        int result = 0;

        for (int i = 0; i <= heights.length; i++){
            //完毕
            if (i == heights.length && stack.isEmpty())
                break;

            //遍历数组完毕，开始遍历栈
            if (i == heights.length){
                int pop = stack.pop();
                int curArea = 0;
                if (stack.isEmpty())
                    curArea = heights[pop] * i;// 0 到 (i-1) 一共i个单位
                else
                    curArea = heights[pop] * (i - 1 - stack.peek());// stack.peek+1 到 i-1


                result = Math.max(result, curArea);
                i--;
                continue;
            }

            // 栈内存的是index，方便后面计算水平方向差值
            // 保证栈内的是升序
            // 如果栈内是 1 2 5，本次要弹出5，那么可以形成heights[5] * （5 - 1 - 2）的面积 
            //                                         高      *      底 
            // 如果栈内是 2，    本次要弹出2，那么可以形成heights[2] *      2      的面积
            // ok
            if (stack.isEmpty() || heights[stack.peek()] <= heights[i])
                stack.push(i);
            else {
                //pop的时候计算一下本次pop出的高度可以形成多大的面积
                int pop = stack.pop();
                int curArea = 0;
                if (stack.isEmpty())
                    curArea = heights[pop] * i;// 0 到 (i-1) 一共i个单位
                else
                    curArea = heights[pop] * (i - 1 - stack.peek());// stack.peek+1 到 i-1


                result = Math.max(result, curArea);
                i--;
            }
        }



        return result;

    }
}
```
