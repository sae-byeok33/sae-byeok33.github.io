---
title: "[운영체제] Booting Up"
date: 2025-04-17 14:00:00 +0900
category: [컴퓨터공학,운영체제]
---
# BOOTING UP
우리가 컴퓨터를 실행시키기 위해서 파워버튼을 누르면 일어나는일

<hr style="border: none; border-top: 1px solid #ccc; height: 1px; width: 100%">

## BASIC STEP
1. BIOS 시작
2. CMOS에서 설정 불러오기
3. 장치 초기화
4. POST(Power on self test)실행
5. 부트스트랩 시퀀스 시작


<hr style="border: none; border-top: 1px solid #ccc; height: 1px; width: 100%">  

### 1.Starting the BIOS
**기본 입출력 시스템(BIOS)**  
    → 칩에 내장된 mini-OS  
+ **PC 전원이 켜지면 즉시 실행이 시작된다.**  
    → BIOS 칩의 코드가 RAM의 낮은 주소(ex:0xFF)에 복사된다.  
    → jmp 0xff(16bits 명령어)가 0xFFFF0 ($2^20$ -16)에 기록된다.  
    → x86 CPU는 항상 RIP 레지스터의 0xFFFF0에서 시작된다. 
+ **BIOS의 주요 목표**  
    → 하드웨어가 정상 작동하는지 확인하기    
    → 간단한 low-level 장치 드라이버 설치  
    → 저장장치에서 마스터 부트 레코드 (MBR) 스캔함  
        → 부트 레코드를 RAM으로 로드함  
        → CPU에게 로드된 코드를 실행하라고 지시함  


<hr style="border: none; border-top: 1px solid #ccc; height: 1px; width: 100%">

### 2. Loading Settings from CMOS
**BIOS는 종종 설정 가능한 옵션들을 제공한다**  
    → 이 값들은 배터리로 유지되는 CMOS 메모리에 저장된다.  


<hr style="border: none; border-top: 1px solid #ccc; height: 1px; width: 100%">

### 3. Initialize Devices    
**하드웨어를 검색하고 초기화 한다**  
    → CPU 및 MEMORY  
    → 키보드 와 마우스  
    → 비디오  
+ **부팅 가능한 저장 장치**  
    → 메모리에 인터럽트 핸들러 설치   
+ **인터럽트 백터 테이블(Interrupt Vector Table)생성**  
    → 확장 카드에서 추가 BIOS 실행  
+ **비디오 카드 및 SCSI 카드에서는 자체 BIOS 가 있는 경우가 많음**  
    → POST(전원 켜기 자가 진단) 테스트 실행  
+ **각 주소에 대해 RAM 읽기/쓰기를 수행하여 검사**  

<hr style="border: none; border-top: 1px solid #ccc; height: 1px; width: 100%">

### 4. POST 실행
**컴퓨터가 전원을 켜자마자 수행하는 자가 진단 과정이다**
+ **기본 목적 : 필수 하드웨어 부품이 정상적으로 작동하는지 확인**  
+ 검사 대상 예 :  
    CPU , RAM , 키보드 , 마우스 , GPU 등  
+ **진단 실패시 오류 비프음 또는 에러 메세지 출력**   
+ **성공시 BIOS는 계속 부팅 절차 진행**   

<hr style="border: none; border-top: 1px solid #ccc; height: 1px; width: 100%">

### 5. Bootstrapping
**BIOS는 잠재적으로 부팅 가능한 모든 장치를 식별한다**  
    → 각 장치에서 마스터 부트 레코드(MBR)를 찾으려고 시도함  
    → 순서는 사용자가 구성 가능함   
+ **MBR에는 실제 OS를 로드할 수 있는 코드가 포함됨**  
    → 해당 코드는 부트로더(bootlooader)라고 불림  
+ 부팅 가능한 장치의 예:  
    하드 드라이브 , SSD , 플로피 디스크 , CD/DVD/Blu-Ray , USB  


<hr style="border: none; border-top: 1px solid #ccc; height: 1px; width: 100%">


## the master boot record (MBR)
**특정 512 바이트 파일이 저장장치의 섹터1(주소0)에 기록된다**  
+ 포함내용  
    → 446bytes의 실행 가능한 코드
    → 4개의 파티션 엔트리
+ **전체 OS를 저장하기에는 너무 작다**    
+ **chain-loading sequence를 시작한다**  

<hr style="border: none; border-top: 1px solid #ccc; height: 1px; width: 100%">

## 예제 부트로더 (GRUB)
**Grand Unified Bootloader**  
+ unix , linux , solaris 등에서 사용된다  
