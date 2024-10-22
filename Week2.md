Week 2
Count 11

1. Reverse Linked List
https://leetcode.com/problems/reverse-linked-list/description/

```
Example 1:
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```
![image](https://github.com/user-attachments/assets/1f6deed8-9a24-4f86-859d-a37de76a9b9a)

```
Example 2:
Input: head = [1,2]
Output: [2,1]
```
![image](https://github.com/user-attachments/assets/d4743a74-181f-4015-a5ef-43ecb96cdfc1)

```
Example 3:
Input: head = []
Output: []
```
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode curr, prev;
        prev=null;
        curr=head;
        while( curr!=null){
            ListNode next = curr.next;
            curr.next=prev;
            prev=curr;
            curr=next;
        }
        return prev;
    }
}
```

2. Linked List Cycle
https://leetcode.com/problems/linked-list-cycle/description/

```
Example 1:
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```
![image](https://github.com/user-attachments/assets/b9478b31-60be-4af5-b5b7-7b2a915740f2)

```
Example 2:
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.
```
![image](https://github.com/user-attachments/assets/7b6ac1e5-11e0-484f-9673-ae6330e653a1)

```
Example 3:
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```
![image](https://github.com/user-attachments/assets/3816e27a-580e-4d25-a351-66e2152e3885)

```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow=head, fast=head;
        while( fast!=null && fast.next!=null){
            slow=slow.next;
            fast=fast.next.next;
            if(slow==fast){
                return true;
            }
        }
        return false;
    }
}
```

3. Container With Most Water
https://leetcode.com/problems/container-with-most-water/description/
```
Example 1:
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```
![image](https://github.com/user-attachments/assets/a9e69dbd-2f74-4791-b43d-243e22e6b7d0)

```
Example 2:
Input: height = [1,1]
Output: 1
```

```
class Solution {
    public int maxArea(int[] height) {
        int start=0;
        int end=height.length-1;
        int maxArea = 0;
        while(start<end){
            int minHeight = Math.min(height[start], height[end]);
            int currLength = end-start;
            int currArea = minHeight*currLength;
            maxArea = Math.max(maxArea, currArea);
            if(height[start]<height[end]){
                start++;
            }else{
                end--;
            }
        }
        return maxArea;
    }
}
```

4. Find Minimum In Rotated Sorted Array
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/
```
Example 1:
Input: nums = [3,4,5,1,2]
Output: 1
Explanation: The original array was [1,2,3,4,5] rotated 3 times.

Example 2:
Input: nums = [4,5,6,7,0,1,2]
Output: 0
Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.

Example 3:
Input: nums = [11,13,15,17]
Output: 11
Explanation: The original array was [11,13,15,17] and it was rotated 4 times. 
```
```
class Solution {
    public int findMin(int[] nums) {
        int start=0;
        int end=nums.length-1;
        while(start<end){
            int mid=start+(end-start)/2;
            if(nums[mid]>nums[end]){
                start=mid+1;
            }else{
                end=mid;
            }
        }
        return nums[start];
    }
}
```

5. Longest Repeating Character Replacement
https://leetcode.com/problems/longest-repeating-character-replacement/description/
```
Example 1:
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.

Example 2:
Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may exists other ways to achieve this answer too.
```

```
class Solution {
    public int characterReplacement(String s, int k) {
        Map<Character, Integer> hm = new HashMap();
        int l=0;
        int maxRepeat=0;
        int maxLen=0;
        for(int r=0; r<s.length(); r++){
            int currLen=r-l+1;
            char ch=s.charAt(r);
            hm.put(ch, hm.getOrDefault(ch, 0)+1);
            maxRepeat=Math.max(maxRepeat, hm.get(ch));
            int nonRepeat = currLen-maxRepeat;
            if(nonRepeat>k){
                hm.put(s.charAt(l), hm.get(s.charAt(l))-1);
                l++;
                currLen=r-l+1;
            }
            maxLen=Math.max(maxLen, currLen);
        }
        return maxLen;

    }
}
```

6. Longest Substring Without Repeating Characters
https://leetcode.com/problems/longest-substring-without-repeating-characters/description/
```
Example 1:
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2:
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Example 3:
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```
```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> set = new HashSet();
        int maxLen=0;
        int l=0;
        for(int r=0; r<s.length(); r++){
            char ch=s.charAt(r);
            if(!set.contains(ch)){
                set.add(ch);
                maxLen=Math.max(maxLen, r-l+1);
            }else{
                while(set.contains(ch)){
                    set.remove(s.charAt(l));
                    l++;
                }
                set.add(ch);
            }
        }
        return maxLen;
    }
}
```

7. Number Of Islands
https://leetcode.com/problems/number-of-islands/description/
```
Example 1:
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1

Example 2:
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```
```
class Solution {
    public int numIslands(char[][] grid) {
        int count=0;
        for( int r=0; r<grid.length; r++){
            for(int c=0; c<grid[0].length; c++){
                if(grid[r][c]=='1'){
                    count++;
                    DFSMarking(r,c,grid);
                }
            }
        }
        return count;
    }
    public void DFSMarking(int r, int c, char[][] grid){
        if(
            r<0 || r>=grid.length ||
            c<0 || c>=grid[0].length ||
            grid[r][c]=='0'
        ) return;
        grid[r][c]='0';
        DFSMarking(r-1,c,grid);
        DFSMarking(r,c+1,grid);
        DFSMarking(r+1,c,grid);
        DFSMarking(r,c-1,grid);
    }
}
```

8. Remove Nth Node From End Of List
https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/
```
Example 1:
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```
![image](https://github.com/user-attachments/assets/c111d8ee-a85f-423a-ab84-76ea25a8e898)

```
Example 2:
Input: head = [1], n = 1
Output: []

Example 3:
Input: head = [1,2], n = 1
Output: [1]
```

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode start=new ListNode();
        start.next=head;
        ListNode curr=start, prev=start;

        for(int i=0; i<n; i++){
            curr=curr.next;
        }
        while(curr.next!=null){
            prev=prev.next;
            curr=curr.next;
        }
        prev.next=prev.next.next;
        return start.next;
    }
}
```

9. Palindromic Substring
https://leetcode.com/problems/palindromic-substrings/description/
```
Example 1:
Input: s = "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".

Example 2:
Input: s = "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```

```
class Solution {
    int count=0;
    public int countSubstrings(String s) {
        for(int i=0; i<s.length(); i++){
            makeCount(i, i, s);
            makeCount(i, i+1, s);
        }
        return count;
    }
    public void makeCount(int l, int r, String s){
        while(l>=0 && r<s.length() && s.charAt(l)==s.charAt(r)){
            count++;
            l--;
            r++;
        }
        
    }
}
```

10. Pacific Atlantic Waterflow
https://leetcode.com/problems/pacific-atlantic-water-flow/description/

```
Example 1:
```
![image](https://github.com/user-attachments/assets/e37c4af0-c84e-456c-9f8b-073bba23b7e9)

```
Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
Explanation: The following cells can flow to the Pacific and Atlantic oceans, as shown below:
[0,4]: [0,4] -> Pacific Ocean 
       [0,4] -> Atlantic Ocean
[1,3]: [1,3] -> [0,3] -> Pacific Ocean 
       [1,3] -> [1,4] -> Atlantic Ocean
[1,4]: [1,4] -> [1,3] -> [0,3] -> Pacific Ocean 
       [1,4] -> Atlantic Ocean
[2,2]: [2,2] -> [1,2] -> [0,2] -> Pacific Ocean 
       [2,2] -> [2,3] -> [2,4] -> Atlantic Ocean
[3,0]: [3,0] -> Pacific Ocean 
       [3,0] -> [4,0] -> Atlantic Ocean
[3,1]: [3,1] -> [3,0] -> Pacific Ocean 
       [3,1] -> [4,1] -> Atlantic Ocean
[4,0]: [4,0] -> Pacific Ocean 
       [4,0] -> Atlantic Ocean
Note that there are other possible paths for these cells to flow to the Pacific and Atlantic oceans.

Example 2:
Input: heights = [[1]]
Output: [[0,0]]
Explanation: The water can flow from the only cell to the Pacific and Atlantic oceans.
```

```
class Solution {
    public List<List<Integer>> pacificAtlantic(int[][] heights) {
        List<List<Integer>> list = new ArrayList();

        int rows=heights.length;
        int cols=heights[0].length;

        boolean[][] paci = new boolean[rows][cols];
        boolean[][] atla = new boolean[rows][cols];

        for(int i=0; i<rows; i++){
            DFSMarking(i, 0, rows, cols, paci, heights[i][0], heights);
            DFSMarking(i, cols-1, rows, cols, atla, heights[i][cols-1], heights);
        }
        for(int i=0; i<cols; i++){
            DFSMarking(0, i, rows, cols, paci, heights[0][i], heights);
            DFSMarking(rows-1, i, rows, cols, atla, heights[rows-1][i], heights);
        }

        for(int i=0; i<rows; i++){
            for(int j=0; j<cols; j++){
                if(paci[i][j] && atla[i][j]){
                    list.add(Arrays.asList(i,j));
                }
            }
        }
        return list;

    }
    
    public void DFSMarking(int row, int col, int rows, int cols, boolean[][] island, int height, int [][] heights){
        if(
            row<0 || row>=rows ||
            col<0 || col>=cols ||
            island[row][col] ||
            height>heights[row][col]
        ) return;
        island[row][col]=true;
        DFSMarking(row-1, col, rows, cols, island, heights[row][col], heights);
        DFSMarking(row, col+1, rows, cols, island, heights[row][col], heights);
        DFSMarking(row+1, col, rows, cols, island, heights[row][col], heights);
        DFSMarking(row, col-1, rows, cols, island, heights[row][col], heights);
    }
}
```

11. Minimum Window Substring
https://leetcode.com/problems/minimum-window-substring/description/
```
Example 1:
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

Example 2:
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.

Example 3:
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
```
```
class Solution {
    public String minWindow(String s, String t) {
        String output = "";

        int tlen = t.length();

        Map<Character,Integer> tmap = new HashMap();
        for(char c: t.toCharArray()){
            tmap.put(c, tmap.getOrDefault(c,0)+1);
        }

        int start=0;
        for(int end=0; end<s.length(); end++){
            char c = s.charAt(end);
            if(tmap.containsKey(c)){
                if(tmap.get(c)>0){
                    tlen--;
                }
                tmap.put(c, tmap.get(c)-1);
            }
            if(tlen==0){
                while(start<=end){
                    char sc = s.charAt(start);
                    if(tmap.containsKey(sc)){
                        boolean canSlide = tmap.get(sc)<0;
                        if(canSlide){
                            tmap.put(sc, tmap.get(sc)+1);
                            start++;
                        }else{
                            break;
                        }
                    }else{
                        start++;
                    }
                }
                String temp = s.substring(start, end+1);
                if(output == "" || output.length()>temp.length()){
                    output = temp;
                }
            }
        }
        return output;
    }
}
```
