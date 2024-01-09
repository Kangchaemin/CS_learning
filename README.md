# CS_learning

##### 1. 스레드
CPU가 처리할 수 있는 작업의 단위
> CPU 멀티스레드 : 여러 개의 스레드를 동시에 처리하는 방법
```
처리(job) > 프로세스(task) > 스레드(operation)
여러 개의 스레드가 모여 프로세스를 이루고 여러 개의 프로세스가 모여 처리가 되며,
여러 개의 프로세스를 모아서 한꺼번에 처리하는 과정을 일괄 작업이라고 한다.
```

- 멀티 스레드  
  프로세스 내 작업을 여러 개의 스레드로 분할함으로써 작업의 부담을 줄여줌.
  **하나의 프로세스 내에 여러 개의 스레드를 생성**
  - 단점  
    **모든 스레드가 자원을 공유하기 때문에 한 스레드에 문제가 생기면 전체 프로세스에 영향을 미친다.**

  
- 멀티태스킹  
  운영체제가 CPU에 작업을 줄 때 시간을 잘게 나누어 배분하는 기법. = **시분할 시스템**
  
- 멀티프로세싱  
  여러개의 CPU로 여러 개의 스레드를 동시에 처리. **병렬처리에서 슈퍼스칼라 기법**
- CPU멀티스레드  
  스레드를 파이프라인 기법을 이용하여 동시에 여러 스레드를 처리하도록 만든 병렬처리 기법.

##### 파이프라인 기법
CPU의 사용을 극대화하기 위해 명령을 겹쳐서 실행 - 하나의 코어에 여러 개의 스레드를 사용하는 것.

##### 슈퍼스칼라 기법
코어를 여러 개 구성하여 복수의 명령어가 동시에 실행되도록 하는 방식
> CPU는 대부분 슈퍼스칼라 기법을 사용하고 있다.

##### 프로그램 vs 프로세스
프로그램 : 저장장치에 저장되어 있는 **정적인 상태**  
프로세스 : 프로그램을 마우스로 더블클릭하면 메모리에 올라와서 작업이 진행되는 **동적 상태** ***task라고도 함***  
```
프로세스 = 프로그램 + PCB(프로세스 제어 블록)
```

##### 프로세스 제어 블록(PCB)
모든 프로세스는 고유의 프로세스 제어 블록을 가지며, 프로세스 생성 시 만들어져서 프로세스가 실행을 완료하면 폐기된다.  
>프로세스 제어 블록이 없으면 프로그램이 프로세스로 전환되지 못한다.

##### 스왑 영역
메모리에서 쫓겨난 데이터가 임시로 보관되는 

##### fork(), exec()
fork() : 새로운 프로세스를 복사하는 시스템 호출  
exec() : 프로세스는 그대로 둔 채 내용만 바꾸는 시스템 호출
```
exec() 시스템 호출 : 이미 만들어진 프로세스 구조 재활용
```

##### printf()
컴파일러는 라이브러리 연결 단계에서 printf()문에 해당하는 기계어 코드를 <stdio.h> 라이브러리에서 가져와 **목적코드에 삽입한다.**  
<stdio.h> 라이브러리는 입출력 함수를 미리 만들어놓은 것으로, **사용자가 printf()함수를 따로 정의하지 않고** 소스코드 맨 앞에 #include <stdio.h> 라고 명시하면  
자동으로 라이브러리가 연결된다.

##### return()
main()함수의 맨 마지막줄에 return()문을 사용하는 것은 **자식 프로세스가 끝났음을 부모 프로세스에 알려주기 위함이다.**
```
부모-자식 관계를 만드는 이유는 사용하던 자원을 회수하기가 용이하기 때문이다.
```

##### 메모리 오버레이
프로그램 크기가 실제메모리(물리메모리)보다 클 때 적당한 크기로 잘라서 가져오는 기법을 메모리 오버레이라고 한다.  
메모리 오버레이는 하나의 메모리에 여러 프로그램을 겹겹이 쌓아놓고 실행하는 것을 말한다.  
이는 가상메모리 시스템의 기본이 되는 개념이다.  
프로그램 전체가 아니라 일부만 메모리에 올라와도 실행이 가능하다.  

##### 스왑영역
메모리가 모자라서 쫓겨난 프로세스가 모이는 저장장치 공간  
[최대 절전 모드]를 사용할때 데이터가 옮겨가는 곳! [최대 절전 모드]를 실행하면 하드디스크가 깜박거리다가 전원이 꺼지는 이유이기도 함.  

##### 요구 페이징
메모리를 효율적으로 관리하기 위해서, 응답 속도를 향상하기 위해서 프로세스의 일부만 메모리로 가져오는 것.  

페이지 부재(page fault)
> 프로세스가 페이지를 요청했을 때 그 페이지가 메모리에 없는 상황
> 페이지 부재가 발생하면 스왑 영역에서 물리 메모리로 옮겨야 함.


