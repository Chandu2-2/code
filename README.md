#include <stdio.h>
#include <stdlib.h>

// Structure to store number and its frequency
struct NumFreq {
    int num;
    int freq;
};

// Comparison function for qsort
int compare(const void *a, const void *b) {
    struct NumFreq *x = (struct NumFreq *)a;
    struct NumFreq *y = (struct NumFreq *)b;
    
    // If frequencies are different, sort by frequency (ascending)
    if (x->freq != y->freq) {
        return x->freq - y->freq;
    }
    // If frequencies are same, sort by number (descending)
    return y->num - x->num;
}

int main() {
    int N;
    scanf("%d", &N);
    
    int nums[101];
    for (int i = 0; i < N; i++) {
        scanf("%d", &nums[i]);
    }
    
    // Count frequency of each number using a hash map
    // Since -100 <= nums[i] <= 100, we can use array for counting
    int freq[201] = {0}; // Offset by 100 to handle negative numbers
    for (int i = 0; i < N; i++) {
        freq[nums[i] + 100]++;
    }
    
    // Create array of number-frequency pairs
    struct NumFreq numFreq[201];
    int uniqueCount = 0;
    for (int i = 0; i < 201; i++) {
        if (freq[i] > 0) {
            numFreq[uniqueCount].num = i - 100;
            numFreq[uniqueCount].freq = freq[i];
            uniqueCount++;
        }
    }
    
    // Sort based on frequency and value
    qsort(numFreq, uniqueCount, sizeof(struct NumFreq), compare);
    
    // Output the sorted array
    for (int i = 0; i < uniqueCount; i++) {
        for (int j = 0; j < numFreq[i].freq; j++) {
            printf("%d ", numFreq[i].num);
        }
    }
    
    return 0;
}
