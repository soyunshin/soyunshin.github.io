---
title:  "[Programmers] 숫자의 표현"
excerpt: "코딩테스트 연습 : :star: :star:  "

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2022-09-18
last_modified_at: 2022-09-18
---


# 0. 문제 설명


Finn은 요즘 수학공부에 빠져 있습니다. 수학 공부를 하던 Finn은 자연수 n을 연속한 자연수들로 표현 하는 방법이 여러개라는 사실을 알게 되었습니다. 예를들어 15는 다음과 같이 4가지로 표현 할 수 있습니다.<br>

- 1 + 2 + 3 + 4 + 5 = 15
- 4 + 5 + 6 = 15
- 7 + 8 = 15
- 15 = 15

자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return하는 solution를 완성해주세요.
<br>

**제한 조건**

- n은 10,000 이하의 자연수 입니다.

<br>

## 입출력 예

|n | result |
|---|---|
|15 |	4|

<br>



<br>

# 1. 풀이 정리


```python
def solution(n):
    cnt = 0
    for i in range(1,n+1) :
        sum = 0
        for j in range(i,n+1) : 
            sum += j
            if sum == n :
                cnt += 1
                break
            elif sum > n :
                break
    return cnt
```


<br>
