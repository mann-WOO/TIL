# 병합정렬 (merge sort)

<br>

## 개요

- 분할 정복(divide and conquer): 문제를 작은 부분 문제로 나누어, 부분 문제를 해결하며 전체 문제를 해결
- 정렬 할 원소의 리스트를 반씩 나누는 것을 반복해 원소 단위까지 쪼개고, 다시  두 집단씩 정렬된 상태로 하나로 병합하면서 결과적으로 전체 리스트를 정렬한다.
- 함수로 구현 시, merge(병합) 함수를 구현하고, merge 함수를 이용해 sort(정렬, 분할) 함수를  완성한다.
- O(nlogn)의 시간 복잡도를 가진다. 

<br>

## 구현

### merge 함수

- 두 리스트를 인자로 받는다. (`left`, `right`로 설정)
- 각 리스트의 첫 번째 원소를 비교하여 작은 원소를 결과 리스트에 추가한다. 만약 `left `의 첫 번째 원소가 더 작아 해당 원소가 추가되었다면, 다음엔 `left`의 두 번째 원소와 `right`의 첫 번째 원소(아직 사용되지 않았기 때문에)를 비교하여 작은 쪽을 추가한다.
- 같은 방법을 반복해 두 리스트가 정렬된 상태로 병합된 하나의 리스트를 반환한다.

### sort 함수

- 중간점 (`mid = len(list)//2`) 을 설정한다.
- 중간점을 기준으로 왼쪽, 오른쪽 리스트를 재귀를 이용해 하나의 원소만 남을 때까지 분할한다.
- 왼쪽, 오른쪽 리스트에 merge 함수를 적용한 결과를 반환하며 거슬러 올라와 전체 리스트를 정렬한다.

<br>

```python
# python
# 병합 함수
def merge(left, right):
    # 결과로 반환할 리스트
    merged_list = []
    # 현재 확인중인 원소 인덱스를 표시한 _point
    left_point = 0
    left_len = len(left)
    right_point = 0
    right_len = len(right)
    # 왼쪽, 오른쪽에서 받은 리스트 둘 모두에 남은 원소가 있을 때
    while left_point != left_len and right_point != right_len:
        # 왼쪽에 첫 번째 원소가 오른쪽 첫 번째 원소보다 작거나 같을때
        if left[left_point] <= right[right_point]:
            # 결과 리스트에 추가, left_point를 한 칸 이동
            merged_list.append(left[left_point])
            left_point += 1
        # 오른쪽 첫 번째 원소가 더 작을 때
        else:
            # 결과 리스트에 추가, right_point를 한 칸 이동
            merged_list.append(right[right_point])
            right_point += 1
    # 왼쪽 리스트가 남아있을 때(오른쪽을 먼저 다 추가했을 때)
    if right_point == right_len:
        # 남은 원소를 모두 추가
        merged_list.extend(left[left_point:])
        # 결과 리스트를 반환
        return merged_list
    # 오른쪽 리스트가 남아있을 때
    else:
        # 남은 원소를 모두 추가
        merged_list.extend(right[right_point:])
        # 결과 리스트를 반환
        return merged_list


# 병합정렬 함수
def merge_sort(nums):
    # 원소의 수가 1개 이하라면 해당 리스트를 반환
    if len(nums) <= 1:
        return nums
    # 중간점 설정
    mid = len(nums) // 2
    # 왼쪽 리스트를 정렬
    left = merge_sort(nums[0:mid])
    # 오른쪽 리스트를 정렬
    right = merge_sort(nums[mid:len(nums)])
    # 병합한 리스트를 반환
    return merge(left, right)
```

