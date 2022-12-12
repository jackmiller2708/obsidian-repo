Tags: #algorithm #search-string-algorithm

The Knuth-Morris-Pratt (KMP) [[Algorithm In General |algorithm]] is a string matching algorithm that uses a pre-processing step to create a "partial match" table, which allows the algorithm to skip over certain characters in the text when it determines that they cannot match the pattern. This can lead to significant improvements in the algorithm's performance over a simple brute-force search. 

The basic logic behind the KMP algorithm is as follows: 

1. The algorithm begins by pre-processing the pattern to create the partial match table. This table stores the length of [[Prefix Function|the longest proper prefix of the pattern that is also a suffix of the pattern up to the given index]]. For example, if the pattern is "ABCDABD", the partial match table would be [0, 0, 0, 0, 1, 2, 0]. 
2. Once the "partial match" table has been constructed, the algorithm searches for the pattern in the text by comparing the characters in the pattern and the text one by one. If the characters match, the algorithm advances to the next character in both the pattern and the text. If the characters do not match, the algorithm uses the partial match table to skip over certain characters in the text and continue the search. 
3. When the algorithm reaches the end of the pattern, it has found a match and can return the position of the match in the text. If the algorithm reaches the end of the text without finding a match, it returns -1 to indicate that the pattern was not found.

Below is an exemplary implementation of the KMP algorithm in TypeScript: 

``` typescript
function kmpSearch(pattern: string, text: string): number {
  // Create the partial match table
  const partialMatchTable = generatePartialMatchTable(pattern);

  // Search for the pattern
  let textIndex = 0;
  let patternIndex = 0;

  while (textIndex < text.length) {
    if (text[textIndex] === pattern[patternIndex]) {
      textIndex++;
      patternIndex++;
    }

    if (text[textIndex] !== pattern[patternIndex]) {
      if (patternIndex > 0) {
        patternIndex = partialMatchTable[patternIndex - 1];
      }

      // Skip one character in the text
      textIndex++;
    }

    if (patternIndex === pattern.length) {
      // Pattern found at position textIndex - patternIndex
      return textIndex - patternIndex;
    }
  }

  return -1; // Pattern not found
}

function generatePartialMatchTable(pattern: string): number[] {
  let partialMatchTable = [0];
  
  for (let i = 1; i < pattern.length; i++) {
    let j = partialMatchTable[i - 1];

    while (j > 0 && pattern[j] != pattern[i]) {
      j = partialMatchTable[j - 1];
    }

    partialMatchTable[i] = pattern[j] == pattern[i] ? j + 1 : 0;
  }

  return partialMatchTable;
}
```

The example is an implementation of the Knuth-Morris-Pratt (KMP) algorithm, a string matching algorithm that uses a pre-processing step to create a "partial match" table. This table allows the algorithm to skip over certain characters in the text when it determines that they cannot match the pattern, which can lead to significant improvements in the algorithm's performance over a simple brute-force search. 

The implementation shown in the example uses an array to store the partial match table, which is constructed as the pattern is processed. This allows the algorithm to easily update and access the values in the table as needed. 

Additionally, the implementation uses a while loop to search for the pattern in the text, which allows it to efficiently skip over characters in the text when it determines that they cannot match the pattern.

Overall, this implementation provides a simple and efficient way to search for a pattern in a text using the KMP algorithm.