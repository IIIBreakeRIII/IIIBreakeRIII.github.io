---
layout: post
title: "[Git] About Git & Github"
author: "Dev.Paul"
categories: Github
tags: [Git, Github, Develop, Developer, Student, VCS, DVCS]
image: github-logo.png
---
<br>

> 개발자의 목숨줄을 파헤쳐보자!

<br>
<h3>0. 들어가며</h3>
<hr>

무릇 개발자라면, Git과 Github을 안들어봤다면 가히 개발자라고 할 수 없을 것이다.
<br><br>
그만큼 개발자에게 Git과 Github은 필수불가결하다.
<br><br>
그렇다면 Git과 Github의 시스템에 대해 알고 쓰는 사람은 얼마나 될까? *~~(일단 필자는 몰랐다)~~*
<br><br>
그래서 오늘은 간단하게 Git과 Github에 대해 좀 알아보고자 한다.

<br>
<h3>1. Git이란?</h3>
<hr>

먼저 Git이란 무엇일까.
<br><br>
Git은 **분할 버전 관리 시스템**, 영어로는 **Distributed Version Control System**이라고 칭한다.
<br>
흔히들 개발자들 사이에서는 **VCS**라고 하면 알고 있는 개발자가 많다.
<br><br>
쉽게 생각하자면 *코드를 관리*하고, *파일의 변화를 추적*하는 역할을 한다고 보면 편하다.
<br>
그림으로 표현하면 다음과 같다.
<br>

<p align="center">
	<img src="https://user-images.githubusercontent.com/89850286/219851673-d36f96cd-3f4b-40b8-811f-4fdf076b39b5.png">
</p>


프로젝트의 시작부터 마지막 변경까지 각 부분들에 어떠한 변경 내용이 들어갔는지 확인이 가능하다.
<br>
즉, 각 단계별로 코드들이 어떻게 변하는지 변화 내용들과 주석과 함께 확인하기 편하다는 장점을 가진다.
<br><br>
그렇다면 이러한 Git은 누구에 의해 만들어졌을까?
<br><br>
미국의 리눅스 개발자였던 Linus Benedict Torvalds는 평소에 메일링 시스템을 이용하여 버전 관리를 지속해왔다.
<br>
하지만 이에 불편함을 느끼고 당시 가장 많은 사람들이 사용한 VCS인 BitKeeper를 사용하게 되는데,
<br>
이 BitKeeper마저도 불편함을 느끼게 된다.
<br><br>
그리고 여기서 그는, **개발자다운 면모**를 보여준다.
<br><br>
바로 ***직접 VCS를 만들게 되는데***, 이렇게 탄생하게 된 것이 Git이었다.
<br><br>
효율적인 버전 관리가 가능하며, 무료이며 오픈 소스라는 큰 장점을 안고 Git은 2005년 12월 21일에 첫 상용화 되었다.
<br>

<br>
<h3>2. Git의 기본 동작 구조</h3>
<hr>

Git의 동작 구조에 앞서 먼저 간단한 용어들부터 알아보자.
<br><br>
> * Version : 버전, 문서 혹은 코드를 수정하고 저장할 때 생기는 식별 메모
> * Stage : 스테이지, 작업 파일들을 버전으로 만들기 전 대기하는 공간
> * Repository : 레파지토리(개발자들은 일반적으로 **레포**라고 얘기함), Stage에서 대기하던 파일들이 Version으로 만들면 저장되는 공간
> * Working Directory : Working Tree와도 같은 말, 개발자의 작업 공간

<br>
자, 그렇다면 이 용어들로 다음 그림을 확인해보자.
<br>

![Group 2](https://user-images.githubusercontent.com/89850286/219870908-2c5c5930-705a-4b43-a72e-7f22a8c046a7.png)

위 그림이 일반적인 Git의 동작 구조이다.
<br><br>
순서대로 설명해보자면,
1. `New Ver.`과 `Original Ver.`두개의 파일이 내 작업 공간에 있다고 가정하자.
2. Terminal에서 `git add .`이라는 코드를 입력하면 수정된 파일은 Staging Area로 올라간다.
3. 여기에서 `git commit`과 함께 commit 내용을 작성하면 수정된 파일이 commit 내용과 함께 `Local Repository`에 올라간다.
4. 마지막으로 `git push` 명령어를 입력하게 되면, 최종적으로 내 Github에 있는 `Remote Repository`로 수정 파일들이 올라가게 된다.

<br>
그럼 여기서 궁금한 것이 생긴다.
<br><br>
`Local Repository`가 뭘까?
<br>
`Local Repository`를 알게 되면 Git이 가진 최고의 장점 중에 하나를 알게 된다.
<br><br>
바로, 내 작업 공간에 있는 또 하나의 Repository이다.
<br><br>
즉, 내 작업 공간에 또 하나의 저장소가 만들어지는 것인데
<br>
이는 내 파일들이 최종적으로 `Remote Repository`로 올라가기 전까지 오프라인으로 저장되어 있는 공간이다.
<br><br>
다시 말해, Git이 가진 최고의 장점 중 하나는 오프라인에서도 작동이 가능하다는 것이다.
<br><br>
기존까지의 VCS들의 치명적인 단점 중 하나는, 네트워크를 통해서만 이용이 가능하다는 것이다.
<br>
하지만 Git의 경우 오프라인으로도 이용이 가능하며, 무수히 많은 commit들 후에 네트워크가 온라인 상태일 때 한번만 push를 해도 내 모든 commit 내용들이 온라인에 등록되게 된다.
<br><br>
위에 정리된 내용들을 한번에 정리하면 다음과 같다.

```terminal
$ git init                          # git 저장소 초기화
$ git add .

# 수정된 코드를 Staging Area로 전달
# 뒤에 .은, 내가 수정한 모든 코드들을 한번에 지칭할 때 사용
# 내가 원하는 코드만 올리고 싶다면 . 대신 [파일 이름] 입력

$ git commit -m "Commit Message"    # Staging Area에서 Local Repository로 전달

$ git push [branch name]            # 온라인 상태에서 Github의 Remote Repository로 전달
```

위 과정들을 통해 최종적으로 Git은 작동하게 된다.

<br>
<h3>3. Github이란?</h3>
<hr>

그렇다면 Github은 도대체 무엇인가.
<br><br>
뭐 굳이 어렵게 얘기하면
> Internet Hosting Service For Git

이라고 위키 백과에는 나와있지만...
<br>
그냥 쉽게 생각해서 Git을 온라인으로 호스팅 해준다고 보면 편하다.
<br><br>
온라인으로 Repository를 생성하여 다른 사람들과 공유도 가능하고, 저장소로도 쓰이는 그런 다재다능한 친구이다.
<br><br>
제공해주는 기능들 중 요약하자면 다음과 같다.
<br>
> * Git의 VCS 기능
> * 접근 제어
> * 버그 트래킹
> * 작업 관리
> * 오픈 소스
> * GUI ~~결국 개발자는 터미널이지만~~

뭐 매우 다양하다.
<br><br>
하지만 우리 개발자들에게는 사실 VCS보다 **포트폴리오**와 **협업**을 위해 쓰이는 게 현실이다. *~~예를 들면 잔디 심기...~~*
<br><br>
사실 뭐 Github이 없었다면 우리 개발자들은 아직까지도 BitKeeper나 Mailing System을 쓰고 있지 않았을까.
<br><br>
여튼 본론으로 돌아와서, 이제부턴 그럼 Github에 Repository를 생성하고 해당 Repository로 내 작업 내역을 push하는 과정을 알아보자.
<br><br>
먼저, Github에 로그인하여 Repository 탭으로 들어간다.
<br>
그 후, 오른쪽 상단의 `New` 탭을 눌러, Repository 이름을 정하고 Visibility를 `Public`으로 할 것인지, `Private`으로 할 것인지를 정한다.
<br>
`Public`의 경우, 다른 사람이 내 `Repository`를 볼 수 있게 되며 때에 따라 수정을 사용자에게 요구할 수 있다.
<br>
반대로 `Private`은 사용자만 확인이 가능하다.
<br>
다 되었다면, `README`를 추가할 것인지 정한 후, `Create Repository`버튼을 누르면 나의 Repository가 완성된다.
<br><br>
완성이 되었다면, `Terminal`에서 나의 Local 작업 공간으로 이동한 후, 다음과 같이 입력한다.

```terminal
$ git init
$ git remote add origin [Repository Address]

# 위 명령어는, Github에 생성된 Remote Repository의 주소와 내 Local Repository를 연결하는 작업이다.
# 해당 명령어를 입력해야 내가 Local에서 작업한 내용들이 Github에 Push 할 수 있게 된다.

$ git add [File or Directory Name or . ]
$ git commit -m "Commit Message"
$ git push origin main(master)
```

이렇게 Local과 Remote Repository를 연결했다면, 이 이후부터는 수정이 생길 시에 다음과 같이 입력하면 된다.

```terminal
$ git init
$ git add .
$ git commit -m "Commit Message"
$ git push origin [Branch Name]
```

이렇게 Github은 이용하면 된다.

<br>
<h3>4. Github에서의 협업과 Branch</h3>
<hr>

자 그럼, 이제부터 Github을 이용하는 중요한 이유 중 하나인 Github을 이용한 협업을 알아보자.
<br><br>
사실 Github을 이용하는 협업에 대해 알려면, 먼저 Github에서 Branch에 대한 개념부터 알아야한다.
<br><br>
Branch는 우리가 아는 그 나뭇가지와 같다.
<br>
여러 개발자들이 각자의 코드를 하나의 Repository에 각자의 Branch 이름으로 올리는 모양이 마치 나뭇가지와 같다 하여 Branch로 부른다.
<br><br>
그림으로 살펴보자.

![Group 5](https://user-images.githubusercontent.com/89850286/219934666-673abcbf-7258-4f05-895d-d96584758d0d.png)

위 그림에서 보이는 바와 같이, Main Repostiory를 AAA라고 하는 사람과 BBB라는 사람이 각각 Clone 받았다고 가정해보자.
<br><br>
두 사람은 각각이 본인이 작업을 진행한 후에, 본인들이 수정한 코드를 다시 Main Repository에 올릴 예정이다.
<br><br>
이때 브랜치를 그냥 Main으로 올리게되면, 서로 작성한 코드가 섞이거나 때로는 오류가 있는 코드가 올라가게 되면 프로젝트를 망치는 문제가 발생하게 된다.
<br><br>
때문에 이를 방지하기 위해 우리는 Branch를 사용한다.
<br>
Main Repository의 소유자가 각각 개발자들이 올리는 코드를 확인하여 수정 사항이 있거나 혹은 오류가 있을 경우에 수정을 해서 합칠 수 있다는 장점을 가지게 된다.
<br><br>
먼저 BBB가 작성한 코드를 소유자가 확인한 후 Pull Request를 받아주면 코드가 합쳐진다.
<br>
후에 AAA가 작성한 코드를 똑같이 검토하여 코드를 합치는 것이다.
<br><br>
때문에 일반적으로 Branch 이름의 작명의 경우 개발자의 이름이나 본인이 작성한 코드를 기반으로 기능의 이름을 붙인다.
<br><br>
이 전체적인 흐름을 Git코드로 나타내면 다음과 같다.

```terminal
$ git clone [Respository Address]     # Main Repository Clone, 코드 수정 후

$ git add .
$ git commit -m "Commit Message"
$ git checkout -b [Branch Name]       # Branch 생성 및 전환
$ git push origin [Branch Name]       # 전환한 Branch로 깃 Push
```

그런 다음, Repository의 소유자는 Repository로 들어가 해당 Branch의 Pull Request를 받아준다.
<br><br>
그렇다면 Main Repository의 소유자 혹은 다른 Branch 작업자는 어떻게 받고 수정하면 될까.
<br>
코드는 다음과 같다.

```terminal
$ git add .
$ git commit -m "Commit Message"      # 작업한 부분까지 Commit
$ git pull origin main(master)        # Pull Request가 완료된 Repository Pull
$ git push origin [Branch Name]       # 본인이 작업한 내용 업로드
```

이렇게 하면 전반적인 Git과 Github의 동작 구조 및 협업에 있어서의 기본에 대해 알게 되었다.

<br>
<h3>5. 마치며</h3>
<hr>

사실, 이 이외에도 여러가지 기능을 많이 가지고 있다.
<br><br>
하지만 아직 필자도 그 수준까지는 도달하지 못해 이 쯤에서 마무리하려고 한다.
<br><br>
약 3주만에 다시 쓰는 블로그 같은데, 앞으로 다시 열심히 쓰기를 바라며...
<br><br>
다짐과 함께.. Adios!
<br>
*~~다음에 뭐 쓰지~~*