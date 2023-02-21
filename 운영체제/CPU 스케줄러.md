# CPU 스케줄러

### 스케줄링 이란?

+ 여러 프로세스가 번갈아가며 사용하는 자원을 어떤 시점에 어떤 프로세스에게 할당할 지 결정하는 것
+ 스케줄링 방법에 따라 프로세서를 할당받을 프로세스를 결정하므로 시스템의 성능에 직/간접적 영향을 미침
+ CPU를 선점한 프로세스가 대기하는 시간을 보다 효율적으로 사용하기 위해 사용

<br>

## <b>선점 스케줄링과 비선점 스케줄링</b>

### 1. 선점 스케줄링

+ 낮은 우선순위를 가진 프로세스보다 높은 우선순위를 가진 프로세스가 CPU를 선점
+ 프로세스 하나가 장시간 동안 프로세서를 독점하는 것을 방지하기 위한 것 (운영체제가 할당된 CPU를 해제할 수 있음)

<br>

+ <b>장점</b> : 우선 순위가 높은 프로세스가 긴급 처리되어야할 때 유용하고 모든 프로세스에 프로세서를 할당해줄 수 있는 기회가 생김
+ <b>단점</b> : 잦은 프로세스 교환(Context Switching)으로 인해 오버헤드가 높음

<br>

### 2. 비선점 스케줄링

+ 한 프로세스가 프로세서를 선택했을 때 다른 프로세스가 해당 프로세서를 빼앗을 수 없도록 한 것
+ Time-slice가 없고, CPU를 사용중인 프로세스가 자율적으로 반납하도록 하는 방식

<br>

+ <b>장점</b> : 실행 시간이 짧은 프로세스가 먼저 자원을 가질 수 있어 가장 짧은 평균 대기 시간을 가질 수 있음
+ <b>단점</b> : 실행 시간이 긴 프로세스는 실행 시간이 짧은 프로세스에 밀려 Starvation 상황이 올 수 있음

<br>

+ 스케줄링이 일어나는 시점
    1. Running -> Waiting (ex. I/O 요청)
    2. Running -> Terminated (ex. 부모프로세스의 종료)
    3. Running -> Ready (ex. 인터럽트 발생)
    4. Waiting -> Ready (ex. I/O 완료)

> 스케줄링이 1번과 2번에만 일어난다면 이를 비선점 스케줄링이라고 하고, 네 가지 경우 모두에 일어난다면 선점 스케줄링이라고 한다.

<center>

![5stateModel](https://user-images.githubusercontent.com/68081743/219364784-7ce8d0df-bd18-4fc1-96c0-67b786dcec88.png)

5 - State Model</center>

***
<br>

## <b>스케줄링 알고리즘의 종류</b>

\* 스케줄링 알고리즘의 결과는 Gantt Chart로 보일 수 있다.

### 1. FCFS (First-Come, First-Serve)

+ 가장 간단한 스케줄링 알고리즘
+ <b>CPU를 먼저 요청한 프로세스</b>가 먼저 할당을 받는 방식
+ 비선점 스케줄링(Non-preemptive scheduling)
    + 프로세스가 실행되기 시작하면, 끝나거나 차단(Block)될 때까지 계속 실행된다.
+ CPU 사용 시간이 긴 프로세스에 의해 사용시간이 짧은 프로세스들이 오래 기다리는 "Convoy effect(호위 효과)"라는 문제가 있다. 

<center>

![Convoy Effect](https://user-images.githubusercontent.com/68081743/219364889-96836a80-9011-4b4a-93b5-f83784bc718f.png)

Convoy Effect</center>

<br>

### 2. SJF (Shortest Job First)

+ 프로세스의 <b>실행시간이 가장 짧은 프로세스</b>가 먼저 할당을 받는 방식
+ 선점 또는 비선점 스케줄링 모두 가능
+ 항상 짧은 작업을 먼저 처리하므로 평균 대기 시간이 가장 짧다.
+ 수행 시간이 긴 작업은 짧은 작업에 밀려 기아(Starvation)가 발생할 수 있다.
+ 실행 시간 예측이 어려워 실용성이 떨어진다.

<br>

### 3. SRTF (Shortest Remaining Time First)

+ <b>최단 잔여시간</b>을 우선으로 하는 스케줄링
+ 선점형 SJF 스케줄링이라고 불린다.
+ SJF와 마찬가지로 실행 시간 추정 작업이 필요하다.
+ SJF와 마찬가지로 실행 시간이 긴 프로세스들의 평균 응답 시간이 길어진다. (마찬가지로 기아 발생 가능)
+ 잦은 선점으로 문맥 교환과 오버헤드가 증가한다.

<br>

### 4. 우선순위 스케줄링 (Priority Scheduling)

+ 프로세스에 우선순위를 할당하고 <b>우선순위가 가장 높은 프로세스</b>에 먼저 할당하는 방식
+ 선점과 비선점 모두 가능하며, 우선순위가 같을 경우 FCFS와 같다.
+ 우선순위가 낮은 프로세스에 기아가 발생할 수 있다.
+ 대기 시간이 길어질수록 그 프로세스의 우선순위를 점차 높이는 에이징 기법을 사용할 수 있다.

<br>

### 5. RR (Round Robin)

+ 작은 단위의 <b>시간 할당량</b>(Time-Slice)를 정의하여 그 시간만큼 자원을 할당하는 방식
+ 선점형 스케줄링
+ 시분할 시스템(Time Sharing System)을 위해 설계되었다.
    + 시분할 시스템: 여러명의 사용자가 사용하는 시스템에서 컴퓨터가 사용자들의 프로그램을 번갈아 처리해주는 방식
+ 모든 프로세스가 같은 우선순위를 가지고, Time slice burst가 일어나면 해당 프로세스는 스케줄링의 큐 끝으로 이동한다.
+ Time slice가 심하게 크다면 FCFS와 다를게 없어진다.
+ Time slice가 너무 작다면 불필요한 Contect Switch가 많이 일어난다.
<center>

![TimeSharingSystem](https://user-images.githubusercontent.com/68081743/219364904-c019e264-d132-458e-a086-1dc47f2b402e.png)

Time Sharing System</center>

<br>

### 6. Multilevel Queue

+ Ready Queue를 여러 개로 분할하고, 각각 queue에 우선순위를 정하고, 각각의 프로세스는 해당 프로세스의 우선순위에 따라 각 queue에 배치되며, queue간의 우선순위에 따라 하나의 queue가 CPU를 점유하는 방식
+ Queue간에 기아가 발생할 수 있으므로 Time slice를 통해 각 큐의 CPU time을 적절하게 할당할 수 있다.

<br>

### 7. Multilevel Feedback Queue

+ 이 기술은 Multilevel Queue와 유사하지만 프로세스가 알고리즘에 따라 대기열 간을 이동할 수 있다.
+ 예를 들어, CPU 시간을 많이 사용하는 프로세스는 다른 프로세스의 기아를 방지하기 위해 다른 큐로 이동할 수 있다.