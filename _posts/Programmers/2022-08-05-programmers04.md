---
title:  "[Programmers] 신고 결과 받기"
excerpt: "코딩테스트 연습"

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2022-08-05
last_modified_at: 2022-08-05
---


# 신고 결과 받기

**문제 설명**

신입사원 무지는 게시판 불량 이용자를 신고하고 처리 결과를 메일로 발송하는 시스템을 개발하려 합니다. 무지가 개발하려는 시스템은 다음과 같습니다.

- 각 유저는 한 번에 한 명의 유저를 신고할 수 있습니다.
신고 횟수에 제한은 없습니다. 서로 다른 유저를 계속해서 신고할 수 있습니다.
한 유저를 여러 번 신고할 수도 있지만, 동일한 유저에 대한 신고 횟수는 1회로 처리됩니다.
- k번 이상 신고된 유저는 게시판 이용이 정지되며, 해당 유저를 신고한 모든 유저에게 정지 사실을 메일로 발송합니다.
유저가 신고한 모든 내용을 취합하여 마지막에 한꺼번에 게시판 이용 정지를 시키면서 정지 메일을 발송합니다.

<br>

**제한 조건**

- 두 수는 1이상 1000000이하의 자연수입니다.


<br>

**입출력 예**

|id_list|report|k|result|
|---|---|---|---|
|["muzi", "frodo", "apeach", "neo"] | ["muzi frodo","apeach frodo","frodo neo","muzi neo","apeach muzi"] | 2|[2,1,1,0]|
|["con", "ryan"]| ["ryan con", "ryan con", "ryan con", "ryan con"] | 3 |[0,0]|




<br>

## 1. 풀이 정리

```python
def solution(id_list, report, k):
    id_dic1 = {id : 0 for id in id_list} # 신고 당한 횟수를 저장
    id_dic2 = {id : 0 for id in id_list} # 신고했을때 응답을 받은 횟수를 저장
    
    rep = list(set(report)) # 중복 없애기
    
    for i in range(len(rep)) : 
        a = rep[i].split()[1]
        id_dic1[a] += 1
    
    reported = {id : num for (id, num) in id_dic1.items() if num >= k}
    reported_id = list(reported.keys())
    
    
    for i in range(len(rep)) :  
        i1 = rep[i].split()[0]
        i2 = rep[i].split()[1]
        
        if i2 in reported_id :
            id_dic2[i1] += 1
    
    b = list(id_dic2.values())
    
    answer = b
    return answer
```


<br>
