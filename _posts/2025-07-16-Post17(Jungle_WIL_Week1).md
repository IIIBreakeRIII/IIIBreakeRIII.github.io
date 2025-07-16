---
layout: post
title: "[Jungle] WIL : Week-1"
author: Dev/ Paul
categories: Krafton-Jungle
tags:
  - Develop
  - Developer
  - CS
  - Computer-Science
  - Study
  - Project
  - Krafton-Jungle
  - Jungle
---

> 크래프톤 정글에서의 1주차를 마치는 Week-I-Learn

## 2025.07.12 ~ 13

#### 재귀 함수와 꼬리 재귀에 대하여
- 재귀 함수란
  - 자기 자신을 참조하는 함수를 의미
  - Base-Case 즉, `Return` 문이 꼭 있어야함
  - 함수를 호출할 때에는, 이전과 달라진 값을 넣어야 함
  - _👍 Pros_
    - 재사용성이 좋음 (모듈화 및 함수화가 가능)
    - 변수 사용이 줄어든다.
  - _👎 Cons_
    - 반복 작업이 늘어나면 메모리 관리가 불리
      - 일반적으로 Call-Stack이 쌓이며, 정해진 Stack의 용량을 초과할 경우 Stack-Overflow가 발생
    - 유지 보수에 있어 불리함
      - 재귀의 탈출 조건 설정은 까다로움
      - 협업을 하는 과정에 있어 `for`문에 비해 개발자에 따라 가독성이 떨어질 수 있음

<br/>
위는 일반적인 재귀 함수의 특징이다.  
그렇다면, Computer Memory 동작 구조에 대해 조금 알아보고 재귀 함수를 다시 알아보자.  
<br/>

> 🧑‍💻 Computer Memory에 대한 간단한 이해

- OS로부터 전달받는 메모리 공간은 크게 4개가 존재
  - `Code Space`
    - 실행할 프로그램의 코드가 저장되는 영역
    - 프로그램의 생명주기 동안 메모리에 계속 남아있음
    - 컴파일된 기계어(Machine Code)가 저장됨
    - CPU는 코드 영역에 저장된 명령어를 하나씩 가져가서 처리
  - `Data Space`
    - 프로그램의 전역 / 정적 변수 및 문자열 상수 저장
    - 프로그램이 시작하고 끝날 때까지 메모리에 계속 남아있음
  - `Stack Space`
    - 함수의 호출과 관계되는 지역변수 및 매개변수가 저장되는 영역
    - 함수의 호출과 함께 할당되며, 함수의 호출이 완료되면 소멸
      - 이러한 함수의 호출 정보를 `Stack Frame`이라고 부름
    - 프로그램이 자동을 사용하는 임시 메모리 영역
  - `Heap Space`
    - User가 직접 관리해야하는 영역
    - 사용자에 의해 메모리 공간이 동적으로 할당 / 해제
      - `malloc()/new`연산자를 통해 할당, `free()/delete`연산자를 통해 해제 가능
      - Runtime시에 크기 결정
- Heap Overflow vs Stack Overflow
  - `Heap Overflow` : Heap이 아래에서부터 주소값을 채워서 올라가다, Stack 영역을 침범할 때 발생
  - `Stack Overflow` : Stack영역이 Heap을 침범했을 때 발생
- Call Stack?
  - 함수의 호출과 함께 Stack이 할당되며, 함수의 호출이 완료되었을 때 소멸
  - 함수의 호출과 관계되는 지역 변수와 매개변수가 저장되는 영역
  - 정리하면,
    - `Call Stack` : 프로그램이 함수 호출을 추적할 때 사용하는 것
    - 함수의 Call당 하나씩의 Stack Block으로 이루어져 있음

_Example Code_
```
func roll_die() -> Int {
    return Int.random(in: 1...6)
}

func rollTwoAndSum() {
    var total = 0
        total = total + roll_die()
    
    print(total)
}

rollTwoAndSum()
```
_Code Review_
1. `rollTwoAndSum()` 호출
    > rollTwoAndSum()
2. `rollTwoAndSum()` -> `roll_die()` 호출
    > roll_die()  
    > rollTwoAndSum()
3. `roll_die()`에서 `Int.random(in:)` 호출
    > Int.random()  
    > roll_die()  
    > rollTwoAndSum()
4. `Int.random(in:)` 실행이 끝났을 때, Stack에서 제거, roll_die()에게 반환
    > roll_die()  
    > rollTwoAndSum()
5. `roll_die()`가 return
    > rollTwoAndSum()

<br/>
> 🧑‍💻 그렇다면, 재귀함수가 Stack Overflow가 나는 이유는?

- 재귀 함수의 특징
  - 자기 자신을 반복적으로 호출함
    - 일정한 조건을 만났을 때 탈출하는데,
      - 탈출보단, 자기 자신을 불렀던 **이전의 함수를 찾아서 돌아감**.
      - A -> A' -> A'' -> A'''(return) -> A'' -> A' -> A
    - 이때, `python`의 경우, Default로 호출할 수 있는 함수는 총 1000번

> The interpreter sets a maximum recursion depth in order to catch runaway recursion before filling the C stack and causing a core dump or GPF.. … _The default value is 1000_, and a rough maximum value for a given platform can be found by running a new script, `Misc/find_recursionlimit.py`.  

> [What's New in Python 2.0 참고](https://docs.python.org/3/whatsnew/2.0.html)


_Description_
- 언어별로 제한을 두는 이유는 당연히 Call Stack 초과로 인한 Stack Overflow를 방지하기 위함
- 이러한 이유에서 재귀함수는 잘 사용되지 않음
  - 무엇보다도 거의 같은 역할을 하는 `for` or `while`에 비해 그 사용성 및 cost가 월등히 떨어지기 때문

> 🧑‍💻 꼬리 재귀란?

- 꼬리 재귀는 재귀함수에서 기존에 호출된 함수의 정보를 지속적으로 저장하는 과정을 생략하기 위해 도입
  - 함수 안에서 함수의 호출이 발생할 때, 함수의 가장 마지막 순서에 위치하는 것을 말함
  - Pseudo Code로 확인하면,

_Example Code_
```
// 일반 재귀 함수
int factorial(int n) {
    if (n == 1) return 1;
        return n * factorial(n - 1);
}
```

```
// 꼬리 재귀 함수
int factorialTail(int n, int acc) {
    if(n == 1) return acc;
        return factorialTail(n - 1, acc * n);
}

int factorial(int n) {
    return factorialTail(n, 1);
}
```


_Code Review_
- 일반 재귀 함수는 재귀 호출 이후에, `n`을 곱하는 연산이 존재
- 반면 꼬리 재귀의 경우, `factorialTail` 이후에 연산이 존재하지 않음
  - 대신, `factorialTail` 안에서 `acc`를 `parameter`로 전달 받음
  - 이유는, `factorialTail` 함수가 실행이 됨과 동시에
  - 현재의 `n`값을 추적하여 `acc`에 곱해주고,
  - 최종적으로 `return acc;`를 통해 원하고자 하는 값 `1 * 5 * 4 * 3 * 2`를 반환하기 위함

> 🧑‍💻 꼬리 재귀를 정리하며

- 이러한 꼬리 재귀는, 겉으로 보기에는 재귀 함수와 같은 모습을 하지만,
  - 컴파일러의 시각에서는 반복문으로 실행이 되게 됨
- 일반적으로 꼬리 재귀는 2가지의 조건을 충족해야 정상적으로 실행이 가능함
  > 꼬리 재귀로 구현 할 것  
  > 컴파일러가 꼬리 재귀의 최적화를 지원해줄 것
  - 대표적으로 C++, C#, Kotlin, Swift는 꼬리 재귀의 최적화를 지원하지만,
  - Java, Python, Go는 지원하지 않음

<br/>
- 참고 자료
  - [재귀함수와 꼬리 재귀](https://velog.io/@dldhk97/%EC%9E%AC%EA%B7%80%ED%95%A8%EC%88%98%EC%99%80-%EA%BC%AC%EB%A6%AC-%EC%9E%AC%EA%B7%80)
  - [Memory 구조 (code, data, stack, heap)](https://velog.io/@xxhaileypark/Memory-%EA%B5%AC%EC%A1%B0-code-data-stack-heap)
  - [What's New in Python 2.0](https://docs.python.org/3/whatsnew/2.0.html)

#### Time Complexity & Space Complexity

- 시간 복잡도
  - 입력을 나타내는 문자열 길이의 함수로서 작동하는 알고리즘의 동작 시간을 정량화 하는 것이다. (출처 : [위키피디아](https://docs.python.org/3/whatsnew/2.0.html))
  - 최악 / 최선 / 평균의 시간 복잡도가 있는데 각각 표기법은 다음과 같다
    - Big-O Notation
      - 상한 점근 이라고도 표현
      - 일반적으로 최악의 경우를 표현하며, 가장 많이 쓰이는 표기법
        - 표기 방식은 최고차항을 제외한 나머지의 항과 상수를 제거하고, 최고차항의 계수도 제거하여 계산한다.
    - Big-Ω Notation
      - 하한 점근 이라고도 표현
      - 일반적으로 최선의 경우를 표현
    - Big-Θ Notation
      - 상한 점근과 하한 점근의 평균을 표현
      - 일반적으로 최악과 최선의 평균값
  - Terminology
    - 상수 시간 알고리즘 : `(Constant time algorithm)` T(n) = O(1)
    - 선형 시간 알고리즘 : `(Linear time algorithm)` T(n) = O(n)
    - log 시간 알고리즘 : `(Logarithmic time algorithm)` T(n) = O(logn)
    - 2차 시간 알고리즘 : `(Quadratic time algorithm)` T(n) = O(n^2)
    - 지수 시간 알고리즘 : `(Exponential time algorithm)` T(n) = O(2^n)
- 공간 복잡도
  - 입력의 특성에 따라 인스턴스를 해결하는 데 필요한 메모리 공간의 양이다 (출처 : [위키피디아](https://ko.wikipedia.org/wiki/%EA%B3%B5%EA%B0%84_%EB%B3%B5%EC%9E%A1%EB%8F%84))
  - 시간 복잡도와 마찬가지고 Big-O-Notation으로 계산된다.
  - 보통은 알고리즘이 완전하게 solved 되는데 필요한 메모리 공간이며, `Input Memory` + `실행 중에 사용되는 보조 Memory`까지 포함하여 계산된다.
- 시공간 복잡도의 추이 차트
<img src="../assets/img/complexity-graph.png" />
$O(1) < O(logn) < O(n) < O(nlogn) < O(n^2) < O(2^n) < O(n!)$
- [시 / 공간 복잡도 계산기](https://github.com/IIIBreakeRIII/Time-Space-Complexity-Checker?tab=readme-ov-file)

## 2025.07.14

#### Sorting Algorithm

시작하기에 앞서, 본인이 정렬 알고리즘에 대한 공부가 처음이라면 다음의 페이지가 매우 좋은 길라잡이가 된다.
<div style="text-align: center;">
  <a href="https://visualgo.net/en" target="_blank">VisuAlgo</a>
</div>
알고리즘과 자료구조를 시각화하여 보여주는 페이지이다.  
필자도 해당 페이지로부터 도움을 많이 얻어 공유한다.

<br/>
> 🧑‍💻 Quick Sort란

- Charles Antony Richard Hoare가 개발한 범용 정렬 알고리즘
- 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬에 속함
- 문제를 더 작은 문제로 쪼개는 "분할 정복 알고리즘"
- 합병 정렬과 달리 추가 메모리 공간이 필요 없음
- 정렬된 배열일 경우 오히려 수행시간이 늘어날 수 있음

> 알고리즘

- 분할 : 먼저 pivot으로 사용할 원소 하나를 설정하고 pivot보다 작은 값은 left_list, 큰값은 right_list에 배치
  - e.g., `[3, 2, 5, 4, 1]` → `pivot = 3` → `left_list = [2, 1]` `pivot = [3]`, `right_list = [5, 4]`
- 정복 : 부분 배열을 정렬. 이때, 배열의 길이가 1이 될 때까지 재귀적으로 분할 과정을 호출
- 결합 : 정렬한 부분 배열을 하나로 합침. 이 때, 퀵 정렬을 제자리 정렬(In-place Algorithm)으로 구현하면 결합 단계 불필요

- _👍 Pros_
  - 추가적인 메모리를 거의 사용하지 않음
  - 매우 빠른 실행 속도 `O(nlogn)`
- _👎 Cons_
  - 최악의 경우 시간 복잡도는 `O(n^2)`까지 증가
  - 불안정 정렬임

_Code Example_
```python
def quick_sort(arr):

    if len(arr) < 2:
        return arr
    
    # pivot을 0번째 인덱스로 설정할 경우
    pivot = arr[0]
    left_list = []
    right_list = []

    for value in arr[1:]:
        if value < pivot:
            left_list.append(value)
        else:
            right_list.append(value)

    return quick_sort(left_list) + [pivot] + quick_sort(right_list)
```
- 시간 복잡도 및 공간 복잡도
  - 시간 복잡도의 경우,
    - 평균 : `O(nlogn)`
    - 최악 : `O(n^2)`
<div>
    <img src="../assets/img/quick_sort_time_complexity.png" />
</div>
  - 공간 복잡도의 경우
    - 제자리 정렬을 사용 시 : `O(1)`
    - 일반 구현 시 : `O(n)`
<div>
    <img src="../assets/img/quick_sort_space_complexity.png" />
</div>

<br/>
> 🧑‍💻 퀵 정렬이 빠른 이유?

위키피디아에 따르면,

> 퀵 정렬의 내부 루프는 대부분의 컴퓨터 아키텍처에서 효율적으로 작동하도록 설계되어 있고(그 이유는 메모리 참조가 지역화(locality)되어 있기 때문에 CPU 캐시의 히트율이 높아지기 때문이다.),  
대부분의 실질적인 데이터를 정렬할 때 제곱 시간이 걸릴 확률이 거의 없도록 알고리즘을 설계하는 것이 가능하다.

- 메모리 참조의 지역성
  - 컴퓨터는 프로그램을 실행할 때, 메모리를 일정한 패턴으로 접근 -> `지역성`
    - 시간적 지역성 : 최근에 접근한 데이터는 가까운 미래에도 다시 접근할 가능성이 큼
    - 공간적 지역성 : 어떤 메모리 주소가 접근되면, 그 주변 주소들도 곧 접근될 가능성이 큼
  - 지역성 특성을 기반으로 CPU 캐시라는 임시 저장소를 사용하게 되는데...
- 퀵정렬과 메모리 지역성
  - 퀵 정렬 알고리즘을 자세히 살펴보면
    - 피벗으로 선택하여 작은 값, 큰 값을 양쪽으로 분할하는 과정을 재귀적으로 반복
- 이 때 주목할 점은,
  - 퀵 정렬은 배열 내에서 대부분의 작업을 연속된 인접 메모리 공간에서 수행하게 됨
  - e.g., [1, 5, 9, 3, 7] -> 작은 범위로 나누며 반복해서 정렬
    - 이 작은 범위들은 메모리 상에 연속적으로 존재
    - 메모리 범위를 순차적으로 접근하고, 이는 캐시 라인에 이미 적재되어 있을 가능성이 높음
    - 때문에, 캐시에서 Hit Rate가 높아지는 결론에 도달
- 퀵 정렬이 빠른 이유는 결론적으로,
  - 연속된 메모리 접근 : 인접한 메모리 공간을 반복해서 참조 -> 공간 지역성 👍
  - 작은 서브 배열 처리 : 재귀 호출을 통해 더 작은 범위를 다루므로 캐시에 충분히 적재될 수 있음 -> 캐시 Hit Rate 👍

- 참고 자료
  - [퀵 정렬](https://ko.wikipedia.org/wiki/%ED%80%B5_%EC%A0%95%EB%A0%AC)
  - [13-05. 퀵 정렬 #1](https://wikidocs.net/219271)

