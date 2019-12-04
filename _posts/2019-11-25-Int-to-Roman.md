## Integer to Roman
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.  

String[] roman = new String[]{"M", "CM", "D","CD","C", "XC","L","XL","X","IX","V","IV","I"};
        int[] numerial =    new int[]{1000, 900, 500, 400, 100,  90,  50, 40, 10,   9,   5,  4,  1};

Convert an int to Roman format; Like 4 -> IV, 5->V;

The hardest part of this problem is that you need to list all unseen situation. Like 4 is IV, not IIII, 900 is CM, not DCCCC.

The best way to tackle this is to list all posiblle minimum unit of roman number, and then the problem is easy. Just substrsct the number with the largest unit of Roman, when it is larger/equal then 0, continue going.



```java
public String intToRoman(int num) {
   String[] roman = new String[]{"M", "CM", "D","CD","C", "XC","L","XL","X","IX","V","IV","I"};
        int[] numerial =    new int[]{1000, 900, 500, 400, 100,  90,  50, 40, 10,   9,   5,  4,  1};
  
  int i=0;
  StringBuilder sb = new StringBuider();
  
  while(num > 0) {
    if(num-numerial[i] >= 0) {
      num -= numerial[i];
      sb.append(roman[i]);
    } else {
      i++;
    }
  }
  
  return sb.toString();
}
```

