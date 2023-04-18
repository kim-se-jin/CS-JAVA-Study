# 운영체제

# CPU Sheduling
[Process Sheduling 알고리즘에는 어떤 것들이 있나요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#process-sheduling-알고리즘에는-어떤-것들이-있나요)  

[Q) 단기, 장기 , 중기 스케줄러가 무엇인가요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-단기-장기--중기-스케줄러가-무엇인가요)   
- [Q-1) 중기 스케줄러 동작방식에 대해 설명해주세요](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-중기-스케줄러-동작방식에-대해-설명해주세요)   
- [Q-2) 장기 스케줄러와 단기스케줄러의 실행속도는 얼마나 차이가 날까요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-장기-스케줄러와-단기스케줄러의-실행속도는-얼마나-차이가-날까요)   


[Q) 선점형 / 비선점형 스케줄러는 무엇인가요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-선점형--비선점형-스케줄러는-무엇인가요)   
- [Q-1) 선점형 / 비선점형 알고리즘의 종류는 무엇이있나요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-선점형--비선점형-알고리즘의-종류는-무엇이있나요)   


[Q) FCFS 알고리즘 사용시 문제되는점이 있을까요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-fcfs-알고리즘-사용시-문제되는점이-있을까요)   
- [Q) 위의 예에서 B,C같은 프로세스처럼 처리시간이 오래걸리는 작업이 먼저 도착해서 B,C가 오래기다리게 되는현상을 부르는 용어는 무엇인가요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-위의-예에서-bc같은-프로세스처럼-처리시간이-오래걸리는-작업이-먼저-도착해서-bc가-오래기다리게-되는현상을-부르는-용어는-무엇인가요)   
  
[Q) 라운드로빈은 어떤 스케줄링기법인지 말씀해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-라운드로빈은-어떤-스케줄링기법인지-말씀해주세요)   
- [Q) 그럼 라운드로빈은 왜 등장하게 된건가요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-그럼-라운드로빈은-왜-등장하게-된건가요)   
- [Q) 잔여시간이 긴 프로세스가 선점하지 못한채로 머무르게 되는 현상은 무엇인가요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-잔여시간이-긴-프로세스가-선점하지-못한채로-머무르게-되는-현상은-무엇인가요)   
- [Q) 라운드로빈의 타임슬라이스는 어느정도로 잡아야하나요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-라운드로빈의-타임슬라이스는-어느정도로-잡아야하나요)   
- [Q) 일반적으로 라운드로빈시 타임슬라이스의 권장 할당량이 어느정도인지 아시나요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-일반적으로-라운드로빈시-타임슬라이스의-권장-할당량이-어느정도인지-아시나요)   

[Q) 우선순위 스케줄링에서 기아현상을 해결하기위한 방법이 어떤것이있나요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-우선순위-스케줄링에서-기아현상을-해결하기위한-방법이-어떤것이있나요)   

[Q) 스케줄링기법중 멀티레벨 큐와 멀티레벨 피드백큐가 있는데, 둘다 아시는내용을 설명해주세요](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-스케줄링기법중-멀티레벨-큐와-멀티레벨-피드백큐가-있는데-둘다-아시는내용을-설명해주세요)   

[Q) 프로세스 관리가 필요한 이유는무엇일까요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-프로세스-관리가-필요한-이유는무엇일까요)   

[Q) 스레드 스케줄링은 어떻게 되나요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-스레드-스케줄링은-어떻게-되나요)   

[Q) 각 자원의 우선순위, CPU대기시간 등의 내용들은 어디에 저장될까요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-각-자원의-우선순위-cpu대기시간-등의-내용들은-어디에-저장될까요)   

[Q) CPU가 여러개일때의 스케줄링 기법에대해 설명해주세요](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/CPU%20Sheduling.md#q-cpu가-여러개일때의-스케줄링-기법에대해-설명해주세요)   

---

# [Context Switching & PCB](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Context%20Switching%20%26%20PCB.md#cs-java-studyoperating-systemcontext-switching--pcbmd)   
[PCB와 Context Switching](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Context%20Switching%20%26%20PCB.md#pcb와-context-switching)   

[Q) Context Switching이 일어날 때, 캐시 관련해서도 프로세스와 스레드의 처리 방법이 다르다고 알고 있습니다. 이를 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Context%20Switching%20%26%20PCB.md#q-context-switching이-일어날-때-캐시-관련해서도-프로세스와-스레드의-처리-방법이-다르다고-알고-있습니다-이를-설명해주세요)    

[Q) 프로세스는 여러개의 스레드를 가지고 있는데, 이 스레드들에 대한 정보를 어떻게 가지고 있는가](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Context%20Switching%20%26%20PCB.md#q-프로세스는-여러개의-스레드를-가지고-있는데-이-스레드들에-대한-정보를-어떻게-가지고-있는가)   
- [Q) 프로세스와 스레드는 Context Switching이 발생할 때 어떤 차이가 있는가](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Context%20Switching%20%26%20PCB.md#q-프로세스와-스레드는-context-switching이-발생할-때-어떤-차이가-있는가)   
  
[Q) Context Switching 에서 프로세스 수행 중에 입출력 상태로 전환되어서 대기 상태로 전환 되는데, CPU를 어떻게 하는 것이 효율적인가?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Context%20Switching%20%26%20PCB.md#q-context-switching-에서-프로세스-수행-중에-입출력-상태로-전환되어서-대기-상태로-전환-되는데-cpu를-어떻게-하는-것이-효율적인가)   
- [Q) Context Switching이 인터럽트가 발생할 때만 발생하는가?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Context%20Switching%20%26%20PCB.md#q-context-switching이-인터럽트가-발생할-때만-발생하는가)   
  - [Q) 인터럽트는 무조건 들어오는 순서대로 처리를 하는가?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Context%20Switching%20%26%20PCB.md#q-인터럽트는-무조건-들어오는-순서대로-처리를-하는가)   

[Q) 프로세스 컨트롤 블록이 어떤 자료구조로 관리 되는지 알고 있는가](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Context%20Switching%20%26%20PCB.md#q-프로세스-컨트롤-블록이-어떤-자료구조로-관리-되는지-알고-있는가)   

[Q) Context Switching 시에 주소공간에 대한 캐시 처리가 어떻게 이루어지는지 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Context%20Switching%20%26%20PCB.md#q-context-switching-시에-주소공간에-대한-캐시-처리가-어떻게-이루어지는지-설명해주세요)   


---

# [Critical Section](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#cs-java-studyoperating-systemcritical-sectionmd)   
[임계구역 문제가 무엇인 지 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#임계구역-문제가-무엇인-지-설명해주세요)   

- [Q) 임계구역 문제를 해결하기 위한 조건을 말해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-임계구역-문제를-해결하기-위한-조건을-말해주세요)   
- [Q) 임계구역을 해결하기 위한 동기화 기법을 말해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-임계구역을-해결하기-위한-동기화-기법을-말해주세요)   
- [Q-1) 세마포어는 여러개의 프로세스, 스레드를 허용하는데 이 방식과 용어에 대해 말해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-1-세마포어는-여러개의-프로세스-스레드를-허용하는데-이-방식과-용어에-대해-말해주세요)   
    - [Q-1-1) Binary Semaphore란?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-1-1-binary-semaphore란)   
  - [Q-2) 이진 세마포어와 뮤텍스는 같은 것이라고 볼 수 있나요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-2-이진-세마포어와-뮤텍스는-같은-것이라고-볼-수-있나요)   
  - [(+) 세마포어가 해결해주는 문제](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#-세마포어가-해결해주는-문제)   
  
[Q) IPC의 여러가지 통신 중 가장 기억에 남는 것을 말해주세요. (Process part)](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-ipc의-여러가지-통신-중-가장-기억에-남는-것을-말해주세요-process-part)   
- [Q-1) 소켓 통신에 대해 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-1-소켓-통신에-대해-설명해주세요)   
[Q) 동기화를 위한 하드웨어 명령어 2가지를 말해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-동기화를-위한-하드웨어-명령어-2가지를-말해주세요)   
- [(+) 소프트웨어적 해결 방식의 문제점 (HW 명령어 존재 이유)](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#-소프트웨어적-해결-방식의-문제점-hw-명령어-존재-이유)   
- [(+) SW적 해결방식은 무엇인가요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#-sw적-해결방식은-무엇인가요)   
  - [Q-1) test&set 진행 시 Polling을 계속하며 상태를 계속해서 확인하는 용어를 뭐라고 하나요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-1-testset-진행-시-polling을-계속하며-상태를-계속해서-확인하는-용어를-뭐라고-하나요)   
  
[Q) 임계영역 문제 방지 조건 중 "상호배제" 조건을 만족하기 위해 interrupt를 사용하는 것이 가능할까요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-임계영역-문제-방지-조건-중-상호배제-조건을-만족하기-위해-interrupt를-사용하는-것이-가능할까요)   

[Q) 임계구역 조건이 지켜지지 않으면 발생하는 문제를 말해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-임계구역-조건이-지켜지지-않으면-발생하는-문제를-말해주세요)   
- [Q-1) 두 개 이상의 프로세스, 스레드가 공유 자원에 접근해서 일어나는 문제 상황에 대한 용어를 말해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-1-두-개-이상의-프로세스-스레드가-공유-자원에-접근해서-일어나는-문제-상황에-대한-용어를-말해주세요)   
- [Q-2) race condition을 방지하기 위한 방법을 말해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-2-race-condition을-방지하기-위한-방법을-말해주세요)   
  
[Q) JAVA, Spring 에서 데이터 정합성 문제가 발생했던 경험과, 있다면 해결 경험도 말해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-java-spring-에서-데이터-정합성-문제가-발생했던-경험과-있다면-해결-경험도-말해주세요)   
- [Q-1) 동시성 문제와 데이터 정합성 문제의 차이를 말해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-1-동시성-문제와-데이터-정합성-문제의-차이를-말해주세요)   
- [Q-2) 트랜잭션과 더불어서 데이터 정합성 문제에 대해 설명해주세요. (DB part)](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-2-트랜잭션과-더불어서-데이터-정합성-문제에-대해-설명해주세요-db-part)   
  
[Q) Thread-safe에 대해 어떤 의미인지 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-thread-safe에-대해-어떤-의미인지-설명해주세요)   
- [Q-1) Thread-safe를 구현할 수 있는 방법에 대해 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-1-thread-safe를-구현할-수-있는-방법에-대해-설명해주세요)   
- [Q-2) 재진입성 (Reenterant) 개념에 대해 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Critical%20Section.md#q-2-재진입성-reenterant-개념에-대해-설명해주세요)   

---
# [Cache Memory](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#cache-memory)   

[캐시메모리 및 메모리 계층성에 대해서 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#캐시메모리-및-메모리-계층성에-대해서-설명해주세요)   

[Q) L1, L2, L3 캐시 메모리에 대해서 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#q-l1-l2-l3-캐시-메모리에-대해서-설명해주세요)   
- [Q) L1, L2, L3 캐시 메모리는 CPU 내부 어디에 위치하나요?](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#q-l1-l2-l3-캐시-메모리는-cpu-내부-어디에-위치하나요)   
- [Q) 메모리 계층을 분류한 이유와 이점에 대해서 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#q-메모리-계층을-분류한-이유와-이점에-대해서-설명해주세요)   

[Q) 캐시는 데이터를 어떻게 관리하는지 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#q-캐시는-데이터를-어떻게-관리하는지-설명해주세요)   
- [Redis의 캐시 전략 4가지](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#q-캐시는-데이터를-어떻게-관리하는지-설명해주세요)   

[Q) 캐시의 지역성에 대해서 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#q-캐시의-지역성에-대해서-설명해주세요)   
- [Q) 캐시의 지역성을 기반으로, 이차원 배열을 탐색했을 때의 성능 차이에 대해서 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#q-캐시의-지역성을-기반으로-이차원-배열을-탐색했을-때의-성능-차이에-대해서-설명해주세요)   
  - L1 캐시는 세부적인 영역으로 추가적으로 나누어지는데, 이에 대해서 설명해주세요.
  
[Q) 캐시 메모리와 메인 메모리의 매핑 방식에 대해서 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#q-캐시-메모리와-메인-메모리의-매핑-방식에-대해서-설명해주세요)   

[Q) 캐시 동기화에 대해서 설명해주세요.](https://github.com/kim-se-jin/CS-JAVA-Study/blob/main/Operating%20System/Cache%20Memory%20%26%20Memory%20Layered.md#q-캐시-동기화에-대해서-설명해주세요)   

