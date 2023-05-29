# Desafio-0
#include <stdio.h>

#include <stdlib.h>

#include <limits.h>

 

typedef struct {

    int first;

    int second;

} Pair;

 

Pair* menorDiff(int array[], int size, int* resultSize) {

    for (int i = 0; i < size - 1; i++) {

        for (int j = 0; j < size - i - 1; j++) {

            if (array[j] > array[j + 1]) {

                int temp = array[j];

                array[j] = array[j + 1];

                array[j + 1] = temp;

            }

        }

    }

 

    int minDifference = INT_MAX;

    for (int i = 0; i < size - 1; i++) {

        int difference = abs(array[i] - array[i + 1]);

        if (difference < minDifference) {

            minDifference = difference;

        }

    }

 

    int count = 0;

    for (int i = 0; i < size - 1; i++) {

        if (abs(array[i] - array[i + 1]) == minDifference) {

            count++;

        }

    }

 

    Pair* pairs = (Pair*)malloc(count * sizeof(Pair));

    if (pairs == NULL) {

        printf("Erro de alocação de memoria.\n");

        exit(1);

    }

 

    int index = 0;

    for (int i = 0; i < size - 1; i++) {

        if (abs(array[i] - array[i + 1]) == minDifference) {

            pairs[index].first = array[i];

            pairs[index].second = array[i + 1];

            index++;

        }

    }

 

    *resultSize = count;

    return pairs;

}

 

int main() {

    int array[] = {3, 8, 50, 5, 1, 18, 12};

    int size = sizeof(array) / sizeof(array[0]);

 

    int resultSize;

    Pair* pairs = menorDiff(array, size, &resultSize);

 

    printf("Pares com a menor diferenca:\n");

    for (int i = 0; i < resultSize; i++) {

        printf("(%d, %d)\n", pairs[i].first, pairs[i].second);

    }

 

    free(pairs);

 

    return 0;

}
