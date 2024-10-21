Week 1
Count 10

1. Two Sum
https://leetcode.com/problems/two-sum/description/

```
Example 1:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:
Input: nums = [3,2,4], target = 6
Output: [1,2]

Example 3:
Input: nums = [3,3], target = 6
Output: [0,1]
```
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> hm = new HashMap();
        for(int i=0; i<nums.length; i++){
            hm.put(nums[i], i);
        }
        for(int i=0;i<nums.length; i++){
            int diff=target-nums[i];
            if(hm.containsKey(diff) && hm.get(diff)!=i){
                return new int[]{i, hm.get(diff)};
            }
        }
        return new int[]{};
    }
}
```

2. Contains Duplicate
https://leetcode.com/problems/contains-duplicate/

```
Example 1:
Input: nums = [1,2,3,1]
Output: true
Explanation:
The element 1 occurs at the indices 0 and 3.

Example 2:
Input: nums = [1,2,3,4]
Output: false
Explanation:
All elements are distinct.

Example 3:
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```
```
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> hs = new HashSet();

        for(int num: nums){
            if(hs.contains(num)){
                return true;
            }else{
                hs.add(num);
            }
        }
        return false;
    }
}
```

3.  Best Time to Buy and Sell Stock
https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/
```
Example 1:
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

Example 2:
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```
```
class Solution {
    public int maxProfit(int[] prices) {
        int min = Integer.MAX_VALUE;
        int profit = 0;

        for(int price: prices){
            if(min>price){
                min=price;
            }
            int currProfit = price-min;
            profit = Math.max(profit, currProfit);
        }
        return profit;
    }
}
```

4. Valid Anagram
https://leetcode.com/problems/valid-anagram/description/
```
Example 1:
Input: s = "anagram", t = "nagaram"
Output: true

Example 2:
Input: s = "rat", t = "car"
Output: false
```
```
class Solution {
    public boolean isAnagram(String s, String t) {
        Map<Character, Integer> hm = new HashMap();
        for(char ch: s.toCharArray()){
            hm.put(ch, hm.getOrDefault(ch,0)+1);
        }
        for(char ch: t.toCharArray()){
            hm.put(ch, hm.getOrDefault(ch,0)-1);
        }

        for(int count: hm.values()){
            if(count!=0){
                return false;
            }
        }
        return true;
    }
}
```

5. Valid Parentheses
https://leetcode.com/problems/valid-parentheses/description/
```
Example 1:
Input: s = "()"
Output: true

Example 2:
Input: s = "()[]{}"
Output: true

Example 3:
Input: s = "(]"
Output: false

Example 4: 
Input: s = "([])"
Output: true
```
```
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stk = new Stack();
        for(char ch: s.toCharArray()){
            if(ch=='('){
                stk.push(')');
            }else if(ch=='['){
                stk.push(']');
            }else if(ch=='{'){
                stk.push('}');
            }else if(stk.isEmpty() || stk.pop()!=ch){
                return false; 
            }
        }
        return stk.isEmpty();
    }
}
```

6. Maximum Subarray
https://leetcode.com/problems/maximum-subarray/description/
```
Example 1:
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.

Example 2:
Input: nums = [1]
Output: 1
Explanation: The subarray [1] has the largest sum 1.

Example 3:
Input: nums = [5,4,-1,7,8]
Output: 23
Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.
```
```
class Solution {
    public int maxSubArray(int[] nums) {
        int currSum = 0;
        int maxSum = Integer.MIN_VALUE;
        for(int num: nums){
            currSum = currSum+num;
            if(currSum>maxSum){
                maxSum = currSum;
            }
            if(currSum<0){
                currSum=0;
            }

        }
        return maxSum;
    }
}
```

7. Product of Array Except Self
https://leetcode.com/problems/product-of-array-except-self/description/
```
Example 1:
Input: nums = [1,2,3,4]
Output: [24,12,8,6]

Example 2:
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```
```
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] preProduct = new int[n];
        int[] postProduct = new int[n];
        int[] result = new int[n];

        preProduct[0] = 1;
        postProduct[n-1] = 1;

        for(int i=1; i<n; i++){
            preProduct[i] = preProduct[i-1]*nums[i-1];
        }
        for(int i=n-2; i>=0; i--){
            postProduct[i] = postProduct[i+1]*nums[i+1];
        }

        for(int i=0; i<n; i++){
            result[i]= preProduct[i]*postProduct[i];
        }
        return result;
    }
}
```
8. 3Sum
https://leetcode.com/problems/3sum/description/
```
Example 1:
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

Example 2:
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.

Example 3:
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
```
```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> set = new HashSet();
        List<List<Integer>> ans = new ArrayList();

        Arrays.sort(nums);

        for(int i=0; i<nums.length; i++){
            int j=i+1;
            int k=nums.length-1;
            while(j<k){
                if(nums[i]+nums[j]+nums[k]==0){
                    set.add(Arrays.asList(nums[i], nums[j], nums[k]));
                    j++;
                    k--;
                }else if(nums[i]+nums[j]+nums[k]<0){
                    j++;
                }else{
                    k--;
                }
            }
        }
        ans.addAll(set);
        return ans;
    }
}
```

9. Merge Intervals
https://leetcode.com/problems/merge-intervals/description/
```
Example 1:
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

Example 2:
Input: intervals = [[1,4],[4,5]] 
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```
```
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a,b)->a[0]-b[0]);

        List<int[]> list = new ArrayList();
        int start = intervals[0][0];
        int end = intervals[0][1];

        for(int i=1; i<intervals.length; i++){
            int s = intervals[i][0];
            int e = intervals[i][1];

            if(s<=end){
                end = Math.max(end, e);

            }else{
                list.add(new int[]{start, end});
                start=s;
                end=e;
            }
        }
        list.add(new int[]{start, end});
        return list.toArray(new int[list.size()][]);
    }
}
```

10. Group Anagrams
https://leetcode.com/problems/group-anagrams/description/
```
Example 1:
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
Explanation:
There is no string in strs that can be rearranged to form "bat".
The strings "nat" and "tan" are anagrams as they can be rearranged to form each other.
The strings "ate", "eat", and "tea" are anagrams as they can be rearranged to form each other.

Example 2:
Input: strs = [""]
Output: [[""]]
 
Example 3:
Input: strs = ["a"]
Output: [["a"]]
```
```
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> ans = new ArrayList();
        Map<String, List<String>> hm = new HashMap();
        for(String word: strs){
            char[] ch = word.toCharArray();
            Arrays.sort(ch);
            String sortedWord = new String(ch);
            if(!hm.containsKey(sortedWord)){
                hm.put(sortedWord, new ArrayList());
            }
            hm.get(sortedWord).add(word);
        }
        for(List<String> value: hm.values()){
            ans.add(value);
        }
        return ans;
    }
}
```
