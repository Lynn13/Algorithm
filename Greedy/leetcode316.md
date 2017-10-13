## Remove Duplicate Letters

### 解法1 贪心+递归
- 给出字符串s，如果结果是result, 本思路是每次得出result的最前面的字符。
- 每次想要找到s[pos],必须保证s[pos....length-1]包含所有的字符，并且保证s[pos]的字典序
- 找到之后删除pos前面的字符，删除pos后面所有和s[pos]相同的字符
- 继续递归
```
public class Solution {
    public String removeDuplicateLetters(String s) {
        int[] cnt = new int[26];
        int pos = 0; // the position for the smallest s[i]
        for (int i = 0; i < s.length(); i++) cnt[s.charAt(i) - 'a']++;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) < s.charAt(pos)) pos = i;
            if (--cnt[s.charAt(i) - 'a'] == 0) break;
        }
        return s.length() == 0 ? "" : s.charAt(pos) + removeDuplicateLetters(s.substring(pos + 1).replaceAll("" + s.charAt(pos), ""));
    }
}
```

### 解法2 贪心+迭代
- 跟上面差不多

### 解法3 栈
- int[26]表示字符个数
- boolean[26]表示字符是否在stack中
- 每次来一个char，该字符个数-1，在stack中就跳过
- stack空，不能pop，入stack
- stack顶元素个数=0，不能pop，入stack
- 来的char字典序更小？那就pop，然后入stack，记得要记录boolean[26]
- 循环一遍即可，最后把stack中的元素挨个拼起来就OK
```
public String removeDuplicateLetters(String sr) {

    int[] res = new int[26]; 
    boolean[] visited = new boolean[26]; 
    char[] ch = sr.toCharArray();
    for(char c: ch){  
        res[c-'a']++;
    }
    
    
    Stack<Character> st = new Stack<>(); 
    int index;
    for(char s:ch){ 
        index= s-'a';
        res[index]--; 
        if(visited[index])
            continue;
        
        while(!st.isEmpty() && s<st.peek() && res[st.peek()-'a']!=0){ 
            visited[st.pop()-'a']=false;
        }
        
        st.push(s); 
        visited[index]=true;
    }



    StringBuilder sb = new StringBuilder();
    while(!st.isEmpty()){
        sb.insert(0,st.pop());
    }
    return sb.toString();
}
```
