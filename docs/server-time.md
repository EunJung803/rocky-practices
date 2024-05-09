### timezone
```sh
# timedatectl
# timedatectl set-timezone Asia/Seoul
```
### Sync Server Time
```sh
# yum -y install chrony
# vi /etc/chrony.conf        (타임서버 수정/추가)
# systemctl restart chronyd
# systemctl status chronyd
# chronyc sources -v
```
