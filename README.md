# GopaxApiTradingExample
[멋쟁이사자처럼 X 고팍스] 가상자산 자동거래 시스템 만들기

GOPAX API 명세서 URL : https://gopax.github.io/API/?lang=ko

### 1.AWS, 고팍스 API 사용에 대한 내용 설명


### 2.EC2 인스턴스, Cloud9 설정
- EC2 접속키 생성(키페어)
    - EC2 > 키 페어 > 키페어 생성 
    - 이름 : GopaxApiTradingExample
    - 파일 다운로드 위치 확인

- 스택생성
    - CloudFormation > 스택 생성
    - Amazon S3 URL : https://gopax-likelion.s3.ap-northeast-2.amazonaws.com/cloudformation.json
    - 스택이름 : GopaxApiTradingExample
    - 파라미터 > EmailAddress : {email}
    - SshKeyName : GopaxApiTradingExample
    - 다음 > 다음 > 체크 후 스택 생성 
        - AWS CloudFormation에서 IAM 리소스를 생성할 수 있음을 승인합니다. 
    - 스택 상태 “CREATE_COMPLETE” 확인

- EC2 ssh 연결
    - EC2 > 인스턴스 > GOPAX API Trading Server 클릭 후 연결
    - Window
        - PuTTY > 카테고리 > 연결 > SSH > 인증 개인키 파일 > .ppk 선택
        - https://github.com/iPuTTY/iPuTTY/releases/tag/l0.70.2i
    - Mac OS
        - pem 권한 변경
            - chmod 400 GopaxApiTradingExample.pem
        - 인스턴스 접속
            - ssh -i "GopaxApiTradingExample.pem" ubuntu@15.164.170.243
            - yes
    - Cloud9 SSH key 추가 // View public SSH key
        - vi .ssh/authorized_keys
        - Windows : o > 마우스 우클릭
        - Mac OS : o > SSH Key 추가

- Cloud9 생성
    - Cloud9 > Create environment
        - Name : GopaxApiTrading
        - Environment type : SSH
        - User : ubuntu
        - Host : 인스턴스 IPv4 퍼블릭 IP

-  UserData 실행 // 트레이딩 프로그램 다운 및 설치
    - 코드 압축파일 다운
        - wget https://gopax-likelion.s3.ap-northeast-2.amazonaws.com/api-trading-example.zip
    - 압출을 풀기위한 패키지
        - sudo apt install -y unzip
    - 코드 압축 해제
        - unzip api-trading-example.zip
        - sudo apt install -y unzip & unzip api-trading-example.zip
    - 코드? 초기 설정 실행
        - sh src/main/sh/initialize.sh

- 고팍스 API Key 설정, 확인
    - API 키 발급
        - 고팍스 홈페이지 로그인
        - 계정 관리 > API 키 > 새 API키 등록
        - 발급 키 PDF 저장
    - API 키 적용
        - Cloud9 > src/main/python/api_key.py
        - KEY : 고팍스 API 키
        - SECRET : 고팍스 시크릿 키
        - python3 src/main/python/api_key.py


### 3.단기 변동성 돌파전략?


### 4.시스템 구조 및 동작 원리 이해
