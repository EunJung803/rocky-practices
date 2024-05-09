1. 작업 디렉토리

```bash
/root
```

2. 다운로드

```bash
wget https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
```

3. 압축 풀기

```bash
tar xvfz apache-maven-3.9.6-bin.tar.gz
```

4. 설치

```bash
mv apache-maven-3.6.6 /usr/local/poscodx/maven3.8
cd /usr/local/poscodx
ln -s maven3.9.6 maven
```

5. 설정(/etc/profile)

```bash
# maven
export PATH=$PATH:/usr/local/poscodx/maven/bin
```
