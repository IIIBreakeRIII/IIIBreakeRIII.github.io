---
layout: post
title: "[Devlog] 나의 NeoVIM Configuration"
author : Dev.Paul
categories: Daily
tags:
  - Develop
  - Developer
  - Studet
  - Vim
  - NVim
  - NeoVim
  - NVim-Config
image: nvim.png
---

<br>

> 내가 세팅한 NeoVim Configuration

<br>
<h3>0. 들어가며</h3>
<hr>

어느날 열심히 Visual Studio Code를 쓰는데, 뭔가 예쁘지가 않으니 코딩할 맛이 안나더라. ~~사실 코딩하기 싫었다~~
<br><br>
그래서 예쁜 에디터를 찾던 와중, 일본의 개발자이자 유튜버인 [devaslife](https://www.youtube.com/@devaslife)의 영상을 보게되었다.
<br><br>
_오.. 생각보다 저 에디터 예쁜데.. 뭐지?_
<br><br>
해당 유튜버의 영상들을 찾다보니 에디터가 NeoVim인걸 알게 되었고,
<br>
__마침__ 맥이 작업환경이던 나는,
<br>
__마침__ 전 학기 수업에서 리눅스 시스템에 대한 기본을 배웠던 나는,
<br><br>
_"한번 써볼까?"_ 를 시전하며 NeoVim을 설치했고, 그렇게 Vim의 세계로 여행을 떠났다.
<br><br>
~~그때 발을 들이지 말았어야 했어..~~

<br>
<h3>1. 내 세팅</h3>
<hr>

결론부터 얘기하면, 내 세팅은 최종적으로 다음 이미지와 같이 나온다.
<br>
<p  align="center">
	<img src="https://github.com/IIIBreakeRIII/IIIBreakeRIII.github.io/assets/89850286/4ddae566-6c35-41ff-9001-1b115089ebd4">
	My NeoVim Preview
</p>
<br>
생각보다 예쁘고 _(내 생각인가 여튼)_ Vi에디터의 사용에만 익숙해지면 충분히 사용할만하다.
<br><br>
먼저, [NeoVim](https://neovim.io/)에 대해 간략히 설명을 해보자면 VI라는 유닉스 계열 운영체제에서 쓰는 빌 조이가 개발한 문서 편집기가 그 시초이다.
<br>
그 이후, vim이라는 vi의 Improved된 형태의 문서 편집기가 출시되었다. 대체로 유닉스 혹은 리눅스 운영체제의 터미널에서 vi 혹은 vim이라고 입력하면 자동으로 vim이 실행된다.
<br>
NeoVim은 이러한 vim을 개선해 나간 프로젝트로서, vim보다 더 다양한 기능을 제공하며, 상대적으로 오픈소스 프로젝트였던 vim이 여러 사람의 손을 거치며 복잡해진 코드와 형태들을 다시 만들어가며 이를 가볍게 만들어낸 프로젝트였다.
<br><br>
neovim의 가장 큰 장점은 여러가지가 있는데 간략하게 정리해보면 다음과 같다.
- 24bit True Color 지원
- 다양한 PlugIn
- 자체 LSP(Language Server Protocol)
- lua, vim을 이용한 설정

등등 여러가지가 있다.

<br>
<h3>2. NeoVim 설치</h3>
<hr>

먼저 NeoVim부터 설치해야한다.
<br>
내 작업용 디바이스는 맥이기에 맥을 기반으로 기술하였다.
<br>
모든 디바이스의 설치 과정에 대해서는 다음 NeoVim에서 제공하는 <a href="https://github.com/neovim/neovim/blob/master/INSTALL.md" target="_blank">Neovim Readme</a>을 참고바란다.
<br>
- Homebrew가 없을 경우
```terminal
curl -LO https://github.com/neovim/neovim/releases/download/nightly/nvim-macos.tar.gz
tar xzf nvim-macos.tar.gz
./nvim-macos/bin/nvim
```
- Homebrew가 있을 경우
```terminal
brew install neovim
```

혹은 위의 리드미 링크를 통해 들어가서 다운로드를 받아도 된다.

<br>
<h3>3. PlugIn 설치를 위한 과정</h3>
<hr>

Nvim에서 플러그인을 관리하기 위한 방법에는 여러가지가 있지만, 필자는 `vim-plug`를 이용한다.
<br>
다음은 <a href="https://github.com/junegunn/vim-plug" target="_blank">`vim-plug`</a>에서 제공하는 Readme이며 다음 과정을 거쳐 설치한다.
<br><br>
터미널에서, 
```terminal
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

설치가 완료되면 터미널에 다음 명령어를 치고 해당 디렉토리로 접근한다.
```terminal
cd ~/.config/nvim
```

해당 디렉토리에 `nvim`이라는 디렉토리를 없다면 `mkdir` 명령어를 이용해 디렉토리를 만들어주고 접근한다.
<br><br>
해당 디렉토리로 접근하면 `init.vim`이라는 파일을 하나 생성해줘야 한다.
<br>
이는 vim 설정을 위한 파일로써, 각종 플러그인 및 키 바인딩, vim 자체 설정 등 모든 설정을 관여하는 파일이다.
<br><br>
해당 파일에서 다음 명령으로 다운받은 `vim-plug`를 불러오면 된다.
```vim
call plug#begin('/plugged' : '~/.config/nvim/after')
" PlugIn 목록
call plug#end()
```
참고로 `'/plugged' : '~/.config/nvim/after'` 코드는 해당 디렉토리에 접근하여 PlugIn 별 환경 설정 파일을 불러올 수 있도록 해주는 코드이다.
<br><br>

<br>
<h3>4. PlugIn 소개</h3>
<hr>

필자가 현재 쓰고 있는 모든 플러그인 및 vim 환경 설정은 다음 두 깃허브 레포지토리에 공개되어 있다.
<br><br>
필요한 사람이 있다면 클론해 가면 된다.
<br>
또한 2023 버전의 경우, 간단하게 리드미도 작성해 놓았으니, 참고하면 된다.

<p style="text-align: center">
	<a href="https://github.com/IIIBreakeRIII/nvim-source-ver.2023" target="_blank">--- NVim Configuration 2023 ---</a>
</p>

<p style="text-align: center">
	<a href="https://github.com/IIIBreakeRIII/nvim-source-ver.2024" target="_blank">--- NVim Configuration 2024 ---</a>
</p>

<br>
플러그인은 2024년을 기준으로 소개하며, 대표적인 플러그인 위주로 소개한다.
<br>
- <a href="https://github.com/nvim-treesitter/nvim-treesitter" target="_blank">nvim-treesitter</a>
	- 언어별 파싱 및 구문 강조(syntax highlighting)와 들여쓰기(indentation)를 지원해주는 플러그인
- <a href="https://github.com/neovim/nvim-lspconfig?tab=readme-ov-file" target="_blank">nvim-lspconfig</a>
	- Language Server Protocol Configuration을 위한 플러그인
- <a href="https://github.com/neoclide/coc.nvim" target="_blank">coc.nvim</a>
	- Conquer Of Completion, 자동완성 및 코드 스니펫을 제공하는 플러그인
- <a href="https://github.com/nvim-lualine/lualine.nvim" target="_blank">lualine.nvim</a>
	- NeoVim 상태 표시줄을 커스터마이징하는 플러그인
- <a href="https://github.com/preservim/nerdtree" target="_blank">nerdtree</a>
	- 파일 시스템 탐색기 플러그인
- <a href="https://github.com/preservim/tagbar" target="_blank">tagbar</a>
	- 현재 작업중인 파일의 태그 및 구조에 대한 overview 제공해주는 플러그인
- <a href="https://github.com/nvim-tree/nvim-web-devicons" target="_blank">nvim-web-devicons</a>
	- 파일 타입에 따라 아이콘을 만들어주는 플러그인, **nerd fonts 필요**
- <a href="https://github.com/romgrk/barbar.nvim" target="_blank">barbar.nvim</a>
	- Neovim 상단 탭라인 플러그인
- <a href="https://github.com/nvim-telescope/telescope.nvim" target="_blank">telescope.nvim</a>
	- nvim 자체 하위 파일 탐색기
- <a href="https://github.com/NeogitOrg/neogit" target="_blank">neogit</a>
	- git 인터페이스
- <a href="https://github.com/sindrets/diffview.nvim" target="_blank">diffview.nvim</a>
	- git  버전 관리를 위한 추적 인터페이스

<br>
해당 플로그인들로 기본적인 인터페이스를 구성할 수 있으며, 각 플러그인 별 사용 방법은 Readme를 참고하면 된다.
<br><br>
플러그인을 다운 받는 방법은 일반적으로 다음과 같다.
```vim
" Plug "깃허브ID"/"플러그인 이름"
" 아래는 예시
Plug 'NeogitOrg'/'neogit'
```

<br>
<h3>5. 키 바인딩 방법</h3>
<hr>

Vim에서 키 바인딩 방법은 vim과 lua에 따라 그 방법이 조금 다르다.
<br><br>
먼저 vim의 경우 다음 방법으로 키 바인딩을 진행한다.
<br>
```vim
" <모드><바인딩할 키><명령어><Enter 키>
" 아래는 NORMAL 모드에서 :w 명령어를 맥 기준 <option> + s 로 바인딩하는 예시
nmap <A-s> :w <CR> 
```

lua 의 경우 다음 방법으로 키 바인딩을 진행한다.
<br>
```lua
-- map('모드', '바인딩할 키', '명령어', 'opts')
-- 아래는 NORMAL 모드에서 :w 명령어를 맥 기준 <option> + s 로 바인딩하는 예시
map('n', '<A-s> <CMD>w<CR>, opts)
```

<br>
<h3>6. 마지막 관문</h3>
<hr>

이제 마지막 관문이다.
<br><br>
**취향에 맞게 꾸미면 된다!**
<br><br>
폰트부터, 색, 플러그인까지 개인의 입맛대로 꾸밀 수 있는것이 vim 에디터의 가장 큰 장점이다.
<br>
일반적으로 폰트는 _Nerd_ 폰트를 추천한다. 필자의 경우, <a href="https://www.nerdfonts.com/font-downloads" target="_blank">CaskaydiaCove Nerd Font</a>를 사용한다.
<br><br>
테마는, 본인이 원하는 테마를 사용하면 된다.
<br>
<a href="https://github.com/topics/vim-colorscheme" target="_blank">깃허브 토픽</a>에서 테마를 찾아도 되고, 색 조합을 제공해주는 것은 해당 색 조합을 입력해주어 세팅해주면 된다.
<br><br>
플러그인 또한, 개인이 편한 플러그인 혹은 필요한 플러그인을 검색하면 없는 건 거의 없다.
<br>
필자의 경우, 추가적으로 깃허브 코파일럿, 마크다운 프리뷰 등과 같은 플러그인도 설치한 상태이다.

<br>
<h3>7. 정리하며</h3>
<hr>

Vim 환경은, 러닝커브가 크다는 단점이 있지만 그만큼 빠르게 작업이 가능하다는 장점이 있다.
<br>
마우스를 사용하지 않아도 되고, 키보드 안에서 모든 개발이 가능해지기 때문이다.
<br><br>
또한, 리눅스 명령어에 익숙한 사람이면 ~~(사실 그런 사람은 Vim이 익숙할테지만)~~ 터미널과 Vim의 환상적인 조합은 그 어떠한 에디터도 따라올 수 없다.
<br><br>
터미널에서 파일을 관리하고, Vim으로 개발하며, 다시 터미널에서 커맨드로 완료하는 그 과정이 정말 끝내준다!
<br><br>
개발자라면 한번쯤은 시도해볼만 한 에디터라고 생각한다.
<br><br>
그럼, Adios.