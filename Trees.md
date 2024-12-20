Trees

Count - 10

1. Diameter of Binary Tree

https://www.naukri.com/code360/problems/920552?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Example :
Input: Consider the given binary tree:
```
![image](https://github.com/user-attachments/assets/21740734-0558-4efc-86ea-6aa5b4aee630)
```
Output: 6

Explanation:
Nodes in the diameter are highlighted. The length of the diameter, i.e., the path length, is 6.
```
```
/*************************************************************

 Following is the Binary Tree Node structure:

 class TreeNode<T> {
     public T data;
     public BinaryTreeNode<T> left;
     public BinaryTreeNode<T> right;

     TreeNode(T data) {
         this.data = data;
         left = null;
         right = null;
     }
 }

 *************************************************************/

public class Solution {
    static int diameter;
    public static int diameterOfBinaryTree(TreeNode<Integer> root) {
        diameter=0;
        findHeight(root);
        return diameter;
    }
    public static int findHeight(TreeNode<Integer> root){
        if(root==null) return 0;

        int leftHeight = findHeight(root.left);
        int rightHeight = findHeight(root.right);
        diameter = Math.max(diameter, leftHeight+rightHeight);
        return 1+Math.max(leftHeight,rightHeight);
    }
}
```

2. LCA of Binary Tree

https://www.naukri.com/code360/problems/920541?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
![image](https://github.com/user-attachments/assets/0a597138-28cd-41dd-803e-2f7866129d3f)
```
LCA of ‘X’ and ‘Y’ is highlighted in yellow colour.
```
```
/************************************************************

 Following is the TreeNode class structure

 class TreeNode<T>
 {
     T data;
     TreeNode<T> left;
     TreeNode<T> right;

     TreeNode(T data)
     {
         this.data = data;
         left = null;
         right = null;
     }
 };

 ************************************************************/

public class Solution {
    public static int lowestCommonAncestor(TreeNode<Integer> root, int x, int y) {
        if(root==null){
            return -1;
        }
        if(root.data==x || root.data==y){
            return root.data;
        }

        int left = lowestCommonAncestor(root.left, x, y);
        int right = lowestCommonAncestor(root.right, x, y);

        if(left!=-1 && right!=-1){
            return root.data;
        }else if(left!=-1){
            return left;
        }else{
            return right;
        }
    }
}

```

3. Level order traversal

https://www.naukri.com/code360/problems/796002?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
![image](https://github.com/user-attachments/assets/b37503c3-9316-4f88-b7f2-f3f217f311d4)
```
The level order traversal will be {1,2,3,4,5,6,7}.
```
```
import java.util.* ;
import java.io.*; 
/*

	Following is the structure used to represent the Binary Tree Node

	class BinaryTreeNode<T> {
		T val;
		BinaryTreeNode<T> left;
		BinaryTreeNode<T> right;

		public BinaryTreeNode(T val) {
			this.val = val;
			this.left = null;
			this.right = null;
		}
	}

*/

public class Solution {

  public static ArrayList<Integer> getLevelOrder(BinaryTreeNode root) {
	  Queue<BinaryTreeNode> q = new LinkedList<>();
	  ArrayList<Integer> list = new ArrayList<>();

	  if(root==null){
		  return list;
	  }
	  q.offer(root);
	  while(!q.isEmpty()){
		  if(q.peek().left!=null){
			  q.offer(q.peek().left);
		  }
		  if(q.peek().right!=null){
			  q.offer(q.peek().right);
		  }
		  list.add(q.poll().val);
	  }
	  return list;
  }

}
```

4. Binary Tree Zig-Zag Traversal

https://www.naukri.com/code360/problems/1062662?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
For the given binary tree
```
![image](https://github.com/user-attachments/assets/10e30ffe-fd35-4bfc-8595-79b81adbf803)
```
The zigzag  traversal is [1, 4, 3, 5, 2, 7, 6]
```
```
import java.util.* ;
import java.io.*; 
/*
	Following is the class used to represent the object/node of the Binary Tree

	class BinaryTreeNode<T> {
	    T data;
	    BinaryTreeNode<T> left;
	    BinaryTreeNode<T> right;

	    public BinaryTreeNode(T data) {
	        this.data = data;
	    }
	}
*/

public class Solution {
	public static List<Integer> zigZagTraversal(BinaryTreeNode<Integer> root) {
		Queue<BinaryTreeNode> queue = new LinkedList<>();
		List<Integer> list = new ArrayList<>();

		if(root==null){
			return list;
		}
		queue.offer(root);
		boolean lToR = true;

		while(!queue.isEmpty()){
			int n = queue.size();
			List<Integer> subList = new ArrayList<>();
			for(int i=0; i<n; i++){
				BinaryTreeNode<Integer> curr  = queue.poll();

				if(curr.left!=null){
					queue.offer(curr.left);
				}
				if(curr.right!=null){
					queue.offer(curr.right);
				}

				if(lToR){
					subList.add(curr.data);
				}else{
					subList.add(0, curr.data);
				}				
			}
			lToR=!lToR;
			list.addAll(subList);
		}
		return list;
	}
}
```

5. Left View of Binary Tree

https://www.naukri.com/code360/problems/920519?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
![image](https://github.com/user-attachments/assets/fe64ea28-69f4-4c46-befd-90c51896fe87)
```
The left view of the above binary tree is  {5, 7, 14, 25}.
```
```
import java.util.* ;
import java.io.*; 
/************************************************************

    Following is the TreeNode class structure

    class TreeNode<T> 
    {
       public:
        T data;
        TreeNode<T> left;
        TreeNode<T> right;

        TreeNode(T data) 
        {
            this.data = data;
            left = null;
            right = null;
        }
    };

************************************************************/

public class Solution 
{
    public static ArrayList<Integer> getLeftView(TreeNode<Integer> root) 
    {
        Queue<TreeNode<Integer>> queue = new LinkedList<>();
        ArrayList<Integer> list = new ArrayList<>();

        if(root==null){
            return list;
        }

        queue.offer(root);

        while(!queue.isEmpty()){
            int n = queue.size();
            int leftMost = -1;
            for(int i=0; i<n; i++){
                TreeNode<Integer> curr = queue.poll();
                if(curr.left!=null) queue.offer(curr.left);
                if(curr.right!=null) queue.offer(curr.right);

                if(i==0) leftMost = curr.data;
            }
            list.add(leftMost);
        }
        return list;
    }
}
```

6. Top View of Binary Tree

https://www.naukri.com/code360/problems/799401?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Example :
Input: Let the binary tree be:
```
![image](https://github.com/user-attachments/assets/799dc656-8085-4597-82b7-3f5095f9e1e5)
```
Output: [10, 4, 2, 1, 3, 6]
```
```
/*********************************************

 Following is the TreeNode class structure

 class TreeNode {
     int data;
     TreeNode left;
     TreeNode right;

     TreeNode(int data) {
         this.data = data;
         this.left = null;
         this.right = null;
     }
 }

 *********************************************/

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;
import java.util.Queue;
import java.util.TreeMap;

class Pair {
    TreeNode node;
    int hd;

    Pair(TreeNode node, int hd){
        this.node = node;
        this.hd = hd;//horizontal distance
    }
}
public class Solution {
    public static List<Integer> getTopView(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        if(root==null) return list;

        Queue<Pair> queue = new LinkedList<>();
        Map<Integer, Integer> map = new TreeMap<>();

        queue.offer(new Pair(root, 0));

        while(!queue.isEmpty()){
            Pair currPair = queue.poll();
            TreeNode temp = currPair.node;
            int hd = currPair.hd;

            if(map.get(hd)==null){
                map.put(hd, temp.data);
            }
            if(temp.left!=null){
                queue.add(new Pair(temp.left, hd-1));
            }
            if(temp.right!=null){
                queue.add(new Pair(temp.right, hd+1));
            }
        }
        for(int data: map.values()){
            list.add(data);
        }
        return list;
    }
}
```

7. Construct Binary Tree From Inorder and Preorder Traversal

https://www.naukri.com/code360/problems/920539?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
For example :
For the preorder sequence = [1, 2, 4, 7, 3] and the inorder sequence = [4, 2, 7, 1, 3], we get the following binary tree.
```
![image](https://github.com/user-attachments/assets/4a8bcfe3-37b6-4266-90b2-052ef933a938)

```
import java.util.HashMap;

/*********************************************************

 Following is the TreeNode structure:

 class TreeNode {
     int data;
     TreeNode left;
     TreeNode right;
     TreeNode() {
         this.data = 0;
         this.left = null;
         this.right = null;
     }
     TreeNode(int data) {
         this.data = data;
         this.left = null;
         this.right = null;
     }
     TreeNode(int data, TreeNode left, TreeNode right) {
         this.data = data;
         this.left = left;
         this.right = right;
     }
 };
 ********************************************************/

public class Solution {
    public static TreeNode buildBinaryTree(int[] inorder, int[] preorder) {
        HashMap<Integer, Integer> inMap = new HashMap<>();
        for(int i=0; i<inorder.length; i++){
            inMap.put(inorder[i], i);
        }
        return contructTree(preorder, 0, preorder.length-1, inorder, 0 , inorder.length-1, inMap);
    }

    public static TreeNode contructTree(int[] preorder, int preStart, int preEnd, int[] inorder, int inStart, int inEnd, HashMap<Integer, Integer> inMap){
        if(preStart>preEnd || inStart>inEnd){
            return null;
        }

        TreeNode root = new TreeNode(preorder[preStart]);
        int inRoot = inMap.get(root.data);
        int range = inRoot - inStart;

        root.left = contructTree(preorder, preStart+1, preStart+range, inorder, inStart , inRoot-1, inMap);
        root.right = contructTree(preorder, preStart+range+1, preEnd, inorder, inRoot+1, inEnd, inMap);

        return root;
    }
}
```

8. Vertical Order Traversal

https://www.naukri.com/code360/problems/vertical-order-traversal_920533?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube&leftPanelTabValue=PROBLEM
```
For example:
For the binary tree in the image below.
```
![image](https://github.com/user-attachments/assets/e84802f5-e3fd-4a84-81d0-4631eb354c4d)

```
The vertical order traversal will be {2, 7, 5, 2, 6, 5, 11, 4, 9}.
```
```
import java.util.* ;
import java.io.*; 
/************************************************************

    Following is the TreeNode class structure

    class TreeNode<T> 
    {
       public:
        T data;
        TreeNode<T> left;
        TreeNode<T> right;

        TreeNode(T data) 
        {
            this.data = data;
            left = null;
            right = null;
        }
    };

************************************************************/

import java.util.ArrayList;

class Tuple {
    TreeNode<Integer> node;
    int x;
    int y;

    Tuple(TreeNode<Integer> node, int x, int y){
        this.node = node;
        this.x=x;
        this.y=y;

    }
}
public class Solution 
{
    public static ArrayList<Integer> verticalOrderTraversal(TreeNode<Integer> root) 
    {
        TreeMap<Integer, TreeMap<Integer, PriorityQueue<Integer>>> map = new TreeMap<>();
        Queue<Tuple> queue = new LinkedList<>();

        queue.offer(new Tuple(root, 0, 0));

        while (!queue.isEmpty()) {
            Tuple tuple = queue.remove();
            TreeNode<Integer> node = tuple.node;
            int x = tuple.x;
            int y = tuple.y;

            if (!map.containsKey(x)) {
                map.put(x, new TreeMap<>());
            }
            if (!map.get(x).containsKey(y)) {
                map.get(x).put(y, new PriorityQueue<>());
            }
            map.get(x).get(y).add(node.data);

            if (node.left != null) queue.offer(new Tuple(node.left, x - 1, y + 1));
            if (node.right != null) queue.offer(new Tuple(node.right, x + 1, y + 1));
        }
        System.out.println(map);

        ArrayList<Integer> list = new ArrayList<>();
        for (TreeMap<Integer, PriorityQueue<Integer>> m : map.values()) {
            for (PriorityQueue<Integer> q : m.values()) {
                while (!q.isEmpty()) {
                    list.add(q.poll());
                }
            }
        }
        return list;
    }
}
```

9. Inorder Travsersal

https://www.naukri.com/code360/problems/inorder-traversal_3839605?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube&leftPanelTabValue=PROBLEM
```
For example :
For the given binary tree:
```
![image](https://github.com/user-attachments/assets/e0ef9ee5-ef87-417f-af33-cc8f34b415ed)

```
The Inorder traversal will be [5, 3, 2, 1, 7, 4, 6].
```
```
/*
    Following is the TreeNode class structure:

    public class TreeNode {
        int data;
        TreeNode left;
        TreeNode right;
        TreeNode() {
            this.data = 0;
            this.left = null;
            this.right = null;
        }
        TreeNode(int val) {
            this.data = val;
            this.left = null;
            this.right = null;
        }
        TreeNode(int val, TreeNode left, TreeNode right) {
            this.data = val;
            this.left = left;
            this.right = right;
        }
    };
*/

import java.util.ArrayList;
import java.util.List;

public class Solution {
    static List<Integer> list = new ArrayList<>();
    public static List< Integer > getInOrderTraversal(TreeNode root) {

        if(root!=null){
            getInOrderTraversal(root.left);
            list.add(root.data);
            getInOrderTraversal(root.right);
        }
        return list;
    }
}
```

10. LCA of Two Nodes in BST.

https://www.naukri.com/code360/problems/981280?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
For example:
'P' = 1, 'Q' = 3
tree = 2 1 4 -1 -1 3 -1 -1 -1,

The BST corresponding will be- 
```
![image](https://github.com/user-attachments/assets/76a57fc8-92ef-48da-b8f5-49f664a061fe)
```
Here, we can clearly see that LCA of node 1 and node 3 is 2.
```
```
/*********************************************************

 Following is the TreeNode structure:

 class TreeNode {
     int data;
     TreeNode left;
     TreeNode right;
     TreeNode() {
         this.data = 0;
         this.left = null;
         this.right = null;
     }
     TreeNode(int data) {
         this.data = data;
         this.left = null;
         this.right = null;
     }
     TreeNode(int data, TreeNode left, TreeNode right) {
         this.data = data;
         this.left = left;
         this.right = right;
     }
 };
 ********************************************************/

public class Solution {
    public static TreeNode LCAinaBST(TreeNode root, TreeNode p, TreeNode q) {
        if(root==null){
            return null;
        }
        if(root.data==p.data || root.data==q.data){
            return root;
        }
        TreeNode left = LCAinaBST(root.left, p, q);
        TreeNode right = LCAinaBST(root.right, p, q);

        if(left!=null && right!=null){
            return root;
        }else if(left!=null){
            return left;
        }else{
            return right;
        }
    }
}
```
