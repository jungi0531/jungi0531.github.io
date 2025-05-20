---
title: "[PS] 백준 1389번 - 케빈 베이컨의 6단계 법칙 [실버 1] (Java)"
date: 2025-05-19 11:03 +09:00
categories: [PS]
tags:
  [
    BFS,
    그래프,
    최단경로,
    실버1,
    백준,
    Java,
  ]
---

> 이제 실버 상위권 문제를 풀다 보니 한 번에 해결되지 않는 경우가 많아졌다.  
> 앞으로는 풀지 못한 문제도 블로그에 정리하며 복습하고, 실력을 체계적으로 키워나갈 계획이다.  
> 우선 BFS 알고리즘에 익숙해지기 위해 관련 문제들을 집중적으로 풀어보려고 한다.

---

# 🧠 문제 개요

[백준 1389번 - 케빈 베이컨의 6단계 법칙](https://www.acmicpc.net/problem/1389)

- 각 유저 간 연결 관계가 주어졌을 때,
- 특정 유저로부터 다른 모든 유저까지의 거리 합이 가장 작은 사람을 구하는 문제
- 즉, **모든 노드에 대해 최단 거리 합을 구한 후, 그 합이 가장 작은 노드를 출력**하면 된다.

---

# ❌ DFS로 접근했을 때의 실패

처음엔 단순 탐색 문제라고 생각하고 DFS로 접근했다.  
하지만 곧 **시간 초과**가 발생했고, 그 원인을 분석해보니 다음과 같았다:

- DFS는 경로의 모든 경우를 탐색해야 최단 경로를 알아낼 수 있어
- 그래프가 커질수록 **비효율적** -> 불필요한 경로를 모두 탐색해야 하기에
- 스택 오버플로우가 발생할 수 있음
- **최단 거리를 구하기에 비효율적**

---

# ✅ BFS로 해결한 이유

이 문제는 "최단 거리"를 구해야 하므로, **답이 나오는 순간 그 답이 최단 거리임을 보장하는 BFS**가 적절하다.

- BFS는 레벨 단위로 탐색을 진행
- 처음으로 도달한 경로가 최단 경로임을 보장
- **최단 거리 계산이 자연스럽게 가능**
- 각 유저를 시작점으로 BFS를 돌리고, 거리 합이 가장 작은 유저를 선택하면 된다

---

# 🔍 DFS와 BFS 비교

| 항목        | DFS (Depth First Search)        | BFS (Breadth First Search)       |
|-------------|----------------------------------|-----------------------------------|
| 탐색 방식   | 한 방향으로 깊게 탐색            | 가까운 노드부터 넓게 탐색         |
| 자료구조     | 스택 (재귀 포함)                | 큐                                |
| 적합한 상황 | 모든 경로 탐색, 조합/백트래킹    | 최단 거리 구하기                  |
| 최단 경로   | 보장하지 않음                    | **항상 보장됨**                   |

---

# 🧩 구현 요약

1. 각 유저를 시작점으로 BFS 수행
2. 다른 모든 유저까지의 거리 합 계산
3. 거리 합이 가장 작은 유저를 선택

```java
import java.io.*;
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        String[] num = br.readLine().split(" ");
        int N = Integer.parseInt(num[0]);
        int M = Integer.parseInt(num[1]);
        ArrayList<Integer>[] list = new ArrayList[N + 1];
        for (int i = 0; i <= N; i++) {
            list[i] = new ArrayList<>();
        }
        for (int i = 0; i < M; i++) {
            String[] input = br.readLine().split(" ");
            int A = Integer.parseInt(input[0]);
            int B = Integer.parseInt(input[1]);
            if (!list[A].contains(B))
                list[A].add(B);
            if (!list[B].contains(A))
                list[B].add(A);
        }
        // 자기 제외 total 횟수를 구해서 min 값에 저장
        int minCount = Integer.MAX_VALUE;
        int minCountIndex = 0;
        for (int i = 1; i <= N; i++) {
            int count = bfs(i, list, N);
            // BFS로 최단 경로 찾기
            bfs(i, list, N);
            // 최소 값일 경우 변경
            if (count < minCount) {
                minCount = count;
                minCountIndex = i;
            }
        }
        // 정답 출력
        bw.write(String.valueOf(minCountIndex) + "\n");
        bw.flush();
        bw.close();
        br.close();
    }
    public static int bfs(int start, ArrayList<Integer>[] list, int N) {
        Queue<Integer> q = new LinkedList<>();
        boolean[] visited = new boolean[N + 1];
        int[] dist = new int[N + 1];

        q.add(start);
        visited[start] = true;
        while (!q.isEmpty()) {
            int cur = q.poll();
            for (int next : list[cur]) {
                if (!visited[next]) {
                    visited[next] = true;
                    dist[next] = dist[cur] + 1;
                    q.add(next);
                }
            }
        }
        
        int total = 0;
        for (int i = 1; i <= N; i++) {
            total += dist[i];
        }
        return total;
    }
}
```

# 📌 배운 점 & 회고

문제를 처음 봤을 때 단순 탐색으로 생각하고 DFS로 접근한 건 **문제 분석 없이 코딩부터 시작하는 습관**이 드러난 결과였다.

이 문제를 통해

- 문제의 목적(최단 거리, 전체 탐색)을 먼저 파악하기
- 알고리즘의 선택 기준을 확실히 갖기
- BFS/DFS 등 알고리즘을 이론뿐 아니라 **문제에 따라 적절히 적용할 수 있는 감각** 가지기

의 필요성을 느꼈다.

앞으로는 문제를 풀기 전에 **문제의 본질**을 파악하고, 그에 맞는 알고리즘을 선택하는 연습을 해야겠다.

우선 각 알고리즘에 대한 이해도를 높이기 위해 한동안 BFS 문제를 집중적으로 풀어볼 예정이다.

+ 자바를 사용하니까 코드를 좀 더 객체 지향적으로 구성해보는 것도 좋을 것 같다.