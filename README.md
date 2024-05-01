# Neetcode 150 Typescript
Neetcode 150 problems and answers. Language used - TypeScript

<details>
  <summary>1. 217-Contains Duplicate </summary>
  
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
