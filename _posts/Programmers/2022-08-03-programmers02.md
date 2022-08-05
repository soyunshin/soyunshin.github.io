---
title:  "[Programmers] 최대공약수와 최소공배수"
excerpt: "코딩테스트 연습"

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2022-08-03
last_modified_at: 2022-08-03
---


# 최대공약수와 최소공배수

**문제 설명**

두 수를 입력받아 두 수의 최대공약수와 최소공배수를 반환하는 함수, solution을 완성해 보세요. <br>
배열의 맨 앞에 최대공약수, 그다음 최소공배수를 넣어 반환하면 됩니다. <br>
예를 들어 두 수 3, 12의 최대공약수는 3, 최소공배수는 12이므로 solution(3, 12)는 [3, 12]를 반환해야 합니다.

<br>

**제한 조건**

- 두 수는 1이상 1000000이하의 자연수입니다.


<br>

**입출력 예**

|n | m | return |
|---|---|---|
|3 | 12 | [3, 12]|
|2 | 5 | [1, 10]|




<br>

## 1. 풀이 정리

```python
def solution(n, m):
    # 최대 공약수
    n1 = [x for x in range(1,n//2+1) if n%x == 0] + [n]
    m1 = [x for x in range(1,m//2+1) if m%x == 0] + [m]
    max_num = 1
    for i in n1 : 
        for j in m1 : 
            if i == j : 
                max_num = i    

    # 최소 공배수
    min_num = n*m
    n2 = [n*i for i in range(1,m+1)]
    m2 = [m*i for i in range(1,n+1)]
    min_num1 = min_num
    for i in n2 : 
        for j in m2 : 
            if i == j : 
                min_num1 = i
                break
        if min_num1 < min_num : 
            min_num = min_num1
            break
    
    answer = [max_num, min_num]
    return answer
```


<br>

## 2. 다른 사람의 풀이
두 수의 크기 비교를 통해 보다 간단한 코드를 작성할 수 있다.

```python
def solution(a, b):
    c, d = max(a, b), min(a, b)
    t = 1
    while t > 0:
        t = c % d
        c, d = d, t
    answer = [c, int(a*b/c)]

    return answer
```
<br>

lambda 함수를 사용하면 더욱 더 간결한 코드 작성이 가능하다.

```python
def solution(n, m):
    gcd = lambda a,b : b if not a%b else gcd(b, a%b)
    lcm = lambda a,b : a*b//gcd(a,b)
    return [gcd(n, m), lcm(n, m)]
```