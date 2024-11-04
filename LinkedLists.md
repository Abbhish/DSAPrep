Linked Lists

1. Reverse Linked List

https://www.naukri.com/code360/problems/reverse-the-singly-linked-list_799897?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
import java.io.*;
import java.util.* ;

/*
	Following is the structure of the Singly Linked List.	
	class LinkedListNode<T> 
    {
    	T data;
    	LinkedListNode<T> next;
    	public LinkedListNode(T data) 
        {
        	this.data = data;
    	}
	}

*/
public class Solution 
{
    public static LinkedListNode<Integer> reverseLinkedList(LinkedListNode<Integer> head) 
    {
        LinkedListNode curr = head;
		LinkedListNode prev = null;
		while(curr!=null){
			LinkedListNode next  = curr.next;
			curr.next = prev;
			prev= curr;
			curr=next;
		}
		return prev;
    }
}
```

2. Middle of Linked List

https://www.naukri.com/code360/problems/middle-of-linked-list_973250?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
/****************************************************************

 Following is the class structure of the Node class:

 class Node {
     public int data;
     public Node next;

     Node()
     {
         this.data = 0;
         this.next = null;
     }
     Node(int data)
     {
         this.data = data;
         this.next = null;
     }
     Node(int data, Node next)
     {
         this.data = data;
         this.next = next;
     }
 }

 *****************************************************************/

public class Solution
{
    public static Node findMiddle(Node head)
    {
        Node fast = head;
        Node slow = head;
        
        while(fast!=null && fast.next!=null){
            fast=fast.next.next;
            slow=slow.next;
        }
        return slow;
    }
}
```

3. Merge Sort
https://www.naukri.com/code360/problems/merge-sort_920442?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube

```
public class Solution {
	public static void mergeSort(int[] arr, int n) {
		divide(arr, 0, n-1);
	}

	public static void divide(int[] arr, int si, int ei){

		if(si>=ei) return;

		int mid = si+(ei-si)/2;

		divide(arr, si, mid);
		divide(arr, mid+1, ei);

		conquer(arr, si, mid, ei);

	}
	public static void conquer(int[] arr, int si, int mid, int ei){
		int idx1=si;
		int idx2=mid+1;
		int x=0;
		int[] merged = new int[ei-si+1];

		while(idx1<=mid && idx2<=ei){
			if(arr[idx1]<=arr[idx2]){
				merged[x++]=arr[idx1++];
			}else{
				merged[x++]=arr[idx2++];
			}
		}
		while(idx1<=mid){
			merged[x++]=arr[idx1++];
		}
		while(idx2<=ei){
			merged[x++]=arr[idx2++];
		}

		for(int i=0, j=si; i<merged.length; i++, j++){
			arr[j]=merged[i];
		}
	}
}
```

4. Add Two Numbers

https://www.naukri.com/code360/problems/add-two-numbers-as-linked-lists_1170520?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
import java.util.* ;
import java.io.*; 
/****************************************************************

    Following is the class structure of the Node class:

    class LinkedListNode {
        int data;
        LinkedListNode next;
        
        public LinkedListNode(int data) {
            this.data = data;
        }
    }

*****************************************************************/


public class Solution {
    static LinkedListNode addTwoNumbers(LinkedListNode head1, LinkedListNode head2) {
        LinkedListNode ans = new LinkedListNode(0);
        LinkedListNode head = ans;
        int carry = 0;
        while(head1!=null || head2!=null || carry!=0){
            int sum=0;
            if(head1!=null){
                sum= sum+head1.data;
                head1=head1.next;
            }
            if(head2!=null){
                sum=sum+head2.data;
                head2=head2.next;
            }
            sum=sum+carry;
            carry=sum/10;
            sum=sum%10;
            LinkedListNode temp = new LinkedListNode(sum);
            head.next=temp;
            head=head.next;
        }
        return ans.next;
    }
}
```

5. Insertion Sort

https://www.naukri.com/code360/problems/insertion-sort-in-linked-list_1090544?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
import java.util.* ;
import java.io.*; 
/****************************************************************
    Following is the Linked List node structure

    class Node
    {
    public:
        int data;
        Node *next;
        Node(int data)
        {
            this->data = data;
            this->next = NULL;
        }
    };

*****************************************************************/

public class Solution
{
public static Node insertionSortLL(Node head)
    {
        Node start = new Node(0);
        start.next=head;
        Node prev = start;
        Node curr = head;
        
        while(curr!=null){
            if(curr.next!=null && curr.next.data<curr.data){
                while(prev.next.data<curr.next.data){
                    prev=prev.next;
                }
                Node temp = prev.next;
                prev.next = curr.next;
                curr.next = curr.next.next;
                prev.next.next = temp;
                prev = start;
            }else{
                curr = curr.next;
            }
        }
        return start.next;

    }
}

```

6. Delete Kth Node From End

https://www.naukri.com/code360/problems/delete-kth-node-from-end-in-linked-list_799912?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
/****************************************************************

 Following is the class structure of the Node class:

 class Node {
     public int data;
     public Node next;
     public Node prev;

     Node()
     {
         this.data = 0;
         this.next = null;
         this.prev = null;
     }

     Node(int data)
     {
         this.data = data;
         this.next = null;
         this.prev = null;
     }

     Node(int data, Node next)
     {
         this.data = data;
         this.next = next;
         this.prev = next;
     }
 };

 *****************************************************************/

public class Solution
{
    public static Node removeKthNode(Node head, int K)
    {
        Node start = new Node(0);
        start.next = head;
        Node curr = start;
        Node ahead = start;

        for(int i=0; i<K; i++){
            ahead=ahead.next;
        }
        while(ahead.next!=null){
            ahead=ahead.next;
            curr=curr.next;
        }
        curr.next=curr.next.next;
        return start.next;
    }
}
```

7. Detect and Remove Loop

https://www.naukri.com/code360/problems/interview-shuriken-42-detect-and-remove-loop_241049?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
/*****************************************************
  
  Following is the structure of Node.
  public static class Node {
    
    int data;
    Node next;

    Node(int data) {
      this . data = data;
      this . next = null;
    }
  }

*****************************************************/

import java.util.ArrayList;

public class Solution {
  public static Node removeLoop(Node head) {
    Node fast = head;
    Node slow = head;

    while(fast!=null && fast.next!=null){
      slow=slow.next;
      fast=fast.next.next;
      if(slow == fast){
        break;
      }
    }
    if(slow!=fast){
      return head;
    }
    slow=head;
    while(slow.next!=fast.next){
      slow=slow.next;
      fast=fast.next;
    }
    fast.next=null;
    return head;
  }
}
```

8. Swap Nodes in Pair

https://www.naukri.com/code360/problems/pair-swap_759396?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
import java.util.* ;
import java.io.*; 
/****************************************************************

    Following is the class structure of the Node class:

	class Node {
		int data;
		Node next;

		Node(int data) {
		this.data = data;
		this.next = null;
	   }
   }

*****************************************************************/

public class Solution {
	public static Node pairsSwap(Node head) {
		Node start = new Node(0);
		start.next=head;
		Node prev=start;
		Node curr=start;
		Node ahead=start.next;

		while(curr!=null && curr.next!=null && ahead!=null && ahead.next!=null){
			curr=curr.next;
			ahead= ahead.next;

			prev.next=ahead;
			curr.next=ahead.next;
			ahead.next=curr;

			prev=prev.next.next;
			ahead=ahead.next.next;
		}
		return start.next;
	}
}
```

9. Append Nodes

https://www.naukri.com/code360/problems/append-nodes_763407?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
import java.util.* ;
import java.io.*; 
/****************************************************************

    Following is the class structure of the Node class:

    class Node<Integer>
    {
        int data;
        Node<Integer> next;

        public Node(int data)
        {
            this.data = data;
            this.next = null;
        }
    }

 *****************************************************************/
public class Solution {

    public static Node<Integer> addNodes(Node<Integer> head, int n, int m) {
        Node curr = new Node(0);
        curr.next=head;

        while(curr!=null && curr.next!=null){
            for(int i=0; i<m; i++){
                if(curr.next!=null){
                    curr=curr.next;
                }else{
                    return head;
                }
            }
            int sum=0;
            for(int i=0; i<n; i++){
                if(curr.next!=null){
                    curr=curr.next;
                    sum=sum+curr.data;
                }else{
                    if(sum>0){
                        Node newNode = new Node(sum);
                        newNode.next = curr.next;
                        curr.next=newNode;
                        return head;
                    }else{
                        return head;
                    }
                }
            }
            Node newNode = new Node(sum);
            newNode.next=curr.next;
            curr.next=newNode;
            curr=curr.next;
        }
        return head;

    }
}
```

10. Segregate Odd Even
https://www.naukri.com/code360/problems/segregate-odd-even_920524?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
public class Solution {
	public static Node segregateOddEven(Node head) {
		Node oddHead = new Node(-1), oddTail = oddHead;
		Node evenHead = new Node(-1), evenTail = evenHead;
		Node curr = head, temp;

		while(curr!=null){
			temp = curr;
			curr=curr.next;
			temp.next=null;
			if(temp.data%2!=0){
				oddTail.next = temp;
				oddTail = temp;
			}else{
				evenTail.next = temp;
				evenTail = temp;
			}
		}
		oddTail.next = evenHead.next;
		return oddHead.next;
	}
}
```
