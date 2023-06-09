# 스도쿠 Solution
(https://www.acmicpc.net/problem/2580)

작성일: 2023. 05. 02. 화. 이재현

**(참고)** 비슷하면서 조금은 더 쉬운 문제 -> https://www.acmicpc.net/problem/9663 

```
시간 제한	메모리 제한	제출	정답	맞힌 사람	정답 비율
1 초	256 MB	85018	24697	15510	26.764%
문제
스도쿠는 18세기 스위스 수학자가 만든 '라틴 사각형'이랑 퍼즐에서 유래한 것으로 현재 많은 인기를 누리고 있다. 이 게임은 아래 그림과 같이 가로, 세로 각각 9개씩 총 81개의 작은 칸으로 이루어진 정사각형 판 위에서 이뤄지는데, 게임 시작 전 일부 칸에는 1부터 9까지의 숫자 중 하나가 쓰여 있다.

나머지 빈 칸을 채우는 방식은 다음과 같다.

각각의 가로줄과 세로줄에는 1부터 9까지의 숫자가 한 번씩만 나타나야 한다.
굵은 선으로 구분되어 있는 3x3 정사각형 안에도 1부터 9까지의 숫자가 한 번씩만 나타나야 한다.
위의 예의 경우, 첫째 줄에는 1을 제외한 나머지 2부터 9까지의 숫자들이 이미 나타나 있으므로 첫째 줄 빈칸에는 1이 들어가야 한다.

또한 위쪽 가운데 위치한 3x3 정사각형의 경우에는 3을 제외한 나머지 숫자들이 이미 쓰여있으므로 가운데 빈 칸에는 3이 들어가야 한다.

이와 같이 빈 칸을 차례로 채워 가면 다음과 같은 최종 결과를 얻을 수 있다.

게임 시작 전 스도쿠 판에 쓰여 있는 숫자들의 정보가 주어질 때 모든 빈 칸이 채워진 최종 모습을 출력하는 프로그램을 작성하시오.

입력
아홉 줄에 걸쳐 한 줄에 9개씩 게임 시작 전 스도쿠판 각 줄에 쓰여 있는 숫자가 한 칸씩 띄워서 차례로 주어진다. 스도쿠 판의 빈 칸의 경우에는 0이 주어진다. 스도쿠 판을 규칙대로 채울 수 없는 경우의 입력은 주어지지 않는다.

출력
모든 빈 칸이 채워진 스도쿠 판의 최종 모습을 아홉 줄에 걸쳐 한 줄에 9개씩 한 칸씩 띄워서 출력한다.

스도쿠 판을 채우는 방법이 여럿인 경우는 그 중 하나만을 출력한다.

제한
12095번 문제에 있는 소스로 풀 수 있는 입력만 주어진다.
C++14: 80ms
Java: 292ms
PyPy3: 1172ms
예제 입력 1 
0 3 5 4 6 9 2 7 8
7 8 2 1 0 5 6 0 9
0 6 0 2 7 8 1 3 5
3 2 1 0 4 6 8 9 7
8 0 4 9 1 3 5 0 6
5 9 6 8 2 0 4 1 3
9 1 7 6 5 2 0 8 0
6 0 3 7 0 1 9 5 2
2 5 8 3 9 4 7 6 0
예제 출력 1 
1 3 5 4 6 9 2 7 8
7 8 2 1 3 5 6 4 9
4 6 9 2 7 8 1 3 5
3 2 1 5 4 6 8 9 7
8 7 4 9 1 3 5 2 6
5 9 6 8 2 7 4 1 3
9 1 7 6 5 2 3 8 4
6 4 3 7 8 1 9 5 2
2 5 8 3 9 4 7 6 1
```

중간 중간에 빈칸이 있는 9 x 9 스도쿠 퍼즐이 주어지면,

스도쿠 규칙을  만족하도록 빈칸을 채우면 된다.

하나의 입력 당, 여러 개의 출력이 존재할 수 있는데 그러한 경우에는 한 개만 출력하면 된다.


9x9 스도쿠 규칙은 아래 3 가지를 만족하면 된다.

1. 같은 열의 원소들은 1~9 까지 중복 X

2. 같은 행의 원소들은 1~9 까지 중복 X

3. 같은 box(3x3) 내의 원소들은 1~9 까지 중복 X


문제를 보면, 일단 어떻게 구현해야 할 지 감이 오지 않는데...

그러면 어떻게 접근을 할 수 있을까?

인풋 사이즈가 고정되어있고, 9x9 이므로 그렇게 크지는 않으므로

일단 가장 단순한 방법(완전탐색)으로 생각해보자. 

스도쿠를 순회하며, 빈칸을 발견하면

해당 칸에 들어갈 숫자를 임의로 넣어보자. 

(스도쿠 규칙을 만족하는 수)

그리고 다음 빈칸을 만났을 때도, 스도쿠 규칙을 만족하도록 숫자를 넣어보는 작업을 반복한다.

만약, 더이상 나아갈 수 없다면

( 또 다른 빈칸을 만났는데 어떠한 숫자를 넣어도 스도쿠 규칙을 만족하지 않는 경우 )

직전의 상태로 돌아가서, 스도쿠 규칙을 만족하는 '다른' 숫자를 넣어본다.

이 과정을 스도쿠 전체에 대해서 반복하면, 스도쿠를 완성할 수 있을 것이고

이는 사실 '백트래킹' 알고리즘을 적용한 것이다.

백트래킹 알고리즘은 완전 탐색을 수행하며 더 깊은 상태 공간으로 나아가는데,

최종 깊이로 나아가기 이전에 목적 상태에 도달하지 못할 것으로 판단한다면

더 깊게 탐색하지 않고 돌아가서, 다른 상태 공간으로 나아간다.

(일단 채워보고, 되면 좋고 안되면 다시 돌아가서 다른 경우로 나아가면 된다는 마인드)

![image](https://user-images.githubusercontent.com/96612168/235575199-5a3b4349-bd1f-4712-b354-a12bc3a331a4.png)


---

백트래킹 알고리즘을 이용하면 시간 복잡도는 어떻게 될까?

기본적으로 완전 탐색을 이용한다는 것을 유의하자.

빈칸의 개수가 k 라고 하면, 각각의 빈칸마다 1~9 의 경우로 분기가 가능하므로 9^k

최악의 경우라고 치면 k = 81 으로 굉장히.. 커질 텐데

이는 모~~든 경우의 수를 다 탐색한 것이고,

우리는 스도쿠를 완성하지 못하는 경우는 끝까지 탐색하지 않도록 사전에 cut 하여 시간 제한 내에 들어오도록 최적화할 것이다. 

(완전탐색이 아닌 백트래킹을 하겠다는 의미)

---

그럼에도 불구하고 알고리즘의 구상이 잘 안된다면, 이렇게 생각해보자.

기본적인 아이디어는 스도쿠 판을 순회하며, 빈칸을 만나면 1~9 중, 가능한 숫자를 넣어보고

다음 빈칸으로 진행한다. 도중에 스도쿠 규칙을 도저히 만족하지 못하는 상황이 온다면 이전 단계로 back 하여 다른 숫자를 넣는다.

이를 구현하기 위해서 먼저 '스도쿠 규칙을 만족하는 지 못하는 지 판단하는 메서드' 가 필요할 것이다.

해당 메서드를 isitPossible 이라고 하면, 현재 (row, col) 위치에 x 라는 값을 넣었을 때 스도쿠 규칙을 위반하는 지 판단하도록 구현하자.

그리고 나서 모든 경우를 탐색하는 함수를 make 라고 하자.

어떤 인자가 필요할까? 기본적으로 각각의 상태 공간을 구분하는 index 역할을 하는 것은 row, col 이다.

row, col 을 make 의 인자로 설정하고 구현을 시도해보자.

make 함수를 실행했는데, col 이 9 라면 현재 row 에서 스도쿠의 빈칸을 모두 채운 것이므로

make(row+1, 0) 을 호출하자.

그러다가 row 가 9 가 되면, 스도쿠 퍼즐을 완성한 것이므로 출력해주고 프로그램을 종료하면 된다.

row 와 col 이 9 가 아니면서, {row, col} 이 빈칸이라면?

isitPossible(row, col, value) 가 true 이면 해당 위치에 value 를 넣고 다음 상태 공간으로 진행한다. 

row 와 col 이 9 가 아니면서, {row, col} 이 빈칸이 아니라면?

그냥 다음 상태공간으로 진행하면 된다.

⭐ (중요) n 번쨰 상태 공간에서 row, col 위치에 Val 이라는 값을 넣고, 다음 상태공간으로 넘어갔는데 n+1 상태공간에서는 어떠한 수를 넣어도 스도쿠 규칙을 만족하지 않는 경우가 발생할 수있다. 
이러한 경우가 발생하면 n+1 번째 상태공간에서 n 번째 상태공간으로 넘어가고, n 번째 상태 공간의 row, col 값에 다른 값을 넣어줘야 할텐데... 이를 어떻게 구현할까?? 

(열린 결말)
