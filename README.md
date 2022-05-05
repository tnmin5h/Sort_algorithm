# 정렬 알고리즘

`202101614 오수민`

## 버블 정렬

- 이웃하는 숫자를 비교하여 작은 수를 앞쪽으로 이동시키는 과정을 반복하여 정렬하는 알고리즘

```
#include <stdio.h>
#include <stdlib.h>

int main() {
	int i, j, temp;
	int arr[16] = { 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 65536, 131072, 262144, 524288, 1048576 };
	for (i = 0; i < 16; i++) {
		for (j = 0; j < 15 - i; j++) {
			if (arr[j] > arr[j + 1]) {
				temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
	for (i = 0; i < 16; i++)
		printf("%d ", arr[i]);

	return 0;
}
```


---
## 선택 정렬

- 입력 배열 전체에서 최솟값을 선택하여 배열의 0번째 원소와 자리를 바꾸고, 다음에는 0번째 원소를 제외한 나머지 원소에서 최솟값을 선택하여, 배열의 1번째 원소와 자리를 바꾼다. 이러한 방식으로 마지막에 2개의 원소 중에서 작은 값을 택하고 자리를 바꿈으로써 오름차순의 정렬을 마친다.

```
#include <stdio.h>
#include <stdlib.h>

int main() {
	int i, j, min, index, temp;
	int arr[16] = { 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 65536, 131072, 262144, 524288, 1048576 };
	for (i = 0; i < 16; i++) {
		min = INT_MAX;
		for (j = i; j < 16; j++) {
			if (min > arr[j]) {
				min = arr[j];
				index = j;
			}
		}
		temp = arr[i];
		arr[i] = arr[index];
		arr[index] = temp;
	}
	for (i = 0; i < 16; i++)
		printf("%d ", arr[i]);
	return 0;
}
```
---
## 삽입 정렬

- 배열을 정렬된 부분과 정렬이 되지 않은 부분으로 나눈 후, 정렬이 되지 않은 부분의 가장 왼쪽 원소를 정렬된 부분의 적절한 위치에 삽입하여 정렬되도록 하는 과정을 반복한다.

```
#include <stdio.h>
#include <stdlib.h>

int main() {
	int i, j, temp;
	int arr[16] = { 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 65536, 131072, 262144, 524288, 1048576 };
	for (i = 0; i < 15; i++) {
		j = i;
		while (j >= 0 && arr[j] > arr[j + 1]) {
			temp = arr[j];
			arr[j] = arr[j + 1];
			arr[j + 1] = temp;
			j--;
		}
	}
	for (i = 0; i < 16; i++)
		printf("%d ", arr[i]);

	return 0;
}
```
---
## 쉘 정렬

- 버블 정렬이나 삽입 정렬이 수행될 때 작은 숫자가 배열의 앞부분으로 매우 느리게 이동하는데, 이러한 단점을 보완하기 위해서 삽입 정렬을 이용하여 배열 뒷부분의 작은 숫자를 앞부분으로 빠르게 이동시키고, 동시에 앞부분의 큰 숫자는 뒷부분으로 이동시키며 가장 마지막에 삽입 정렬을 수행하는 것이 바로 쉘 정렬이다.

```
# include <stdio.h>

void inc_insertion_sort(int list[], int first, int last, int gap) {
    int i, j, key;

    for (i = first + gap; i <= last; i = i + gap) {
        key = list[i];
        for (j = i - gap; j >= first && list[j] > key; j = j - gap) {
            list[j + gap] = list[j];
        }
        list[j + gap] = key;
    }
}
void shell_sort(int list[], int n) {
    int i, gap;

    for (gap = n / 2; gap > 0; gap = gap / 2) {
        if ((gap % 2) == 0)(
            gap++
            );
    }
            for (i = 0; i < gap; i++) {
                inc_insertion_sort(list, i, n - 1, gap);
            }
    }
}

void main() {
    int i;
    int list[16] = { 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 65536, 131072, 262144, 524288, 1048576 };
    shell_sort(list, 16);
    for (i = 0; i < 16; i++) {
        printf("%d\n", list[i]);
    }
}
```
---
## 힙 정렬

- 힙 : 힙 조건을 만족하는 완전 이진트리

- 힙 조건 : 각 노드의 값이 자식 노드의 값보다 커야 하는 조건

- 노드의 값 = 우선순위

- 힙의 루트에는 가장 높은 우선순위 즉, 가장 큰 값이 저장되어 있고, 값이 작을수록 우선순위가 높은 경우에는 가장 작은 값이 루트에 저장된다.

- 힙 정렬 : 위의 힙 자료 구조를 이용하는 정렬 알고리즘

- 오름차순의 정렬을 위해 입력 배열을 먼저 큰 숫자가 높은 우선쉰위를 가지는 최대힙을 만든 후, 힙의 루트에는 가장 큰 수가 저장되기 때문에 루트의 숫자를 힙의 가장 마지막 노드에 있는 숫자와 바꾼다. 그 후, 힙의 크기를 1개 줄인 다음에 루트에 새롭게 저장된 숫자로 인하여 위배된 힙 조건을 해결하여 힙 조건을 만족시킨다. 이러한 과정을 계속해서 반복하면서 나머지 숫자를 정렬하는 것이 힙 정렬 알고리즘에 해당한다.

```
#include <stdio.h>
#include <stdlib.h>

int size = 16;
int heap[16] = { 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 65536, 131072, 262144, 524288, 1048576 };

int main() {
	for (int i = 1; i < size; i++) {
		int child = i;
		do {
			int root = (child - 1) / 2;
			if (heap[root] < heap[child]) {
				int temp = heap[root];
				heap[root] = heap[child];
				heap[child] = temp;
			}
			child = root;
		} while (child != 0);
	}

	for (int i = size - 1; i >= 0; i--) {
		int temp = heap[0];
		heap[0] = heap[i];
		heap[i] = temp;
		int root = 0;
		int child = 1;
		do {
			child = 2 * root + 1;
			if (heap[child] < heap[child + 1] && child < i - 1) {
				child++;
			}
			if (heap[root] < heap[child] && child < i) {
				int temp = heap[root];
				heap[root] = heap[child];
				heap[child] = temp;
			}
			root = child;
		} while (child < i);
	}
	for (int i = 0; i < size; i++)
		printf("%d ", heap[i]);

	return 0;
}
```
---
## 정렬 알고리즘의 시간복잡도 비교
![image](https://user-images.githubusercontent.com/101817735/166953388-a1b308b4-9c6f-4e5d-91b7-e88b065e16a9.png)
