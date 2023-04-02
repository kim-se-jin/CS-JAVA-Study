# TLB, MMU

## 페이지 테이블의 TLB, MMU 에 대해 설명해주세요.
페이징 단위로 분할하여 적재를 하게 되면, **불연속적으로 데이터가 저장**되는데 , 이러한 데이터를 **CPU가 접근**할 수 있게 해주는 것이 **MMU** 입니다.

TLB(Translation Lookaside Buffer)는 **주소 변환 속도를 높이기 위해** MMU(Memory Management Unit)에 저장된 최근에 액세스한 페이지 테이블 캐시입니다.

  ### Q) MMU가 생겨난 이유에 대해 설명해주세요.
  -  컴퓨터에서 제한된 메모리 문제를 해결하기 위해 만들어졌습니다. 초기 컴퓨터는 적은 양의 메모리를 가지고 있었으며 운영 체제가 수동으로 관리해야 했습니다. 프로그램의 크기와 복잡성이 증가함에 따라 운영 체제가 모든 메모리를 추적하는 것이 점점 어려워졌습니다. MMU는 **메모리 관리 과정을 자동화하고 CPU가 메모리를 더 효율적으로 관리할 수 있는 방법**을 제공하기 위해 설계되었습니다.


  ### Q) MMU에서 base register 를 통해 물리주소로 변환하는데 여기서 발생할 수 있는 문제에 대해 설명해주세요.
  > 💡 Hint: Memory Protection   
  
  프로세스를 불연속적으로 할당하면, 다른 프로세스가 메모리에 접근하는 경우가 생길 수 있습니다. 이를 예방하기 위해 limit 레지스터를 사용합니다.
  프로세스의 접근 가능한 합법적인 메모리 영역(`x`)은 `base <= x < base+limit` 이 됩니다.따라서 이 영역 밖에서 접근을 요구하면 trap을 발생시킵니다. 
  안전성을 위해 base와 limit 레지스터는 사용자 모드에서는 직접 변경할 수 없도록 커널 모드에서만 수정 가능하도록 설계되어 있습니다.
  
  - **base 레지스터** : 메모리상의 프로세스 시작주소를 물리 주소로 저장
  - **limit 레지스터** : 프로세스의 사이즈를 저장
  
  ### Q) MMU, TLB, Page Table이 어디에 위치해있는 지 설명해주세요.
![image](https://user-images.githubusercontent.com/67494004/229360874-7a54c6e7-4b95-4ef6-b24f-36de1dbbb533.png)

  - MMU : CPU 내부
  - TLB : MMU 내부
  - Page Table : Main Memory
    - 💡 MMU : Page Table 의 위치정보를 관리하는 레지스터가 있음


### Q) MMU 와 TLB의 프로세스 사이 정보 공유 여부에 대해 설명해주세요.
- TLB는 각 프로세스마다 개별적 메모리 공간에 지정되기 때문에, **프로세스 간에 정보를 공유하지 않습니다**. 가상메모리의 장점인 보호성에 기반하여, 서로 다른 프로세스가 같은 주소를 가르켜도 가상메모리에 의해 서로 영향을 주지 않습니다.


### Q) 가상메모리를 구현하기 위해 MMU가 사용하는 방식
> Hint ! Page Table, Page Fault, Page Replacement 를 MMU 와 연관지어 설명
- MMU는 **가상 메모리를 구현하기 위해 페이지 테이블을 사용**합니다.
페이지 테이블은 프로세스에서 사용하는 가상 주소와 물리 주소(해당 데이터가 저장되어있는 RAM)를 매핑합니다.

**Page fault**는 페이지를 요구하였을 때 
1. MMU가 페이지 테이블 내에 메모리에 있는 지, 해당 페이지의 valid bit 를 확인합니다.(0,1)
2. valid bit가 0 이라면, 페이지가 없는 경우이므로 Page fault 를 발생시킵니다.
3. 운영체제는 디스크에서 필요한 페이지를 검색하여 메모리에 로드합니다.
4. 페이지 테이블에 해당하는 메모리 valid bit를 1로 변경해줍니다.
  - valide bit는 dirty bit 등과 함께 사용되어 메모리의 페이지 상태를 추적 및 관리

> ### Q) TLB를 사용할 때의 문제점
> 💡 Hint ! Context Switching

![image](https://user-images.githubusercontent.com/67494004/229360941-a5749520-2a3f-452e-a68e-413a77c07f42.png)


컨텍스트 전환이 발생하면 운영 체제는 현재 프로세스의 상태를 저장하고 새 프로세스의 상태를 로드해야 합니다. 컨텍스트 전환 중에 TLB가 제대로 관리되지 않으면 새 프로세스에서 더 이상 유효하지 않은 이전 프로세스의 매핑이 포함될 수 있으며 이로 인해 잘못된 변환 및 시스템 충돌이 발생할 수 있습니다.

이 문제를 처리하기 위해 최신 운영 체제는 컨텍스트 전환 중에 "TLB flush"라는 기술을 사용합니다. TLB flush는 컨텍스트 스위치가 발생할 때 TLB의 모든 항목을 제거하는 프로세스로, CPU가 새 프로세스에 대한 올바른 매핑으로 TLB를 다시 로딩합니다.

TLB flush는 CPU가 전체 TLB를 다시 로드해야 하기 때문에 시간이 걸릴 수 있습니다. 이 비용을 줄이기 위해 일부 최신 CPU에는 컨텍스트 전환 중에 이전 프로세스에 속한 페이지에 대해서만 TLB를 선택적으로 플러시할 수 있는 "PCID(프로세스 컨텍스트 식별자)"라는 기능이 포함되어 있습니다. 이렇게 하면 TLB를 다시 로드하는 데 필요한 시간이 줄어들고 전체 시스템 성능이 향상됩니다.


### Q) page Table 의 두가지 유형에 대해 설명해주세요.
page Table 이 메모리에 함께 적재가 되면서 많은 크기를 차지한다는 단점이 있습니다. 만약 2^20(대략 100만)개의 페이지가 있다면, Page table 또한 각 페이지들이 물리 주소와 매핑될 수 있도록 100만개의 Page entry를 가지고 있어야 합니다. 

페이지 테이블의 크기가 커지면서 전체 테이블을 메모리에 저장하는 것이 점점 어려워졌습니다. 이로 인해 페이지 테이블을 여러 수준으로 나누어 크기를 줄이고 메모리 효율성을 향상시키는 계층적 페이지 테이블(Hierarchical Page Table)이 개발되었습니다.

- 계층적 페이지 테이블(Hierarchical page table)
- 해시 페이지 테이블 (Hashed page table)
- 역페이지 테이블 (Inverted page table)

<img width="887" alt="image" src="https://user-images.githubusercontent.com/67494004/229361023-8ecf21d0-a3ac-4698-b18b-b181a58b6526.png">


계층적 페이지 테이블 에 대해 더 자세하게 설명해보겠습니다.
계층적 페이지는 Page table의 사이즈를 줄이기 위해 고안된 방법으로, 기존에 프로세스 하나당 하나의 Page table을 사용하던 것을 여러 개로 나누어 사용하는 방식을 의미합니다. 
계층을 나눈 횟수만큼 level이 증가하여 두 번 나누었다면 2-level page table, 세 번 나누었다면 3-level page table 이라는 이름을 붙입니다.

- Level 1인 outer page table에서는 해당 page number가 valid한지 invalid한지 판단
   - invalid : level 2에 page table이 존재하지 않는 것이기 떄문에 memory 절약을 할 수 있게 되는 것
   - valid : outer page table이 가리키고 있는 level 2의 page table에서 page number를 찾아 frame number를 통해 physical address를 계산

- P1은 outer page table의 entry 개수(인덱스)이고 P1을 통해 Level 2의 page table의 시작주소를 알 수 있다. 
- P2값을 통해 frame number를 알 수 있다. 만약 64bit를 사용한다면 P1은 42, P2는 10, offset은 12bit를 가진다. 만약 계층 구조의 page table을 사용하지 않는다면 page number는 52bit를 사용하게 되어 size가 더욱 커질 것이다.
- level을 늘려서 page table의 사이즈를 더 줄일 수 있다. 실제 Linux에서는 Level 3의 계층 구조를 사용하고 있다. 위 그림에서 하나의 page table을 추가하여 P1->P2->P3을 거쳐 frame number를 찾는 구조로 되어있다.

계층을 나누면 페이지 테이블을 Paging하기 때문에 기존에 메모리를 효율적으로 사용할 수 있습니다.
또한 나눌수록 페이지 테이블의 크기는 줄어들지만, 각 페이지 테이블을 참조하기 위해 level이 커질수록 메모리를 자주 참조해야 한다는 단점이 발생합니다.



### Q) TLB 에 원하는 주소가 없을 때의 2가지 경우, Main Memory와 Page 용어를 사용해서 말씀해주세요.
miss가 일어났을 때 TLB에 원하는 주소가 없는 경우는 2가지로 나뉠 수 있습니다.
1. TLB는 없지만 mainMemory 에 있는 경우, mainMemory에서 가져와 -> TLB
2. mainMemory에도 없다면 , page Fault -> 관련 처리 루틴    
을 통해 TLB miss 를 처리합니다.

### MultiLevel pageTable
== Hierarchical Page Table


#### 이미지 및 내용 참고   
https://velog.io/@mardi2020/페이지-교체-알고리즘   
TLB: https://icksw.tistory.com/149   
계층 테이블 : https://itstory1592.tistory.com/103
