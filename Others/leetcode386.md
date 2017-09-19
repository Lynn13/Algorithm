###  Lexicographical Numbers
- solution里面的思路比较灵性，就是每次计算出下一个要加进list的数。
```
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<Integer> lexicalOrder(int n) {
        List<Integer> res = new ArrayList<>();
        int cur = 1;
        for (int i = 0; i < n; i++){
            res.add(cur);
            
            if (cur * 10 <= n){// 末尾加个0的情况
                cur = cur * 10;
            }
            else if (cur % 10 != 9 && cur + 1 <= n){ //自加的情况
                cur++;
            }
            else {
                while ((cur / 10) % 10 == 9){ //末尾是9，次末尾也是9情况
                    cur = cur / 10;
                }
                cur = cur / 10 + 1;
            }
        }
        return res;
    }
}
```
