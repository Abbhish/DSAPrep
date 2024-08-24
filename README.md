# DSAPrep

Week 1
1. Two Sum
https://leetcode.com/problems/two-sum/description/

`class Solution {
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
`


3. Contains Duplicate
https://leetcode.com/problems/contains-duplicate/
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
