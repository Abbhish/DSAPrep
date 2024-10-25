Week 4

1. Subtree of Another Tree
https://leetcode.com/problems/subtree-of-another-tree/description/
```
Example 1:
```
![image](https://github.com/user-attachments/assets/952d87f3-6ebe-49c8-87c4-2d0e440e87c6)
```
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true

Example 2:
```
![image](https://github.com/user-attachments/assets/50d24b3e-188c-4213-a5fc-27906001f071)
```
Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
Output: false
```
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if(root==null) return false;
        if(isSame(root, subRoot)) return true;
        return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
    }
    public boolean isSame(TreeNode root, TreeNode subRoot){
        if(root==null && subRoot==null) return true;
        if(root==null || subRoot==null) return false;
        if(root.val!=subRoot.val) return false;
        return isSame(root.left, subRoot.left) && isSame(root.right, subRoot.right);
    }
}
```

2. Lowest Common Ancestor of a Binary Search Tree.
https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/
```
Example 1:
```
![image](https://github.com/user-attachments/assets/9ae4c683-0c5c-4511-a58a-2071d993c5c8)
```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.

Example 2:
```
![image](https://github.com/user-attachments/assets/9959a336-12af-4536-9457-b0ce445b7d61)
```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

Example 3:
Input: root = [2,1], p = 2, q = 1
Output: 2

```
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {

        if(root==null) return root;
        if(root == p || root == q) return root;

        TreeNode leftLCA = lowestCommonAncestor(root.left, p, q);
        TreeNode rightLCA = lowestCommonAncestor(root.right, p, q);

        if(leftLCA!=null && rightLCA!=null){
            return root;
        }else if(leftLCA!=null){
            return leftLCA;
        }else{
            return rightLCA;
        }
    }
}
```

3. Implement Trie
https://leetcode.com/problems/implement-trie-prefix-tree/description/
```
Example 1:
Input
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output
[null, null, true, false, true, null, true]

Explanation
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
```
```
class Trie {
    Trie[] children;
    boolean isEnd;
    public Trie() {
        children = new Trie[26];
        isEnd=false;
    }
    
    public void insert(String word) {
        Trie node = this;
        for(char ch: word.toCharArray()){
            if(node.children[ch-'a']==null){
                node.children[ch-'a'] = new Trie();
            }
            node = node.children[ch-'a'];
        }
        node.isEnd = true;
    }
    
    public boolean search(String word) {
        Trie node = this;
        for(char ch: word.toCharArray()){
            if(node.children[ch-'a']==null) return false;
            node = node.children[ch-'a'];
        }
        return node.isEnd;
    }
    
    public boolean startsWith(String prefix) {
        Trie node = this;
        for( char ch: prefix.toCharArray()){
            if(node.children[ch-'a']==null) return false;
            node=node.children[ch-'a'];
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

4. Design Add and Search Word Data Structure.
https://leetcode.com/problems/design-add-and-search-words-data-structure/description/
```
Example:
Input
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output
[null,null,null,null,false,true,true,true]

Explanation
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True
```
```
class WordDictionary {
    WordDictionary[] children;
    boolean isEnd;

    public WordDictionary() {
        children = new WordDictionary[26];
        isEnd = false;
    }
    
    public void addWord(String word) {
        WordDictionary node = this;
        for(char ch: word.toCharArray()){
            if(node.children[ch-'a']==null){
                node.children[ch-'a'] = new WordDictionary();
            }
            node = node.children[ch-'a'];
        }
        node.isEnd=true;
    }
    
    public boolean search(String word) {
        WordDictionary node = this;
        for(int i=0; i<word.length(); i++){
            char ch=word.charAt(i);
            if(ch=='.'){
                for(WordDictionary nod: node.children){
                    if(nod!=null && nod.search(word.substring(i+1))) return true;
                }
                return false;
            }
            if(node.children[ch-'a']==null) return false;
            node = node.children[ch-'a'];
        }
        return node.isEnd;
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```

5. Kth Smallest Elemnet in the BST.
https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/
```
Example 1:
```
![image](https://github.com/user-attachments/assets/30387a3b-ac3c-4309-a68f-414aaed2022d)
```
Input: root = [3,1,4,null,2], k = 1
Output: 1

Example 2:
```
![image](https://github.com/user-attachments/assets/3ce87ca4-e3e6-4255-927e-6f7b00929cfe)
```
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
```
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        Stack<TreeNode> stk = new Stack();
        int cnt=0;
        while(root!=null || !stk.isEmpty()){
            while(root!=null){
                stk.push(root);
                root=root.left;
            }
            root=stk.pop();
            cnt++;
            if(cnt==k) break;
            root=root.right;
        }
        return root.val;
    }
}
```

6. Merge K Sorted List
https://leetcode.com/problems/merge-k-sorted-lists/description/
```
Example 1:
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6

Example 2:
Input: lists = []
Output: []

Example 3:
Input: lists = [[]]
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
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists==null || lists.length==0) return null;
        PriorityQueue<ListNode> pq = new PriorityQueue<ListNode>(lists.length, (a,b)->a.val-b.val);
        ListNode head = new ListNode(0);
        ListNode tail = head;
        for(ListNode node: lists){
            if(node!=null){
                pq.add(node);
            }
        }
        while(!pq.isEmpty()){
            tail.next=pq.poll();
            tail=tail.next;
            if(tail.next!=null){
                pq.add(tail.next);
            }
        }
        return head.next;
    }
}
```

7. Find Median From Data Stream
https://leetcode.com/problems/find-median-from-data-stream/description/
```
Example 1:
Input
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
Output
[null, null, null, 1.5, null, 2.0]

Explanation
MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1);    // arr = [1]
medianFinder.addNum(2);    // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3);    // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0
```
```
class MedianFinder {
    PriorityQueue<Integer> maxHeap;
    PriorityQueue<Integer> minHeap;
    public MedianFinder() {
        maxHeap = new PriorityQueue<Integer>(Collections.reverseOrder());
        minHeap = new PriorityQueue<Integer>();
    }
    
    public void addNum(int num) {
        if(maxHeap.isEmpty() || maxHeap.peek()>=num){
            maxHeap.add(num);
        }else{
            minHeap.add(num);
        }
        if(maxHeap.size()>minHeap.size()+1){
            minHeap.add(maxHeap.poll());
        }else if(maxHeap.size()<minHeap.size()){
            maxHeap.add(minHeap.poll());
        }
    }
    
    public double findMedian() {
        if(maxHeap.size()==minHeap.size()){
            return (maxHeap.peek()+minHeap.peek())/2.0;
        }
        return maxHeap.peek();
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

8. Insert Interval
https://leetcode.com/problems/insert-interval/
```
Example 1:
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]

Example 2:
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

```
```
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> list = new ArrayList();
        for(int[] in: intervals){
            if(in[1]<newInterval[0]){
                list.add(in);
            }else if(newInterval[1]<in[0]){
                list.add(newInterval);
                newInterval=in;
            }else{
                newInterval[0] = Math.min(in[0], newInterval[0]);
                newInterval[1] = Math.max(in[1], newInterval[1]);
            }
        }
        list.add(newInterval);
        return list.toArray(new int[list.size()][]);
    }
}
```

9. Longest Consecutive Subsequence
https://leetcode.com/problems/longest-consecutive-sequence/description/
```
Example 1:
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Example 2:
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```
```
class Solution {
    public int longestConsecutive(int[] nums) {
        if(nums.length==0) return 0;
        HashMap<Integer, Boolean> hm = new HashMap();
        int max = 1;
        for(int num: nums){
            hm.put(num, true);
        }
        for(int num: nums){
            if(hm.containsKey(num-1)){
                hm.put(num, false);
            }
        }
        for(int num: hm.keySet()){
            if(hm.get(num)==true){
                max= Math.max(max, findLength(hm, num));
            }
        }
        return max;
    }
    public int findLength(Map<Integer, Boolean> hm, int num){
        int cnt=0;
        while(hm.containsKey(num)){
            cnt++;
            num++;
        }
        return cnt;
    }
}
```

10. Word Search II
https://leetcode.com/problems/word-search-ii/description/
```
Example 1:
```
![image](https://github.com/user-attachments/assets/708b713c-8aa5-445d-bc3f-24a5a9e7cdba)
```
Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]

Example 2:
```
![image](https://github.com/user-attachments/assets/3611c2bb-0416-4e16-9f09-9bd658a72fc4)
```
Input: board = [["a","b"],["c","d"]], words = ["abcb"]
Output: []
```
```
class Solution {
    class Trie {
        Trie[] child = new Trie[26];
        boolean isEnd = false;
    }
    Trie root = new Trie();
    boolean[][] flag;
    public List<String> findWords(char[][] board, String[] words) {
        Set<String> ans = new HashSet();
        flag = new boolean[board.length][board[0].length];

        for(String word: words){
            addToTrie(word);
        }
        for(int i=0; i<board.length; i++){
            for(int j=0; j<board[0].length; j++){
                if(root.child[board[i][j]-'a']!=null){
                    DFS(root, i, j, board, "", ans);
                }
            }
        }
        return new ArrayList<String>(ans);
    }
    public void addToTrie(String word){
        Trie node = root;
        for(char ch: word.toCharArray()){
            if(node.child[ch-'a']==null){
                node.child[ch-'a']= new Trie();
            }
            node = node.child[ch-'a'];
        }
        node.isEnd=true;
    }
    public void DFS(Trie node, int i, int j, char[][] board, String word, Set<String> ans){
        if(
            i<0 || i>=board.length ||
            j<0 || j>=board[0].length ||
            flag[i][j] ||
            node.child[board[i][j]-'a']==null
        ) return;
        flag[i][j]=true;
        char ch = board[i][j];
        node = node.child[ch-'a'];
        if(node.isEnd){
            ans.add(word+ch);
        }
        DFS(node, i-1, j, board, word+ch, ans);
        DFS(node, i, j+1, board, word+ch, ans);
        DFS(node, i+1, j, board, word+ch, ans);
        DFS(node, i, j-1, board, word+ch, ans);
        flag[i][j]=false;
    }
}
```
