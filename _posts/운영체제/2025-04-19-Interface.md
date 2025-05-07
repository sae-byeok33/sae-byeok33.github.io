---
title: "[운영체제] Interface"
date: 2025-04-19 14:00:00 +0900
category: [컴퓨터공학,운영체제]
---

# Interface to applications
## 시스템 호출 인터페이스 (System Call Interface)
시스템 호출 테이블
+ OS API룰 추상화 하는 간접 계층
+ 테이블은 항상 고정된 위치에 있다
+ 각 OS API는 테이블에서 특정 Index를 가진다  

프로그램은 함수 주소를 하드코딩하는 대신에 테이블을 통해서 API에 접근하게 된다

## Traps = Software interrupts
소프트웨어는 인터럽트를 생성할 수 있다
+ 트랩과 예외는 소프트웨어 인터럽트

예시
+ mov eax , 1
+ xor ebx , ebx
+ int 0x80

## 간단한 시스템 호출 예시
1. 소프트웨어가 int 0x80을 실행하는 EIP를 푸시한다
2. CPU는 IVT에서 핸들러를 찾는다
3. CPU는 제어를 OS핸들러로 전달한다
4. 핸들러는 SYSCALL 테이블에서 EAX를 찾는다
5. API코드로 점프한다

## 시스템 호출에 대한 CPU 지원
많은 CPU는 시스템 호출을 호출하기 위한 명령어 지원을 제공한다  
    -> x86에서는 시스템 호출이 인터럽트를 통해 시작된다  
예시 : 리눅스 시스템 호출  
+ x86에서 int0x80은 시스템 호출 인터럽트  
+ EAX는 원하는 API의 테이블 인덱스를 보유