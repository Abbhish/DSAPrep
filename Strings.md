Strings

Count - 8

1. Reverse String Word Wise

https://www.naukri.com/code360/problems/reverse-string-word-wise_1262348?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
Welcome to Coding Ninjas
Sample Output 1:
Ninjas Coding to Welcome
```
```
import java.util.Scanner;

class Solution {

    static String reverseStringWordWise(String input) {
        String[] words = input.split(" ");
        int left=0;
        int right=words.length-1;
        while(left<=right){
            String temp = words[left];
            words[left]=words[right];
            words[right]=temp;
            left++;
            right--;
        }
        return String.join(" ", words);
    }

    public static void main(String args[]) {
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine();
        String ans = reverseStringWordWise(input);
        System.out.println(ans);
    }
}
```

2. Encode the Message

https://www.naukri.com/code360/problems/encode-the-message_699836?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube&leftPanelTabValue=PROBLEM
```
Sample Input 1 :
3
aabbc
abcd
abbdcaas
Sample Output 1 :
a2b2c1
a1b1c1d1
a1b2d1c1a2s1
```
```
import java.util.* ;
import java.io.*; 
public class Solution {
	public static String encode(String message) {
		StringBuilder ans = new StringBuilder();
		int n=message.length();

		for(int i=0; i<n; i++){
			int count =1;
			char currChar = message.charAt(i);

			while(i+1<n && message.charAt(i+1)==currChar){
				count++;
				i++;
			}
			ans.append(currChar);
			ans.append(count);
		}
		return ans.toString();
	}
}
```

3. Minimum Parenthesis

https://www.naukri.com/code360/problems/mnfrj_1075018?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
2
)((()
((
Sample Output 1:
3
2
```
![image](https://github.com/user-attachments/assets/74a165f8-6d58-422f-a43d-f8e3716634f5)

```
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int minimumParentheses(String pattern) {
		Stack<Character> stk = new Stack<>();
		for(char c: pattern.toCharArray()){
			if(stk.size()==0){
				stk.push(c);
			}
			else if(c==')' && stk.peek()=='('){
				stk.pop();
			}else{
				stk.push(c);
			}
		}
		return stk.size();
	}
}
```

4. Beautiful String

https://www.naukri.com/code360/problems/beautiful-string_1115625?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
2
0000
1010
Sample Output 1 :
2
0
```
```
public class Solution {
    public static int makeBeautiful(String str) {
        int compare1=0;
        int compare2=0;
        for(int i=0; i<str.length(); i++){
            if(i%2==0){
                if(str.charAt(i)!='1'){
                    compare1++;
                }else{
                    compare2++;
                }
            }else{
                if(str.charAt(i)!='0'){
                    compare1++;
                }else{
                    compare2++;
                }
            }
        }
        
        return Math.min(compare1, compare2);
    }
}
```

5. Next Smallest Palindrome

https://www.naukri.com/code360/problems/given-a-string-find-the-next-smallest-palindrome_874577?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
1
4
1221
Sample Output 1:
1331
```
```
import java.util.* ;
import java.io.*; 


// Approach
// 1. Add 1 to the number
// 2. start making last digit same as first, if less than i/p set condiyion violates to true, else false
// 3. if condition violates, inc the pos++ from both ends and make inbetween pos as 0.


public class Solution {
	public static String nextLargestPalindrome(String number, int length) {
		char s[] = number.toCharArray();
        int carry=1;
        int temp;
        for(int i=length-1; i>=0; i--){
            if(s[i]-48+carry<9){
                s[i]=(char)((s[i]-48+carry)+48);
                carry=0;
            }else{
                temp=(s[i]-48+carry)%10;
                s[i] = (char)(temp+48);
            }
        }

        if(carry!=0){
            String str="";
            for(char c: s){
                str=str+c;
            }
            str=(char)(carry+48)+str;
            s=str.toCharArray();
        }

        int i=0, pos=0, j=s.length-1;
        boolean conditionViolated = false;
        while(i<=j){
            if(s[i]<s[j]){
                s[j]=s[i];
                conditionViolated=true;
                pos=i;
            }else if(s[i]>s[j]){
                s[j]=s[i];
                conditionViolated=false;
            }else if(conditionViolated && s[i]!='9'){
                pos=i;
            }
            i++;
            j--;
        }
        if(conditionViolated){
            s[pos]++;
            s[s.length-1-pos]=s[pos];
            for(int k=pos+1; k<=(s.length-1)/2; k++){
                s[k] = s[s.length-1-k] = '0';
            }
        }
        number=new String(s);
        return number;
	}
}
```

6. First non Repeating Character

https://www.naukri.com/code360/problems/first-non-repeating-character_920324?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
2
aDcadhc
AabBcC
Sample Output 1:
 D
 A
```
```
import java.util.* ;
import java.io.*; 
public class Solution {

	public static char firstNonRepeatingCharacter(String str) {

		Map<Character, Integer> hm = new HashMap();
		for(char c: str.toCharArray()){
			hm.put(c, hm.getOrDefault(c, 0)+1);
		}
		for(char c: str.toCharArray()){
			if(hm.get(c)==1){
				return c;
			}
		}
		return str.charAt(0);
	}
}
```

7. Check Permumtation

https://www.naukri.com/code360/problems/check-permutation_1172164?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1:
2
listen silent
east eats
Sample Output 1:
1
1
```
```
import java.util.* ;
import java.io.*; 
public class Solution {
    public static boolean areAnagram(String str1, String str2){
        Map<Character, Integer> hm = new HashMap<>();
        for(char c: str1.toCharArray()){
            hm.put(c, hm.getOrDefault(c, 0)+1);
        }
        for(char c: str2.toCharArray()){
            hm.put(c, hm.getOrDefault(c, 0)-1);
        }
        for(int count: hm.values()){
            if(count!=0){
                return false;
            }
        }
        return true;
    }
}
```

8. Find Kth Character of Decrypted String

https://www.naukri.com/code360/problems/find-k-th-character-of-decrypted-string_630508?utm_source=youtube&utm_medium=affiliate&utm_campaign=parikh_youtube
```
Sample Input 1 :
a2b3cd3
8
Sample Output 1 :
c
 Explanation to Sample Input 1 :
S = "a2b3cd3"
Decrypted String of S = "aabbbcdcdcd"
According to 1-based indexing for S, the 8th character is 'c'.
Sample Input 2 :
ab12c3
20
Sample Output 2 :
b
 Explanation to Sample Input 2 :
S = "ab12c3"
Decrypted String of S = "ababababababababababababccc"
So 20th character is 'b'.
```
```
public class Solution 
{
    public static char kThCharaterOfDecryptedString(String s, Long k) 
    {
        long n = s.length();
        long i=0, j;
        long substr;
        long freq;
        long resLen;
        char ans='a';

        while(i<n){
            j=i;
            substr = 0;
            freq=0;
            while(j<n && Character.isAlphabetic(s.charAt((int)j))){
                substr++;
                j++;
            }

            while(j<n && Character.isDigit(s.charAt((int)j))){
                freq = freq*10+(s.charAt((int)j)-'0');
                j++;
            }

            resLen = substr*freq;

            if(k>resLen){
                k=k-resLen;
                i=j;
            }else{
                k--;//bcoz i is already there
                k=k%substr;
                ans=s.charAt((int)(i+k));
                break;
            }
        }
        return ans;
    }
}
```
