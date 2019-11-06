#### Linux(RHEL/CentOS)에 Ruby 2.3.0설치하기 (yum 없이)

------

yum 이 완전히 필요 없는 건 아니다.

사진 설치 부분이 필요 ! 

이것도 대체하는 방법이 있긴 하겠지만. 

yum repository를 변경하는게 더 빠른 방법 인 거 같다.

yum 이 있음에도 사용하지 않은 이유는 yum 이 있긴하나 bundler를 사용하는 부분에서 

yum에서 제공하는 Ruby2.0 은 아무런 소용이 없기 때문이다.(제껀 그랬어요/업뎃불가)



**1st. yum으로 사전 필요 요소 설치**

```shell
$ yum install openssl-devel readline-devel zlib-devel curl-devel libyaml-devel
```

**2nd. wget 으로 원하는 버전의 Ruby 파일 다운로드 및 압축해제** 

/usr/local 아래에 다운로드

압축 해제 후 압축파일 삭제 ~ 

```shell
$ wget https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.0.tar.gz
$ tar xvf ruby-2.3.0.tar.gz
```

**3rd. 설치**

```shell
$ cd /usr/local/ruby-2.3.0
$ ./configure --disable-install-doc
$ make
$ make install
$ make clean
```

4th. bundler 설치

```shell
$ gem install bundler --no-rdoc --no-ri
```



설치 완료 ! 