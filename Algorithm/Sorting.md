# Sorting (정렬)
* 원소들을 번호순이나 사전 순서와 같이 일정한 순서대로 열거하는 알고리즘입니다. 효율적인 정렬은 탐색이나 병합 알고리즘처럼 (정렬된 리스트에서 바르게 동작하는) 다른 알고리즘을 최적화하는 데 중요하며 데이터의 정규화나 의미있는 결과물을 생성하는 데 유용히 쓰입니다. 


<details>
<summary> 버블 정렬(Bubble sort) </summary>

- 서로 인접한 두 원소를 검사하여 정렬하는 알고리즘입니다.

- 인접한 2개의 레코드를 비교하여 크기가 순서대로 되어 있지 않으면 서로 교환합니다.

- 구체적인 과정
   - 버블 정렬은 첫 번째 자료와 두 번째 자료를, 두 번째 자료와 세 번째 자료를, 세 번째와 네 번째를, … 이런 식으로 (마지막-1)번째 자료와 마지막 자료를 비교하여 교환하면서 자료를 정렬합니다.
   - 1회전을 수행하고 나면 가장 큰 자료가 맨 뒤로 이동하므로 2회전에서는 맨 끝에 있는 자료는 정렬에서 제외됩니다. 2회전을 수행하고 나면 끝에서 두 번째 자료까지는 정렬에서 제외됩니다. 
   - 이렇게 정렬을 1회전 수행할 때마다 정렬에서 제외되는 데이터가 하나씩 늘어납니다.
- 배열에 7, 4, 5, 1, 3이 저장되어 있다고 가정하고 자료를 오름차순으로 정렬하는 과정은 아래와 같습니다. 

![image](https://user-images.githubusercontent.com/76711238/232315651-bb7400e7-d4ca-42b8-a06b-2e299581c938.png)

**버블 정렬(bubble sort) 알고리즘의 특징**
- **장점**
   - 구현이 매우 간단합니다.
- **단점** 
   - 순서에 맞지 않은 요소를 인접한 요소와 교환합니다. 
   - 하나의 요소가 가장 왼쪽에서 가장 오른쪽으로 이동하기 위해서는 배열에서 모든 다른 요소들과 교환되어야 합니다. 특히 특정 요소가 최종 정렬 위치에 이미 있는 경우라도 교환되는 일이 일어납니다.
   - 일반적으로 자료의 교환 작업(SWAP)이 자료의 이동 작업(MOVE)보다 더 복잡하기 때문에 버블 정렬은 단순성에도 불구하고 거의 쓰이지 않습니다.

- **시간복잡도**
   - **비교 횟수**
      - 정렬이 돼있던 안돼있던, 2개의 원소를 비교하기 때문에 최선, 평균, 최악의 경우 모두 시간복잡도가 O(n^2) 으로 동일합니다. 따라서 최상, 평균, 최악 모두 일정합니다.
      - n-1, n-2, … , 2, 1 번 = n(n-1)/2
   - **교환 횟수**
      - 입력 자료가 역순으로 정렬되어 있는 최악의 경우, 한 번 교환하기 위하여 3번의 이동(SWAP 함수의 작업)이 필요하므로 (비교 횟수 * 3) 번 = 3n(n-1)/2
      - 입력 자료가 이미 정렬되어 있는 최상의 경우, 자료의 이동이 발생하지 않습니다.
      - T(n) = O(n^2)
      
</details>


<details>
<summary> 선택 정렬 (Selection Sort) </summary>
- 
</details>


<details>
<summary> 삽입 정렬 (Insertion Sort) </summary>
- 
</details>


<details>
<summary> 버블 정렬, 삽입 정렬, 삽입 정렬의 비교 </summary>
- 
</details>


<details>
<summary> 퀵 정렬 (Quick Sort) </summary>
- 
</details>


<details>
<summary> 병합 정렬 (Merge Sort) </summary>
- 
</details>


<details>
<summary> 힙 정렬 (Heap Sort) </summary>

- 

</details>


<details>
<summary> 기수 정렬 (Radix Sort) </summary>
- 
</details>


<details>
<summary> 계수 정렬 (Counting Sort) </summary>

- 최대 힙 트리나 최소 힙 트리를 구성해 정렬을 하는 방법입니다. 
- **내림차순 정렬**을 위해서는 **최대 힙**을 구성합니다.
- **오름차순 정렬**을 위해서는 **최소 힙**을 구성하면 됩니다. 
- 최댓값과 최솟값을 찾는데 최적화되어있는 이유는 heap의 특성상 최대 힙일 때는 가장 큰 값이 루트 노드로 오게 되고 최소 힙일 때는 가장 작은 값이 루트 노드로 오기 때문입니다. 

**과정 설명**
- 정렬해야 할 n개의 요소들로 최대 힙(완전 이진 트리 형태)을 만듭니다. 
- 내림차순을 기준으로 정렬합니다.
- 그 다음으로 한 번에 하나씩 요소를 힙에서 꺼내서 배열의 뒤부터 저장하면 됩니다.
- 삭제되는 요소들(최댓값부터 삭제)은 값이 감소되는 순서로 정렬되게 됩니다.

**힙 정렬(heap sort) 알고리즘의 특징**
- **장점**
   - 시간 복잡도가 좋습니다. 
   - 힙 정렬이 유용한 경우는 전체 자료를 정렬하는 것이 아닌 가장 큰 값 몇개만 필요할 때입니다.

- **시간복잡도**
   - 힙 트리의 전체 높이가 거의 log₂n(완전 이진 트리이므로)이므로 하나의 요소를 힙에 삽입하거나 삭제할 때 힙을 재정비하는 시간이 log₂n만큼 소요된다.
   - 요소의 개수가 n개 이므로 전체적으로 O(nlog₂n)의 시간이 걸린다.
   - T(n) = O(nlog₂n)
   
</details>

### Q) 정렬의 `stable`과 `in-memory`의 개념을 말해주세요.
**Stable sort**
- Stable sort란 sorting을 할 경우에 같은 값의 숫자더라도 그 상대적인 위치가 유지되는 sorting 방식입니다.

| Stable sort | Unstable sort |
| ------------ | ------------- |
| Insertion Sort, Merge Sort, Bubble Sort, Counting Sort | Heap Sort, Selection sort, Quick Sort | 

**In-memory sort**
- In-memory sort란 추가적인 메모리가 거의 들지 않는 sorting 방식입니다.

| In-memory O | In-memory X |
| ------------ | ------------- |
| Insertion Sort, Selection Sort, Bubble Sort, Heap Sort, Quick Sort | Merge Sort ,Counting Sort, Radix Sort , Bucket Sort | 


### Q) 정렬 시 이진탐색을 사용할 수 있는데, 이진탐색은 중복된 갯수가 몇 개 있는지 추측할 수 없습니다. 이때 이진탐색 bound 개념을 사용해서 이진탐색에서 중복된 갯수를 알 수 있는 방법이 있을까요?
- lower bound
   - 타겟보다 같거나 큰 값이 나오는 처음 위치를 반환합니다.
- higher bound : 들어갈 수 있는 범위에서 처음으로 
   - 타겟보다 처음으로 큰 값이 나오는 위치를 반환합니다.
- 따라서 중복인 갯수를 구하기 위해서는 `higher bound - lower bound` 의 값을 반환하면 됩니다.  

### Q) Quick sort 의 pivot 선택 방식을 설명해주세요.
1. Random Pivot : Random으로 선택합니다. 
2. median - of - three :  random index 3개를 뽑은 후, 이 3개가 가리키는 원소들의 median 값으로 pivot을 설정합니다.

   ### Q-1) Quick sort는 항상 최적의 정렬 알고리즘인가요? 
   - 아닙니다. 이미 정렬된 상황이라면 선택 정렬이 더 유리 (O(N)) 합니다. 또한 Quick sort는 최악의 경우 O(N^2) 이기에 항상 최적이라고 할 수 없습니다. 

### Q) Merge sort는 항상 재귀적인 방법으로 구현하나요?
- 예
  ### Q-1) 모든 재귀는 재귀가 아닌 다른 방법으로 사용가능할까요?
  - 예
     ### Q-1-1) 비재귀로 구현할 수 있는데 재귀를 사용하는 이유는 무엇일까요?
     - 비재귀는 코드가 방대하고, 종료 조건이 존재하지 않을 시 코드를 어디까지 작성해야할 지 알 수 없기에 재귀를 사용하는 것이 유리한 경우가 있습니다. 

### Q) 계수 정렬은 어떤 조건에서만 진행 가능한가요?
- 계수 정렬은 인덱스로 구현됩니다. 따라서 양의 정수를 정렬할 시에만 사용가능합니다. 
- 숫자 범위가 너무 크면 배열이 지나치게 크게 만들어져 낭비되는 공간이 존재합니다. 
   - CountingSort는 빠르지만 추가적인 배열을 하나 만들어야 합니다.
   - 만약 int타입 배열에 { 1, 10, 1000000 }이 있다면 겨우 3개를 정렬하기 위하여 크기가 최소 1000001인 배열을 만들어야 합니다.
   - 정렬해야하는 배열의 크기가 작을 경우 이처럼 비효율적인 상황이  발생하기 때문에 어느정도 크기 이상일 경우에만 사용됩니다.

### Q) 병합 정렬과 퀵 정렬 둘 다 기존의 정렬을 작게 쪼개서 구현하는 것입니다. 그렇다면 이를 구현하는 방식의 차이는 무엇인가요?
- 병합 정렬은 추가적인 메모리를 요구하지만 퀵 정렬은 in place 정렬을 수행해 추가적인 메모리를 요구하지 않습니다.
- 퀵 정렬은 pivot을 기준으로 divide 한다면, 병합 정렬은 쪼갤 수 있는 크기까지 divide한다는 차이가 존재합니다. 

  ### Q-1) Linked List를 정렬할 시에 병합 정렬과 퀵 정렬 중 어느 것을 사용해서 정렬하는 것이 적합할까요?
  - Merge Sort가 유리합니다. 
  - Linked List는 삽입, 삭제 시에는 유리하지만 탐색 시에는 시간 복잡도가 큽니다. 

  ### Q-2) 병합 정렬을 구현할 때 Linked List와 Array로 각각 구현을 할 때 차이점에 대해 설명해주세요.
   - divide 후 merge 하는 과정에서 
      - Linked List는 연결된 포인터의 위치만 변경해주면 돼서 구현이 간단합니다.  
      - Array는 추가적인 배열 공간에서 이를 병합해야 합니다. 

### Q) JAVA의 Arrays.sort은 DualPivotQuick Sort, Collections.sort는 Tim Sort알고리즘을 사용합니다. 혹시 100만개의 데이터를 정렬하신다면 어떤 방식으로 정렬하시겠습니까? 
- DualPivotQuick는 자칫하면 최악의 경우 (O(N^2)) 시간 복잡도가 발생할 수 있기에, 자료형을 Reference type으로 변경 후 Tim Sort알고리즘(Merge + Selection)을 사용할 수 있도록 유도하는 것이 안정성 측면에서 좋습니다. 

<details>
<summary> Arrays.sort - Dual pivot quick sort </summary>

- 배열의 크기가 286이상일 경우 `MergeSort`를 수행합니다.
    - 깊이가 O(logN) 보다 깊어지는 경우

- 배열의 크기가 286보다 작은 경우 `QuickSort`를 MergeSort보다 우선 수행합니다.
    - 깊이가 O(logN) 보다 깊지 않은 경우 quick 이 더 빠릅니다.

- 배열의 크기가 47보다 작은 경우 `InsertionSort`를 QuickSort보다 우선 수행합니다.
    - 길이가 짧은 배열에 대해서는 참조지역성이 높은 삽입정렬이 우세합니다.
    - 또한 최선의 경우에는 O(N) 이라는 점에서 짧은 길이에는 삽입정렬 사용합니다.

- 일정 크기 이상의 BYTE, SHORT , CHAR 배열은 COUNTING SORT 가 수행됩니다.
    -  CountingSort를 byte, short, char 배열에서만 사용하는 이유는  이 자료형들은 크기가 작아 배열의 값으로 들어갈 범위가 작기 때문입니다. 
    - 따라서 CountingSort를 하기위해 추가하는 배열의 크기가 그만큼 작아지므로  효율이 올라갑니다. 
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/362d2e63-0d41-4069-9e4c-5c92fbf147e8/Untitled.png)
    
    - `byte배열`의 크기가 29보다 큰 경우 `CountingSort`를 `InsertionSort`보다 우선 수행합니다.
        - CountingSort는 빠르지만 추가적인 배열을 하나 만들어야 합니다.
        - 만약 int타입 배열에 { 1, 10, 1000000 }이 있다면 겨우 3개를 정렬하기 위하여 크기가 최소 1000001인 배열을 만들어야 합니다.
        - 정렬해야하는 배열의 크기가 작을 경우 이처럼 비효율적인 상황이  발생하기 때문에 어느정도 크기 이상일 경우에만 사용됩니다.
    - `short, char 배열`의 크기가 3200보다 큰 경우 `CountingSort`를 `QuickSort`보다 우선 수행합니다.
    
- 또한 이 경우 QUICK SORT 는 `DualPivotQuicksort`방법을사용합니다.
    - Pivot을 총 두 개를 선정, 영역을 세 개로 나눔으로써 분할의 이점을 더 높인 알고리즘
    - 기존의 SinglePivotQuicksort보다 더 많은 케이스에 대해서 O(nlogn)을 보장합니다.

</details>

### Q) Heap 정렬 시 이진 트리로 구현합니다. 이를 배열로 구현하며 어떻게 구현하나요?
- index를 이용해서 왼쪽, 오른쪽 자식 노드를 표기합니다.
- 왼쪽 노드 : 자기자신 idx * 2 
- 오른쪽 노드 : 자기자신 idx * 2 + 1
   ### Q-1) Heap 정렬의 시간 복잡도는 O(NlogN)
   - 이진 트리는 최대 높이가 O(logN) 입니다. 
   - N개의 원소를 정렬할 때 N개의 원소를 트리 루트로 올려주는 과정이 필요하기에 heapfiy를 N번 수행해주어야 합니다. 
   - 이때 heapfiy는 트리 높이 만큼인 O(logN)이 걸리는 데, 이를 N번 수행해주기에 N번*O(logN) <N번의 heapfiy>, 즉 O(NlogN)의 시간복잡도가 소요됩니다.

#### 사진 & 내용 출처

https://ko.wikipedia.org/wiki/%EC%A0%95%EB%A0%AC_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98

https://gmlwjd9405.github.io

https://underdog11.tistory.com
