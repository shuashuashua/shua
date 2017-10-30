## Find intersection of two sorted arrays
#### If the sizes of two arrays are similar, we go through both arrays and record intersections. Time: O(m+n). Space: O(1) except output.
#### If one array is significantly larger than the other, apply binary seach for each element in the shorter array in the longer array. If found: add to intersection. given m>n-->Time: O(nlogm). Space: O(1) except output.

#### Follow Up: Union? if not found, add it. add shorter array at last.
#### Follow Up: Unsorted arrays? m>n--> Time complexity: O(nlogn+mlogn)
1) Initialize intersection I as empty.
2) Find smaller of m and n and sort the smaller array.
3) For every element x of larger array, do following
…….b) Binary Search x in smaller array. If x is present, then copy it to I.
4) Return I.

```C++
#include <iostream>
#include <vector>
using namespace std;

int binarySearch(vector<int>arr, int target) {
	int l = 0, r = arr.size()-1;
	int mid;
	while (l <= r) {
		mid = (l + r) / 2;
		if (target == arr[mid])
			return mid;
		if (target<arr[mid])
			r = mid - 1;
		else
			l = mid + 1;
	}
	return -1;
}

vector<int> getIntersection(vector<int>arr1, vector<int>arr2) {
	vector<int>intersection;
	int m = arr1.size();
	int n = arr2.size();
	if (m*n == 0)
		return intersection;
	if (m<n)//swap
		arr1.swap(arr2);
	for (int a : arr2) {
		if (binarySearch(arr1, a)>-1)
			intersection.push_back(a);
	}
	return intersection;
}
int main() {
	//code
	vector<int>arr1 = { 1,2,5,7,9,11 };
	vector<int>arr2 = { 5,9,10 };
	vector<int>intersection = getIntersection(arr2, arr1);
	cout << "Size:" << intersection.size() << endl;
	for (int i : intersection) {
		cout << i << " ";
	}
	cout << endl;
	getchar(); 
	return 0;
}
```
