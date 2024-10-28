---
title: 백준 1914번 - 하노이 탑[골드 5](Java)
date: 2024-10-04 20:39 +09:00
categories: [알고리즘, Java]
tags:
  [
    알고리즘,
    백준,
    문제풀이,
    Java,
    골드,
    골드 5,
    하노이 타워,
    .
    .
    .
  ]
---

이번에 해달에서 알고리즘 문제 풀이 소모임에 들어가서 매주 문제를 풀기로 했다.

# 하노이 탑 (골드 5)

[문제 백준 링크](https://www.acmicpc.net/problem/1914)

![하노이 타워](https://github.com/jungi0531/images/blob/main/hanoi.png?raw=true)

하노이 타워 문제다. 하노이 타워는 원판을 옮기는 문제로, 원판을 옮기는 규칙은 다음과 같다.

1. 한 번에 한 개의 원판만 옮길 수 있다.

2. 큰 원판이 작은 원판 위에 있어서는 안 된다.

---

하노이 탑의 기본적인 원리는 다음과 같다.

위 하노이 탑 사진 N = 5일 때의 step

1. 1번 기둥에 있는 4개의 원판을 2번 기둥으로 옮긴다.

2. 1번 기둥에 있는 가장 큰 원판을 3번 기둥으로 옮긴다.

3. 2번 기둥에 있는 4개의 원판을 3번 기둥으로 옮긴다.

이 step을 일반화 하면

1. 1번 기둥에 있는 N - 1개의 원판을 2번 기둥으로 옮긴다.

2. 1번 기둥에 있는 가장 큰 원판을 3번 기둥으로 옮긴다.

3. 2번 기둥에 있는 N - 1개의 원판을 3번 기둥으로 옮긴다.

이 문제를 보고 재귀 함수로 풀면 되겠다고 생각했다. 그래서 바로 시도.

---

처음 작성한 코드

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // 원판의 개수 N 입력 받기
        int N = scanner.nextInt();

        int K = hanoi(N, 1,  3, 2);

        // 옮긴 횟수 K 출력
        System.out.println(K);

        // N이 20이하면 수행 과정 출력
        if (N <= 20) {
            printHanoi(N, 1, 3, 2);
        }

        scanner.close();
    }
    // 하노이탑 재귀 함수
    public static int hanoi(int N, int from, int to, int by) {
        if (N == 1) {
            return 1;
        }
        return hanoi(N - 1, from, by, to) + hanoi(1, from, to, by) + hanoi(N - 1, by, to, from);
    }
    // 수행 과정 출력 함수
    public static int printHanoi(int N, int from, int to, int by) {
        if (N == 1) {
            System.out.println(from + " " + to);
            return 1;
        }
        return printHanoi(N - 1, from, by, to) + printHanoi(1, from, to, by) + printHanoi(N - 1, by, to, from);
    }
}
```

하지만 제출하니까 4%에서 바로 시간 초과가 발생했다.

N은 0 ~ 100이 가능하다. N이 100일 때, 이동 횟수는 2^100 - 1이다. 이동 횟수가 너무 많아서 시간 초과가 발생한 것 같다. 

재귀로는 시간 내에 풀 수 없을 듯하다.

위 step을 일반화한 식을 통해 코딩해야할 거 같다. -> 점화식

N = 1인 경우 -> K = 1

N = 2인 경우 -> K = 3

N = 3인 경우 -> K = 7

N = 4인 경우 -> K = 15

N = 5인 경우 -> K = 31

여기서 규칙을 찾아보면 

**K = 2^N - 1이다.**

따라서 이 문제를 시간 내에 풀려면 재귀 함수로 모든 경우를 탐색하는 것이 아니라 규칙을 찾아서 풀어야 하는 문제인 거 같다.

N <= 20인 경우만 재귀 함수를 통해 수행 과정을 출력하도록 했다.

---

수정한 코드

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // 원판의 개수 N 입력 받기
        int N = scanner.nextInt();

        // 옮긴 횟수 K 출력
        System.out.println((int)Math.pow(2, N) - 1);

        // N이 20이하면 수행 과정 출력
        if (N <= 20) {
            printHanoi(N, 1, 3, 2);
        }
        scanner.close();
    }
    // 수행 과정 출력 함수
    public static int printHanoi(int N, int from, int to, int by) {
        if (N == 1) {
            System.out.println(from + " " + to);
            return 1;
        }
        return printHanoi(N - 1, from, by, to) + printHanoi(1, from, to, by) + printHanoi(N - 1, by, to, from);
    }
}
```

테스트도 잘 되고 해서 다시 제출 했는데 또 틀렸다.

여기서 틀린 이유를 모르겠어서 검색해보니까 2^100을 출력하려면 BigInteger를 사용해야 한다고 한다.

---

재수정 코드

```java
import java.math.BigInteger;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // 원판의 개수 N 입력 받기
        int N = scanner.nextInt();

        // 일반화 식 (2^n) - 1
        BigInteger K = BigInteger.TWO.pow(N).subtract((BigInteger.ONE));
        // 옮긴 횟수 K 출력
        System.out.println(K);

        // N이 20이하면 수행 과정 출력
        if (N <= 20) {
            printHanoi(N, 1, 3, 2);
        }
        scanner.close();
    }
    // 수행 과정 출력 함수
    public static int printHanoi(int N, int from, int to, int by) {
        if (N == 1) {
            System.out.println(from + " " + to);
            return 1;
        }
        return printHanoi(N - 1, from, by, to) + printHanoi(1, from, to, by) + printHanoi(N - 1, by, to, from);
    }
}
```

BigInteger를 사용해서 제출하니까 맞았다.

자바 공부를 다시 해야겠다..

이렇게 나는 점화식과 재귀 함수를 통해 문제를 풀었지만, 스택을 사용해서 푸는 방법도 있다.

스택을 사용해서 푸는 방법으로도 한번 풀어봐아겠다.

---

### 이 문제에서 알아야 할 점

- 규칙이 있는 문제는 규칙을 찾아서 일반화해서 풀어야 한다. -> 그냥 보이는 대로 막 코드를 짜려하지 말고 효율적인 코드 생각하기.

- BigInteger를 사용해야 하는 문제 -> 큰 수 다루는 방법을 알아두자.

