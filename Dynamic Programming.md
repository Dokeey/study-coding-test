# 코딩테스트 알고리즘

## 동적 프로그래밍

### 개념

하나의문제는 단 한 번만 풀도록 하는 알고리즘

즉, 한 번 푼 것을 여러 번 다시 푸는 비효율적인 알고리즘을 개선시키는 방법이기도 함

분할 정복 기법은 동일한 문제를 다시 푼다는 단점이 있다.(정렬 제외)

단순 분할 정복으로 풀게 되면 심각한 비효율성을 낳는 대표적인 예시로 피보나치 수열

DP는 다음의 가정 하에 사용할 수 있다.

- 큰 문제를 작은 문제로 나눌 수 있다.
- 작은 문제에서 구한 정답은 그것을 포함하는 큰 문제에서도 동일하다.

EX) 메모이제이션 기법



### 문제

### 정수 삼각형

> 출처: 프로그래머스

#### 문제 설명

![스크린샷 2018-09-14 오후 5.44.19.png](https://grepp-programmers.s3.amazonaws.com/files/production/97ec02cc39/296a0863-a418-431d-9e8c-e57f7a9722ac.png)

위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다. 아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.

삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

#### 제한사항

- 삼각형의 높이는 1 이상 500 이하입니다.
- 삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.



#### CODE

```python
def get_sum(triangle, sum_list, index, child):
    len_triangle = len(triangle)
    if len_triangle == index + 1:
        return triangle[index][child]

    if not sum_list[index][child] == '':
        return sum_list[index][child]
    sum_list[index][child] = triangle[index][child] + max(get_sum(triangle, sum_list, index + 1, child), get_sum(triangle, sum_list, index + 1, child + 1))
    return sum_list[index][child]


def solution(triangle):
    sum_list = [['' for _ in rows] for rows in triangle]
    return get_sum(triangle, sum_list, 0, 0)
```

