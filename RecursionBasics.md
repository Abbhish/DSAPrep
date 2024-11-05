Recursion Basics

Count - 5

1. Merge Sort

https://www.naukri.com/code360/problems/merge-sort_920442?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
![image](https://github.com/user-attachments/assets/f2e1f8f8-3612-4e25-8e3b-ab16057586aa)

```
Sample Input 1 :
2
7
3 4 1 6 2 5 7
4
4 3 1 2
Sample Output 1 :
1 2 3 4 5 6 7
1 2 3 4
```
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

2. Quick Sort

https://www.naukri.com/code360/problems/quick-sort_983625?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
![image](https://github.com/user-attachments/assets/5923fe8d-1739-4464-ae3f-c41614fd258e)
```
Sample Input 1:
2
5
4 2 5 1 3
4     
6 2 4 1
Sample Output 1:
1 2 3 4 5
1 2 4 6
```
```
import java.util.* ;
import java.io.*; 
public class Solution {
    public static List<Integer> quickSort(List<Integer> arr){
        int n = arr.size();

        quickSort(arr, 0, n-1);
        return arr;
    }

    public static void quickSort(List<Integer> arr, int low, int high){
        if(low<high){
            int piid = partition(arr, low, high);
        quickSort(arr, low, piid-1);
        quickSort(arr, piid+1, high);
        }
        
    }

    public static int partition(List<Integer> arr, int low, int high){
        int pivot = arr.get(high);
        int i=low-1;
        for(int j=low; j<high; j++){
            if(arr.get(j)<pivot){
                i++;
                Collections.swap(arr, i, j);
            }
        }
        i++;
        Collections.swap(arr, i, high);
        return i;
    }
}
```

3. Find Kth Element

https://www.naukri.com/code360/problems/find-k-th-element_1214963?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample input 1:
2
4 3 4
1 4 7 10
2 5 6
1 1 2
7
1
Sample output 1:
5
7
```
```
import java.util.* ;
import java.io.*; 
public class Solution {
    public static int findKthElement(ArrayList<Integer> arr1, ArrayList<Integer> arr2, int k) {
        int idx1=0;
        int idx2=0;
        int x=0;
        int[] merged = new int[arr1.size()+arr2.size()];
        while(idx1<arr1.size() && idx2<arr2.size()){
            if(arr1.get(idx1)<arr2.get(idx2)){
                merged[x++]=arr1.get(idx1++);
            }else{
                merged[x++]=arr2.get(idx2++);
            }
        }
        while(idx1<arr1.size()){
            merged[x++]=arr1.get(idx1++);
        }
        while(idx2<arr2.size()){
            merged[x++]=arr2.get(idx2++);
        }
        return merged[k-1];
    }
}
```

4. Family Structure

https://www.naukri.com/code360/problems/family-structure_981243?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
![image](https://github.com/user-attachments/assets/f8c87cd5-cce0-4f3f-b62f-5542e14ce0c9)
```
Sample Input 1:
2
2 2 
3 4  
Sample Output 1:
Female
Male
```
```
public class Solution {
	public static String kthChildNthGeneration(int n, long k) {
		if(n==1||k==1){
			return "Male";
		}
		if(kthChildNthGeneration(n-1, (k+1)/2)=="Male"){
			return k%2>0?"Male":"Female";
		}else{
			return k%2>0?"Female":"Male";
		}
	}

}
```

5. Binary String with no consecutive 1's

https://www.naukri.com/code360/problems/binary-strings-with-no-consecutive-1s_893001?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
4
Sample Output 1:
0000 0001 0010 0100 0101 1000 1001 1010 
Explanation of sample input 1:
For N = 4 we get the following Strings:

0000 0001 0010 0100 0101 1000 1001 1010
```
```
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public static List< String > generateString(int N) {
        List<String> ans = new ArrayList<>();
        generateBinaryString(N, "", ans );
        return ans;
    }
    public static void generateBinaryString(int n, String current, List<String> ans){
        if(n==0){
            ans.add(current);
        }else{
           if(current.isEmpty() || current.charAt(current.length()-1)=='0'){
                generateBinaryString(n-1, current+"0", ans );
                generateBinaryString(n-1, current+"1", ans );
            }else{
                generateBinaryString(n-1, current+"0", ans );
            } 
        }
        
    }
}

```
