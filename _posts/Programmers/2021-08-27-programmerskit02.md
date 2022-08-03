---
title:  "[Programmers] 코딩테스트 고득점 Kit Hash 02"
excerpt: "Hash 02 전화번호 목록"

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2021-08-27
last_modified_at: 2021-08-28
---


# 전화번호 목록

**문제 설명**

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.


- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421


전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

<br>

**제한 사항**

* phone_book의 길이는 1 이상 1,000,000 이하입니다.
    * 각 전화번호의 길이는 1 이상 20 이하입니다.
    * 같은 전화번호가 중복해서 들어있지 않습니다.

<br>

**입출력 예제**

|phone_book	| return|
|---|---|
|["119", "97674223", "1195524421"] | false|
|["123","456","789"]	|true|
|["12","123","1235","567","88"]	|false|


<br>


**입출력 예 설명**

입출력 예 #1
앞에서 설명한 예와 같습니다.

입출력 예 #2
한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 true입니다.

입출력 예 #3
첫 번째 전화번호, “12”가 두 번째 전화번호 “123”의 접두사입니다. 따라서 답은 false입니다.



## 1. 풀이 정리

```python
def solution(phone_book):
    a = []
    for j in range(len(phone_book)) :
        for i in range(len(phone_book)) :
            if i != j :
                a.append(phone_book[i].startswith(phone_book[j]))
    
    if True in a: 
        answer = False
    else: 
        answer = True

    return answer
```
```
채점 결과
정확성: 83.3
효율성: 0.0
합계: 83.3 / 100.0
```

<br>

## 2. 풀이 정리

```python
def solution(phone_book):
    for j in range(len(phone_book)) :
        for i in range(len(phone_book)) :
            if i != j :
                if phone_book[i].startswith(phone_book[j]) :
                    return False
                
    return True
```

```
채점 결과
정확성: 83.3
효율성: 8.3
합계: 91.7 / 100.0
```

<br>

## 3. 풀이 정리 (정답)

```python
def solution(phone_book):
    phone_book.sort()
    for i in range(len(phone_book)-1) :
        if phone_book[i+1].startswith(phone_book[i]) :
            return False
                
    return True
```
```
채점 결과
정확성: 83.3
효율성: 16.7
합계: 100.0 / 100.0
```


## 4. 다른 사람의 풀이

```python
def solution(phone_Book):
    phone_Book.sort()

    for p1, p2 in zip(phone_Book, phone_Book[1:]):
        if p2.startswith(p1):
            return False
    return True
```

1. `sort`를 통해 같은 접두어를 가진 문자열끼리 모이도록 정렬이 된다.
2. `zip`함수를 사용해서 서로 붙어 있는 문자열끼리 접두어인지 검사한다.


<br>
<br>


# 새롭게 알게된 내용

## 1. 접두어 검사 함수 : `startswith`
```python
a = "1195524421"
a.startswith("11")
```

```
True
```

<br>

## 2. break
`break`는 하나의 반복문을 빠져나올 수 있다.

<br>

## 3. for문
2중 for문보다 sort로 리스트를 정렬한 다음 비교하면 속도가 훨씬 빠르다.


