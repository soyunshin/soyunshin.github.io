---
title:  "[Programmers] 소수 만들기"
excerpt: "코딩테스트 연습"

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2022-07-27
last_modified_at: 2022-08-03
---


# 0. 문제 설명

주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 
숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

<br>

**제한 조건**

- nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.
- nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.


<br>

**입출력 예**

|nums | result |
|---|---|
|[1,2,3,4] | 1 |
|[1,2,7,6,4] | 4 |



<br>

**입출력 예 설명**

** 입출력 예 01 **
- [1,2,4]를 이용해서 7을 만들 수 있습니다.

<br>

** 입출력 예 02 **
- [1,2,4]를 이용해서 7을 만들 수 있습니다.
- [1,4,6]을 이용해서 11을 만들 수 있습니다.
- [2,4,7]을 이용해서 13을 만들 수 있습니다.
- [4,6,7]을 이용해서 17을 만들 수 있습니다.


<br>

## 1. 풀이 정리

```python
from itertools import combinations

def solution(nums):
    ans = list(map(lambda  x : sum(x) , list(combinations(nums,3))))
    
    a = ans.copy()
    
    for j in ans :
        for i in range(2, j) :
            if j % i == 0 :
                a.remove(j)
                break

    answer = len(a)
    
    
    return answer
```


<br>

## 새롭게 알게된 내용

itertools 모듈의 permutations, combinations