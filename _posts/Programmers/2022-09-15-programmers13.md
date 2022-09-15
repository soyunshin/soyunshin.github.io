---
title:  "[Programmers] 최댓값과 최솟값"
excerpt: "코딩테스트 연습 : :star: :star:  "

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2022-09-15
last_modified_at: 2022-09-15
---


# 0. 문제 설명


문자열 s에는 공백으로 구분된 숫자들이 저장되어 있습니다. <br>
str에 나타나는 숫자 중 최소값과 최대값을 찾아 이를 "(최소값) (최대값)"형태의 문자열을 반환하는 함수, solution을 완성하세요.<br>
예를들어 s가 "1 2 3 4"라면 "1 4"를 리턴하고, "-1 -2 -3 -4"라면 "-4 -1"을 리턴하면 됩니다.
<br>

**제한 조건**

- s에는 둘 이상의 정수가 공백으로 구분되어 있습니다.

<br>

## 입출력 예

|s|return|
|---|---|
|"1 2 3 4" | "1 4" |
|"-1 -2 -3 -4" | "-4 -1" |
|"-1 -1" | "-1 -1"|

<br>



<br>

# 1. 풀이 정리


```python
def solution(s):
    int_s = list(map(int,s.split(' ')))
    answer = str(min(int_s))+ " " +str(max(int_s))
    return answer
```


<br>
