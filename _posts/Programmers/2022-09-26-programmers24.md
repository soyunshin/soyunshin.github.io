---
title:  "[Programmers] 영어 끝말잇기"
excerpt: "코딩테스트 연습 : :star: :star:  "

categories:
  - Coding Test
tags:
  - [Coding Test, Algorithm, Python]

toc: true
toc_sticky: true
 
date: 2022-09-26
last_modified_at: 2022-09-26
---


# 0. 문제 설명

1부터 n까지 번호가 붙어있는 n명의 사람이 영어 끝말잇기를 하고 있습니다. 영어 끝말잇기는 다음과 같은 규칙으로 진행됩니다.
  
  1. 1번부터 번호 순서대로 한 사람씩 차례대로 단어를 말합니다.
  2. 마지막 사람이 단어를 말한 다음에는 다시 1번부터 시작합니다.
  3. 앞사람이 말한 단어의 마지막 문자로 시작하는 단어를 말해야 합니다.
  4. 이전에 등장했던 단어는 사용할 수 없습니다.
  5. 한 글자인 단어는 인정되지 않습니다.

다음은 3명이 끝말잇기를 하는 상황을 나타냅니다.<br><br>

tank → kick → know → wheel → land → dream → mother → robot → tank<br><br>

위 끝말잇기는 다음과 같이 진행됩니다.


  - 1번 사람이 자신의 첫 번째 차례에 tank를 말합니다.
  - 2번 사람이 자신의 첫 번째 차례에 kick을 말합니다.
  - 3번 사람이 자신의 첫 번째 차례에 know를 말합니다.
  - 1번 사람이 자신의 두 번째 차례에 wheel을 말합니다.
  - (계속 진행)

끝말잇기를 계속 진행해 나가다 보면, 3번 사람이 자신의 세 번째 차례에 말한 tank 라는 단어는 이전에 등장했던 단어이므로 탈락하게 됩니다.<br>

사람의 수 n과 사람들이 순서대로 말한 단어 words 가 매개변수로 주어질 때, 가장 먼저 탈락하는 사람의 번호와 그 사람이 자신의 몇 번째 차례에 탈락하는지를 구해서 return 하도록 solution 함수를 완성해주세요.


<br><br>

**제한 조건**

- 끝말잇기에 참여하는 사람의 수 n은 2 이상 10 이하의 자연수입니다.
- words는 끝말잇기에 사용한 단어들이 순서대로 들어있는 배열이며, 길이는 n 이상 100 이하입니다.
- 단어의 길이는 2 이상 50 이하입니다.
- 모든 단어는 알파벳 소문자로만 이루어져 있습니다.
- 끝말잇기에 사용되는 단어의 뜻(의미)은 신경 쓰지 않으셔도 됩니다.
- 정답은 [ 번호, 차례 ] 형태로 return 해주세요.
- 만약 주어진 단어들로 탈락자가 생기지 않는다면, [0, 0]을 return 해주세요.

<br>

## 입출력 예

|n|words| result |
|---|---|---|
|3|	["tank", "kick", "know", "wheel", "land", "dream", "mother", "robot", "tank"]|	[3,3]|
|5|	["hello", "observe", "effect", "take", "either", "recognize", "encourage", "ensure", "establish", "hang", "gather", "refer", "reference", "estimate", "executive"]	|[0,0]|
|2|	["hello", "one", "even", "never", "now", "world", "draw"]|	[1,3]|



<br><br>

# 1. 풀이 정리

`stack`구조를 활용한다.

```python
def solution(n, words):
    lst = []
    m = 1
    while len(lst) <= len(words) :
        if len(lst) == len(words) : 
            break 
        for i in range(1,n+1) : 
            lst.append([m,i])
        m+=1
    
    o = words[0]
    for i in range(1,len(words)+1) :
        if i == len(words) :
            return [0,0]
        if o[-1] != words[i][0] : 
            break
        o = words[i]
        if i > 2 and o in words[0:i] : 
            break
    if i != len(words) : 
        return [lst[i][1],lst[i][0]]


```


<br>
