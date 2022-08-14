---
title:  "[Programmers] 숫자 문자열과 영단어"
excerpt: "코딩테스트 연습" :star:

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2022-08-14
last_modified_at: 2022-08-14
---


# 숫자 문자열과 영단어

**문제 설명**

네오와 프로도가 숫자놀이를 하고 있습니다. <br>
네오가 프로도에게 숫자를 건넬 때 일부 자릿수를 영단어로 바꾼 카드를 건네주면 프로도는 원래 숫자를 찾는 게임입니다.

<br>

다음은 숫자의 일부 자릿수를 영단어로 바꾸는 예시입니다.

- 1478 → "one4seveneight"
- 234567 → "23four5six7"
- 10203 → "1zerotwozero3"

<br>

이렇게 숫자의 일부 자릿수가 영단어로 바뀌어졌거나, 혹은 바뀌지 않고 그대로인 문자열 s가 매개변수로 주어집니다. <br>
s가 의미하는 원래 숫자를 return 하도록 solution 함수를 완성해주세요.<br>

참고로 각 숫자에 대응되는 영단어는 다음 표와 같습니다.


|숫자|영단어|
|---|---|
|0|	zero|
|1|	one|
|2|	two|
|3|	three|
|4|	four|
|5|	five|
|6|	six|
|7|	seven|
|8|	eight|
|9|	nine|


<br>



**제한 조건**

- 1 ≤ `s`의 길이 ≤ 50
- `s`가 "zero" 또는 "0"으로 시작하는 경우는 주어지지 않습니다.
- return 값이 1 이상 2,000,000,000 이하의 정수가 되는 올바른 입력만 `s`로 주어집니다.

<br>

## 입출력 예

|s|result|
|---|---|
|"one4seveneight"|1478|
|"23four5six7"|234567|
|"2three45sixseven"|234567|
|"123"|123|


## 입출력 예 #1
- 문제 예시와 같습니다.

<br>

## 입출력 예 #2
- 문제 예시와 같습니다.

<br>

## 입출력 예 #3
- "three"는 3, "six"는 6, "seven"은 7에 대응되기 때문에 정답은 입출력 예 #2와 같은 234567이 됩니다.
- 입출력 예 #2와 #3과 같이 같은 정답을 가리키는 문자열이 여러 가지가 나올 수 있습니다.

<br>

## 입출력 예 #4
- s에는 영단어로 바뀐 부분이 없습니다.

<br>

# 1. 풀이 정리

먼저 숫자에 대응하는 영단어 리스트`str_l`를 생성한다.
`str_l`을 사용해 영단어와 숫자가 대응되는 딕셔너리를 생성한다.
입력 문자열 `s`에 영단어가 존재한다면, 숫자로 변경한다.

<br>


```python
str_l = ['zero','one','two','three','four','five','six','seven','eight','nine']
dic = {string : i for i,string in enumerate(str_l)}
def solution(s):
    for i in dic.items() :
        if i[0] in s : 
            s = s.replace(i[0], str(i[1]))
    answer = int(s)
    return answer
```


<br>
