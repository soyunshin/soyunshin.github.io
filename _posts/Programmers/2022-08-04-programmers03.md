---
title:  "[Programmers] 모의고사"
excerpt: "코딩테스트 연습-완전탐색"

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2022-08-04
last_modified_at: 2022-08-04
---


# 0. 문제 설명

수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.
<br>
1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...<br>
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...<br>
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...<br>
<br>
1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

<br>

**제한 조건**

- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

<br>

**입출력 예**

|answers | return |
|---|---|
|[1,2,3,4,5]| [1] | 
|[1,3,2,4,2] | [1,2,3]|

**입출력 예 설명**

** 입출력 예 01 **
- 수포자 1은 모든 문제를 맞혔습니다.
- 수포자 2는 모든 문제를 틀렸습니다.
- 수포자 3은 모든 문제를 틀렸습니다.

따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.

<br>

** 입출력 예 02 **
- 모든 사람이 2문제씩을 맞췄습니다.


<br>

## 1. 풀이 정리

```python
p1 = [1,2,3,4,5]
p2 = [2,1,2,3,2,4,2,5]
p3 = [3,3,1,1,2,2,4,4,5,5]

def solution(answers):
    p11 = p1*(len(answers)//len(p1)) + p1[:(len(answers)%len(p1))]
    p22 = p2*(len(answers)//len(p2)) + p2[:(len(answers)%len(p2))]
    p33 = p3*(len(answers)//len(p3)) + p3[:(len(answers)%len(p3))]
    
    p = [0,0,0]
    for i in range(len(answers)) : 
        if answers[i] == p11[i] : 
            p[0] += 1
        if answers[i] == p22[i] : 
            p[1] += 1
        if answers[i] == p33[i] : 
            p[2] += 1
    
    answer = [x for x in range(1,4) if max(p) == p[x-1]]
    return answer
```


<br>
