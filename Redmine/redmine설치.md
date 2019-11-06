####Bitnami 로 Redmine 설치하기

-----

리눅스에 개발환경 셋팅 시작 ! 

얼마나 오랜만에 Linux를 만지는지 .. 맨날 PPT만 작성하다가 .. :-(

레고~~:) 

새로운 프로젝트를 위한 개발환경 구성. 



DB 부터 한땀한땀 설치해보려 했지만

rhel 이미지가 문제인건지 회사 네트워크가 문제인건지 redhat 미러 서버 접속 불가 상태였다.

Bitnami로 Windows에 설치해본 결과 쓸만 했었기에 열정 잠시 내려두고, 

현실적으로 Bitnami로 설치하기로 했다.



> 열심히 설치를 다하고 났더니...  뭐때문인제 레드마인에 레드도 안보인다 ? 
>
> 레드마인 아니였음 .. 램프스택 
>
> 왜그래 진짜 .. 너 뭐해? 정신차렷
>
> 문서 수정... 



###1. VM 사전 설정

**설치환경 정보**

```
Openstack VM
Linux redhat7.2
```

##### 1st . DNS 변경 설정

로컬 DNS 서버로 불가능하므로 Google nameserver 추가 ! 

vi /etc/resolv.conf  < 추가

```shell
# Google IPv4 nameservers
nameserver 8.8.8.8
nameserver 168.126.63.1
```



### 2. Bitnami로 설치하기

설치하기 전 설치할 위치에 다운받기 !!!!! (레드마인 서버니까 위치는 root 밑에 ??  $ mkdir /redmine)

#####1st.  파일 다운로드

파일 확인 ::: <https://bitnami.com/stack/redmine/installer>

```shell
$ wget https://bitnami.com/redirect/to/520895/bitnami-redmine-4.0.3-2-linux-x64-installer.run
```

#####2nd. 다운받은 파일에 대한 위한 권한 변경 

```
$ chmod 755 bitnami-lampstack-7.2.18-0-dev-linux-x64-installer.run
```

```shell
[root@redhat7 redmine]# ls -al
total 230044
drwxr-xr-x.  2 root root        67 May 27 00:31 .
dr-xr-xr-x. 19 root root      4096 May 27 00:30 ..
-rwxr-xr-x.  1 root root 235557182 May  3 20:57 bitnami-redmine-4.0.3-2-linux-x64-installer.run
```

##### 3rd. 사전 설정 완료 ! 설치 시작 :) 

root 권한으로 실행했어요.

```shell
$ ./bitnami-redmine-4.0.3-2-linux-x64-installer.run
```

설치를 시작하면 ' press [Enter] to continue: ' 를 시작으로 설치될 컴포넌트에 대해 yes or no (y/n) 을 수 없이 묻는다.

다음으로 설치 할 디렉토리 입력!  default 는 /opt 아래, 하지만 난 /redmine 아래 설치.

그리고 계정 입력.

단 몇 가지 조건이 있다.

- 6자 이상 (equal or greater than 6)
- 알파벳과 숫자만 (use only alphanumeric)

요즘은 다 특수문자 써야 하는데 얘는 예외다. 

매번 하는 고민 . 비번 뭘로 하지 ? 사이트마다 다 다르고, 쓸데마다 비번 찾기 바쁘고. 

저만 그런가요 ? 

다시 y/n 을 몇 번 묻고 나면 설치 완료 ! 

간편하긴 하다. 정말 



**4th. 설치 완료! 접속하기** 

VM(or host) IP로 접속하면 웹페이지를 확인 할 수 있다.

관리자 권한으로 로컬에 설치하였다면 80 포트 이외이 계정이라면 8080 포트로 접속하면 된다.

공인 IP 대역의 VM 에 설치 했으니 IP를 변경 해야한다. 

설치폴더/apache2/conf/httpd.conf 에서 Servername **localhost**:80 부분 수정.

그리고 접속해 보았을때 Access Redmine 이 뜬다면 성공 :)

