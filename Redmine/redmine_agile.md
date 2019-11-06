#### Bitnami Redmine에 Agile 플러그인 설치하기

----

Bitnami 에 Redmine + Agile 스택도 있는데 

그냥 괜히 따로 설치해 보고싶어서 :)



회사에서 VM 을 사용하는데 .. 막힌것도 많고 안되는 것도 많고. 

인프라를 잘 모르니 이런 점이 너무 답답 ..  공부해야겠... 



설치 레고~

설치 시작하려했더니 총체적 난국 ..

- yum 을 지금 현재 사용할 수 없어서 unzip 사용 불가.
  - 로컬에 Linux용 설치파일 다운로드 > tar로 압축변경

- SFTP 막힘 .
  - Github 업로드 > wget으로 다운로드

살아날 구멍 찾았다.

쉬운방법 있을 수 있지만 당장 급하게 내 머릿속에는 저정도 생각밖에 없었다.

오래 걸리는 방법은 아니니 . 

.

.

.

실컷 설치하다가 Ruby 설치에서 막히고 다시 yum 이 안됬던 문제를 풀었다.

yum repository 변경하고 

ruby 설치하고 bundler 설치하고 재진행 !! 

하지만 현재 나의 Repo에서는 Ruby 2.0 까지만 지원한는데 그럼 bundler가 설치 되지 않는다.

산넘어 산이로다..

그냥 wget으로 받아서 설치 ! 설치는 아래 참조.



사전 작업해주세요 ~~~ 꼭!!



**1st. 어떤 방법이든 설치파일 다운로드**

/redmine/redmine-4.0.3-2/apps/redmine/htdocs/plugins 위치에 다운로드.

**2nd. htdocs 디렉토리에 gem 설치**

```shell
$ /redmine/redmine-4.0.3-2/use_redmine
$bash : cd apps/redmine/htdocs
$bash bundle install --without development test  --no-deployment
```

설치하면서 수많은 에러가 뜬 부분. 

대체적으로 에러 내용에 해결책이 제시 되어있다.

사전에 설치 되어야할 항목이 설치 되지 않았거나 system 라이브러리를 참조시켜준다

nokogiri -v '1.10.2' 를 설치할 수 없을 경우 :

```shell
$bash bundle config build.nokogiri --use-system-libraries
```

**3rd. redmine agile datavase에 설치 및 마이그레이션**

```shell
$bash bundle exec rake redmine:plugins NAME=redmine_agile RAILS_ENV=production
```

**4th. redmine 재시작**

```shell
$bash /redmine/redmine-4.0.3-2/ctlscript.sh restart
```

**5th. redmine에서 애자일 사용 !** 



삽질 삽질 ... 또 삽질 ... 

삽질하다 하루가 갔다 .. 

실컷 설치했더니 안되고, 지웠다 설치했다 반복하다 본건데 ... 

./use_redmine 으로 bash shell 에 접속하면 

자체적으로 있는 ruby 를 사용하나보다 . 

현재 설치한 버전은 ruby 2.4 까지지를 지원하지만 . 

자체적으로는 2.5 지원 . 결론은 ? 

프로젝트랑 뭐랑 다 404가 뜬다 .. 이 문제가 맞길 바라며 redmine 버전 변경 중 . 

제발 맞아라 ㅜㅜㅜ 힘들어 



후기 :

음 두개의 버전은 서로 지원을 하고 있으며 어디서 꼬였는지 찾지는 못했지만 . 

성공 !