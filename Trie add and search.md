#### Time: add O(n)----search O(n)
#### Space: add O(n*26) for each word----search O(1)

```C++
class TrieNode{
public:
    bool isEnd;
    TrieNode* children[26];
    TrieNode():isEnd(false){
        //memset(children, NULL, sizeof(TrieNode*) * 26); 
        fill_n(children,26,nullptr);
    }
};

class WordDictionary {
public:
    /** Initialize your data structure here. */
    WordDictionary() {
        root=new TrieNode();
    }
    
    /** Adds a word into the data structure. */
    void addWord(string word) {
        if(search(word))//exist in tree
            return;
        TrieNode* curr=root;
        int j;
        for(int i=0;i<word.size();i++){
            j=word[i]-'a';
            if(curr->children[j]==nullptr)
                curr->children[j]=new TrieNode();
            curr=curr->children[j];
        }
        curr->isEnd=true;
    }
    
    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    bool search(string word) {
        return query(word,0,root);
    }
    
    ~WordDictionary(){
        delete root;
    }
private:
    TrieNode* root;
    bool query(string word,int pos,TrieNode* curr){
        if(pos==word.size())
            return curr->isEnd;
        if(word[pos]=='.'){
            for(int j=0;j<26;j++){
                if(curr->children[j]&&query(word,pos+1,curr->children[j]))
                    return true;
            }
        }
        else{
            int k=word[pos]-'a';  
            if(curr->children[k]&&query(word,pos+1,curr->children[k]))
                return true;
        }
        return false;
    }
};

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * bool param_2 = obj.search(word);
 */
 ```
