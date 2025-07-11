---
layout: post
title: "[Algorithm] 소수 찾기와 에라토스테네스의 체"
author : Dev.Paul
categories: Coding Test
tags:
  - Develop
  - Developer
  - Studet
  - CS
  - Computer-Science
  - Coding Test
  - Study
---

<br>

> 프로그래머스 - 소수 찾기  Feat.에라토스테네스의 체

<br>
<h3>소수 찾기와 에라토스테네의 체</h3>
<hr>

개발을 거의 처음 배운다면, 한번쯤은 소수와 관련된 코드를 작성하게 된다.
<br><br>
제일 대표적으로는, "0 ~ N 사이에 있는 소수를 출력하시오." 또는 "0 ~ N 사이의 소수 개수를 구하시오." 라는 형태의 문제들이 많으며 거의 대체적으로는 **이중 반복문**을 이용하여 해결한다.
<br><br>
하지만 오늘은 조금 다른 방법을 이용해서 해결해보고자 한다.
<br>
바로, _에라토스테네스의 체_ 를 이용한 방법이다.
<br><br>
고대 그리스의 수학자인 에라토스테네스는 소수를 찾는 새로운 방법을 제시한다.
<br><br>
기존의 소수를 찾는 방법이라 하면(코딩에서도 그렇고), N이라는 수를 N - 1까지 모두 나눠보며 나머지가 0이 되는지 안되는지 확인을 하는 방법을 이용한다.
<br>
코드로 표현하면 다음과 같을 것이다.
```python
# num까지의 소수 개수 구하기
num = 10
count = 0

for i in range(1, num + 1):
    if i == 2:
        count += 1
    else:
        for j in range(2, i):
            if i % j == 0:
                break
            elif j == i - 1:
                count += 1

print(count)
```
가장 익숙한 방법이며, 우리가 코딩을 배우면서 소수를 구할 때 가장 많이 쓰는 코드 중 하나일 것이다.
<br><br>
하지만 이 코드의 가장 큰 문제점은, 시간 복잡도를 고려하지 않은 코드라는 것이다.
<br><br>
개발을 조금만 배우다 보면, 특히 이러한 알고리즘과 관련된 문제를 풀 때 시간 복잡도에 대한 개념이 꽤나 중요하다는 것을 알게 된다.
<br>
실제로 우리가 일반적으로 보는 코딩 테스트들에서도 이러한 시간 복잡도의 문제를 꽤나 중요하게 다룬다는 것을 조금만 연습해보면 바로 알게 된다.
<br><br>
필자가 작성한 블로그에도 이러한 시간 복잡도에 대한 내용이 있다. 아래의 링크를 통해 확인하길 바란다.

<p style="text-align: center" >
	<a  href="https://iiibreakeriii.github.io/Post9(CSPart1_3)" target="_blank"> --- 시간 복잡도 --- </a>
</p>

그렇다면, 이러한 소수 찾기 문제의 경우 어떤 방식으로 시간 복잡도를 줄일 수 있을까.
<br>
바로 위에서 기술한 **에라토스테네스의 체**를 이용하는 것이다.
<br><br>
에라토스테네스의 체에 대한 개념은 다음과 같다.
<br><br>
다음과 같이, 1부터 25까지 수를 나열해보자.

<p  align="center">
	<img src="https://github.com/IIIBreakeRIII/IIIBreakeRIII.github.io/assets/89850286/d2619108-556c-4885-9261-660219c9e325">
</p>

여기에서, 1은 소수에도 합성수에도 해당되지 않는 수 이기에 제외해준다.
<br><br>
다음은 2이다. 2는 소수이다. 하지만, 2의 배수들은 최소한 2를 약수로 갖기에 소수가 아니다. 때문에, 2를 제외하고 2의 배수는 모두 지워준다.

<p  align="center">
	<img src="https://github.com/IIIBreakeRIII/IIIBreakeRIII.github.io/assets/89850286/e97ca3aa-7d14-4913-9bc7-af1f577093c5">
</p>

다음은 3이다. 3도 2와 마찬가지로 소수이다. 하지만, 3의 배수들은 최소한 3을 약수로 갖기에 소수가 아니다. 때문에, 3을 제외하고 3의 배수들은 모두 지워준다.

<p  align="center">
	<img src="https://github.com/IIIBreakeRIII/IIIBreakeRIII.github.io/assets/89850286/8c9c754a-ad34-42ae-a347-2bee776e5daa">
</p>

다음은 4인데, 4는 2의 배수이므로 지워줄 필요 없이 이미 지워진 상태이다.
<br>
그 다음은 5인데, 5는 소수이지만 마찬가지로 5의 배수는 소수가 될 수 없다. 때문에 5를 제외하고 모든 5의 배수를 지워준다.

<p  align="center">
	<img src="https://github.com/IIIBreakeRIII/IIIBreakeRIII.github.io/assets/89850286/77ddcded-042a-4f0a-9afd-2c78985557c7">
</p>

그러면 최종적으로 다음과 같이 소수들만 남게 된다.

<p  align="center">
	<img src="https://github.com/IIIBreakeRIII/IIIBreakeRIII.github.io/assets/89850286/1f26293c-572a-4e7f-8e63-f8e4ff4df336">
</p>

25를 기준으로 5까지만 비교했는데 나머지 소수가 어떤 것들이 있는지 알게 되었다.
<br><br>
이것이 바로 에라토스테네스가 발견한 소수의 특징이다.
<br><br>
N이라는 수까지 나열되어 있는 상태에서 소수만 찾고 싶다면, N의 제곱근까지만 비교하여 그 배수들을 정리하면, **N의 제곱근의 배수에 해당하지 않는 수들은 모두 소수**임을 증명한 것이 _에라토스테네스의 체_ 이다.
<br><br>
위의 그림들에서 우리는 1부터 25까지의 수들 중에서 소수를 찾고 싶었기에, 25의 제곱근인 5까지만 비교해보면 소수를 모두 찾을 수 있는 것이다.
<br><br>
그렇다면 이를 코딩으로 풀어낸다면 어떻게 풀 수 있을까.
<br><br>
필자는 2가지의 방법을 생각했다.
<br>
정석적인 방법은 내가 찾고자 하는 수(앞으로는 n으로 정의한다)까지 리스트에 정렬한 후, n의 제곱근의 배수들을 모두 리스트에서 지워나가며 최종적으로 남은 수들을 반환하는 방식이다.
<br>
코드로 나타내면 다음과 같다.
```python
import math

num = 100
num_list = [i for i in range(2, num + 1)]

for i in range(2, int(math.sqrt(num)) + 1):
    for j in range(i + i, num + 1, i):
        if j in num_list:
            num_list.remove(j)

print(num_list)
```
하지만, 이런 방법도 가능하다.
<br><br>
`num_list`라는 리스트를 생성 후, n까지의 모든 수를 비교하며 소수의 경우 `num_list`에 추가해주는 방법이다. 단, 여기에서 조건은 n의 제곱근까지만 나눠가며, _n이라는 수가 n의 제곱근보다 작은 수들에서 약수를 갖는지 확인_ 하고, 약수가 있을 경우에는 `False`를, 약수가 없다면 `True`를 반환하게 하는 것이다. 그리고 반환한 값에 따라, `True`일 경우 위에처럼 리스트에 추가해주고, `False`일 경우에는 추가하지 않는다.
<br>
코드로 나타내면 다음과 같다.
```python
num_list = []
n = 100

def prime_num(num):
    for i in range(2, int(math.sqrt(num) + 1)):
        if num % i == 0:
            return False
    return True

for i in range(2, n + 1):
    if prime_num(i):
        num_list.append(i)

print(num_list)
```
`prime_num`이라는 함수는 파라미터로 넘어오는 `num`에 대해서 `num`의 제곱근까지만 수를 나눠본다.
<br>
이 때, 나누어 떨어진다면 `False`를 반환하고, 최종적으로 나누어 떨어지는 수가 없다면 소수로 판단하고 `True`를 반환한다.
<br>
이렇게 반환된 수들은 `num_list`에 저장되고, 최종적으로 `num_list`는 모두 소수만 담게 되는 것이다.
<br><br>
에라토스테네스의 체는 이 정도로 정리할 수 있다.
<br><br>
그럼, _Adios_