Week 3

1. Invert Binary Tree
https://leetcode.com/problems/invert-binary-tree/description/
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
