---
title: 알고리즘 문제 풀이(Java)
date: 2024-10-04 20:39 +09:00
categories: [백준, Java]
tags:
  [
    백준,
    알고리즘,
    Java,
    골드
    .
    .
    .
  ]
---

이번에 해달에서 알고리즘 문제 풀이 소모임에 들어가서 매주 문제를 풀기로 했다.

이번 문제 - 하노이 탑 (골드 5)

https://www.acmicpc.net/problem/1914

![하노이 타워](https://github.com/jungi0531/images/blob/main/hanoi.png?raw=true)

하노이 타워 문제다. 하노이 타워는 원판을 옮기는 문제로, 원판을 옮기는 규칙은 다음과 같다.

1. 한 번에 한 개의 원판만 옮길 수 있다.

2. 큰 원판이 작은 원판 위에 있어서는 안 된다.

이 문제는 재귀함수를 이용해서 풀 수 있다.