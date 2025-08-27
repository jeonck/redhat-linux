# RHEL 9.4 주요 명령어 모음

Red Hat Enterprise Linux (RHEL) 9.4의 활용도를 극대화할 수 있는 주요 명령어들을 목적별로 정리한 문서입니다.

### 1. 시스템 관리 및 정보 확인

- **`systemctl`**: 서비스와 시스템 유닛(unit)을 관리하는 가장 중요한 명령어입니다.
  - `systemctl start [서비스명]`: 서비스 시작
  - `systemctl stop [서비스명]`: 서비스 중지
  - `systemctl restart [서비스명]`: 서비스 재시작
  - `systemctl enable [서비스명]`: 부팅 시 서비스 자동 시작 설정
  - `systemctl disable [서비스명]`: 부팅 시 서비스 자동 시작 해제
  - `systemctl status [서비스명]`: 서비스 상태 확인

- **`journalctl`**: systemd 저널 로그를 확인하고 분석합니다.
  - `journalctl -u [서비스명]`: 특정 서비스의 로그 확인
  - `journalctl -f`: 실시간 로그 확인
  - `journalctl --since "1 hour ago"`: 특정 시간 이후의 로그 확인

- **`hostnamectl`**: 시스템의 호스트 이름을 확인하고 변경합니다.

- **`timedatectl`**: 시스템의 시간, 날짜, 타임존을 관리합니다.

### 2. 소프트웨어 패키지 관리 (DNF)

RHEL 9에서는 `yum` 대신 `dnf`를 기본 패키지 관리자로 사용합니다.

- **`dnf install [패키지명]`**: 새로운 패키지를 설치합니다.
- **`dnf remove [패키지명]`**: 설치된 패키지를 삭제합니다.
- **`dnf update`**: 시스템의 모든 패키지를 최신 버전으로 업데이트합니다.
- **`dnf search [키워드]`**: 패키지를 검색합니다.
- **`dnf list installed`**: 설치된 모든 패키지 목록을 보여줍니다.
- **`dnf info [패키지명]`**: 패키지의 상세 정보를 확인합니다.

### 3. 네트워크 관리

- **`nmcli` (NetworkManager Command Line Interface)**: 네트워크 연결을 관리하는 표준 도구입니다.
  - `nmcli device status`: 네트워크 장치 상태 확인
  - `nmcli connection show`: 활성화된 연결 정보 확인
  - `nmcli connection up [연결이름]`: 특정 연결 활성화

- **`ip`**: IP 주소, 라우팅 테이블 등 네트워크 인터페이스를 관리합니다. (`ifconfig`를 대체)
  - `ip addr show`: 모든 네트워크 인터페이스의 IP 주소 확인
  - `ip route`: 라우팅 테이블 확인

- **`ss`**: 네트워크 소켓 정보를 확인합니다. (`netstat`을 대체)
  - `ss -tuln`: TCP/UDP 리스닝 소켓 정보 확인

- **`firewall-cmd`**: `firewalld` 방화벽을 제어하는 명령어입니다.
  - `firewall-cmd --list-all`: 현재 방화벽 설정 확인
  - `firewall-cmd --add-service=[서비스명] --permanent`: 특정 서비스를 영구적으로 허용
  - `firewall-cmd --add-port=[포트/프로토콜] --permanent`: 특정 포트를 영구적으로 허용
  - `firewall-cmd --reload`: 방화벽 설정을 다시 로드

### 4. 파일 시스템 및 디스크 관리

- **`df -h`**: 디스크 사용량을 사람이 읽기 쉬운 형식으로 보여줍니다.
- **`du -sh [경로]`**: 특정 디렉토리의 총 사용량을 보여줍니다.
- **`lsblk`**: 블록 디바이스(디스크, 파티션) 목록을 트리 형태로 보여줍니다.
- **`find [경로] -name "[파일명]"`**: 특정 이름의 파일을 검색합니다.
- **`grep -r "[문자열]" [경로]`**: 특정 디렉토리 내의 모든 파일에서 문자열을 검색합니다.

### 5. 성능 모니터링 및 트러블슈팅

- **`top` / `htop`**: 시스템의 실시간 프로세스 및 리소스 사용량을 확인합니다. (`htop`은 별도 설치 필요)
- **`ps aux`**: 현재 실행 중인 모든 프로세스를 상세하게 보여줍니다.
- **`free -h`**: 메모리 사용량을 사람이 읽기 쉬운 형식으로 보여줍니다.
- **`iostat`, `vmstat`, `sar`**: CPU, 메모리, I/O 등 시스템 리소스의 통계 정보를 확인합니다. (`sysstat` 패키지 설치 필요)
- **`strace [명령어]`**: 특정 명령어의 시스템 호출(system call)을 추적하여 디버깅에 활용합니다.

### 6. 보안 (SELinux)

RHEL의 강력한 보안 기능인 SELinux를 제어합니다.

- **`sestatus`**: SELinux의 현재 상태와 모드를 확인합니다.
- **`getenforce`**: SELinux의 현재 모드(Enforcing, Permissive, Disabled)를 확인합니다.
- **`setenforce [0|1]`**: SELinux 모드를 임시로 변경합니다. (0: Permissive, 1: Enforcing)
- **`chcon` / `restorecon`**: 파일이나 디렉토리의 SELinux 보안 컨텍스트(context)를 변경하거나 복원합니다.
