1. 의존성 라이브러리

```bash
yum -y install curl-devel
yum -y install expat-devel
yum -y install gettext-devel
yum -y install openssl-devel
yum -y install zlib-devel
yum -y install perl-devel
```

2. 다운로드

```bash
wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.45.0.tar.gz
```

3. 압축 풀기

```bash
tar xvfz git-2.45.0.tar.gz
```

4. 소스 디렉토리 이동

```bash
cd git-2.45.0
```

5. configure compile & build Environment

```bash
./configure --prefix=/usr/local/poscodx/git-2.45.0
```

6. 빌드

```bash
make all
또는
make
```

7. 설치

```bash
make install
```

8. 링크 달기 (절대경로 걸기)

```bash
cd /usr/local/poscodx
들어가서
ln -s git-2.45.0 git
```

9. 설정(/etc/profile)

```bash
export PATH=$PATH:/usr/local/poscodx/git/bin
```

10. 확인

```bash
source /etc/profile
git --version
```

