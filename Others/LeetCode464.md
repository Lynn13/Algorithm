```
import java.util.HashMap;
import java.util.Map;

/**
 *
 * 因为 maxChoosableInteger will not be larger than 20
 * 所以用一个visited（int）值来代表有哪些值被选了，110110代表2 3 5 6被选了
 *
 * 每个visited也代表一种情况下胜负是固定的，用哈希map来记录每个visited的胜负
 */
class Solution {

    int maxChooseInt;
    Map<Integer, Boolean> map = new HashMap<>();

    public boolean canIWin(int maxChoosableInteger, int desiredTotal) {
        maxChooseInt = maxChoosableInteger;
        if (maxChoosableInteger >= desiredTotal)
            return true;
        if ((1 + maxChoosableInteger) * maxChoosableInteger / 2 < desiredTotal)
            return false;
        return func(desiredTotal, 0);
    }

    private boolean func(int total, int visited){
        if (map.containsKey(visited))
            return map.get(visited);

        for (int i = 1; i <= maxChooseInt; i++){
            int mask = (1 << i);

            // 这个数没被选过，而且选了就超过目标了，胜
            if ((mask & visited) == 0 && i >= total){
                map.put(visited, true);
                return true;
            }

            // 这个数没被选过，而且选了之后，对手只能输，胜
            if ((mask & visited) == 0 && !func(total - i, mask | visited)){
                map.put(visited, true);
                return true;
            }
        }

        map.put(visited, false);
        return false;
    }
}
```
