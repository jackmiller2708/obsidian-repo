Tags: #algorithm #proper-prefix #prefix-function

# Definition
It is defined as for a string **s** of length **n**, **π[i]** is the length of the longest proper prefix of the substring **s[0…i]**, which is also a suffix of this substring where the proper prefix of a string is a prefix that is not equal to the string itself. **π[i]** is the i-th element of an n-length array **π**. By definition, **π[0]=0**; **π[i]= max**;  **k=0...i**, **k : s[0…k−1]=s[i−(k−1)…i]**, where **s[0…k−1]** is the proper prefix and **s[i−(k−1)…i]** is the suffix of length **k** of the string **s**.

Mathematically the definition of the prefix function can be written as follows:
$\pi[i] = \max_ {k = 0 \dots i} \{k : s[0 \dots k-1] = s[i-(k-1) \dots i] \}$

The goal of the table is to allow the algorithm not to match any character of **s** more than once. The key observation about the nature of a linear search that allows this to happen is that in having checked some segment of the main string against an _initial segment_ of the pattern, we know exactly at which places a new potential match which could continue to the current position could begin prior to the current position. In other words, we "pre-search" the pattern itself and compile a list of all possible fallback positions that bypass a maximum of hopeless characters while not sacrificing any potential matches in doing so.

e.g.  For string "ababaca", prefix function array π is [0,0,1,2,3,0,1].

![[prefix-function.png]]
# Optimized approach
- At first, compute the prefix values π[i] in a loop by iterating from i=1 to i=n−1 (π[0] is assigned with 0).
- To calculate the current value π[i], set the variable j denoting the length of the best suffix for i−1. Initially, j=π[i−1].
- Test if the suffix of substring s[0....i] of length j+1 is also a prefix of the substring s[0....i] by comparing s[j] and s[i]. If they are equal, we assign π[i]=j+1 (the values of the prefix function can only increase by at most one); otherwise, reduce j to π[j−1] ( greatest k<j, for which the prefix property holds is π[j−1]) and repeat this step.
- If length j=0 is reached and still don't have a match, then assign π[i]=0 and go to the next index i+1

Below is an exemplary implementation in TypeScript:

```TypeScript
function prefixFn(text: string): number[] {
  let pi = [0];
  
  for (let i = 1; i < text.length; i++) {
    let j = pi[i - 1];

    while (j > 0 && text[j] != text[i]) {
      j = pi[j - 1];
    }

    pi[i] = text[j] == text[i] ? j + 1 : 0;
  }

  return pi;
}
```

This algorithm was proposed by Knuth and Pratt and independently from them by Morris in 1977. It was used as the main function of a substring search algorithm.