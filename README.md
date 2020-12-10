# Generate-one-umber-with-corresponding-probability
You are given n numbers as well as n probabilities that sum up to 1. Write a function to generate one of the numbers with its corresponding probability.  For example, given the numbers [1, 2, 3, 4] and probabilities [0.1, 0.5, 0.2, 0.2], your function should return 1 10% of the time, 2 50% of the time, and 3 and 4 20% of the time.  You can generate random numbers between 0 and 1 uniformly.


#include <bits/stdc++.h> 
using namespace std; 
  
// Utility function to find ceiling of r in arr[l..h]  
int findCeil(int arr[], int r, int l, int h)  
{  
    int mid;  
    while (l < h)  
    {  
        mid = l + ((h - l) >> 1); // Same as mid = (l+h)/2  
        (r > arr[mid]) ? (l = mid + 1) : (h = mid);  
    }  
    return (arr[l] >= r) ? l : -1;  
}  
  
// The main function that returns a random number 
// from arr[] according to distribution array  
// defined by freq[]. n is size of arrays.  
int myRand(int arr[], int freq[], int n)  
{  
    // Create and fill prefix array  
    int prefix[n], i;  
    prefix[0] = freq[0];  
    for (i = 1; i < n; ++i)  
        prefix[i] = prefix[i - 1] + freq[i];  
  
    // prefix[n-1] is sum of all frequencies. 
    // Generate a random number with  
    // value from 1 to this sum  
    int r = (rand() % prefix[n - 1]) + 1;  
  
    // Find index of ceiling of r in prefix arrat  
    int indexc = findCeil(prefix, r, 0, n - 1);  
    return arr[indexc];  
}  
  
// Driver code  
int main()  
{  
    int arr[] = {1, 2, 3, 4};  
    int freq[] = {10, 5, 20, 100};  
    int i, n = sizeof(arr) / sizeof(arr[0]);  
  
    // Use a different seed value for every run.  
    srand(time(NULL));  
  
    // Let us generate 10 random numbers accroding to  
    // given distribution  
    for (i = 0; i < 5; i++)  
    cout << myRand(arr, freq, n) << endl;  
  
    return 0;  
}  
