## Java17 설치

1. JDK 다운로드
```sh
# wget https://download.oracle.com/java/17/archive/jdk-17.0.10_linux-x64_bin.tar.gz
```

2. 압축을 푼다.
```sh
# tar xvfz jdk-17.0.10_linux-x64_bin.tar.gz
```

3. 포스코dx 소프트웨어 설치 디렉토리 만들기
```sh
# mkdir /usr/local/poscodx
```

4. 설치
```sh
# mv jdk-17.0.10 /usr/local/poscodx
```

5. 링크 파일 생성
```sh
# ln -s /usr/local/poscodx/jdk-17.0.10 /usr/local/poscodx/java
```

6. 설정(/etc/profile)
```sh
# java
export JAVA_HOME=/usr/local/poscodx/java
export CLASSPATH=.:$JAVA_HOME/lib/*
export PATH=$PATH:$JAVA_HOME/bin

```

7. 확인
```sh
# source /etc/profile
# java --version
java 17.0.10 2024-01-16 LTS
Java(TM) SE Runtime Environment (build 17.0.10+11-LTS-240)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.10+11-LTS-240, mixed mode, sharing)

#
```
