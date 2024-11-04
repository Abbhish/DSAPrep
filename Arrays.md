Arrays

1. Second Largest Element in the Array.

https://www.naukri.com/code360/problems/second-largest-element-in-the-array_873375?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
2
6
12 1 35 10 34 1
5
10 10 10 10 10
Sample Output 1:
34
-1
```
```
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int findSecondLargest(int n, int[] arr) {
		int largest = Integer.MIN_VALUE;
		int secondLargest = Integer.MIN_VALUE;

		for(int i=0; i<n; i++){
			if(arr[i]>largest){
				secondLargest=largest;
				largest=arr[i];
			}else if(arr[i]>secondLargest && arr[i]<largest){
				secondLargest=arr[i];
			}
		}
		return secondLargest==Integer.MIN_VALUE?-1:secondLargest;
	}
}
```

2. Rotate Array

https://www.naukri.com/code360/problems/rotate-array_1230543?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
8
7 5 2 11 2 43 1 1
2
Sample Output 1:
2 11 2 43 1 1 7 5
```
```
import java.util.ArrayList;

public class Solution {
	public static ArrayList<Integer> rotateArray(ArrayList<Integer> arr, int k) {
        ArrayList<Integer> list = new ArrayList<>();
        for(int i=k; i<arr.size(); i++){
            list.add(arr.get(i));
        }
        for(int i=0; i<k; i++){
            list.add(arr.get(i));
        }
        return list;
    }
}
```

3. Non-Decreasing Array

https://www.naukri.com/code360/problems/non-decreasing-array_699920?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
2
3
8 4 6
3
8 4 2
Sample Output 1 :
true
false
```
```
import java.util.* ;
import java.io.*; 
public class Solution {
	public static boolean isPossible(int[] arr, int n) {
		int cnt=0;
		for(int i=0; i<n-1; i++){
			if(arr[i]>arr[i+1]){
				cnt++;
				if(cnt>1){
					return false;
				}
				if(i>0 && arr[i+1]<arr[i-1]){
					arr[i+1]=arr[i];
				}else{
					arr[i]=arr[i+1];
				}
			}
		}
		return true;
	}
}
```

4. Equilibrium Index

https://www.naukri.com/code360/problems/equilibrium-index_893014?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
1
6
1 7 3 6 5 6
Sample Output 1:
3
Explanation for Sample Input 1:
The sum of elements to the left of arr[3] = 1 + 7 + 3 = 11.
The sum of elements to the right of arr[3] = 5 + 6 = 11.
Hence the answer is 3.
```
```
import java.util.* ;
import java.io.*; 
public class Solution {

	public static int arrayEquilibriumIndex(int[] arr){  
		int prefixSum=0;
		int suffixSum=0;
		for(int num: arr){
			suffixSum+=num;
		}
		for(int i=0; i<arr.length; i++){
			suffixSum=suffixSum-arr[i];
			if(prefixSum==suffixSum){
				return i;
			}
			prefixSum+=arr[i];
		}
		return -1;
	}
}
```

5. First Missing Positive

https://www.naukri.com/code360/problems/first-missing-positive_699946?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
1
5
3 2 -6 1 0
Sample Output 1:
4
```
```
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int firstMissing(int[] arr, int n) {
		for(int i=0; i<n; i++){
            int element=arr[i];
            int chair=element-1;
            if(element>=1 && element<=n){
                if(arr[chair]!=element){
                    swap(arr, i, chair);
                    i--;
                }
            }
        }
        for(int i=0; i<n; i++){
            if(
                arr[i]<1 ||
                arr[i]>n ||
                arr[i]!=i+1
            ){
                return i+1;
            }
        }
        return n+1;	
        //Another easy way but taking long time.
        // Set<Integer> set = new HashSet<>();
        // for(int num: arr){
        //     set.add(num);
        // }	
        // for(int i=1; i<=n; i++){
        //     if(!set.contains(i)){
        //         return i;
        //     }
        // }
        // return n+1;
	}
    public static void swap(int [] arr, int a, int b){
        int temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }
}
```

6. Make Unique Array

https://www.naukri.com/code360/problems/make-unique-array_920329?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
2
4
1 2 1 2
5
3 6 7 12 13 
Sample Output 1 :
2
0  
```
```
import java.util.* ;
import java.io.*; 
public class Solution {

	public static int minElementsToRemove(ArrayList<Integer> arr) {

		Set<Integer> set = new HashSet<>();
		int cnt=0;
		for(int num: arr){
			if(set.contains(num)){
				cnt++;
			}else{
				set.add(num);
			}
		}
		return cnt;
	}
}
```

7. Sum of Zeroes

https://www.naukri.com/code360/problems/array-sum_893287?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
1
2 2 
1 0
0 1
Sample Output 1:
4
Explanation of Input 1:
In the given matrix, there are 2 zeros. 
For the 0 at the 1st row, 2nd column position, coverage is 2(there is 1 adjacent top one and 1 adjacent right one).
For the 0 at the 2nd row, 2nd column the coverage is 2(there is 1 adjacent top one and 1 adjacent right one).

Hence the net coverage is 2 + 2 = 4.
```
```
import java.util.* ;
import java.io.*; 
import java.util.ArrayList;

public class Solution {

	static int rows;
	static int cols;
	public static Integer coverageOfMatrix(ArrayList<ArrayList<Integer>> mat) {
		int count = 0;
		rows = mat.size();
		cols = mat.get(0).size();
		for(int i=0; i<rows; i++){
			for(int j=0; j<cols; j++){
				if(mat.get(i).get(j)==0){
					int cnt=calCount(i, j, mat);
					count+=cnt;
				}
			}
		}
		return count;
	}
	public static int calCount(int i, int j, ArrayList<ArrayList<Integer>> mat){
		int[][] directions = {{-1, 0}, {0, -1}, {1, 0},{0, 1}};
		int cnt=0;
		for( int[] path: directions){
			int ii = i+path[0];
			int jj = j+path[1];
			if(
				ii>=0 && ii<rows &&
				jj>=0 && jj<cols &&
				mat.get(ii).get(jj)==1
			){
				cnt++;
			}
		}
		return cnt;
	}
}

```

8. Matrix is Symmetric

https://www.naukri.com/code360/problems/matrix-is-symmetric_799361?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube&leftPanelTabValue=SUBMISSION
```
Sample Input 1 :
1
3
1 2 3 2 4 5 3 5 8
Sample Output 1 :
Yes
Explanation For The Sample Output 1 :
```
![image](https://github.com/user-attachments/assets/00436964-2442-4edc-933e-7c9f547c5ccb)
```
import java.util.* ;
import java.io.*; 
public class Solution {
    public static boolean isMatrixSymmetric(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;

        for(int i=0; i<rows; i++){
            for(int j=0; j<cols; j++){
                if(matrix[i][j]!=matrix[j][i]){
                    return false;
                }
            }
        }
        return true;
    }
}
```

9. Pair Sum

https://www.naukri.com/code360/problems/pair-sum_1171154?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
2
5 6
1 2 3 4 5
6 7
1 2 3 4 5 6
Sample Output 1:
2
3
```
```
import java.util.* ;
import java.io.*; 
public class Solution {
    public static int pairSum(int arr[], int n, int target) {
        int start =0;
        int end=n-1;
        int cnt=0;
        while(start<end){
            if(arr[start]+arr[end]==target){
                cnt++;
                start++;
                end--;
            }else if(arr[start]+arr[end]<target){
                start++;
            }else{
                end--;
            }
        }
        return cnt>0?cnt:-1;
    }
}
```

10. Bubble Sort

https://www.naukri.com/code360/problems/bubble-sort_980524?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
![image](https://github.com/user-attachments/assets/9dcab665-81c1-4636-a46d-6259ff21a1a9)
```
Sample Input 1:
1
5
6 2 8 4 10
Sample Output 1:
2 4 6 8 10
```
```
import java.util.* ;
import java.io.*; 

public class Solution {
    
    public static void bubbleSort(int[] arr, int n) {   
        for(int i=0; i<n-1; i++){
            for(int j=0; j<n-i-1; j++){
                if(arr[j+1]<arr[j]){
                    int temp = arr[j+1];
                    arr[j+1]=arr[j];
                    arr[j]=temp;
                }
            }
        }
    }

}
```

11. Selection Sort

https://www.naukri.com/code360/problems/selection-sort_981162?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
![image](https://github.com/user-attachments/assets/8067db18-397b-47b6-834b-ecbb93047c85)
```
Sample Input 1:
1
5
6 2 8 4 10
Sample Output 1:
2 4 6 8 10
```
```
import java.util.* ;
import java.io.*; 
public class Solution {
	public static void selectionSort(int arr[], int n) {
		for(int i=0; i<n-1; i++){
			for(int j=i; j<n; j++){
				if(arr[j]<arr[i]){
					int temp=arr[i];
					arr[i]=arr[j];
					arr[j]=temp;
				}
			}
		}
	}
}
```

12. Insertion Sort

https://www.naukri.com/code360/problems/insertion-sort_3155179?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
2
4
3 1 2 2
3
1 4 2
Sample Output 1 :
1 2 2 3
1 2 4
```
```
import java.util.* ;
import java.io.*; 

public class Solution {

	public static void insertionSort(int n , int[] arr) {
		for(int i=1; i<n; i++){
			int j=i-1;
			int current = arr[i];
			while(j>=0 && arr[j]>current){
				arr[j+1]=arr[j];
				j--;
			}
			arr[j+1]=current;
		}
	}
}
```

13. Intersection of Two Sorted Arrays

https://www.naukri.com/code360/problems/intersection-of-2-arrays_1082149?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
2
6 4
1 2 2 2 3 4
2 2 3 3
3 2
1 2 3
3 4  
Sample Output 1 :
2 2 3
3  
```
```
import java.util.* ;
import java.io.*; 
public class Solution
{
	public static ArrayList<Integer> findArrayIntersection(ArrayList<Integer> arr1, int n, ArrayList<Integer> arr2, int m)
	{
		ArrayList<Integer> list = new ArrayList<>();
		Map<Integer, Integer> hm1 = new HashMap<>();
		Map<Integer, Integer> hm2 = new HashMap<>();
		for(int num: arr1){
			hm1.put(num, hm1.getOrDefault(num,0)+1);
		}
		for(int num: arr2){
			hm2.put(num, hm2.getOrDefault(num,0)+1);
		}
		if(n>m){
			for(int num: arr1){
				if(hm1.containsKey(num) && hm2.containsKey(num) && hm1.get(num)>0 && hm2.get(num)>0){
					list.add(num);
					hm1.put(num, hm1.get(num)-1);
					hm2.put(num, hm2.get(num)-1);
				}
			}
		}else{
			for(int num: arr2){
				if(hm1.containsKey(num) && hm2.containsKey(num) && hm1.get(num)>0 && hm2.get(num)>0){
					list.add(num);
					hm1.put(num, hm1.get(num)-1);
					hm2.put(num, hm2.get(num)-1);
				}
			}
		}
		return list;
	}
}

```

14. Maximum Subarray Sum (Kandane's Algo)

https://www.naukri.com/code360/problems/630526?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
9
1 2 7 -4 3 2 -10 9 1


Sample Output 1 :
11
```
```
import java.util.* ;
import java.io.*; 

public class Solution {
	
	public static long maxSubarraySum(int[] arr, int n) {
		int currSum=0;
		int maxSum = Integer.MIN_VALUE;
		for(int num: arr){
			currSum=currSum+num;
			if(currSum>maxSum){
				maxSum=currSum;
			}
			if(currSum<0){
				currSum=0;
			}
		}	
		return maxSum<0?0:maxSum;
	}

}
```

15. Move Zeroes to End

https://www.naukri.com/code360/problems/interview-shuriken-41-move-zeroes-to-end_240143
```
Sample Input 1:
2
7
2 0 4 1 3 0 28
5
0 0 0 0 1
Sample Output 1:
2 4 1 3 28 0 0
1 0 0 0 0
```
```
public class Solution {
	public static void pushZerosAtEnd(ArrayList<Integer> arr)
	{
		int n=arr.size();
		int count=0;
		for(int num: arr){
			if(num!=0){
				count++;
				arr.set(count, num);
			}
		}
		while(count<n){
			arr.set(count, 0);
			count++;
		}
	}
}
```

16. Square Root of a number

https://www.naukri.com/code360/problems/square-root-integral_893351?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
6
Sample Output 1:
2
Explanation of Sample Input 1:
The square root of the given number 6 lies between 2 and 3, so the floor value is 2.
Sample Input 2:
100
Sample Output 2:
10
```
```
import java.util.* ;

import com.sun.org.apache.xml.internal.utils.res.LongArrayWrapper;

import java.io.*; 

public class Solution {

	public static int sqrtN(long N) {
		long left = 1;
		long mid=-1;
		long right=N;

		while(left<=right){
			mid = left+(right-left)/2;
			if(mid*mid==N){
				return Math.round(mid);
			}else if(mid*mid>N){
				right=mid-1;
			}else{
				left=mid+1;
			}
		}
		return Math.round(right);
	}
}

```

17. Search In Rotated Sorted Array

https://www.naukri.com/code360/problems/630450?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
4
2 5 -3 0
2
5
1
Sample Output 1:
1
-1
```
```
public class Solution {
    public static int search(int arr[], int key) {
        int left=0;
        int right = arr.length-1;
        while(left<=right){
            int mid = left+(right-left)/2;
            if(arr[mid]==key) return mid;
            if(arr[left]<=arr[mid]){
                if(arr[left]<=key && key<arr[mid]){
                    right=mid-1;
                }else{
                    left=mid+1;
                }
            }else{
                if(arr[mid]<key && key<=arr[right]){
                    left=mid+1;
                }else{
                    right=mid-1;
                }
            }
        }
        return -1;
    }
}
```

18. Move All Negative Numbers To Beginning And Positive To End

https://www.naukri.com/code360/problems/move-all-negative-numbers-to-beginning-and-positive-to-end_1112620?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
2
5
1 -4 -2 5 3
2
2 1 
Sample Output 1:
-2 -4 1 5 3
2 1
```
```
public class Solution {
    public static int[] separateNegativeAndPositive(int a[]) {
        int left=0;
        int right=a.length-1;
        while(left<=right){
            if(a[left]<0 && a[right]>0){
                left++;
                right--;
            }else if(a[left]>0 && a[right]<0){
                int temp = a[left];
                a[left] = a[right];
                a[right] = temp;
                left++;
                right--;
            }else if(a[left]<0 && a[right]<0){
                left++;
            }else{
                right--;
            }
        }
        return a;
    }
}
```

19. Container with most water

https://www.naukri.com/code360/problems/container-with-most-water_873860?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
![image](https://github.com/user-attachments/assets/cbb0bb93-19f2-4d12-8d10-fe8c3abe3170)
```
Sample Input 1 :
2
5
4 3 2 1 4
3
1 2 1
Sample Output 1 :
16
2 
```
```
public class Solution {

	public static int maxArea(int[] height) {
	    int left = 0;
		int right = height.length-1;
		int maxAr = 0;

		while(left<=right){
			int currArea = (right-left)*Math.min(height[left], height[right]);
			if(maxAr<currArea){
				maxAr=currArea;
			}
			if(height[left]<height[right]){
				left++;
			}else{
				right--;
			}
		}
		return maxAr;
	}
}
```

20. Longest Subarray Zero Sum

https://www.naukri.com/code360/problems/longest-subset-zero-sum_920321?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
2 
5
1 3 -1 4 -4
4
1 -1 2 -2 
Sample Output 1:
2
4 
```
```
import java.io.*;
import java.util.* ;

import java.util.ArrayList;

public class Solution {

	public static int LongestSubsetWithZeroSum(ArrayList<Integer> arr) {
		Map<Integer, Integer> hm = new HashMap();
		int currSum = 0;
		int maxLen = 0;
		for(int i=0; i<arr.size(); i++){
			currSum = currSum+arr.get(i);
			if(currSum==0){
				maxLen = Math.max(maxLen, i+1);
			}

			if(hm.containsKey(currSum)){
				maxLen = Math.max(maxLen, i-hm.get(currSum));
			}else{
				hm.put(currSum, i);
			}
		}
		return maxLen;
	}
}
```

21. Sort 0 1 2 (Dutch National Flag Algo)

https://www.naukri.com/code360/problems/631055?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
2
6
0 1 2 2 1 0
7
0 1 2 1 2 1 2
Sample Output 1 :
0 0 1 1 2 2
0 1 1 1 2 2 2
```
```
import java.util.* ;
import java.io.*; 
public class Solution 
{
    public static void sort012(int[] arr)
    {
        int start=0;
        int mid=0;
        int end=arr.length-1;

        while(mid<=end){
            if(arr[mid]==0){
                swap(arr, start, mid);
                start++;
                mid++;
            }else if(arr[mid]==1){
                mid++;
            }else{
                swap(arr, mid, end);
                end--;
            }
        }
    }
    public static void swap(int[] arr, int a, int b){
        int temp=arr[a];
        arr[a]=arr[b];
        arr[b]=temp;
    }
}
```

22. Majority Element (Moore's Voting Algo)

https://www.naukri.com/code360/problems/842495?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
2
5
2 3 9 2 2
4
8 5 1 9 
Sample Output 1:
2
-1
```
```
import java.io.*;
import java.util.* ;

public class Solution {
	public static int findMajority(int[] arr, int n) {
		int candidate=0;
		int count=0;
		for(int i=0; i<n; i++){
			if(count==0){
				count++;
				candidate=arr[i];
			}else if(arr[i]==candidate){
				count++;
			}else{
				count--;
			}
		}
		int candidateVotes=0;
		for(int num: arr){
			if(num==candidate){
				candidateVotes++;
			}
		}
		return candidateVotes>n/2 ? candidate : -1;
	}
}
```

23. Is Subsequence

https://www.naukri.com/code360/problems/is-subsequence_892991?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
![image](https://github.com/user-attachments/assets/1366411b-de98-44cd-a1b4-57391ebe22ed)
```
Sample Input 1:
2
AE
BADE
AB
AC
Sample Output 1:
True
False
```
```
import java.util.* ;
import java.io.*; 
public class Solution {

	public static String isSubsequence(String str1, String str2) {    
    	int i=0; 
		int j=0;
		while(i<str1.length() && j<str2.length()){
			if(str1.charAt(i)==str2.charAt(j)){
				i++;
			}
			j++;
		}	
		return i==str1.length() ? "True" : "False";
	}

}
```
