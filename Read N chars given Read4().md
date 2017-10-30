#### could left some chars in the buff from last call
#### Time: O(n)--n is desired length to read---suppose read4 is O(1)
#### Space: O(1) extra space

```C++
// Forward declaration of the read4 API.
int read4(char *buf);

class Solution {
public:
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    int read(char *buf, int n) {
        int i=0;
        while(i<n){
            if(buffPointer==0)//ready to read
                buffCounter=read4(buff4);
            if(buffCounter==0)//end
                break;
            while(i<n && buffPointer<buffCounter){
                buf[i++]=buff4[buffPointer++];
            }
            if(buffPointer>=buffCounter)
                buffPointer=0;
        }
        return i;
    }
private:
    char buff4[4];//could contain chars loaded previously
    int buffPointer=0;
    int buffCounter=0;
};
```
