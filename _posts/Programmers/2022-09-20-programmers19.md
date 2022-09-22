---
title:  "[Programmers] N개의 최소공배수"
excerpt: "코딩테스트 연습 : :star: :star:  "

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2022-09-20
last_modified_at: 2022-09-20
---


# 0. 문제 설명


두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.
<br><br>

**제한 조건**

- arr은 길이 1이상, 15이하인 배열입니다.
- arr의 원소는 100 이하인 자연수입니다.

<br>

## 입출력 예

|arr | result |
|---|---|
|[2,6,8,14]|168|
|[1,2,3]|	6|

<br>



<br>

# 1. 풀이 정리


```python
def gcd(a, b):
    return b if a % b == 0 else gcd(b, a % b)
def lcm(a, b):
    return int(a * b / gcd(a, b))

def solution(arr):
    if len(arr) == 1 :
        return arr[0]
    else : 
        LCM = lcm(arr[0],arr[1])
        for i in arr[2:] : 
            LCM = lcm(LCM,i)
    return LCM
```


<br>
