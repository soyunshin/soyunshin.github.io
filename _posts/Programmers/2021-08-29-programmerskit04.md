---
title:  "[Programmers] 코딩테스트 고득점 Kit Hash 04"
excerpt: "Hash 04 베스트 앨범"

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2021-08-29
last_modified_at: 2021-08-29
---


# 베스트 앨범

**문제 설명**

스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.

1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.

노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

<br>

**제한사항**

- genres[i]는 고유번호가 i인 노래의 장르입니다.
- plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
- genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
- 장르 종류는 100개 미만입니다.
- 장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
- 모든 장르는 재생된 횟수가 다릅니다.


<br>

**입출력 예**

|genres	|plays|	return|
|---|---|---|
|["classic", "pop", "classic", "classic", "pop"]|	[500, 600, 150, 800, 2500]|	[4, 1, 3, 0]|

<br>

**입출력 예 설명**

classic 장르는 1,450회 재생되었으며, classic 노래는 다음과 같습니다.

- 고유 번호 3: 800회 재생
- 고유 번호 0: 500회 재생
- 고유 번호 2: 150회 재생

pop 장르는 3,100회 재생되었으며, pop 노래는 다음과 같습니다.

- 고유 번호 4: 2,500회 재생
- 고유 번호 1: 600회 재생

따라서 pop 장르의 [4, 1]번 노래를 먼저, classic 장르의 [3, 0]번 노래를 그다음에 수록합니다.


<br>

## 1. 풀이 정리

```python
def solution(genres, plays):
    all_dict = {}
    together = []
    answer = []
    
    for i in range(len(genres)):
        together.append((genres[i],plays[i],i))
        all_dict[genres[i]] = 0
        
    for i in range(len(genres)) :
        all_dict[genres[i]] += plays[i]    
        
    maxkey = list(dict(sorted(all_dict.items(), key=lambda x: x[1], reverse=True)).keys())
    
    together = sorted(together, key = lambda x : x[1], reverse = True)
    
    for k in maxkey:
        count = 0
        for j in range(len(together)):
            if count < 2:
                if together[j][0] == k:
                    count += 1
                    answer.append(together[j][2])
            else:
                continue

    return answer
```

```
채점 결과
정확성: 100.0
합계: 100.0 / 100.0
```



## 2. 다른 사람의 풀이


```python
def solution(genres, plays):
    answer = []
    d = {e:[] for e in set(genres)}
    for e in zip(genres, plays, range(len(plays))):
        d[e[0]].append([e[1] , e[2]])
    genreSort =sorted(list(d.keys()), key= lambda x: sum( map(lambda y: y[0],d[x])), reverse = True)
    for g in genreSort:
        temp = [e[1] for e in sorted(d[g],key= lambda x: (x[0], -x[1]), reverse = True)]
        answer += temp[:min(len(temp),2)]
    return answer
```


# 새롭게 알게된 내용

lambda 함수