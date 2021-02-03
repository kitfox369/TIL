# 정렬

## 1. 선택 정렬

배열을 탐색해서 가장 작은 값을 보통 가장 고정되지 않은 왼쪽 값과 맞바꾼 후 바꿔진 왼쪽 자리를 고정하는 방식

![](../.gitbook/assets/1.png)

```text
void selectSort(int list[], int n)
{
    int i,j,least,temp;
    for(int i=0;i<n-1;i++){
        least=i;
        for(int j=i+1;j<n;j++){
            if(list[j]<list[least])
                least = j;
        }
        //탐색이 끝난 후 고정되지 않은 왼쪽 값과 맞바꿈
        temp = list[i];
        list[i] = list[least];
        list[least] = temp;
    }
} 
```

* 시간 복잡도 : 

$$
n(n-1)/2 = O(n^2)
$$

## 2. 삽입 정렬

고정된 앞의 배열의 Value값을 뒤에서부터 확인하여 

**자신보다 큰 경우** 배열을 한칸 뒤로 삽입한 후 계속 탐색하고

**자신보다 작은 경우** 해당 자리에 자신이 들어감

ex\)                                        \(4\)  : 2번째 자리 \(5\)와 비교해서 작으면  오른쪽으로 값을 옮긴 후 삽입

           \(3\) \(5\) \(4\) -&gt; \(3\) \(5\) \(4\) -&gt; \(3\) \(5\) \(5\) -&gt; \(3\) \(4\) \(5\)

![](../.gitbook/assets/image%20%282%29.png)

```text
void insertSort(int list[], int n)
{
    int i,j,key;
    for(int i=1;i<n;i++){
        key = list[i];
        for(int j=i-1;j>=0&&list[j]>key;j--){
            list[j+1] = list[j];
        }
        list[j+1] = key;
    }
}
```

