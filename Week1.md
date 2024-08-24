Week 1

1. Two Sum
https://leetcode.com/problems/two-sum/description/

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

8. 3Sum
https://leetcode.com/problems/3sum/description/
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
