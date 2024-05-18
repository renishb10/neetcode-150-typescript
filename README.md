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

<details>
  <summary>5. 121 - Best Time to Buy and Sell Stock </summary>
  
  ### You are given an array prices where prices[i] is the price of a given stock on the ith day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

  **Answer 1**
  ```ts
    // Sliding Window Approach
    function maxProfit(prices: number[]): number {
      let i = 0;
      let j = i + 1;
      let profit = 0;
  
      while(i < prices.length - 1) {
          if (prices[i] < prices[j]) {
              profit = Math.max(prices[j] - prices[i], profit);
              j++;
          }
          else {
              i = j;
              j = i + 1;
          }
      }
  
      return profit;
  };
  ```
</details>

<details>
  <summary>6. 20 - Valid Parentheses </summary>
  
  ### Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

  **Answer 1**
  ```ts
    function isValid(s: string): boolean {
      if (s.length % 2 !== 0) return false;
  
      const stk: string[] = [];
  
      for (let i = 0; i < s.length; i++) {
          if(s[i] === '('   || s[i] === '{' || s[i] === '['){
             stk.push(s[i]);
          }
          else {
              const p = stk.pop();
  
              if(s[i] === ')' && p !== '(' || s[i] === '}' && p !== '{'  || s[i] === ']' && p !== '[') {
                  return false;
              }
          }
      }
  
      return stk.length === 0;
  };
  ```
</details>

<details>
  <summary>6. 704 - Binary Search </summary>
  
  ### Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

  **Answer 1**
  ```ts
    function search(nums: number[], target: number): number {
      let low = 0;
      let high = nums.length - 1;
  
      while(low <= high) {
          let mid = Math.floor((low + high) / 2); // CAUTION but nitpick: enclose low + high with brackets.
          if (target === nums[mid]) return mid;
          else if (target > nums[mid]) {
              low = mid + 1;
          }
          else if (target < nums[mid]) {
              high = mid - 1;
          }
      }
  
      return -1;
  };
  ```
</details>

<details>
  <summary>7. 206 - Reverse Linked List </summary>
  
  ### Given the head of a singly linked list, reverse the list, and return the reversed list.

  **Answer 1**
  ```ts
    function reverseList(head: ListNode | null): ListNode | null {
        let currentNode = head;
        let prevNode = null;
    
        while(currentNode !== null) {
            let nextNode = currentNode.next;
            currentNode.next = prevNode;
            prevNode = currentNode;
            currentNode = nextNode;
        }
    
        return prevNode;
    };
  ```
</details>

<details>
  <summary>8. 21 - Merge Two Sorted Lists </summary>
  
  ### Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

  **Answer 1**
  ```ts
    function mergeTwoLists(list1: ListNode | null, list2: ListNode | null): ListNode | null {
      const head: ListNode = new ListNode();
      let curr: ListNode = head;
  
      while(list1 !== null && list2 !== null) {
              if (list1.val < list2.val) {
                  curr.next = list1
                  list1 = list1.next
              }
              else {
                  curr.next = list2
                  list2 = list2.next
              }
  
          curr = curr.next;
      }
  
      curr.next = list1 || list2;
      
      return head.next;
  };
  ```
</details>

<details>
  <summary>8. 202 - Happy Number </summary>
  
  ### Write an algorithm to determine if a number n is happy.
  A happy number is a number defined by the following process:

  Starting with any positive integer, replace the number by the sum of the squares of its digits.
  Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
  Those numbers for which this process ends in 1 are happy.
  Return true if n is a happy number, and false if not.

  **Answer 1**
  ```ts
    function isHappy(n: number): boolean {
      const seen = new Set();
  
      while(n !== 1) {
          let sum = 0;
          
          while(n > 0) {
              sum += (n%10) ** 2;
              n = Math.floor(n/10);
          }
  
          if (seen.has(sum)) {
              return false;
          }
          else {
              seen.add(sum);
              n = sum;
          }
      }
  
      return true;
  };
  ```
</details>
