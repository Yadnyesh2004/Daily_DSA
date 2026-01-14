Pair with Target Sum (easy)

##Explanation :

Problem: Find two numbers in a sorted array that add up to a target value.
Approach: Two-pointer technique

Start with pointers at both ends: i at the beginning (0) and j at the end (length-1)
Calculate the sum of elements at these positions
If sum equals target → found the answer, return indices (1-indexed)
If sum is less than target → move left pointer right (i++) to increase the sum
If sum is greater than target → move right pointer left (j--) to decrease the sum
Repeat until pointers meet

Why it works: Since the array is sorted, moving i right increases values, and moving j left decreases values, allowing you to efficiently narrow down to the target sum.
Time Complexity: O(n) - single pass through the array
Space Complexity: O(1) - only using two pointers


##Problem:-https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

##Code:-
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int i= 0;
        int j= numbers.length-1;
        while(i<j){
            int sum = numbers[i] + numbers[j];
            if(sum == target){
                return new int[]{i+1,j+1};
            }else if(sum<target){
                i++;
            } else
            {
                j--;
            }
        }
        return new int []{-1,-1};
    }
}
