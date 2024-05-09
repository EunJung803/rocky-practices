1. tomcat9 다운로드

```bash
wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.89/bin/apache-tomcat-9.0.89.tar.gz
```

2. 압축 풀기

```bash
tar xvfz apache-tomcat-9.0.89.tar.gz
```

3. 설치

```bash
mv apache-tomcat-9.0.89 /usr/local/poscodx
cd /usr/local/poscodx
ln -s apache-tomcat-9.0.89 tomcat
```

4. 포트 확인(/usr/local/poscodx/tomcat/conf/server.xml)

```xml
...
 <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
...
```

5. 실행

```bash
/usr/local/poscodx/tomcat/bin/catalina.sh start
ps -ef | grep tomcat
```

6. 방화벽(firewalld, 8080 포트) 열기
7. [/etc/firewalld/zones/public.xml](https://github.com/bitacademy-poscodx/rocky-practices/blob/main/lx/etc/firewalld/zones/public.xml) 생성

```xml
<?xml version="1.0" encoding="utf-8"?>
<zone>
  <short>Public</short>
  <description>For use in public areas. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted.</description>
  <service name="ssh"/>
  <service name="tomcat"/>
  <service name="dhcpv6-client"/>
  <service name="cockpit"/>
  <forward/>
</zone>
```

8. [/usr/lib/firewalld/services/tomcat.xml](https://github.com/bitacademy-poscodx/rocky-practices/blob/main/lx/usr/lib/firewalld/services/tomcat.xml) 생성

```xml
<?xml version="1.0" encoding="utf-8"?>
<service>
  <short>Tomcat</short>
  <description></description>
  <port protocol="tcp" port="8080"/>
</service>
```

9. 방화벽 서비스 재실행

```bash
systemctl stop firewalld
systemctl start firewalld
```

10. 방화벽 켜져도 브라우저로 접근 하기
[http://192.168.64.7:8080](http://192.168.80.203:8080/)
211 중지 시키기

```bash
/usr/local/poscodx/tomcat/bin/catalina.sh stop
```

12. 서비스 등록 하기

```bash
vi /usr/lib/systemd/system/tomcat.service
```

```xml
[Unit]
Description=tomcat9
After=network.target syslog.target

[Service]
Type=forking

Environment=JAVA_HOME=/usr/local/poscodx/java

User=root
Group=root

ExecStart=/usr/local/poscodx/tomcat/bin/startup.sh
ExecStop=/usr/local/poscodx/tomcat/bin/shutdown.sh

UMask=0007
RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target
```

13. tomcat 서비스 실행/중지/재실행

```bash
systemctl start tomcat
systemctl stop tomcat
systemctl restart tomcat
```

14. tomcat manager 설정
    - tomcat-users.xml 설정

```bash
cd /usr/local/poscodx/tomcat/conf
vi tomcat-users.xml
```

```xml
<tomcat-users>
  . . .
  . . . 
  <role rolename="manager"/>
  <role rolename="manager-gui" />
  <role rolename="manager-script" />
  <role rolename="manager-jmx" />
  <role rolename="manager-status" />
  <role rolename="admin"/>
  <user username="admin" password="manager" roles="admin,manager,manager-gui, manager-script, manager-jmx, manager-status"/>
</tomcat-users>
```

- context.xml 설정

```bash
cd /usr/local/poscodx/tomcat/webapps/manager/META-INF
vi context.xml
```

```xml
<!--
<Context>
 ....
</Context>
-->
기존꺼 주석처리 -> 새로 다음내용 추가
<Context antiResourceLocking="false" privileged="true" docBase="${catalina.home}/webapps/manager">
  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="^.*$" />
</Context>
```

15. tomcat 재시작

```bash
systemctl stop tomcat
ps -ef | grep tomcat
systemctl start tomcat
```

16. [http://192.168.64.7/manager](http://192.168.80.131/manager) 접속 !
