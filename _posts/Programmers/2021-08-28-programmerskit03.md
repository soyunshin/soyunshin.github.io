---
title:  "[Programmers] 코딩테스트 고득점 Kit Hash 03"
excerpt: "Hash 03 위장"

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2021-08-28
last_modified_at: 2021-08-28
---


# 위장

**문제 설명**

스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다.

예를 들어 스파이가 가진 옷이 아래와 같고 오늘 스파이가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야 합니다.

<br>

|종류|	이름|
|---|---|
|얼굴|	동그란 안경, 검정 선글라스|
|상의|	파란색 티셔츠|
|하의|	청바지|
|겉옷|	긴 코트|

<br>

스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.

<br>

**제한사항**
* clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
* 스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.
* 같은 이름을 가진 의상은 존재하지 않습니다.
* clothes의 모든 원소는 문자열로 이루어져 있습니다.
* 모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '_' 로만 이루어져 있습니다.
* 스파이는 하루에 최소 한 개의 의상은 입습니다.

<br>

**입출력 예**
|clothes|	return|
|---|---|
|[["yellowhat", "headgear"], ["bluesunglasses", "eyewear"], ["green_turban", "headgear"]]	|5|
|[["crowmask", "face"], ["bluesunglasses", "face"], ["smoky_makeup", "face"]]	|3|


<br>

**입출력 예 설명** 

예제 #1

headgear에 해당하는 의상이 yellow_hat, green_turban이고 eyewear에 해당하는 의상이 blue_sunglasses이므로 아래와 같이 5개의 조합이 가능합니다.

```python
1. yellow_hat
2. blue_sunglasses
3. green_turban
4. yellow_hat + blue_sunglasses
5. green_turban + blue_sunglasses
```

<br>

예제 #2

face에 해당하는 의상이 crow_mask, blue_sunglasses, smoky_makeup이므로 아래와 같이 3개의 조합이 가능합니다.

```python
1. crow_mask
2. blue_sunglasses
3. smoky_makeup
```

<br>

## 1. 풀이 정리

```python
from collections import Counter

def solution(clothes):
    kind = Counter([cloth[1] for cloth in clothes])
    answer = 1
    for i in kind :
        answer *= (kind[i]+1)
    
    answer -= 1
    return answer
```


```
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```

의상 종류별로 짝지어질 경우의 수를 계산하면된다.<br>
의상이 A, B가 있고, 각각 2개, 1개 가지고 있다면
다음과 같이 5가지 의상을 선택하는 경우가 발생한다.
```
[A1], [A2], [B1], [A1, B1], [A2, B1]
```

따라서 의상의 종류에 선택하지 않는 경우도 포함시키도록 한다.

```
A : [선택x, A1, A2]
B : [선택x, B1]
```
마지막으로 A, B 모두 `[선택x, 선택x]`일 경우를 제외하면

(A의 개수) x (B의 개수) - 1 = 5 의 경우의 수가 존재한다.

이와 같은 방식으로 함수를 작성한다.


## 2. 다른 사람의 풀이

```python
def solution(clothes):
    from collections import Counter
    from functools import reduce
    cnt = Counter([kind for name, kind in clothes])
    answer = reduce(lambda x, y: x*(y+1), cnt.values(), 1) - 1
    return answer

```



# 새롭게 알게된 내용

collections 모듈

참고 : https://wikidocs.net/84392

