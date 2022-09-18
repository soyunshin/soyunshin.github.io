---
title:  "[Programmers] 피보나치 수"
excerpt: "코딩테스트 연습 : :star: :star:  "

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2022-09-19
last_modified_at: 2022-09-19
---


# 0. 문제 설명


피보나치 수는 F(0) = 0, F(1) = 1일 때, 1 이상의 n에 대하여 F(n) = F(n-1) + F(n-2) 가 적용되는 수 입니다.<br>
예를들어

- F(2) = F(0) + F(1) = 0 + 1 = 1
- F(3) = F(1) + F(2) = 1 + 1 = 2
- F(4) = F(2) + F(3) = 1 + 2 = 3
- F(5) = F(3) + F(4) = 2 + 3 = 5

와 같이 이어집니다.<br><br>

2 이상의 n이 입력되었을 때, n번째 피보나치 수를 1234567으로 나눈 나머지를 리턴하는 함수, solution을 완성해 주세요.
<br>

**제한 조건**

- n은 2 이상 100,000 이하인 자연수입니다.

<br>

## 입출력 예

|n | result |
|---|---|
|3 |2|
|5 |5|

<br>



<br>

# 1. 풀이 정리


```python
def solution(n):
    l = [0,1]
    for i in range(2,n+1) : 
        new = l[i-2] + l[i-1]
        l.append(new)
    return l[n] % 1234567
```


<br>
