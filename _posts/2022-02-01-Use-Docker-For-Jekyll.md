---
layout: post
title: "Using Docker for Jekyll and Blog Development"
tags: tech
date: 2022-02-01
author: Dr.You
---

# Jekyll를 이용해서 만든 GitHub Blog Docker 에서 작업하기

In Mac

`$ docker run jekyll/jekyll:4.0 --volume="[directory]:/srv/jekyll" -p 4000:4000 --rm -it /bin/bash`

#### 명령어 설명

`docker run` : docker 실행

`jekyll/jekyll:4.0` : Blog 개발 시 사용한 도커 허브 이미지 (Jekyll 4.0 version)

`--volume="[directory]:/srv/jekyll"` : 로컬과 Jekyll 컨테이너 사이에 공유할 폴더 지정. 로컬에서는 [directory] 폴더, 지킬 컨테이너에서는 /srv/jekyll 의 폴더를 동기화하여 사용한다. 보통은 https://dr-you-group.github.io/ github 을 clone 한 후 이후 작업하는 github repo 를 입력한다. Mac의 경우 docker 앱에서 공유할 폴더를 추가로 지정하는 것이 필요했다(docker app>Preferences>Resources>FILE SHARING)

`-p 4000:4000` : 컨테이너의 특정 포트를 외부로 노출하는 명령어로 -p <호스트 포트="">:<컨테이너 포트="">의 형식으로 이루어진다. 지킬 컨테이너에서 serve 한 결과를 로컬 포트에서 확인할 수 있다. 4000:3999 이런 식으로 지정도 가능하다.

`--rm` : docker container 실행이 끝나면 container 삭제

`-it` : Interactive terminal option으로 결과를 터미널에 출력

`/bin/bash` : bash로 실행한다.

위와 같이 명령어 실행 후 docker container 에서 하기 명령어 실행하여 blog를 로컬에 deploy

`$ jekyll serve`

이후 로컬에서 `http://0.0.0.0:4000/` 으로 접속하여 확인 가능.
파일 변경 시 바로바로 웹페이지 새로고침을 이용하여 변경 내역을 확인할 수 있다.
container 종료 시에는 Ctrl + C (webpage deployment 종료) 이후 `exit` 을 입력하면 된다.

### Reference
https://jgtonys.github.io/blog/2019/04/25/docker-jekyll/

https://youtu.be/sFM0J-8OTP4
