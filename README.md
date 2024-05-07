# Neetcode 150 Typescript
Neetcode 150 problems and answers. Language used - TypeScript

<details>
  <summary>1. 217 - Contains Duplicate </summary>
  
  ### Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

  **Answer 1**
  ```ts
    // Using N^2 Loops
    function containsDuplicate(nums: number[]): boolean {
        for (let i = 0; i < nums.length; i++) {
            for (let j=i+1; j<= nums.length; j++) {
                if (nums[i] === nums [j]) {
                    return true;
                }
            }
        }
        return false;
    };
  ```

 **Answer 2**
  ```ts
    // Using Map
    function containsDuplicate(nums: number[]): boolean {
      const store = new Map();
      for (let i of nums) {
          if (store.has(i)) return true;
          else store.set(i, 1);
      }
      return false;
    };
  ```

 **Answer 3**
  ```ts
    // Using SET, has slight advantage over Map
    // Set is optimized to store duplication
    // In this case, we are not going to use the values of Map, so its unnecessary
    function containsDuplicate(nums: number[]): boolean {
      const seenNumbers = new Set<number>();
      for (const num of nums) {
          if (seenNumbers.has(num)) {
              return true; // If we've already seen the number, return true
          } else {
              seenNumbers.add(num); // Otherwise, add it to the set of seen numbers
          }
      }
      return false; // If we've gone through the loop without finding duplicates, return false
    }
  ```
</details>

<details>
  <summary>2. 242 - Valid Anagram </summary>
  
  ### Given two strings s and t, return true if t is an anagram of s, and false otherwise. An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

  **Answer 1**
  ```ts
    function isAnagram(s: string, t: string): boolean {
      // Using Map
      if (s.length !== t.length) return false;
  
      const store = new Map();
      for (let char of s) {
          const val = store.has(char) ? store.get(char) + 1 : 1;
          store.set(char, val);
      }
  
      for (let char of t) {
          if (store.has(char)) {
              const val = store.get(char);
              if (val <= 0) return false;
  
              store.set(char, val - 1);
          }
          else {
              return false;
          }
      }
      return true;
  };
  ```

 **Answer 2**
  ```ts
    function isAnagram(s: string, t: string): boolean {
      // Using Map, +/- map in single pass
      if (s.length !== t.length) return false;
  
      const store = new Map();
      for (let i = 0; i < s.length; i++) {
          store.set(s[i], (store.get(s[i]) || 0)  + 1);
          store.set(t[i], (store.get(t[i]) || 0) - 1);
      }
  
      for (let [_, v] of store) {
          if (v !== 0) return false;
      }
      return true;
  };
  ```
</details>

<details>
  <summary>3. 1 - Two Sum </summary>
  
  ### Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target. You may assume that each input would have exactly one solution, and you may not use the same element twice.

  **Answer 1**
  ```ts
    function twoSum(nums: number[], target: number): number[] {
    const store = new Map();
    const result: number[] = [];

    for(let [i, n] of nums.entries()) {
        const val = target - n;
        if (store.has(val)) {
            return [i, store.get(val)]
        }
        store.set(n, i);
    }

    return result;
};
  ```

 **Answer 2**
 - In case if we want to solve it without using HashMap, then use **Two pointers approach**, but that needs Sorting the array and we need to preserve the index by [(val1, index1), (val2, index2) ...] and it is not a best approach.
</details>

<details>
  <summary>4. 125 - Valid Palindrome </summary>
  
  ### A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

  **Answer 1**
  ```ts
    function isPalindrome(s: string): boolean {
      let i = 0;
      let j = s.length - 1;
  
      function isAlphanumeric(str) {
          return /^[a-zA-Z0-9]+$/.test(str);
      }
  
      while(i<j) {
          if (!isAlphanumeric(s[i])) {
              i++;
          }
          else if (!isAlphanumeric(s[j])) {
              j--;
          }
          else if (s[i].toLowerCase() === s[j].toLowerCase()) {
              i++;
              j--;
          }
          else {
              return false;
          }
      }
      return true;
      };
  };
  ```

 **Answer 2**
 - Clean the whole string initially and loop through
```ts
function isPalindrome(s: string): boolean {
    const str = s.replace(/[^0-9a-z]/gi, '').toLowerCase();
    let i = 0;
    let j = str.length - 1;

    while (i < j) {
        if (str[i] !== str[j]) return false;
        i++;
        j--;
    }

    return true;
};
```
</details>
