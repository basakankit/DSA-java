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
import java.util.*;

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

4. Valid Anagram: Given two strings s and t, return true if t is an anagram of s, and false otherwise.  
eg. Input: s = "anagram", t = "nagaram"  
    Output: true  
Brute Force Approach - O(nlogn)

```java
import java.util.Arrays;

class Solution {
    public boolean isAnagram(String s, String t) {
        // Brute force

        if(s.length()!=t.length()){
            return false;
        }
        char[] S = s.toCharArray();
        char[] T = t.toCharArray();

        Arrays.sort(S);
        System.out.println(S);
        Arrays.sort(T);
        System.out.println(T);

        return Arrays.equals(S,T);
    }
}
```
Optimized approach using hash map. - O(n)


```java
class Solution {
    public boolean isAnagram(String s, String t) {
        // Convert both to lowecase to case to ignore case mishmatch
        s=s.toLowerCase();
        t=t.toLowerCase();

        // Strip of all white spaces
        s=s.replace(" ","");
        t=t.replace(" ","");
        
        // Initialize bucket array
        int[] counts = new int[26];
        // Fill the buckets
        for(int i=0;i<s.length();i++){
            counts[s.charAt(i)-'a']++;
        }
        // Empty the buckets
        for(int i=0;i<t.length();i++){
            counts[t.charAt(i)-'a']--;
        }

        // Check if all the buckets are empty
        for(int count:counts){
            if(count!=0) return false;
        }
        return true;
    }
}
```
5. Intersection of two arrays: Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must be unique and you may return the result in any order.  
eg. Input: nums1 = [1,2,2,1], nums2 = [2,2]  
    Output: [2]

```java
import java.util.*;

class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> set1 = new HashSet<>();
        HashSet<Integer> resultSet = new HashSet<>();

        // Add elements of nums1
        for(int num:nums1){
            set1.add(num);
        }

        // Check Intersection
        for(int num:nums2){
            if(set1.contains(num)){
                resultSet.add(num);
            }
        }

        // Convert set to array
        int[] result = new int[resultSet.size()];
        int i=0;
        for(int num:resultSet){
            result[i++]=num;
        }
        return result;
    }
}   
```
6. First Unique character in a string: Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.  
eg. Input: s = "leetcode"  
Output: 0  
Explanation: The character 'l' at index 0 is the first character that does not occur at any other index.  

```java
import java.util.HashMap;
class Solution {
    public int firstUniqChar(String s) {
        HashMap<Character, Integer> map = new HashMap<>();
        int n=s.length();
        
        // Store the frequencies with characters in the bucket
        for(int i=0;i<n;i++){
            if(map.containsKey(s.charAt(i))){
                map.put(s.charAt(i), map.get(s.charAt(i))+1);
            }
            else{
                map.put(s.charAt(i),1);
            }
        }
        // Iterate through string and find the element in the bucket.
        for(int i=0;i<n;i++){
            if(map.get(s.charAt(i))==1){
                return i;
            }
        }
        return -1;
    }
}
```

## Very Important for interviews  

7. Subarray sum equals K: Given an array of integers nums and an integer k, return the total number of subarrays whose sum equals to k.

A subarray is a contiguous non-empty sequence of elements within an array.  

eg. Input: nums = [1,2,3], k = 3  
    Output: 2

Brute Force - O(n^2)

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int count=0;
        int n=nums.length;

        for(int i=0;i<n;i++){
            int sum=0;
            for(int j=i;j<n;j++){
                sum+=nums[j];
                if(sum==k){
                    count++;
                }    
            }
        }
        return count;
    }
}
```
Optimized approach using prefix sum and hashmap - O(n)

```java
//  Not understood fully, more practise in similar pattern might help.

class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> sumCountMap = new HashMap<>();
        sumCountMap.put(0,1);

        int result=0;
        int prefixSum=0;

        for(int num:nums){
            prefixSum+=num;
            if(sumCountMap.containsKey(prefixSum-k)){
                result+=sumCountMap.get(prefixSum-k);
            }
            if(sumCountMap.containsKey(prefixSum)){
                sumCountMap.put(prefixSum,sumCountMap.get(prefixSum)+1);
            }
            else{
                sumCountMap.put(prefixSum,1);
            }
        }
        return result;
    }
}
```

8. Longest Subarray with sum K: Given an array arr[] containing integers and an integer k, your task is to find the length of the longest subarray where the sum of its elements is equal to the given value k. If there is no subarray with sum equal to k, return 0.  
   eg.   
Input: arr[] = [10, 5, 2, 7, 1, -10], k = 15
Output: 6
Explanation: Subarrays with sum = 15 are [5, 2, 7, 1], [10, 5] and [10, 5, 2, 7, 1, -10]. The length of the longest subarray with a sum of 15 is 6.

Brute Force - O(n^2)

```java
class Solution {
    public int longestSubarray(int[] arr, int k) {
        // code here
        int maxlen=0;
        int n=arr.length;
        
        for(int i=0;i<n;i++){
            int sum=0;
            for(int j=i;j<n;j++){
                sum+=arr[j];
                if(sum==k){
                    maxlen=Math.max(maxlen,j-i+1);
                }
            }
        }
        return maxlen;
    }
}
```
Optimized with HashMap and prefixSum


