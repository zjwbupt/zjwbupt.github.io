#ZigZag Conversion

## Intro

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string s, int numRows);
```

**Example 1:**

```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

**Example 2:**

```
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```

## Idea

The description of the problem is misleading. This is just a way to output the string s;

And the rule is, give you a number n(NumRows), you start to scan the string. When i < n, keep i increasing, and when i reached n, then keep i decreasing. 

|Line| 	|	 |	 | 

|0	 | a  |	 |	 | g

|1 	| b  |	 | f  | h

|2	 | c  | e  |	|  i

|3	 | d  |	 |	| j

## Code

```java
public String convert(String s, int numRows) {
        int index = 0;
        StringBuilder[] sb = new StringBuilder[numRows];

        for(int i=0; i<numRows; i++) {
            sb[i] = new StringBuilder();
        }
        
        while(index < s.length()) {
            // first increse i from 0 -> n-1;
            for(int i=0; i<numRows && index < s.length(); i++) {
                sb[i].append(s.charAt(index));
                index++;
            }
          	// then decrease i fron n-2 -> 1;
            for(int i=numRows-2; i>0 && index < s.length(); i--) {
                sb[i].append(s.charAt(index));
                index++;
            }
        }
        
        StringBuilder ans = new StringBuilder();
        for(StringBuilder ss : sb) {
            ans.append(ss);
        }      
        return ans.toString();
}
```

