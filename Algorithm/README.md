# 알고리즘

어떤 일을 해결하려는 방법과 절차라

## 조건

- 입력: 제공되는 자료가 0개 이상 존재 해야 한다.
- 출력: 2개 이상의 서로 다른 결과를 내어야 한다.
- 명확성: 무엇을 하기 위한 것인지 명확하게 정의되어야 한다.
- 유한성: 알고리즘의 명령어대로 수행했을 때 처리도니 후 종료 되어야 한다.
- 효율성: 명백하게 실행 가능한 것이며 시공간적 효율성을 가진다.

## 정렬 알고리즘

### 선택 정렬

현재 위치에 들어갈 값을 찾아 정렬하는 배열

- 시간 복잡도: O(N ^ 2)
- 공간 복잡도: O(N)

```JAVA

void Selection(int[] data){
    for(int i = 0; i < data.length; i++){
        int temp = i
        for(int j = i + 1; j < data.length; j++){
            if(data[temp] >= data[j]){
                temp = j;
            }
            swap(data[i], data[temp])
        }
    }
}

```

### 삽입 정렬

현재 위치에서 배열들을 비교하여 자신이 들어갈 위치를 찾아 위치에 삽입하는 배열 알고리즘

- 시간 복잡도: O(N ^ 2)
  - 최소: O(N) (이미 정렬된 경우)
- 공간 복잡도: O(N)

```JAVA

void Insertion(int[] data){
    for(int i = 1; i < data.length; i++){
        int key = data[i];
        int j = i - 1;
        while(j >= 0 && key < data[j]){
            swap(data[j], data[j + 1]);
            j--;
        }
        v[j + 1] = key;
    }
}

```

### 버블 정렬

매번 연속된 두 개 인덱스를 비교하여, 정한 기준의 값을 뒤로 넘겨 정렬하는 방법

- 시간 복잡도: O(N ^ 2)
- 공간 복잡도: O(N)

```JAVA

void Bubble(int[] data){
    for(int i = 0; i < data.length; i++){
        for(int j = 1; j < data.length - i; j++){
            if(data[j - 1] > data[j]){
                swap(data[j - 1], data[j])
            }
        }
    }
}

```

### 합병 정렬

분할 정복 방식으로 연산 중에서 두 개의 배열을 계속 쪼개 나간후 합쳐가면서 하나의 정렬을 출력

- 시간 복잡도: O(NLogN)
- 공간 복잡도: O(2N)

```JAVA

MergeSort(0, data.length - 1);

void MergeSort(int start, int end){
    if(start < end){
        int mid = (start + end) / 2;
        MergeSort(start, mid);
        MergeSort(mid + 1, end);
        Merge(data, start, end, mid)
    }
}

void Merge(int[] data, int start, int end, int mid){
    ArrayList<Int> temp = new ArrayList<>();

    int i = start;
    int j = mid + 1,
    while(i <= mid && j <= end){
        if(data[i] < data[j]){
            temp.add(data[i++]);
        } else{
            temp.add(data[j++]);
        }
    }

    while(i <= mid) temp.add(data[i++]);
    while(j <= end) temp.add(data[j++]);

    for(int x = start; x <= end; x++){
        data[x] = temp.get(x - start);
    }
}

```

### 퀵 정렬

pivot point라고 기준이 되는 값을 하나 설정하고, 그 값을 기준으로 좌우로 값을 옮기는 방식을 통해서 정렬

- 시간 복잡도: O(NlogN)
  - 최악: O(N ^ 2): (이미 정렬되어 잇는 경우)
  - 최악인 경우 전체 데이터를 랜덤으로 설정하여 사용하면 평균으로 돌아온다.
- 공간 복잡도: O(N)

```JAVA
void Quick(int[] data, int start, int end){
    int pivot = data[start];
    int left = start;
    int right = end;
    while(left < right){
        while(pivot <= data[right] && left< right) right--;
        if(left > right) break;
        while(pivot <= data[left] && left< right>) left++;
        if(left > right) break;
        swap(data[left], data[right]);
    }

    swap(data[start], data[left]);

    if(start < left){
        Quick(data, start, left - 1);
    }
    if(end > right){
        Quick(data, left + 1, end);
    }
}


```
