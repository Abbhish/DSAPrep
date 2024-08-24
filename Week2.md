Week 2

1. Reverse Linked List
https://leetcode.com/problems/reverse-linked-list/description/

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
