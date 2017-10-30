## flatten nested list iterator
#### Example 1: Given the list [[1,1],2,[1,1]], By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,1,2,1,1].

```C++
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * class NestedInteger {
 *   public:
 *     // Return true if this NestedInteger holds a single integer, rather than a nested list.
 *     bool isInteger() const;
 *
 *     // Return the single integer that this NestedInteger holds, if it holds a single integer
 *     // The result is undefined if this NestedInteger holds a nested list
 *     int getInteger() const;
 *
 *     // Return the nested list that this NestedInteger holds, if it holds a nested list
 *     // The result is undefined if this NestedInteger holds a single integer
 *     const vector<NestedInteger> &getList() const;
 * };
 */
class NestedIterator {
private:
    stack<vector<NestedInteger>::iterator>heads,tails;
public:
    NestedIterator(vector<NestedInteger> &nestedList) {
        heads.push(nestedList.begin());
        tails.push(nestedList.end());
    }

    int next() {
        //if(hasNext)
        return (heads.top()++)->getInteger();
    }

    bool hasNext() {
        while(heads.size()){
            if(heads.top()==tails.top()){
                heads.pop();
                tails.pop();
            }
            else{
                auto item=heads.top();
                if(item->isInteger())
                    return true;
                //else
                heads.top()++;
                heads.push(item->getList().begin());
                tails.push(item->getList().end());
            }
        }
        return false;
    }
};

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i(nestedList);
 * while (i.hasNext()) cout << i.next();
 */
 ```
