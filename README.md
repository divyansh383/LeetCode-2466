# LeetCode-2466 Count Ways To Build Good Strings

# Problem
Given the integers zero, one, low, and high, we can construct a string by starting with an empty string, and then at each step perform either of the following:

Append the character '0' zero times.
Append the character '1' one times.
This can be performed any number of times.

A good string is a string constructed by the above process having a length between low and high (inclusive).

Return the number of different good strings that can be constructed satisfying these properties. Since the answer can be large, return it modulo 109 + 7.
# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
The problem requires counting the number of good strings within a given range of integers. A good string is defined as a string that does not contain any consecutive zeros or ones. To solve this problem, we can use a dynamic programming approach.

# Approach
<!-- Describe your approach to solving the problem. -->
Initialize a modulo variable mod as (10^9 + 7) to take modulo of the final result.
Create an array tab of size high + 1 to store the count of good strings for each index. Initialize tab[0] as 1, indicating that there is only one good string of length 0 (an empty string).
Initialize a variable count as 0 to keep track of the total count of good strings within the given range.
Iterate over the array tab from index 1 to high.
For each index i, calculate tab[i] as the sum of two values:
If i - zero is greater than or equal to 0, add tab[i - zero] to tab[i]. This represents the count of good strings by appending a zero at the end.
If i - one is greater than or equal to 0, add tab[i - one] to tab[i]. This represents the count of good strings by appending a one at the end.
Take the modulo of the sum to prevent overflow.
If i is within the range [low, high], update count by adding tab[i].
Finally, return count as the total count of good strings within the given range.

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
O(n)

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
O(n)

# Code
```java
class Solution {
    public int countGoodStrings(int low, int high, int zero, int one) {
        int mod=(int)Math.pow(10,9)+7;
        int[] tab=new int[high+1];
        tab[0]=1;
        int count=0;
        for(int i=1;i<tab.length;i++){
            tab[i]=((i-zero>=0?tab[i-zero]:0)+(i-one>=0?tab[i-one]:0))%mod;
            if(i>=low && i<=high){
                count=(count+tab[i])%mod;
            }
        }
        return count;
    }
}

```
