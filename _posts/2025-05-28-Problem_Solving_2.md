---
title: "[PS] 백준 1260번: DFS와 BFS [실버 2] (Java)"
date: 2025-05-28 15:05 +09:00
categories: [PS]
tags:
  [
    DFS,
    BFS,
    그래프,
    실버2,
    백준,
    Java,
  ]
---

> DFS와 BFS 개념 정리 포스팅을 올린 후, 지금부터 그래프 탐색 문제를 쭉 풀어볼 예정이다.

---

# 🧠 문제 개요

[백준 1260번: DFS와 BFS](https://www.acmicpc.net/problem/1260)

- 그래프에 대한 정보가 주어졌을 때,
- 각 그래프를 DFS와 BFS로 탐색하는 문제
- **주어진 그래프를 DFS와 BFS로 탐색한 결과를 출력**하면 된다.

---

# 🧩 구현 요약

1. 그래프 정보 입력 받기
2. DFS와 BFS 구현하기

```Java
import java.io.*;
import java.util.*;

public class Main {
    static ArrayList<Integer>[] list;
    static String[] num;
    static String[] input;
    static int N;
    static int M;
    static int V;
    static int node1;
    static int node2;
    static boolean[] visited;
    static StringBuilder result = new StringBuilder();

    public static void main(String[] args) throws IOException {
        initGraph();
        dfs(V);
        Arrays.fill(visited, false);
        result.append("\n");
        bfs(V);
        printResult();
    }
    public static void initGraph() throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        num = br.readLine().split(" ");
        N = Integer.parseInt(num[0]);
        M = Integer.parseInt(num[1]);
        V = Integer.parseInt(num[2]);
        list = new ArrayList[N + 1];
        for (int i = 0; i <= N; i++) {
            list[i] = new ArrayList<>();
        }
        visited = new boolean[N + 1];
        for (int i = 0; i < M; i++) {
            String[] input = br.readLine().split(" ");
            int node1 = Integer.parseInt(input[0]);
            int node2 = Integer.parseInt(input[1]);
            list[node1].add(node2);
            list[node2].add(node1);
        }
        for (int i = 0; i <= N; i++) {
            list[i].sort(null);
        }
        br.close();
    }
    public static void dfs(int cur) {
        if (visited[cur])
            return;
        visited[cur] = true;
        result.append(cur).append(" ");
        for (int i = 0; i < list[cur].size(); i++) {
            dfs(list[cur].get(i));
        }
//        while (!list[cur].isEmpty()) {
//            dfs(list[cur].removeFirst());
//        }
    }
    public static void bfs(int cur) {
        Queue<Integer> q = new LinkedList<>();

        q.add(cur);
        visited[cur] = true;
        result.append(cur).append(" ");
        while (!q.isEmpty()) {
            int remove = q.poll();
            for (int i = 0; i < list[remove].size(); i++) {
                int curIndex = list[remove].get(i);
                if (!visited[curIndex]) {
                    visited[curIndex] = true;
                    q.add(curIndex);
                    result.append(curIndex).append(" ");
                }
            }
        }
    }
    public static void printResult() throws IOException {
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        bw.write(result.toString() + "\n");
        bw.flush();
        bw.close();
    }
}
```

- DFS 함수는 재귀를 사용해 구현
- BFS 함수는 큐를 사용해 구현
- visited 배열을 사용해 방문 여부를 체크

# 📌 배운 점 & 회고

- 이 문제를 통해 DFS와 BFS의 기본적인 구현 방법을 익혔다.
- 또 살짝 객체지향적으로 구현해보려고 했는데, 이게 PS를 할 때 좋은 건지 모르겠다.
- 그래도 객체지향적으로 구현하는 연습을 해보는 것도 좋을 것 같다.