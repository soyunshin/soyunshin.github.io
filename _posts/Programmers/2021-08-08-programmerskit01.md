---
title:  "[Programmers] 코딩테스트 고득점 Kit Hash 01"
excerpt: "Hash 01 완주하지 못한 선수"

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2021-08-08
last_modified_at: 2021-08-08
---


# 완주하지 못한 선수
**문제 설명** <br>
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

<br>

**제한 사항**

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

<br>

**입출력 예시**

![image](https://user-images.githubusercontent.com/70592135/128622737-37683c81-4683-4c18-9dfe-c52da0a8b8cf.png)


**입출력 예 설명**

예제 #1 <br>
"leo"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #2 <br>
"vinko"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #3 <br>
"mislav"는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.

<br>

---


## 1. 풀이

```python
def solution(participant, completion):
    participant.sort()
    completion.sort()
    completion.append('1')
    for i in range(len(participant)):
        if participant[i]!=completion[i]:
            answer = participant[i]
            break
    return answer
```


## 2. Hash를 이용한 풀이

```python
import collections

def solution(participant, completion):
    answer = collections.Counter(participant) - collections.Counter(completion)
    return list(answer.keys())[0]
```