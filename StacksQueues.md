Stacks & Queues

1.  Stack Implementation Using Array

https://www.naukri.com/code360/problems/stack-implementation-using-array_3210209?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
public class Solution{
    static class Stack {
        int[] arr;
        int top;
        int cap;
        Stack(int capacity) {
            arr = new int[capacity];
            top=-1;
            cap=capacity;
        }
        public void push(int num) {
            if(top<cap-1){
                top++;
                arr[top]=num;
            }
        }
        public int pop() {
            if(top>-1){
                int popped = arr[top];
                top--;
                return popped;
            }else{
                return -1;
            }
        }
        public int top() {
            return top>-1?arr[top]:-1;
        }
        public int isEmpty() {
            return top==-1?1:0;
        }
        public int isFull() {
            return top==cap-1?1:0;
        }
    }
}
```

2.  Implement Stack With Linked List

https://www.naukri.com/code360/problems/implement-stack-with-linked-list_630475?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
/****************************************************************

 Following is the class structure of the Node class:

 static class Node
 {
     int data;
     Node next;
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
 };


 *****************************************************************/
public class Solution {
    static class Stack {
        Node top;
        int size;
        Stack()
        {
            top = null;
            size = 0; 
        }

        int getSize()
        {
            return size;
        }

        boolean isEmpty()
        {
            return size==0;
        }

        void push(int data)
        {
            Node node = new Node(data);
            node.next = top;
            top = node;
            size++;
        }

        void pop()
        {
            if(top!=null){
               top = top.next;
                size--; 
            }
            
        }

        int getTop()
        {
            return top!=null?top.data:-1;
        }
    }
}

```

3. Queue Implementation using Array

https://www.naukri.com/code360/problems/2099908?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube&leftPanelTabValue=PROBLEM
```
import java.util.* ;
import java.io.*; 
public class Queue {
    int[] arr;
    int start;
    int end;
    int currSize;
     int maxSize;
    Queue() {
        arr = new int[1000];
        start = -1;
        end = -1;
        currSize = 0;
        maxSize = 1000;
    }

    /*----------------- Public Functions of Queue -----------------*/

    boolean isEmpty() {
        return currSize == 0 ? true : false;
    }

    void enqueue(int data) {
        if(currSize!=maxSize){
            if(currSize == 0){
            start++;
            end++;
            }else{
                end=(end+1)%maxSize;
            }
            arr[end] = data;
            currSize++;
        }
    }

    int dequeue() {
        if(currSize>0){
            int popped = arr[start];
            if(currSize==1){
                start=-1;
                end=-1;
            }else{
                start=(start+1)%maxSize;
            }
            currSize--;
            return popped;
        }else{
            return -1;
        }
    }

    int front() {
        return currSize>0?arr[start]:-1;
    }

}
```

4. Queue implementation using LinkedList

https://www.naukri.com/code360/problems/2099908?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube&leftPanelTabValue=PROBLEM
```
import java.util.* ;
import java.io.*; 

class Node { 
    Node next;
    int data;

    Node(int data){
        this.next = null;
        this.data = data;
    }
}
public class Queue {
    Node start;
    Node end;
    int size;
    Queue() {
        start = null;
        end = null;
        size = 0;
    }

    /*----------------- Public Functions of Queue -----------------*/

    boolean isEmpty() {
        return size == 0;
    }

    void enqueue(int data) {
        Node node = new Node(data);
        if(size==0){
            start = node;
            end = node;
        }else{
            end.next=node;
            end=node;
        }
        size++;
    }

    int dequeue() {
        if(size>0){
            int dequeued = start.data;
            size--;
            start=start.next;
            if(size==0){
                end = start;
            }
            return dequeued;
        }else{
            return-1;
        }
    }

    int front() {
        return size>0?start.data:-1;
    }

}
```

5. Queue using two Stacks

https://www.naukri.com/code360/problems/queue-using-two-stacks_1170062?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
import java.util.* ;
import java.io.*; 
class Queue {
	// Stacks to be used in the operations.
	Stack<Integer> stk1, stk2;

	public Queue() {
		stk1 = new Stack<>();
		stk2 = new Stack<>();
	}

	// Enqueues 'X' into the queue. Returns true after enqueuing.
	public boolean enqueue(int x) {
		while(!stk1.isEmpty()){
			stk2.push(stk1.pop());
		}
		stk1.push(x);
		while(!stk2.isEmpty()){
			stk1.push(stk2.pop());
		}
		return true;
	}
	/*
	   Dequeues top element from queue. Returns -1 if the queue is empty, 
	   otherwise returns the popped element.
	*/
	public int dequeue() {
		return stk1.isEmpty()?-1:stk1.pop();
	}
};
```

6. Stack using Queue

https://www.naukri.com/code360/problems/stack-using-queue_795152?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
import java.util.LinkedList;
import java.util.Queue;

public class Solution{
    static class Stack {
        // Define the data members.
        Queue<Integer> q1, q2;
        public Stack() {
            q1 = new LinkedList<>();
            q2 = new LinkedList<>();
        }

        /*----------------- Public Functions of Stack -----------------*/

        public int getSize() {
            return q1.size();
        }

        public boolean isEmpty() {
            return q1.isEmpty();
        }

        public void push(int element) {
            while(!q1.isEmpty()){
                q2.add(q1.poll());
            }
            q1.add(element);
            while(!q2.isEmpty()){
                q1.add(q2.poll());
            }
        }

        public int pop() {
            return q1.isEmpty()?-1:q1.poll();
        }

        public int top() {
            return q1.isEmpty()?-1:q1.peek();
        }
    }
}
```

7. Min Stack

https://www.naukri.com/code360/problems/min-stack_3843991?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
import java.util.* ;
import java.io.*; 

class Pair {
    int x;
    int y;

    Pair(int x, int y){
        this.x=x;
        this.y=y;
    }
}
public class Solution {
    static class MinStack {

        Stack<Pair> stk;
        MinStack() {
            stk = new Stack<>();
        }

        // Function to add another element equal to num at the top of stack.
        void push(int num) {
            int min;
            if(stk.isEmpty()){
                min = num;
            }else{
                min = Math.min(num, stk.peek().y);
            }
            stk.push(new Pair(num, min));
        }

        // Function to remove the top element of the stack.
        int pop() {
            if(stk.isEmpty()){
                return -1;
            }else{
                return stk.pop().x;
            }
        }

        // Function to return the top element of stack if it is present. Otherwise
        // return -1.
        int top() {
            if(stk.isEmpty()){
                return -1;
            }else{
                return stk.peek().x;
            }
        }

        // Function to return minimum element of stack if it is present. Otherwise
        // return -1.
        int getMin() {
            if(stk.isEmpty()){
                return -1;
            }else{
                return stk.peek().y;
            }
        }
    }
}
```

8. Next Greater Element

https://www.naukri.com/code360/problems/799354?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
1
4
1 2 4 3
Sample Output 1 :
2 4 -1 -1
Sample Input 2 :
1
4
9 3 6 5
Sample Output 2 :
-1 6 -1 -1
```
```
import java.util.* ;
import java.io.*; 

public class Solution {
	
	public static int[] nextGreater(int[] arr, int n) {

		Stack<Integer> stk = new Stack<>();
		stk.push(-1);

		for(int i=n-1; i>=0; i--){
			int elem = arr[i];
			while(stk.peek()<=elem && stk.peek()!=-1){
				stk.pop();
			}
			arr[i]=stk.peek();
			stk.push(elem);
		}
		return arr;	
		
	}

}
```

9. Online Stock Span

https://www.naukri.com/code360/problems/span-of-ninja-coin_1475049?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
2
3
1 1 1
5
4 2 3 3 6
Sample Output 1 :
1 2 3
1 1 2 3 5
Explanation of sample input 1 :
In the first test case, the price of Ninja Coin is the same for all three consecutive days, so its span at ith day will be the number of days till ‘i’.
```
```
import java.util.* ;
import java.io.*; 
import java.util.ArrayList;
import java.util.Stack;

public class Solution {
    public static ArrayList<Integer> findSpans(ArrayList<Integer> price) {
        ArrayList<Integer> list = new ArrayList<>();
        Stack<Integer> stk = new Stack<>();

        for(int i=0; i<price.size(); i++){
            int elem = price.get(i);
            while(!stk.isEmpty() && price.get(stk.peek())<=elem){
                stk.pop();
            }
            if(stk.isEmpty()){
                list.add(i+1);
            }else{
                list.add(i-stk.peek());
            }
            stk.push(i);
        }
        return list;
    }
}
```

10. Reversing a Queue

https://www.naukri.com/code360/problems/reversing-a-queue_982934?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
import java.util.* ;
import java.io.*; 

public class Solution {

    public static Queue<Integer> reverseQueue(Queue<Integer> q) {
  
      Stack<Integer> stk = new Stack<>();

      while(!q.isEmpty()){
        stk.push(q.poll());
      }

      while(!stk.isEmpty()){
        q.add(stk.pop());
      }

      return q;
      
    }
  }
```

11. Valid Parenthesis

https://www.naukri.com/code360/problems/valid-parenthesis_795104?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
import java.util.Stack;

public class Solution {
    public static boolean isValidParenthesis(String s) {
        Stack<Character> stk = new Stack<>();

        for(char c: s.toCharArray()){
            if(c=='('){
                stk.push(')');
            }else if(c=='['){
                stk.push(']');
            }else if(c=='{'){
                stk.push('}');
            }else if(stk.isEmpty() || stk.pop()!=c){
                return false;
            }
        }
        return true;
    }
}
```
