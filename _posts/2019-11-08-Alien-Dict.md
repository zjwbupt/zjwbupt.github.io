# Alien Diction

There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.
## Example
Example 1:

Input:
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]

Output: "wertf"
Example 2:

Input:
[
  "z",
  "x"
]

Output: "zx"
Example 3:

Input:
[
  "z",
  "x",
  "z"
] 

Output: "" 

Explanation: The order is invalid, so return "".
Note:

You may assume all letters are in lowercase.
You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
If the order is invalid, return an empty string.
There may be multiple valid order of letters, return any one of them is fine.

## Idea
In order to find the order of letters, you need to do following things:  
1. Get a map/graph of letters, with its following letters, eg:  
    Map<Charcater, Set<Character>> graph = {['w',SET{'e'}], ['r',SET{'t'}]}  
2. Then you need to count the indegree of each letter, which is their position in the dict.
3. Once you get the indegree map in the form <Character, Indegree>, you can use topological sort to solve them.

### About Topological Sort
1. You need to remember that: before return final value, check for loop!!!
2. One you build the graph, it is nothing but a normal topological sort problem.

## Code
```java
package BFS;
import java.util.*;

public class AlienDict {
    public String alienOrder(String[] words) {
        Map<Character, Set<Character>> graph = createGraph(words);


        String dict = getDict(graph);
        return dict;
    }

    private  Map<Character, Set<Character>> createGraph(String[] words) {
        Map<Character, Set<Character>> charMap = new HashMap<>();

        // crate nodes
        for(int i=0; i<words.length; i++) {
            String word = words[i];
            for(int j=0; j<word.length(); j++) {
                Character alpha = word.charAt(j);
                if(!charMap.containsKey(alpha)) {
                    charMap.put(alpha, new HashSet<Character>());
                }
            }
        }

        // create edges
        for(int i=0; i<words.length-1; i++) {
            int index = 0;
            while( index < words[i].length() && index < words[i+1].length() ) {
                if(words[i].charAt(index) != words[i+1].charAt(index)) {
                    // we put later char in to the edge;
                    charMap.get(words[i].charAt(index)).add(words[i+1].charAt(index));
                    break;
                }
                index++;
            }
        }

        return charMap;
    }

    private String getDict(Map<Character, Set<Character>> charMap) {
        // the input is a graph, contains chars and its nexts chars;
        Map<Character, Integer> indegree = getIndegree(charMap);
        Queue<Character> queue = new PriorityQueue<>();

        for(Character c : indegree.keySet()) {
            if(indegree.get(c) == 0) {
                queue.offer(c);
            }
        }

        StringBuilder sb = new StringBuilder();

        while(!queue.isEmpty()) {
            Character letter = queue.poll();
            sb.append(letter);
            for( Character let : charMap.get(letter)) {
                indegree.put(let, indegree.get(let)-1);
                if(indegree.get(let) == 0) {
                    queue.offer(let);
                }
            }
        }

        if(sb.length() !=indegree.size()) {
            return "";
        }

        return sb.toString();
    }

    private Map<Character, Integer> getIndegree(Map<Character, Set<Character>> charMap) {
        Map<Character, Integer> indegree = new HashMap<>();

        for (Character u : charMap.keySet()) {
            indegree.put(u, 0);
        }

        for(Character c : charMap.keySet()) {
            for(Character temp: charMap.get(c)) {
                indegree.put(temp, indegree.get(temp)+1);
            }
        }
        return indegree;
    }
}

```