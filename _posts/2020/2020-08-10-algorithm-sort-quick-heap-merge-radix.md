---
layout: single
title: "[Algorithm] 정렬(Sort)-퀵 정렬, 힙 정렬, 병합 정렬, 기수 정렬 정의 및 구현"
date: 2020-08-10 21:21:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Algorithm
tags:
- data structure
- algorithm
- sort
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-sort-quick-heap-merge-radix/"
---
#  Quick Sort, Heap Sort, Merge Sort, Radix Sort

## Quick Sort(퀵 정렬)
- **Divide and Conquer** 알고리즘
- 평균수행능력이 가장 뛰어남
- 분할중심값을 **pivot** 또는 control key 라고 함

### 연산
1. 피벗값을 선택(맨 오른쪽, 왼쪽 또는 중앙값을 선택)
2. 피벗 값을 사용하여 배열 분할
3. 파티션 자료 갯수가 1이 될때까지 왼쪽 파티션을 재귀로 빠르게 정렬
4. 파티션 자료 갯수가 1이 될때까지 오른쪽 파티션을 재귀로 빠르게 정렬

### pseudo code
```java
   if right-left <= 0
      return
   else     
     //맨오른쪽 값을 pivot값으로 선택 했을 경우
      pivot = A[right]
      partition = partitionFunc(left, right, pivot)
      quickSort(left,partition-1)
      quickSort(partition+1,right)    
   end if		

```   

### java로 퀵 정렬 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/sort/quick/QuickSortMain.java)


```java
public static void sort(int[] arr, int start, int end) {
        //int pivot = arr[end];
        int left = start;
        int right = end ;

        // pivot값을 가운데 값으로 셋팅
        int pivot = arr[(left+right)/2];
        while( left <= right) {

            //pivot 왼쪽의 값이  pivot 값 보다 작은 경우 다음 element 탐색
            while(arr[left] < pivot) {
                left++;
            }

            // pivot 오른쪽의 값이 pivot값 보다 큰 경우 다음 element 탐색  
            while(arr[right] > pivot) {
                right--;
            }

            //왼쪽 값 > pivot 이면서
            //오른쪽 값 < pivot 이면서
            //왼쪽값 < 오른쪽 값 인 경우
            if( left <= right) {
                //swap
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;

                //그리고 다음 element 탐색
                left++;
                right--;
            }

        }

        if (start < right ) {
            // 분할된 왼쪽 부분 순환 처리
            sort(arr, start, right);
        }

        if (left < end ) {
            // 분할된 오른쪽 부분 순환 처리
            sort(arr, left, end);
        }
    }

```  


#### Complexity


| Complexity | Best Case | Average Case | Worst Case |
|:--------:|:--------:|:--------:|:--------:|
| Time | O(n) for 3 way partition or O(n log n) simple partition | O(n log n) | O(n<sup>2</sup>) |
| Space | | | O(log n) |




## merge sort (병합 정렬)
- **Divide and Conquer** 알고리즘
- 여러 개의 정렬되어있는 배열 자료들을 혼합하여 하나의 정렬된 배열로 합치는 작업

![datastructure-Merge-Sort-Tutorial]({{ site.baseurl }}/assets/images/posts/2020/algorithm-Merge-Sort-Tutorial.png)


### 연산
0. 리스트의 길이가 1 이하이면 이미 정렬된 것으로 보고, 그렇지 않은 경우에
1. 분할(divide) : 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눔
2. 정복(conquer) : 각 부분 리스트를 재귀적으로 병합 정렬을 이용해 정렬
3. 결합(combine) : 두 부분 리스트를 다시 하나의 정렬된 리스트로 병합. 이때 정렬 결과가 임시배열에 저장 됨
4. 복사(copy) : 임시 배열에 저장된 결과를 원래 배열에 복사


### java로 병합 정렬 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/sort/merge/MergeSortMain.java)


```java

    /**
     * 정렬
     * @param arr
     * @param left
     * @param right
     */
    public static void sort(int[] arr, int left, int right) {
        if (left < right) {
            //(분할) 중앙요소 위치 찾기
            int mid = (left + right) /2;

            //(정렬) 앞 부분 : left (0) ~ mid / 뒷 부분 : mid+1 ~ right (n) 까지  
            sort(arr, left, mid);  
            sort(arr, mid+1 , right);

            //(병합)
            merge(arr, left, mid, right);
        }
    }

    /**
     * 병합
     * 첫번째 서브array array[left..mid]
     * 두번째 서브array array[mid+1..right]
     * @param arr
     * @param left
     * @param mid
     * @param right
     */
    public static void merge(int[] arr, int left, int mid, int right) {

        //병합될 두 sub arrays 의 사이즈 찾기
        int n1 = mid - left + 1 ;
        int n2 = right - mid;

        // (복사) mid를 기준으로 왼쪽 / 오른쪽 2개 파트로 나눌 임시 배열 생성
        // 또는 arr에 대한 임시 배열을 만들어서 넣어주고, 병합 후 임시배열을 arr 복사해서 넣어주어도 됨
        int L[] = new int[n1];
        int R[] = new int[n2];

        // 임시 배열값 복사
        for (int i = 0; i < n1; i++) {
            L[i]  = arr[left + i];
        }

        for (int j = 0; j < n2; j++) {
            R[j] = arr[mid + 1 + j];
        }

        //merge
        //초기 인덱스
        int i = 0;
        int j = 0;

        // 병합된 subarray의 초기 인덱스
        int k = left;

        // L 사이즈만 큼 loop (L배열 초기 인덱스 < L배열 사이즈)
        // R 사이즈만 큼 loop (R배열 초기 인덱스 < R배열 사이즈)  
        while (i < n1 && j < n2) {
            // L 배열의 값 <= R배열의 값
            if (L[i] <= R[j]) {
                // L값 arr에 담아주기
                arr[k] = L[i];
                //L 을 담아주었으니 L의 인덱스 증가
                i++;
            }else {
                // L 배열의 값 > R배열의 값
                // R값 arr에 담아주기
                arr[k] = R[j];
                //R 을 담아주었으니 R의 인덱스 증가
                j++;
            }
            k++;
        }

        //L에 남은 값이 있다면 복사
        while(i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        //R에 남은 값이 있다면 복사  
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }

    }
```


#### Complexity


| Complexity | Best Case | Average Case | Worst Case |
|:--------:|:--------:|:--------:|:--------:|
| Time | O(n log n) | O(n log n) | O(n log (n)) |
| Space | | | O(n) |




## Heap Sort(힙 정렬)
- Max-Heap(최대 힙) : 루트 노드에 있는 키는 모든 자식에 있는 키 중에서 가장 커야 함
- Min-Heap(최소 힙) : 루트 노드에 있는 키는 모든 자식에 있는 키 중에서 최소 여야 함
- 최대 힙 트리나 최소 힙 트리를 구성해 정렬을 하는 방법으로서, 내림차순 정렬을 위해서는 최대 힙을 구성하고 오름차순 정렬을 위해서는 최소 힙을 구성


### 연산
1. n개의 노드에 대한 complete binary tree[^1]를 구성. 이때 루트 노드부터 부모노드, 왼쪽 자식노드, 오른쪽 자식노드 순으로 구성.
2. 최대 힙을 구성. 최대 힙이란 부모노드가 자식노드보다 큰 트리를 말하는데, 단말 노드를 자식노드로 가진 부모노드부터 구성하며 아래부터 루트까지 올라오며 순차적으로 만들수 있음
3. 가장 큰 수(루트에 위치)를 가장 작은 수와 교환
4. 2와 3을 반복


![algorithm-MinHeapAndMaxHeap]({{ site.baseurl }}/assets/images/posts/2020/algorithm-MinHeapAndMaxHeap.png)


```java
입력 data: 4, 10, 3, 5, 1
         4(0)
        /   \
     10(1)   3(2)
    /   \
 5(3)    1(4)

괄호안에 숫자는 index


인덱스 1에 heapify 프로 시저 적용 :
         4(0)
        /   \
    10(1)    3(2)
    /   \
5(3)    1(4)


인덱스 0에 heapify 프로 시저 적용 :
        10(0)
        /  \
     5(1)  3(2)
    /   \
 4(3)    1(4)

heapify 프로시저는  하향식으로 힙을 빌드하기 위해 재귀 적으로 호출 됨
```


### java로 힙 정렬 구현


[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/sort/heap/HeapSortMain.java)


```java

    /**
     * heap sort 구현
     * @param arr
     */
    public static void sort(int[] arr) {
        int n = arr.length;

        // [build heap] 요소들을 heapify 해주기
        // i = tree의 level이 됨 (i= 3 ~ 0 까지)
        for (int i = n/2-1; i>=0; i--) {
            heapify(arr, n, i);
        }

        System.out.println();
        System.out.println("-  max heapify  ----------");
        System.out.println(toString(arr));

        System.out.println();
        System.out.println("- get sorted array  ----------");

        // 0. 힙을 빌드 한 후, max 요소는 힙의 루트에 있음 (root의 값은 array[0]으로 제일 큰 값이 됨 )
        // 1. max 요소를 (n - 1) 번째 위치로(오름차순을 위해 맨 뒤) 교환
        // 2. 가장 큰 요소가 적절한 위치에 있고, n 크기를 줄여 힙에서 제거
        // 3. 가장 큰 요소를 교환하면 max heap 속성을 방해 할 수 있으므로 다시 heapify
        // 4. 힙에 요소가 남지 ​​않을 때까지 위의 단계를 수행 하면 결국 정렬 된 배열을 얻게 됨
        for (int i = n-1; i > 0; i--) {
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;
            heapify(arr, i, 0);
            System.out.println(toString(arr));
        }
    }

    /**
     * hepify : heap속성을 충족하기 위해, 힙의 위치를 ​​조정하는 과정
     * 1. max heap 생성하기 위해 현재 요소를 하위 요소와 비교하여 최대 값을 찾은 후
     * 2. 현재 요소가 최대 값이 아닌 경우 최대 값이 위치한 왼쪽 또는 오른쪽 하위 요소로 교환
     * @param arr
     * @param n
     * @param i
     */
    public static void heapify(int arr[], int n, int i) {
        int largest = i; // parent node
        int left = 2*i + 1; // left node = 2*i + 1
        int right = 2*i + 2; // right node = 2*i + 2

        // left의 크기가 array 사이즈 내에 존재 하면서
        // 왼쪽 노드이 값 > 부모노드의 값을 비교 하여 큰 경우
        if(left < n && arr[left] > arr[largest]) {
            //largest index에 left index값을 넣어 줌 (부모노드가 될 것임)
            largest = left;
        }

        // right의 크기가 array 사이즈 내에 존재하면서
        // 오른쪽 노드의 값이 > 부모 노드의 값과 비교하여 큰 경우
        if (right < n && arr[right] > arr[largest]) {
            //largest index에 right index값을 넣어 줌  (부모노드가 될 것임)
            largest = right;
        }

        //자식 노드의 값이 부모노드 보다 큰 값이 존재 할 경우,
        // largest 값이 변경 되었으므로
        if (largest != i) {
            // 부모노드와 <-> 자식노드 swap   
            // 임시변수에 기존 parent node 를 저장하고
            int temp = arr[i];
            // 부모 노드를 자식 노드 들 중에 컸던 값으로 대체  
            arr[i] = arr[largest];
            // 자식노드에 부모값 저장
            arr[largest] = temp;

            //[순환] 바뀐 largest를 기준으로 다시 heapify
            heapify(arr, n, largest);
        }
    }
```


- output


```java
[ * Heap Sort * ]
- before heap sort ----------
[9,5,6,4,7,2,1,8,3]

-  max heapify  ----------
[9,8,6,5,7,2,1,4,3]

- get sorted array  ----------
[8,7,6,5,3,2,1,4,9]
[7,5,6,4,3,2,1,8,9]
[6,5,2,4,3,1,7,8,9]
[5,4,2,1,3,6,7,8,9]
[4,3,2,1,5,6,7,8,9]
[3,1,2,4,5,6,7,8,9]
[2,1,3,4,5,6,7,8,9]
[1,2,3,4,5,6,7,8,9]

- after heap sort ----------
[1,2,3,4,5,6,7,8,9]

```


### Complexity


| Complexity | Best Case | Average Case | Worst Case |
|:--------:|:--------:|:--------:|:--------:|
| Time | Ω(n log (n)) | θ(n log (n)) | O(n log (n)) |
| Space | | | O(1) |



## Radix Sort(기수 정렬)
- bucket(=queue) 에 분배하면서 정렬하는 방법
- LSD : Least Signification Digit (최하위 자릿수) 우선 정렬
- MSD : Most Siginification Digit (최상위 자릿수) 우선 정렬
- 기억장소 낭비

### 연산
1. 각 자료 최소 유효 자릿수에 해당하는 버킷에 모두 큐 순으로 분배하고 낮은 수의 버킷에서 부터 차례로 큐순으로 자료를 꺼냄
2. 각 자료를 십단위 값에 해당하는 버킷에 모두 분배하여 꺼내는 식으로 최대 유효 자릿수까지 반복 수행하면 정렬 됨  

### Example:

0. 아래와 같은 배열을 준비  


```
10,21,17,34,44,11,654,123
```


1.  LSD 정렬  : 1의 따라 분배  


```
0: 10
1: 21 11
2:
3: 123
4: 34 44 654
5:
6:
7: 17
8:
9:
```


- 결과


```
10,21,11,123,24,44,654,17
```


2. 10의 자리수에 따라 분배


```
0:
1: 10 11 17
2: 21 123
3: 34
4: 44
5: 654
6:
7:
8:
9:
```


- 결과

```
10,11,17,21,123,34,44,654
```


3. 100의 자리수에 따라 분배 (most significant digit)


```
0: 010 011 017 021 034 044
1: 123
2:
3:
4:
5:
6: 654
7:
8:
9:
```


- 결과


```
10,11,17,21,34,44,123,654
```


### java로 radix 정렬 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/sort/radix/RadixSort.java)


```java

    /**
     * 배열내 최대값 구하기
     * @param arr
     * @param n
     * @return
     */
    public static int getMax(int[] arr, int n) {
        int max = arr[0];

        for (int i = 1; i < n; i++) {
             if (arr[i] > max) {
                max = arr[i];
             }
        }
        return max;
    }


    /**
     * count sort
     * 각 자리수에 따른 분배
     * @param arr
     * @param n
     * @param exp
     */
    public static void countSort(int[] arr, int n, int exp) {
        int output[] = new int[n]; // output array
        int i;
        int count[] = new int[10];
        Arrays.fill(count, 0);

        //발생횟수를 count[] 저장
        for (i = 0; i < n ; i++) {
            count [(arr[i]/exp)%10]++;
        }

        //count [i]에 output[]의 숫자의 실제 위치가 포함되도록 count[i]를 변경
        for (i = 1; i < 10; i++) {
            count[i] += count[i-1];
        }

        //출력 배열 저장
        for (i = n-1 ; i >= 0; i--) {
           output[count[(arr[i]/exp)%10]-1]=arr[i];
           count[(arr[i]/exp)%10]--;
        }

        // output[]을 arr[]에 복사
        // arr []에 현재 배열에 따라 정렬 된 숫자가 포함됨
        for (i = 0; i < n; i++) {
            arr[i] = output[i];
        }
    }

```


#### Complexity


| Complexity | Best Case | Average Case | Worst Case |
|:--------:|:--------:|:--------:|:--------:|
| Time | Ω(n+k) | θ(nk) | O(nk) |
| Space | | | O(n+k) |




---

#### references
<https://www.javatpoint.com/quick-sort>  
<https://www.javatpoint.com/heap-sort>  
<https://www.javatpoint.com/merge-sort>  
<https://www.javatpoint.com/radix-sort>   
<https://www.geeksforgeeks.org/quick-sort/?ref=lbp/>  
<https://www.geeksforgeeks.org/heap-data-structure/>  
<https://www.geeksforgeeks.org/merge-sort/>  
<https://www.geeksforgeeks.org/radix-sort/>  
<https://www.tutorialspoint.com/data_structures_algorithms/quick_sort_algorithm.htm>  
<https://www.tutorialspoint.com/data_structures_algorithms/merge_sort_algorithm.htm>  
<https://ko.wikipedia.org/wiki/%EC%84%A0%ED%83%9D_%EC%A0%95%EB%A0%AC>  
<https://ko.wikipedia.org/wiki/%ED%9E%99_%EC%A0%95%EB%A0%AC>  
<https://www.hackerearth.com/practice/algorithms/sorting/radix-sort/tutorial/>  
<https://codenuclear.com/quick-sort-algorithm/>



---
#### 주석
[^1]:마지막 level을 제외하고 모든 level이 완전히 채워지고 마지막 level에 가능한 한 왼쪽에 모든 키가 있는 경우  
