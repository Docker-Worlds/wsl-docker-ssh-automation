# wsl-docker-ssh-automation
이 문서는 WSL, SSH Server, Docker를 설치하였음을 상정한다.  
아래 링크에서 다음 내용을 확인 할 수 있다.  
https://github.com/SongDaeSun/WSL-SSH-Document  
  

### 컴퓨터 부팅시 자동 실행 프로그램 경로 찾기
```
cd /mnt/c/Users/song/AppData/Roaming/Microsoft/Windows/'Start Menu'/Programs/Startup
```
### sshd.bat이라는 파일명에 아래의 코드를 추가 작성한다.
```
"C:\Windows\System32\bash.exe" -c "sudo docker start basic"
"C:\Windows\System32\bash.exe" -c "sudo docker exec basic 'sudo docker exec -itu 0  basic bash_commands/ssh.sh' "
```
basic은 원하는 container의 name이다.  

### container 설정
basic bash_commands/ssh.sh에 다음과 같이 작성한다.
```
#!/bin/bash
sudo service ssh start
```

이렇게 설정을 해두면 컴퓨터를 reboot할 때마다 자동으로 container를 start하고,  
bash_commands/ssh.sh 내부에 작성된 코드가 실행된다.  
