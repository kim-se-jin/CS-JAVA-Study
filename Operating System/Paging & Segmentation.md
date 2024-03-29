# Paging & Segmentation

### Paging & Segmentation에 대해 설명해주세요
- * 둘 다 가상 메모리를 관리하는 기법입니다. 
   페이징은 프로세스를 일정한 크기의 페이지로 분할해서 메모리에 적재하는 방식입니다.
   세그멘테이션은 가상 메모리를 서로 크기가 다른 논리적 단위로 분할한 것을 의미합니다. 세그멘테이션은 프로세스를 물리적 단위인 페이지가 아닌 논리적 단위인 세그먼트로 분할해서 메모리에 적재하는 방식입니다. 

   ### Q) 세그먼트의 크기를 나누는 기준은 무엇인가요?
   - 사용자 관점으로 메모리의 크기를 나누고, 지원합니다. 반면 페이징 기법은 하드웨어에 의해 분리된 하나의 주소를 페이지 번호와 페이지 간격으로 크기를 특정합니다.

   ### Q) 페이징에 비해 외부단편화가 많이 일어날 것 같습니다. 현재에는 이를 어떻게 해결하고 있을까요? 
   - 압축 ( Compaction ) 기법을 사용합니다. 압축 기법은 주기억장치 내 분산되어 있는 단편화된 공간들을 통합하여 하나의 커다란 빈 공간을 만드는 작업을 의미합니다.
   - <외부단편화가 발생한 상황>
    ![image](https://user-images.githubusercontent.com/76711238/229358437-ec2fcee5-8e25-44dd-92c3-a15f800a874e.png)
   - <빈 공간을 하나의 연속된 공간으로 만드는 과정(압축)>
    ![image](https://user-images.githubusercontent.com/76711238/229358459-96821116-2c8b-4a4d-821f-fc62e949435a.png)

   ### Q) 페이징 사용 시 외부 및 내부 단편화 문제에 대해 설명해주세요.
   - 페이징 : 내부 단편화 발생합니다(페이지 내부 메모리 낭비). 반면 외부 단편화는 발생하지 않습니다.(비연속적 할당)

      > Q-1) 페이징 사용 시 내부 단편화가 일어날 수 있는 최대 크기는 무엇일까요?
      - 페이징을 통해 마지막 페이지는 최대 페이지 크기 -1 만큼 메모리가 버려지게 됩니다. 

> ### Q) 세그멘테이션을 위해서 세그멘트 단위 별로 가지고 있는 레지스터에 대해 설명해주세요. 
   - 세그먼트 레지스터 (Segment Register)는 세그먼트 메모리의 한 영역에 대한 주소지정을 제공합니다. 
 
이름|레지스터의 기능
-- | --
CS | 코드 세그먼트의 시작 주소를 가리킵니다. CS레지스터는 프로그램의 코드 세그먼트의 시작 주소를 포함합니다. 이 세그먼트 주소에 명령어 포인터(instruction pointer, IP) 레지스터의 오프셋 값을 더하면, 실행하기 위해 메모리로부터 가져와야 할 명령어의 주소가 됩니다.
DS | 프로그램에 정의된 데이터 세그먼트의 시작 주소를 가리킵니다. 데이터의 오프셋을 DS 레지스터에 저장된 주소 값에 더해 데이터 세그먼트 내에 위치해 있는 데이터의 주소를 참조합니다.
SS | 실행 과정에서 필요한 데이터나 연산 결과 등을 임시로 저장하거나 삭제할 때 사용하는 스택 세그먼트의 시작 주소를 가리킵니다.  메모리 상에 스택의 구현을 가능하게 합니다.
ES | 추가로 사용된 데이터 세그먼트의 주소를 가리킵니다. 메모리 주소지정을 다루는 스트링(문자 데이터) 연산에서 사용됩니다.
FS/GS | 기억장소 요구사항을 다루기 위해서 80386에서 추가로 도입된 여분의 세그먼트 레지스터입니다.
  

   ### Q) 페이지 크기에 따른 성능에 대해서 설명해주세요.
   - 페이지 크기가 작다면 
         - 내부단편화가 줄어듭니다.
         - 페이지 크기가 작을수록 resolution(해당 메모리에 필요한 데이터가 있는 확률)을 높일 수 있습니다. 만약 페이지 크기가 크면 다른 필요없는 부분이 있을 확률이 크기 때문입니다.

   - 페이지 크기가 크다면
      - 페이지 개수가 줄어들기 때문에 그만큼 페이지 테이블 크기도 줄어듭니다.
      - Page fault 발생 확률을 줄이려면 페이지 크기가 큰 것이 좋습니다. 이는 지역성과도 관련이 있는데, 대부분 프로세스는 필요한 부분이 일정 범위 이내인 경우가 많으므로 페이지 크기가 클수록 필요한 부분이 있을 확률이 크기 때문입니다. 

      ![image](https://user-images.githubusercontent.com/76711238/229358856-680efeb3-2698-4a1a-8bc9-80d471d60e0d.png)   

   ### Q) 주소공간이 존재할 때, 주소 공간이 수정 가능한 지 페이지 테이블을 사용해서 알 수 있는 방법을 설명해주세요.
   - 페이지 테이블 내부의 R/W/X 비트를 사용해서 수정/읽기/작성 권한을 확인할 수 있습니다. 
      ![image](https://user-images.githubusercontent.com/76711238/229357591-9a2c9d0f-a91b-4621-ad93-f4d416f3e99e.png)

   ### Q) 페이지 테이블서의 인덱스 필드가 어떻게 결정되는지 설명해주세요.
   - 각 메모리의 크기에 비례해서 인덱스 필드의 크기 또한 유동적으로 바뀝니다.  

   ### Q) PAGE FAULT 발생 과정 
   - PAGE FAULT : 프로세스가 페이지를 요청했을 때 그 페이지가 main 메모리에 없는 상황을 의미합니다.  

   단계|과정
   -- | --
   1 | CPU가 가상 주소를 MMU에게 요청합니다.
   2 | MMU는 먼저 TLB로 가서 그 가상주소에 대한 물리주소가 캐싱돼 있는지 확인합니다.
   3 | TLB에 캐싱된 물리주소가 
   3-1  |- 있으면 MMU가 해당 페이지의 물리 주소로 데이터를 갖고 와서 CPU에게 보냅니다.
   3-2  |- 없으면 MMU가 CR3 레지스터를 가지고 물리 메모리에 해당 프로세스의 페이지 테이블에 접근합니다.
   4 | MMU가 페이지 테이블에서 물리주소가 있는지 valid bit를 확인합니다.
   5 | valid bit의 값이 
   5-1  |- 1이면 MMU가 해당 페이지의 물리 주소로 데이터를 갖고 와서 CPU에게 보냅니다.
   5-2  |- 0이면 MMU가 페이지 폴트 인터럽트를 운영체제에 발생시킵니다.
   6 | 운영체제는 해당 페이지를 저장공간에서 가져옵니다.
   7 | 운영체제는 저장공간에서 가져온 데이터를 메모리에 올려주고, 페이지 테이블을 업데이트 해줍니다. valid bit -> 1, 물리주소를 업데이트합니다.
   8 | 운영체제는 CPU에게 프로세스를 다시 실행하라고 합니다. (PCB 저장 정보 기반으로)
   9 | CPU는 다시 MMU에 가상 주소를 요청합니다.

   ### Q) 처음에 어떻게 필요한 페이지만 메모리에 올릴까요?
   - Demand paging을 사용해서 메모리에 올리게 됩니다. 이는 요구된 page만을 메인 메모리에 적재합니다. 이를 통해 사용되지 않는 page를 메모리에 적재하는 것을 예방하고 교체시간, 메모리 공간을 절약합니다.


  #### 사진 & 내용 출처
  https://hajunyoo.oopy.io/a91edd96-2b39-4a3a-ab25-d5b3504a6f0d#af9aee77-2305-4080-a1b6-3a1194190736

  https://velog.io/@jsb100800/CS-%EC%8A%A4%ED%84%B0%EB%94%94-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B0%80%EC%83%81-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B4%80%EB%A6%AC

  https://eunjinii.tistory.com/142

  https://code-lab1.tistory.com/54

  https://dhhd-goldmilk777.tistory.com/41
