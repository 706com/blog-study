### 1) Deadlock 에 대해 설명해 주세요.

상호배제 기법으로 인해 2개 이상의 프로세스가 각각 자원을 가지고 있으면서 서로의 자원을 요구하며 기다리는 상태를 데드락(교착상태) 라고 합니다.

### 2) Deadlock 이 동작하기 위한 4가지 조건에 대해 설명해 주세요. 

❗ (외우지 말고 이해하기)
상호배제, 점유와대기, 비선점, 환형대기가 있습니다.  
  
상호배제는 하나의 공유 자원에는 하나의 프로세스만 접근할 수 있음을 의미하며,  
점유와 대기는 프로세스가 최소 하나의 자원을 점유하고 있는 상태에서, 추가로 다른 프로세스에서 사용 중인 자원을 점유하기 위해 대기할 수 있음을 의미합니다.  
비선점은 다른 프로세스에 할당된 자원을 뺏을 수 없음을 의미하고  
환형대기는 프로세스가 원의 형태를 띄면서, 자신의 자원을 점유한 채 앞이나 뒤에 있는 프로세스의 자원을 요구함을 의미합니다.  
  
앞서 말한 4개를 모두 성립할 시 교착상태가 발생하게 됩니다.

### 3) 그렇다면 3가지만 충족하면 왜 Deadlock 이 발생하지 않을까요? (외우지말고 이해하기)

❗ (외우지 말고 이해하기)  
상호 배제는 서로 자원을 공유할 수 있다면 서로의 자원을 기다리는 상황을 예방할 수 있으며,  
점유와 대기는 프로세스가 자원을 요구할 때, 필요한 자원1,2를 모두 주거나 가진 자원이 없는 경우에만 할당함으로서
문제를 해결할 수 있습니다.  
비선점은 A가 B의 자원을 선점할 수 있게 한다면 서로의 자원을 기다리는 상황을 예방할 수 있으며,  
환형대기는 작은 번호 프로세스가 큰 번호의 프로세스의 자원을 요구하는 것만 가능하게 한다면 큰 번호 프로세스는 작은 번호 프로세스의
자원을 요구할 수 없으므로 없앨 수 있습니다.

### 4) 어떤 방식으로 예방할 수 있을까요?

교착 상태 예방으로는 예방, 회피, 검출 후 회복 3가지 방식으로 해결할 수 있습니다.
예방 : 상호배제, 점유대기, 비선점, 환형대기의 방식 중 하나를 없애는 방식이지만, 부작용이 많은 방법입니다.  
회피 : 자원을 함부로 할당시킬 수 없도록, 안전순서열의 여부로 안전상태가 될 경우에만 자원을 할당하는 방식입니다. (참고 : 은행원 알고리즘)  
검출 후 회복 : 교착상태가 발생한다면 검출을 한 후에, 선점을 통한 회복 혹은 프로세스 강제 종료를 통한 회복방법이 있습니다.  

>예방 목록 부작용
>1) 상호배제 : 모든 자원을 공유하는 것은 이론상 가능하지만 실생활에 불가능하다고 볼 수 있습니다.
>2) 점유대기 : 특정 프로세스에게 자원을 모두 주거나 모두 없애버린다면 낭비되는 자원과 프로세스가 많아져서, 자원의 활용률이 너무 떨어집니다.
>3) 비선점 : cpu스케줄링 처럼 선점이 가능한 자원에서는 효과적일 수 있겠지만, 프린터와 같이 반드시 비선점이 이루어져야 하는 자원도 있을 수 있을 수 있습니다.
>4) 환형대기 : 자원에 번호를 붙여가며 순차적으로 처리하면 환형대기를 없앨 수 있겠지만, 번호 순서를 매기는 것도 비용이 될 수 있으며, 어떤 자원에
   번호를 매기느냐에 따라 자원의 활용률이 떨어질 수 있습니다.

### 5) 왜 현대 OS는 Deadlock을 처리하지 않을까요?

- 빈번히 발생하는 이벤트가 아니기 때문에 미연에 방지하기 위해 훨씬 더 많은 오버헤드를 들이는것이 비효율적이라고 판단함.
- 현대 시스템의 복잡성으로 인해 교착 상태를 완전히 방지하는 것은 불가능
- 만약 시스템에서 deadlock이 발생한 경우 시스템이 비정상적으로 작동한것을 사람이 느낀후 직접 process를 죽이는 방법으로 대처

### 6) Wait Free와 Lock Free를 비교해 주세요.

❓

동기화를 위해서 Lock을 걸고 해제하는 과정 모두는 사실, 기아현상을 발생할 수 있을 뿐더러, 오버헤드를 발생시키는 과정이므로 
lock free와 wait free는 이를 해결하고자 나온 알고리즘입니다.  
상관관계로 따진다면, Wait free는 Lock free안에 속해있다고 볼 수 있습니다.

Lock-free란, '여러 개의 쓰레드에서 동시에 호출했을 때에도 정해진 단위 시간마다 적어도 한 개의 호출이 완료되는 알고리즘'이라고 정의할 수 있으며
Wait-free는 여러 쓰레드가 하나의 작업을 동시에 호출했을 때 지연 없이 모든 쓰레드가 동시에 작업을 완료할 수 있는 알고리즘이라고 정의할 수 있습니다.

- 공통점 : Wait-free와 Lock-free는 모두 멀티스레딩 환경에서 공유 자원에 대한 동시 접근을 처리하는 기술
- 차이점 : Wait-free는 모든 스레드가 동시에 진행될 수 있는 것에 비해, 
Lock-free는 일부 스레드가 블로킹될 가능성이 있지만, 구현이 더 쉽고 성능이 높은 경우가 많음.

[참고] https://peonyf.tistory.com/entry/OS-DeadLock%EB%8D%B0%EB%93%9C%EB%9D%BD


### Q) Non-blocking : 상호배제의 단점을 해결하는가?