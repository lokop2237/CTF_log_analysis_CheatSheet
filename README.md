# Log Anaylsis Process
1. 침투 경로 파악
2. 권한 상승 파악
3. 지속공격 탐색
##

1. 침투 경로 파악 (취약점 분석, 접속 로그 분석)

```
> 취약점 분석
nmap,scanner,etc...

> 접속 성공 로그 확인 (/var/log/wtmp)
last [user name]   (= last f /var/log/wtmp)           # 최근 접속기록 출력
last -t [YYYYMMDDhhmmss]                              # 특정날짜 이후 접속기록 출

> 접속 실패 로그 확인 (/var/log/btmp)
last -f /var/log/btmp

> 웹 접속 로그 확인 (/var/log/apache2(or nginx,etc...)
포맷에 맞게 잘 뽑아서 보기

> 원격 로그인 인증 정보 확인 (/var/log/secure)

> 명령어 확인 (~/.bash_history)
```

2. 권한 상승 파악
```
> ssh, sudo, PAM 확인 (/var/log/secure)
cat /var/log/secure* | grep Accepted | awk '{print $1, $2, $3, "\t", $9, "\t", $11, "\t", $14}' | sort | uniq
```

3. 지속공격 탐색 (백도어, 프로세스,서비스 등)
```
> 정상 실행중인 서비스 리스트 확인
sudo systemctl list-units --type=service --state=running | grep -v "^\s*●"

> 의심되는 서비스가 어떤건지 확인
systemctl status [의심되는 서비스명] | head -20
```
