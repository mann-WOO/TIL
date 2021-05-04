# 퀵 소트 (quick sort)

<br>

## 개요

- 병합 정렬(merge sort)와 마찬가지로 분할 정복의 개념을 이용한 정렬법이다.
- 리스트 안의 한 원소인 피벗(pivot)을 기준으로, 피벗보다 작은 원소는 왼쪽으로, 피벗보다 큰 원소는 오른쪽으로 이동시킨다. 그 다음 피벗을 기준으로 왼쪽, 오른쪽 리스트를 분할하여 재귀 호출을 이용해 양쪽의 리스트에서 다시 피벗을 기준으로 정렬을 반복한다.
- 피벗을 설정하는 방법도 여러가지가 있지만, 본 구현에서는 가장 왼쪽의 원소를 피벗으로 설정하고 이를 기준값으로 하여 그 뒤의 원소들을 정렬 한 뒤, 피벗 원소를 분기점(왼쪽은 피벗보다 작은 값들, 오른쪽은 피벗보다 큰 값들)으로 옮겨주는 방식을 사용한다.
- 평균 O(nlogn)의 시간복잡도를 가진다. 최악의 경우 O(n^2)의 시간 복잡도를 가진다.

<br>

## 구현

```python
# 피벗 위치가 정해질 때까지 정렬하고, 피벗 인덱스를 반환하는 함수
def get_pivot(nums, start, end):
    # 첫 번째 원소를 피벗으로 설정
    pivot = nums[start]
    left = start + 1
    right = end

    # left, right가 교차하지 않는 동안 반복
    while left <= right:
        # left를 피벗 값과 비교하면서 한 칸씩 오른쪽으로, 피벗 값보다 크다면 멈춘다.
        while left <= N-1 and nums[left] <= pivot:
            left += 1
        # right를 피벗 값과 비교하면서 한 칸씩 왼쪽으로, 피벗 값 이하일 때 멈춘다
        while right >= 0 and nums[right] > pivot:
            right -= 1
        # 교차하지 않았다면 left, right를 교환
        if left < right:
            nums[left], nums[right] = nums[right], nums[left]
    # 교차했을 때 피벗과 right를 교환
    nums[start], nums[right] = nums[right], nums[start]

    # right를 피벗 위치로 반환
    return right


# 퀵 정렬 함수
def quick_sort(nums, start, end):
    if start < end:
        # 피벗 위치를 구하고
        pivot = get_pivot(nums, start, end)
        # 왼쪽, 오른쪽을 나누어 퀵정렬 실행
        quick_sort(nums, start, pivot-1)
        quick_sort(nums, pivot+1, end)
```

