#### Redmine 플러그인 설치 시 유의사항 필독 !!!!!! 

---

#### 1. Redmine Plugin 설치 위치

{설치폴더}/apps/redmine/htdocs/plugins

설치파일 다운로드 후 압축해제 > 압축파일 삭제 > **해당 Plugin 이름으로 폴더명 변경**

> 플러그인 덕분에 ./uninstall 거짓말 하나 안보태고 최소 20번은 했다.
>
> 플로그인 설치 전.. 반드시 Redmine 폴더 백업(cp-rp)해주세요 ^^
>
> 삭제 시 .
>
> > **rake redmine:plugins:migrate NAME=plugin_name VERSION=0 RAILS_ENV=production**
> >
> > 그리고 플러그인 폴더 삭제. 



####2. 권한문제 

에러내용 : Don't run Bundler as root. Bundler can ask for sudo if it is needed ~

Bundle 사용 시 권한 문제로 root 계정이나 sudo 명령어는 사용하지 않는다.

그러므로 htdocs 의 아래에 있는 폴더는 잠시 chmod 777 로 변경.



#### 3. Redmine 2.4.0 이상의 새버전

bundle install 에 --no-deployment 추가 후 실행