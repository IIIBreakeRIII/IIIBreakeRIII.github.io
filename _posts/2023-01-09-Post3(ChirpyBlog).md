---
layout: post
title: "[Jekyll] _config.yml을 부셔보자"
author: "Dev.Paul"
categories: Blog
tags: [Github, Blog, Jekyll, Github-Blog, Jekyll-Chripy, Develop]
image: chirpy.png
---

>Github으로 블로그 호스팅하기 2탄 (Feat. Chirpy Theme)

<br>
이번 포스팅에선 저번 포스팅에 다뤘던 깃허브 블로그를 꾸미는 방법을 올려보고자 한다.
<br><br>
제목에는 `_config.yml`을 조져보자! 라고 했지만 이를 비롯해서 내가 사용한 방법들을 공유해보고자 한다.

<br>
<h3>0. YAML에 대한 기본 설명</h3>
<hr>

YAML은 XML, JSON과 같은 데이터 직렬화 양식이다.
<br>
데이터의 연동 및 호환성을 위해 포맷에 대한 규칙을 정하는 경우가 개발에 있어선 필수불가결한데, YAML 방식은 이를 정의해준다고 생각하면 편하다.
<br><br>
이전에 가장 대표적으로 쓰던 방식은 XML과 JSON인데, 현재에는 JSON도 많이 사용하지만 그만큼 YAML도 꽤나 많이 사용된다.
<br><br>
대표적인 YAML방식이 쓰이는 곳은, Flutter 개발자들은 한번씩은 봤을 dart패키지를 관리하기 위한 `pubspec.yaml`이 매우 대표적이다.
<br><br>
우리가 현재 블로그 생성을 위해 사용하는 Jekyll에서도 이 YAML 방식을 이용해 데이터를 포맷을 규정한다.
<br><br>
> 참고로, Jekyll에서는 `.yml`로 포맷이 정해져 있다.

<br>
<h3>1. _config.yml에서의 기본 설정</h3>
<hr>

먼저, 테마의 `_config.yml`파일에 들어간다.
<br><br>
위에서부터 하나씩 정리해보겠다.
<br><br>
* **언어 및 시간대 설정**
  * 언어 설정
  ```yaml
  $ lang: en
  # ko로 변경
  ```
  하지만, 한국어에 대한 Language Set을 제공하지 않아, 필자의 경우 변경하지 않았다.
  <br>
  후에 커스터마이징을 위해 폰트를 설정한다면, 위 설정을 ko로 변경해준다.
  * 시간대 설정
  ```yaml
  $ timezone: Asia/Shanghai
  # timezone: Asia/Seoul로 변경
  ```
  말 그대로 시간대 변경이다.
  <br>
  기존 세팅은 상하이로 되어 있으니 서울로 변경해준다.
  <br><br>
* **타이틀 및 태그라인 설정**
  * 블로그 제목과 부제목을 설정
  ```yaml
  $ title: Chirpy
  # 제목 부분
  # 필자의 경우 Dev. Paul로 변경
  $ tagline: A text-focused Jekyll theme
  # 부제 부분
  # 필자의 경우 Developer, Photographer로 변경
  ```
  다음 부분에 해당한다.
  ![Post3(1)](https://user-images.githubusercontent.com/89850286/211184147-0df55d05-c1c8-475e-b76b-3bc96e90d25d.png)
  <br><br>
* **Github 및 SNS 아이디 설정**
  * Navigation Bar에 표시되는 SNS 아이디 설정
  ```yaml
  $ github:
  $   username: github_username
  # 본인의 깃허브 아이디를 github_username 부분에 입력
  # 필자의 경우 IIIBreakeRIII 입력
  $ twitter:
  $   username: twitter_username
  # 본인의 SNS 아이디를 twitter_username 부분에 입력
  # 본인이 주력으로 사용하는 SNS 아이디를 설정해주는데, Default 설정은 twitter
  # 다른 링크 및 아이콘을 필자와 같이 바꿀 경우, _data/contact.yml로 들어가 다음과 같이 추가
  $ type: instagram
  $ icon: 'fab fa-instagram'
  $ url: 'https://www.instagram.com/1intheworld_hs.ryu__'
  ```
  <br>
* **저작권 표시 및 개인 링크 연결**
  * Footer에 표시되는 저작권 표시와 개인 링크 연결 설정
  ```yaml
  $ social:
  $   name: your_full_name
  $   email: example@domain.com
  $   links:
  $     - https://twitter.com/username
  $     - https://github.com/username
  # 필자의 경우, 다음과 같이 바꿨다.
  $ social:
  $   name: IIIBreakeRIII
  $   email: ryu990305@gmail.com
  $   links:
  $     - https://www.linkedin.com/in/hyeonsoryu
  # 다음과 같이 링크드인 주소를 넣었다.
  ```
  참고로, 위 이메일 도메인을 설정하면 Navigation Bar에 있는 이메일 UI가 위에 작성한 이메일을 수신자로 자동 설정되게 된다.
<br><br>
* **Avatar 설정**
  * Navigation Bar에 설정되는 메인 사진 설정
  ```yaml
  $ avatar: '/commons/avatar.jpg'
  # 필자는 assets 폴더 안에 img라는 폴더와 profile이라는 폴더를 만들어 이 안에 사진을 넣고 경로를 설정해줬다.
  $ avatar: '/assets/img/profile/paul.png'
  ```

<br>
여기까지하면 기본적인 Navigation Bar 커스터마이징이 끝나게 된다.
<br><br>
이외의 나머지 설정은 다음과 같다.

<br>
<h3>2. 아바타가 뜨지 않는 문제와 Footer 수정</h3>
<hr>
필자의 경우, `_config.yml`에서 Avatar 부분을 수정했음에도 Avatar가 뜨지 않았다.
<br><br>
이에 ~~화가 난~~ 필자는 직접 코드를 일부 수정해주었다.
<br>
동일한 문제를 겪는 사용자는 필자와 같이 다음의 과정을 거치길 바란다.
1. `_includes`폴더로 이동
2. `sidebar.html`파일 열기
3. 19번째 줄을 다음과 같이 수정

```html
$ <img src="{{ avatar_url | strip }}" alt="avatar" onerror="this.style.display='none'">
<!-- 다음과 같이 수정 -->
$ <img src="사진 경로" alt="avatar" onerror="this.style.display='none'">
<!-- 필자는 다음과 같이 수정 -->
$ <img src="/assets/img/profile/paul.png" alt="avatar" onerror="this.style.display='none'">
```
이렇게 설정해주니 깔끔하게 해결되었다.
<br>
뭐든 안될때는 다이렉트로 연결해주는 것만큼 쉬운게 없다.
<br><br>
다음은 개인의 자유지만, 이것저것 난잡한 것이 싫은 필자는 이를 없애주었다.
<br>
바로 Footer에 적혀있는 "Using the Jekyll theme Chirpy"였다.
<br><br>
과감히 없애주자.
<br>
1. 마찬가지로 `_includes`폴더로 이동
2. `footer.html`파일 열기
3. 17번째 줄`<div class="footer-right">`부터 33번째 줄`</div>`까지 모두 주석처리
   * 단축키 : 드래그 후 `command + /`

이와 같이 설정하면 사라진 것을 볼 수 있다.

<br>
<h3>3. Favicon 설정</h3>
<hr>

블로그 탭에 표시되는 Favicon을 설정해보자.
<br>
의외로 간단하다.
<br><br>
먼저, 다음 사이트에 들어가서 Favicon에 필요한 포맷의 파일들을 다운받는다.
<br>
본인이 원하는 사진 혹은 png, jpg 형식의 파일을 업로드하고 변환된 형식의 `zip`파일을 다운받는다.

<p style="text-align: center">
	<a href="https://www.favicon-generator.org/" target="_blank"> --- Favicon Generator--- </a>
</p>

<br>
다운받았으면 압축된 파일을 푼 후 다음 과정을 거친다.
1. `assets/img/favicons`에 들어간다.
2. 기존에 설정되어있는 형식과 같은 형식 및 사이즈의 파일들을 확인한다.
3. 압축을 풀어낸 파일들에 해당하는 파일들을 찾은 후, 기존 파일들과 이름을 동일하게 설정하고 덮어씌운다.
  * **이 때, `browserconfig.xml` 파일과 `site.webmanifest` 파일은 건들지 않는다!!**

<br>
위 과정을 거치고 나면 완성된 나만의 Favicon으로 탭의 아이콘이 변경된 것을 확인할 수 있다.

<br>
<h3>4. 마치며</h3>
<hr>

드디어 나만의 블로그가 완성되었다.
<br><br>
위에 필자가 기술한 파일들 뿐만 아니라, 다른 파일들도 접근하여 수정하면 개인이 원하는 수준까지 커스터마이징이 가능하다.
<br><br>
블로그의 전체적인 배색 조합도 바꿀 수 있으며, 폰트도 수정이 가능하고 전체적인 형태도 수정이 가능하다.
<br><br>
개인의 재량에 따라 원하는 형식을 만들어 갈 수 있다는 게 깃허브 블로그가 가진 장점이 아닐까 싶다.
<br><br>
또한 위에 기술한 일부 파일 및 폴더들은, Chirpy-Starter에서는 해당이 안되는 경우도 있다.
<br>
참고하기를 바란다.
<br><br>
이번 포스팅은 이쯤에서 마무리하며, 다들 즐거운 블로그 생활을 하길 바란다..!!
<br><br>
~~이제 블로그 포스팅 뭐하지...~~