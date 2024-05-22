## File System

- 리눅스 파일시스템은 1994년에 FHS가 제안되면서 재정비 되었다.


| File | Information | Example |
| --- | --- | --- |
| /bin | 필수적인 커맨드의 바이너리들이 들어있음 | la/cp/mv/cat/echo, /bash/mkdir/rm |
| /proc | 커널, 시스템, 프로세스 등에 대한 현재 상태정보를 제공 | /proc/cpuinfo, /proc/sys/kernel |
| /lib | Shared library(.so) 모듈들이 들어있음 | /lib/libc.so.6, /lib/ld-linux.so.2 |
| /sys | 커널 파라미터와 조정을 위한 인터페이스 제공 | /sys/fs/cgroup, /sys/fs/cgroup |
| /boot | 커널, 부트로더 등 부팅에 관련된 필수 파일들 제공 | /boot/vmlinux-5.4.0-90-generic |
| /root | 슈퍼 유저 혹은 루트 유저를 위한 Home 디렉터리 | /root/.bash_profile, /root/.vimrc |
| /media | USB, External HDD 등의 마운트 포인트로 사용됨 | /media/disk, /media/usb0 |
| /tmp | 임시로 생성되는 파일들 시스템이 주기적으로 청소함 | Temporary Directories, Temporary Sockets |
| /dev | 커널과 유저 스페이스 사이의 디바이스 인터페이스 관련 | /dev/tty1, /dev/tty2, /dev/sda, /dev/sdb |
| /run | 시스템 런타임에 생성되는 임시파일들과 상태 저장 | /run/lock/myproc.lock, /run/udev/control |
| /mnt | 시스템 관리자가 외부 장치를 마운트할 때 주로 사용됨 | /mnt/usb0, /mnt/nfs |
| /usr | 시스템 부팅에 필수는 아니지만 유저에 관련된 프로그램들 | /usr/bin/gcc, /usr/sbin/iptables |
| /etc | Host-specific, System-wide한 설정 파일들 | /etc/passwd, /etc/hostname |
| /sbin | 시스템 필수 바이너리들, 시스템 관리나 유지보수 관련 | /sbin/sysctl, /sbin/fsck |
| /opt | Add-on 패키지 같은거 설치 할 때 주로 사용 | /opt/google/chorme, /opt/oracle |
| /var | 로그 같은 런타임에 자주 쓰거나 읽어야 하는 정보들 | /var/log/syslog, /var/spool/cron |
| /home | 유저 어카운트들의 홈 디렉터리 | /home/coderxdox1,, /home/coderxdox2 |
| /srv | Site-specific 한 데이터들 | /srv/git/project.git, /srv/database/mysql |
