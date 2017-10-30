## Implement strStr().
#### Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.
#### KMP algorithm: do not start from beginning if mismatch. absabc
#### Time complexity: O(m+n)
#### Space complexity: extra O(n)

```C++
class Solution {
public:
    int strStr(string haystack, string needle) {
        int m=haystack.size();
        int n=needle.size();
        if(n==0)
            return 0;
        if(m==0)
            return -1;
        vector<int>kmp=preprocess(needle);
        //match
        int match;
        for(int i=0,j=0;i<m;){
            if(haystack[i]==needle[j]){
                i++;
                j++;
            }
            if(j==n)
                return i-j;
            if(i<m && haystack[i]!=needle[j]){
                if(j>0)
                    j=kmp[j-1];
                else
                    i++;
            }
        }
        return -1;
    }
    
private:
    vector<int> preprocess(string needle){
        int n=needle.size();
        vector<int>kmp(n,0);
        for(int i=1,j=0;i<n;){
            if(needle[i]==needle[j]){
                kmp[i]=j+1;
                i++;
                j++;
            }
            else if(j>0){
                    j=kmp[j-1];
            }
            else{//j==0
                    kmp[i]=j;
                    i++;
            }
        }
        return kmp;
    }
};
```
