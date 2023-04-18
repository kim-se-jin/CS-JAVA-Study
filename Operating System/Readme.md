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
