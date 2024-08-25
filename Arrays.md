Arrays
1. 
2.
3.
4.
5.
6.
7.
8.

1. Second Largest Element in the Array.
https://www.naukri.com/code360/problems/second-largest-element-in-the-array_873375?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
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
