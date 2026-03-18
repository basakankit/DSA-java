1. Two Sum: Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.  
eg. Input: nums = [3,2,4], target = 6  
    Output: [1,2]
```java
    import java.util.HashMap;
    class Solution {
    public int[] twoSum(int[] nums, int target) {
    
        HashMap<Integer,Integer> map = new HashMap<>();
        int n=nums.length;
        
        for(int i=0;i<n;i++){
            int rem=target-nums[i];
            if(map.containsKey(rem)){
                return new int[] {map.get(rem),i}
            }
            mpp.put(nums[i],i);
        }
        return new int[] {};
    }
}
```
2. Contains Duplicate: Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.  
Example 1: Input: nums = [1,2,3,1]
           Output: true  
Explanation: The element 1 occurs at the indices 0 and 3.  
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashMap<Integer,Integer> map = new HashMap<>();
        int n=nums.length;

        for(int i=0;i<n;i++){
            if(map.containsKey(nums[i])){
                map.put(nums[i],map.get(nums[i])+1);
            }
            else{
                map.put(nums[i],1);
            }
        }

        for(Map.Entry<Integer,Integer> it:map.entrySet()){
            if(it.getValue()>=2){
                return true;
            }
        }
        return false;
    }
}
```
3. Majority Element: Given an array nums of size n, return the majority element. The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.
Eg. Input: nums = [2,2,1,1,1,2,2]  
    Output: 2
```java
class Solution {
    public int majorityElement(int[] nums) {
        HashMap<Integer,Integer> map = new HashMap<>();
        int n=nums.length;

        // Count frequencies
        for(int i=0;i<n;i++){
            // fmpp.put(num[i], fmpp.getOrDefault(nums[i], 0) + 1);
            if(map.containsKey(nums[i])){
                map.put(nums[i],map.get(nums[i])+1);
            }
            else{
                map.put(nums[i],1);
            }
        }

        int maxf=Integer.MIN_VALUE;
        int maxans=-1;

        // Find the element with maximum frequency
        for(Map.Entry<Integer, Integer> it:map.entrySet()){
            if(it.getValue()>maxf){
                maxf=it.getValue();
                maxans=it.getKey();
            }
        }
        return maxans;        
    }
}
```
