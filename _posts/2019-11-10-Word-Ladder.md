---
layout: post
title: Hello World
---

## Word Ladder 
This is a simple BFS problem, if you have defined what the problem acctually is:
You need to find a path from wordA -> wordB, and the only pathway is the words in dictList.
Try to image you want to travel from city A to cityB, there are a list of cities among A and B, you could only go to one of these city which are adjacent in one day, calculate how many days you need to spend to get the city B.

If the question is clear, now is the solution.
1. Get all possible words you could move from wordA
2. Use BFS search Everytime when you decide which city to move
3. Record answer+=1 everytime you find a valid pathway.
4. Only return when you reached into the destination. Otherwise return 0

Here comes the code part:
```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
		/* convert the List into Set first, become the operation 
		List.contains(sth) is O(n) complexity, 
		Set.contains(sth) is O(1) complexity.
		*/
        Set<String> dict = new HashSet<>(wordList);
        
        if (wordList == null) return 0;
        if(beginWord == endWord) return 1;
        
        wordList.add(beginWord);
        
        Queue<String> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();
        
        queue.offer(beginWord);
        visited.add(beginWord);
        
        int ans = 1;
        while(!queue.isEmpty()) {
            ans++;
            int size = queue.size();
            for(int i=0; i<size; i++) {
                String curr = queue.poll();
                for(String word : nextSteps(curr, dict)) {
                    if(visited.contains(word)) continue;
                    if(word.equals(endWord)) return ans;
                    queue.add(word);
                    visited.add(word);
                }
            }
        }
        
        return 0;
    }
    
    private List<String> nextSteps(String word, Set<String> wordList) {
        // find all possible trans, and check if they are valid, all valid string are their possible 
        // next steps
        List<String> steps = new ArrayList<>();
        for(int i=0; i<word.length(); i++) {
            for(char j='a'; j<='z'; j++) {
                if (j == word.charAt(i)) continue;

                String newWord = replace(word, i, j);
                if(wordList.contains(newWord)) steps.add(newWord);
            }
        }
        return steps;
    }
    
    private String replace(String word, int index, Character chara) {

        StringBuilder sb = new StringBuilder();
        char[] temp = word.toCharArray();
        temp[index] = chara;
        for(char c : temp) {
            sb.append(c);
        }
        return sb.toString();
    }
}
```