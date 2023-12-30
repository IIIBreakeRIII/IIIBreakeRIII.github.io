---
layout: post
title: "[Jekyll] Chirpy를 이용해 깃허브 블로그 호스팅"
author: "Dev.Paul"
categories: Blog
tags: [Github, Blog, Jekyll, Github-Blog, Jekyll-Chripy, Develop]
image: chirpy.png
---

<br>

>Github으로 블로그 호스팅하기 (Feat. Chirpy Theme)

<br>
<h3>0. Chirpy 테마를 이용해 블로그 호스팅하는 방법</h3>
<hr>

이번 포스팅에서는 Jekyll Theme을 이용해 깃허브로 블로그를 호스팅하는 방법에 대해 알아보고자 한다.
<br><br>
시작하지기에 앞서, 필자의 노트북 사양 및 설정값은 다음과 같다.
> **2020 M1 Macbook 13" pro**
> <br>
> **macOS Ventura 13.0.1**


Winodws 시스템의 경우... 다른 블로그를 참고하길 바란다.
<br><br>
다음은 Jekyll을 통해 제작자들이 직접 제공해주는 깃허브 블로그 테마이다.
<br><br>
원하는 블로그 테마를 선택하자.
<br><br>

<p style="text-align: center">
	<a href="https://github.com/topics/jekyll-theme" target="_blank"> --- Jekyll Theme --- </a>
</p>

<br>
혹은 필자가 쓰고 있는 Chirpy테마는 다음 링크를 통해 접속하면 확인할 수 있다.
<br><br>

<p style="text-align: center">
	<a href="https://github.com/cotes2020/chirpy-starter" target="_blank"> --- Chirpy Starter --- </a>
</p>

<p style="text-align: center">
	<a href="https://github.com/cotes2020/jekyll-theme-chirpy" target="_blank"> --- Jekyll Theme Chirpy--- </a>
</p>
<br>
Starter를 이용하면 **많은 설정 없이 간편**하게 설정이 가능하다.
<br><br>
하지만, 그만큼 **개인이 커스터마이징하기 번거롭거나 불가능**한 경우가 있다.
<br>
때문에 필자는 두번째 링크를 압축파일로 다운받아 일부 수정 후 다시 필자의 Repository에 업로드하였다.
<br><br>
Starter를 이용하여 간편하게 이용할 사용자는 필자의 로컬 설정과 Jekyll 설정만 참고한 후, 해당 Repository Readme를 통해 설정하는 것을 권장한다.
<br><br>
그럼 하나하나 살펴보자.

<br>
<h3>1. rbenv 설치</h3>
<hr>

먼저 Jekyll 소프트웨어의 경우 Ruby 언어를 통해 개발되었기 떄문에, Jekyll 실행을 위해선 Ruby가 필수적이다.
<br>
여러 다른 블로그의 많은 포스팅에서 Ruby를 설치하는 방법이 나와있지만, 필자는 이 중 rbenv라고 하는 버전 관리 툴을 통해 설치했다.
<br>
>macOS는 기본적으로 Ruby가 설치되어있지만, Jekyll에서 필요로 하는 Ruby보다 버전이 낮은 경우가 많다.

다음 링크를 참고하면 좋다.
<br><br>

<p style="text-align: center">
	<a href="https://github.com/rbenv/rbenv" target="_blank"> --- rbenv Github Chirpy--- </a>
</p>

<br>
rbenv 설치 과정은 다음과 같다.
<br><br>
**먼저 [Homebrew](https://brew.sh/)를 설치해준다.**
<br><br>
Homebrew 설치과 완료되면 터미널을 실행 후, 다음 명령어를 입력하여 **rbenv를 설치**한다.
``` terminal
$ brew install rbenv ruby-build
````
설치가 완료되면, 다음 명령어를 입력하고 출력되는 명령들을 그대로 Terminal에서 실행한다.
```terminal
$ rbenv init
````
완료되면 **터미널을 종료하고 재실행**한다.
<br>
그리고 rbenv관련 Github 자료들을 Clone 받는다.
```terminal
$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
```
그리고 다음 명령어를 통해 **환경 변수 설정**을 해준다.
<br>
필자는 Z Shell을 사용하기에 다음 명령어를 따른다. bash를 사용하는 사용자는 rbenv Github에 설정 방법이 나와있으니 이를 따라주면 된다.
```terminal
$ echo 'eval "$(~/.rbenv/bin/rbenv init - zsh)"' >> ~/.zshrc
```
마찬가지로 환경변수까지 설정이 마무리되면, **터미널을 종료하고 재실행**한다.
<br><br>
이로써, 기본적인 rbenv 설정은 완료되었다. 이제 Ruby를 설치한다.

<br>
<h3>2. Ruby 설치</h3>
<hr>

설치받은 rbenv를 이용하여 Ruby를 설치해보자.
<br>
rbenv만 깔끔하게 설치되었다면, Ruby설치는 금방이다.
<br><br>
먼저, 다음 명령어를 통해 현재 설치 가능한 **Ruby 버전을 확인**한다.
```terminal
$ rbenv install -l
````
필자의 경우 Ruby 3.1.3을 설치받았다. **다음 명령어를 통해 설치**한다.
```terminal
$ rbenv install [Version]
Example : rbenv install 3.1.3
````
설치가 완료되었으면, 해당 설치받은 Ruby의 버전을 **global로 사용할 것인지 local에서만 사용할 것인지 설정**해준다.
```terminal
$ rbenv global [Version]
or
$ rbenv local [Version]
Example
$ rbenv global 3.1.3
```
다음까지 설정이 끝났다면, Ruby 설치도 마무리 되었다.
<br><br>
이젠, Ruby의 패키지 관리자인 Gems만 설치해주면 된다.
<br>
**Gems 설치는 다음 명령어를 입력**한다.
```terminal
$ gem install bundler
```
여기까지하면 Ruby 설치는 모두 끝이다.
<br><br>
이제 Github으로 돌아가자.

<br>
<h3>3. Github 설정</h3>
<hr>

깃허브에서 설정은 간단하다.
<br><br>
먼저 Repository를 새로 생성한다.
<br>
Repository 이름은 **`[Username].github.io`**으로 설정하고, Visibility는 **`Public`**으로 설정해준다.
<br>
에를 들어, 필자의 Github Username은 **`IIIBreakeRIII`**이므로, **`IIIBreakeRIII.github.io`**으로 설정해주었다.
<br>
어렵다면, 다음을 참고하면 된다.
<br><br>

<p style="text-align: center">
	<a href="https://github.com/iiibreakeriii/iiibreakeriii-blog-closed" target="_blank"> --- IIIBreakeRIII.github.io Repository --- </a>
</p>

<br>
여기까지 완료되었다면 깃허브 설정 또한 마무리 되었다.
<br>
이제 Chirpy Theme으로 이동하자.

<br>
<h3>4. Theme 설정</h3>
<hr>

먼저 내가 사용하고자 하는 Theme (혹은 Chirpy Theme)의 Repository로 이동하여 **전체 코드를 zip 파일**로 받아온다.
<br><br>
다음 과정을 통해 받아올 수 있다.
<br>

<img width="1679" alt="Post2(1)" src="https://user-images.githubusercontent.com/89850286/210208141-e63fdc6c-16d8-4b73-a64b-0376652a38c5.png">

<img width="1679" alt="Post2(2)" src="https://user-images.githubusercontent.com/89850286/210208220-4388b725-4a08-45de-a5b2-9b022450bab3.png">

<br>
이렇게 받아온 Theme은 압축을 푼 후에, **폴더 이름을 Repository 이름과 일치**하게 바꿔준다.
<br><br>
그 후, 다시 터미널을 열어 로컬의 작업 폴더에 접근한 후 다음과 같이 명령어를 입력하여 **Jekyll과 Chirpy Theme에 필요한 모듈을 설치**한다.
```terminal
$ bundle install
```
필자와 같이 진행하면 된다.
<br>

<img width="1361" alt="Post2(3)" src="https://user-images.githubusercontent.com/89850286/210209605-5c4fe427-3738-4728-99d0-d6c2c7a48cda.png">

<br>
설치가 완료되었다면, 그대로 터미널 창에 다음과 같은 명령어를 입력하면 터미널에 표시되는 `Server address`로 블로그가 실행되는 것을 볼 수 있다.
```terminal
$ jekyll serve
```
이 과정을 거치면 최종적으로 나의 로컬에서 Theme이 적용된 최초의 블로그 화면을 ~~감상~~ 볼 수 있다.

<br>
<h3>5. _config.yml 파일 수정 및 깃허브 배포</h3>
<hr>

이제, 최종적으로 내 블로그가 깃허브 도메인을 가지고 배포될 수 있도록 해보자.
<br><br>
먼저 **`_config.yml`파일의 url부분을 다음과 같이 수정**한다.
```yml
$ url: 'https://[Username].github.io'
# Example
$ url: 'https://iiibreakeriii.github.io'
```
다음과 같이 수정해주면, 해당 소스 파일들이 깃허브에 올라갔을 때, 다음 URL을 통해 배포가 이루어진다.
<br><br>
`_config.yml`파일을 다음과 같이 수정 완료했으면, 위에서 지정한 **깃허브 Repository와 로컬 폴더를 연결**해준 후, **Commit과 Push**를 한다.
<br><br>
**<u>이 과정을 거치면, 깃허브 자체적으로 호환성 검사를 거친 후 최종적으로 내 도메인을 가진 블로그가 완성된다!</u>**
<br><br>
이제 지정한 도메인으로 접속하면 완성된 블로그가 배포된 것을 확인할 수 있다.

<br>
<h3>6. 마치며</h3>
<hr>

Ruby 세팅을 시작으로, 원하는 테마를 이용해 블로그를 배포하는 것까지 살펴보았다.
<br><br>
필자 기준에서 여러가지 시도를 하며 배포에 성공했지만, 위에 기술한 방법이 세팅에 있어서 가장 깔끔한 방법이었다.
<br><br>
다음 포스팅은, Chirpy 테마에서 블로그를 꾸밀 수 있는 몇 가지 방법을 기술할 예정이다.
<br><br>
~~다음 포스팅도 지치지 않고 하길 바라며... Adios!~~