# sorting

## `sorted()`

> 정렬된 `list` 클래스의 자료형을 반환하는 함수

### key

- 정렬의 기준이 되는 함수를 지정해준다. 리스트에 속한 요소들에 해당 함수를 적용한 결과값을 기준으로 정렬

```python
a = ['a', 'bc', 'def', 'gh', 'i']
print(sorted(a))
# => ['a', 'bc', 'def', 'gh', 'i']
print(sorted(a, key=len))
# => ['a', 'i', 'bc', 'gh', 'def']
```

- `lambda` 정렬의 기준으로 리스트에 속한 요소들의 인덱스로 접근하여 사용 가능. 혹은 그 요소가 instance attribute를 가진다면 이 또한 사용가능.

```python
b = [5, 8, 6, 2, 5, 9, 1, 2, 5]
e = list(enumerate(b))
print(sorted(e, key=lambda x: x[1]))
# => [(6, 1), (3, 2), (7, 2), (0, 5), (4, 5), (8, 5), (2, 6), (1, 8), (5, 9)]
```

