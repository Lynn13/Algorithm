### Evaluate Division
- 看了solution才知道应该用图
- 一个节点是一个String， 构造一个`HashMap<String, ArrayList<String>>`保存与之联通的节点，`HashMap<String, ArrayList<Double>>`保存本节点与联通节点的value
- a / b = 2, value(a->b)=2, value(b->a)=1
- 想要算a / x 的值，就把a的所有连通节点都深搜一遍
```
import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;

class Solution {
    public double[] calcEquation(String[][] equations, double[] values, String[][] queries) {
        HashMap<String, ArrayList<String>> pairsMap = new HashMap<>();
        HashMap<String, ArrayList<Double>> valuesMap = new HashMap<>();

        for (int i = 0; i < equations.length; i++){
            String[] equ = equations[i];
            if (!pairsMap.containsKey(equ[0])){
                pairsMap.put(equ[0], new ArrayList<String>());
                valuesMap.put(equ[0], new ArrayList<Double>());
            }
            if (!pairsMap.containsKey(equ[1])){
                pairsMap.put(equ[1], new ArrayList<String>());
                valuesMap.put(equ[1], new ArrayList<Double>());
            }

            pairsMap.get(equ[0]).add(equ[1]);
            pairsMap.get(equ[1]).add(equ[0]);
            valuesMap.get(equ[0]).add(values[i]);
            valuesMap.get(equ[1]).add(1 / values[i]);
        }

        double[] res = new double[queries.length];
        for (int i = 0; i < queries.length; i++){
            String[] q = queries[i];
            res[i] = dFS(q[0], q[1], pairsMap, valuesMap, new HashSet<String>(), 1.0);
            if (res[i] == 0.0) res[i] = -1.0;
        }
        return res;
    }

    double dFS(String cur, String end, HashMap<String, ArrayList<String>> pairsMap, HashMap<String, ArrayList<Double>> valuesMap,
               HashSet<String> set, double value){
        if (set.contains(cur))
            return 0.0;
        if (!pairsMap.containsKey(cur))
            return 0.0;
        if (cur.equals(end))
            return value;

        set.add(cur);
        ArrayList<String> strList = pairsMap.get(cur);
        ArrayList<Double> valList = valuesMap.get(cur);
        double tmp = 0.0;
        for (int i = 0; i < strList.size(); i++){
            tmp = dFS(strList.get(i), end, pairsMap, valuesMap, set, value * valList.get(i));
            if (tmp != 0.0)
                break;
        }
        set.remove(cur);
        return tmp;

    }
}
```
