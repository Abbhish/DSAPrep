Week 3

Count 9

1. Invert Binary Tree
https://leetcode.com/problems/invert-binary-tree/description/
```
Example 1:
```
![image](https://github.com/user-attachments/assets/cd47fb98-0f41-42d5-9254-82a80df113ba)
```
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]

Example 2:
```
![image](https://github.com/user-attachments/assets/72be08fc-c1d1-4e9e-b3ed-ef0088807475)
```
Input: root = [2,1,3]
Output: [2,3,1]

Example 3:
Input: root = []
Output: []
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
    public TreeNode invertTree(TreeNode root) {
        if(root==null) return null;

        invertTree(root.left);
        invertTree(root.right);

        TreeNode temp = root.left;
        root.left=root.right;
        root.right=temp;

        return root;
    }
}
```

2. Validate Binary Search Tree
https://leetcode.com/problems/validate-binary-search-tree/description/
```
Example 1:
```
![image](https://github.com/user-attachments/assets/22d482b7-1856-45be-8ef0-aad66dec6429)

```
Input: root = [2,1,3]
Output: true

Example 2:
```
![image](https://github.com/user-attachments/assets/c74b6276-18ca-4131-8d9a-a170147376be)

```
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
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
    public boolean isValidBST(TreeNode root) {
        if(root==null) return true;

        Stack<TreeNode> stk = new Stack();
        TreeNode prev=null;
        while(root!=null || !stk.isEmpty()){
            while(root!=null){
                stk.push(root);
                root=root.left;
            }
            root=stk.pop();
            if(prev!=null && prev.val>=root.val) return false;
            prev=root;
            root=root.right;
        }
        return true;
    }
}
```

3. Non-Overlapping Intervals
https://leetcode.com/problems/non-overlapping-intervals/description/
```
Example 1:
Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: [1,3] can be removed and the rest of the intervals are non-overlapping.

Example 2:
Input: intervals = [[1,2],[1,2],[1,2]]
Output: 2
Explanation: You need to remove two [1,2] to make the rest of the intervals non-overlapping.

Example 3:
Input: intervals = [[1,2],[2,3]]
Output: 0
Explanation: You don't need to remove any of the intervals since they're already non-overlapping.
```
```
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        //Same approach is used in max meeting scheduling.
        Arrays.sort(intervals, (a,b)->a[1]-b[1]);
        int possibleMeetingCount=1;
        int totalMeetings = intervals.length;
        int prev=0;
        for(int i=1; i<totalMeetings; i++){
            if(intervals[i][0]>=intervals[prev][1]){
                possibleMeetingCount++;
                prev=i;
            }
        }
        return totalMeetings-possibleMeetingCount;
    }
}
```

4. Contruct Binary Tree From Inorder And Preorder Traversal
https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/
```
Example 1:
```
![image](https://github.com/user-attachments/assets/feacddc6-988a-4e55-afd0-bd19a8a4e625)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]

Example 2:
Input: preorder = [-1], inorder = [-1]
Output: [-1]
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        Map<Integer, Integer> inMap = new TreeMap();
        for(int i=0; i<inorder.length; i++){
            inMap.put(inorder[i], i);
        }
        return construct(preorder, 0, preorder.length-1, inorder, 0, inorder.length-1, inMap);
    }

    public TreeNode construct(int[] preorder, int preStart, int preEnd, int[] inorder, int inStart, int inEnd, Map<Integer, Integer> inMap){
        if(preStart>preEnd || inStart>inEnd) return null;

        int rootVal = preorder[preStart];
        TreeNode root = new TreeNode(rootVal);
        int inRoot = inMap.get(rootVal);
        int leftCount = inRoot-inStart;

        root.left = construct(preorder, preStart+1, preStart+leftCount, inorder, inStart, inRoot-1, inMap);
        root.right = construct(preorder, preStart+leftCount+1, preEnd, inorder, inRoot+1, inEnd, inMap);

        return root;
    }
}
```

5. Top K Frequent Elements
https://leetcode.com/problems/top-k-frequent-elements/description/
```
Example 1:
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Example 2:
Input: nums = [1], k = 1
Output: [1]
```
```
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        int[] res = new int[k];

        Map<Integer, Integer> hm = new HashMap();
        for(int num: nums){
            hm.put(num, hm.getOrDefault(num, 0)+1);
        }

        List<Integer> keyList = new ArrayList(hm.keySet());
        Collections.sort(keyList, new Comparator<Integer>(){
            public int compare(Integer a, Integer b){
                return hm.get(b)-hm.get(a);
            }
        });

        for(int i=0; i<k; i++){
            res[i]=keyList.get(i);
        }
        return res;

    }
}
```

6. Clone Graph
https://leetcode.com/problems/clone-graph/description/
```
Example 1:
```
![image](https://github.com/user-attachments/assets/264ba631-fabf-4f8b-afc6-0f273b04feb1)

```
Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: [[2,4],[1,3],[2,4],[1,3]]
Explanation: There are 4 nodes in the graph.
1st node (val = 1)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
2nd node (val = 2)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).
3rd node (val = 3)'s neighbors are 2nd node (val = 2) and 4th node (val = 4).
4th node (val = 4)'s neighbors are 1st node (val = 1) and 3rd node (val = 3).

Example 2:
```
![image](https://github.com/user-attachments/assets/f5915df4-0e33-4132-be59-b7c46b18f99c)

```
Input: adjList = [[]]
Output: [[]]
Explanation: Note that the input contains one empty list. The graph consists of only one node with val = 1 and it does not have any neighbors.

Example 3:
Input: adjList = []
Output: []
Explanation: This an empty graph, it does not have any nodes.
```
```
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

class Solution {
    public Node cloneGraph(Node node) {
        if(node==null) return null;
        return clone(node, new HashMap<Integer, Node>());
    }
    public Node clone(Node node, Map<Integer, Node> map){
        if(map.containsKey(node.val)){
            return map.get(node.val);
        }
        Node newNode = new Node(node.val);
        map.put(node.val, newNode);

        for(Node nod: node.neighbors){
            newNode.neighbors.add(clone(nod, map));
        }
        return newNode;
    }
}
```

7. Course Schedule
https://leetcode.com/problems/course-schedule/description/
```
Example 1:
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.

Example 2:
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```
```
class Solution {
    List<Integer>[] adj;
    boolean[] visited;
    boolean[] explored;
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        adj = new ArrayList[numCourses];
        visited = new boolean[numCourses];
        explored = new boolean[numCourses];

        for(int i=0; i<numCourses; i++){
            adj[i] = new ArrayList();
        }
        for(int i=0; i<prerequisites.length; i++){
            adj[prerequisites[i][0]].add(prerequisites[i][1]);
        }
        for(int i=0; i<numCourses; i++){
            if(!visited[i]){
                if(isCyclic(i)){
                    return false;
                }
            }
        }
        return true;
    }
    public boolean isCyclic(int i){
        visited[i]=true;
        for(int j: adj[i]){
            if(!visited[j]){
                if(isCyclic(j)){
                    return true;
                }
            }else{
                if(!explored[j]){
                    return true;
                }
            }
        }
        explored[i]=true;
        return false;
    }
}
```

8. Serialize And Deserialize Binary Tree
https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/
```
Example 1:
```
![image](https://github.com/user-attachments/assets/c6d3801a-a3a0-4c81-ae9b-1a5af428dee8)

```
Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]

Example 2:
Input: root = []
Output: []
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
public class Codec {

    // Encodes a tree to a single string.
    // Preorder traversal
    public String serialize(TreeNode root) {
        if(root==null) return "x";
        String leftSerial = serialize(root.left);
        String rightSerial = serialize(root.right);
        return root.val+","+leftSerial+","+rightSerial;
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] serialArr = data.split(",");
        Queue<String> queue = new LinkedList();
        for(String s: serialArr){
            queue.add(s);
        }
        return constructTree(queue);
    }
    public TreeNode constructTree(Queue<String> queue){
        if(queue.isEmpty()) return null;
        String peek = queue.poll();
        if(peek.equals("x")) return null;
        TreeNode root = new TreeNode(Integer.parseInt(peek));
        root.left = constructTree(queue);
        root.right = constructTree(queue);
        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// TreeNode ans = deser.deserialize(ser.serialize(root));
```

9. Binary Tree Maximum Path Sum
https://leetcode.com/problems/binary-tree-maximum-path-sum/description/
```
Example 1:
```
![image](https://github.com/user-attachments/assets/f5c91556-43df-472b-8b07-9819c50361c4)

```
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.

Example 2:
```
![image](https://github.com/user-attachments/assets/b3e0a9be-c9ef-4fd4-97e2-0153d1afa4cf)

```
Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.
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
    int maxSum = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        calMaxSum(root);
        return maxSum;
    }
    public int calMaxSum(TreeNode root){
        if(root==null) return 0;
        int leftSum = Math.max(0, calMaxSum(root.left));
        int rightSum = Math.max(0, calMaxSum(root.right));
        maxSum = Math.max(maxSum, leftSum+rightSum+root.val);
        return Math.max(leftSum, rightSum)+root.val;
    }
}
```
