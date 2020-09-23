# 코딩테스트 알고리즘

## 1. 그리디

### 개념

기본적으로 당장 눈앞의 최적의 해를 쫓는 알고리즘.

무조건 큰 경우대로, 무조건 작은 경우대로, 무조건 긴 경우대로, 무조건 짧은 경우대로 등 극단적으로 문제에 접근한다는 점에서 정렬 기법이 함께 사용되는 경우가 많음.

대표적으로 크루스칼 알고리즘으로 모든 간선을 정렬한 이후에 짧은 간선부터 연결하는 최소 비용 신장 트리 알고리즘이 있음.

최적의 해를 보장하지 못하는 경우 다이나믹 프로그래밍 등의 기타 알고리즘 기법을 적용해야 하기도 함.

### 대표문제

#### 거스름돈 구하기

```python
def get_coin_count(change):
    coin_count = 0
    coin_count += int(change / 500)
    change %= 500
    coin_count += int(change / 100)
    change %= 100
    coin_count += int(change / 50)
    change %= 50
    coin_count += int(change / 10)
    change %= 10

    return coin_count


# 거스름돈 총 1260원
print(get_coin_count(1260))
>> 6
```



### 큰 수 만들기 문제

> 출처 : 프로그래머스

#### 문제 설명
어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

#### 제한 조건
number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
k는 1 이상 number의 자릿수 미만인 자연수입니다.

#### code

```python
# 정당성: 매 자리에 k 보다 작은 index를 가지는 최대값을 찾는다

def solution(number, k):
    result = []
    while k:
        # 매 자리수에 올 최대값 구하기
        max_num = -1
        for idx in range(k+1):
            if int(max_num) < int(number[idx]):
                max_num = number[idx]
                i = idx
                if max_num == '9':
                    break

        # 최대값을 결과에 넣고 다음 최대값 구할 준비
        result.append(max_num)
        number = number[i+1:]
        k = k - i
        
        # 예외 : 남은 number 개수가 k 값과 같다면 모두 없앤다.
        if len(number) == k:
            number = ''
            k = 0
    
    return "".join(result) + number
```



