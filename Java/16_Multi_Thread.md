## 멀티 스레드

- **프로세스** : 실행중인 하나의 애플리케이션
- **스레드** : 하나의 코드 실행 흐름
- **멀티 스레드** : 애플리케이션 내부에서의 멀티 태스킹
  - 스레드는 하나의 프로세스 내부에 생성되기 때문에 하나의 스레드가 예외를 발생시키면 프로세스 자체가 종료될 수 있어 다른 스레드에게 영향을 미치게 된다.
- **메인 스레드** : 모든 자바 어플리케이션은 메인 스레드가 `main()` 메소드를 실행하면서 시작

<br>

### 작업 스레드 생성과 실행

멀티 스레드로 실행하는 어플리케이션을 개발하려면 먼저 몇 개의 작업을 병렬로 실행할지 결정하고 각 작업별로 스레드를 생성해야 한다. 

<br>

#### ***Thread 클래스로부터 직접 생성***

- `Runnable`을 매개값으로 갖는 생성자를 호출해야 한다.

``` java
Thread thread = new Thread(Runnable target);
```

- `Runnable`은 인터페이스 타입이기 때문에 구현 객체를 만들어 대입해야 한다.
- `Runnable`에는 `run()` 메소드 하나가 정의되어 있는데, 구현 클래스는 `run()`을 오버라이딩해서 작업 스레드가 실행할 코드를 작성해야 한다.

```java
class Task implements Runnable {
    public void run() {
        스레드가 실행할 코드;
    }
}
```

- `Runnable`은 작업 내용을 가지고 있는 객체로 `Runnable` 구현 객체를 생성한 후, 이것을 매개값으로 해서 `Thread` 생성자를 호출하면 작업 스레드가 생성된다.

```java
Runnable task = new Task();

Thread thread = new Thread(task);
```

- 작업 스레드는 `start()` 메소드를 호출하면 실행된다.

```java
thread.start();
```

```java
// ThreadOne.class
public Class ThreadOne implements Runnable {
    
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("스레드1")	// 0.3 초마다 실행
	    try {
            Thread.sleep(300);
        } catch(Exception e) {}
        }
    }
    
}

// main
public Class ThreadTest {
    public static void main(String[] args) {
        
        Runnable threadOne = new ThreadOne();
        Thread thread = new Thread(threadOne);
        thread.start();	// ThreadOne.run() 실행
        
        for (int i = 0; i < 5; i++) {
            System.out.println("메인");
            try {
                Thread.sleep(500);
            } catch(Exception e) {};
        }
    }
}

/*
메인 스레드
1번 스레드
1번 스레드
메인 스레드
1번 스레드
1번 스레드
메인 스레드
1번 스레드
메인 스레드
메인 스레드
*/
```

<br>

### ***Thread 하위 클래스로부터 생성***

- 스레드가 실행할 작업을 `Runnable`로 만들지 않고, `Thread`의 하위 클래스로 작업 스래드를 정의하면서 작업 내용을 포함시킬 수 있다.

```java
public class WorkerThread extends Thread {
    @Override
    public void run() {
        // 스레드가 실행할 코드
    }
}
Thread thread = new WorkerThread();

// 익명 객체로 생성 가능
Thread thread = new thread() {
    public void run() {
        // 스레드가 실행할 코드
    }
}
```

<br>

### ***스레드의 이름***

- 메인 스레드는 `main` 이라는 이름을 가지고 있고 우리가 직접 생성한 스레드는 `Thread-n` 이라는 이름으로 설정된다.
- `setName()` 메소드로 스레드 이름을 변경할 수 있다.
- `getName()` 메소드로 스레드 이름을 구할 수 있다.

<br>

### 스레드 우선순위

- 스레드의 개수가 코어의 수보다 많을 경우, 스레드를 어떤 순서에 의해서 동시성으로 실행할 것인가를 결정한다. 이것을 스레드 스케줄링 이라고 한다. 
- 스레드 우선순위 방식은 스레드 객체에 우선 순위 번호를 부여할 수 있기 때문에 개발자가 코드로 제어할 수 잇다.
  - 우선순위는 1에서 10까지 부여되는데 1이 가장 우선순위가 낮고, 10이 가장 높다.
  - 우선순위의 default 값은 5이다.
  - 우선순위를 변경하고 싶다면 Thread 클래스가 제공하는 `setPriority()` 메소드를 이용한다.

```java
thread.setPriority(우선순위);

// Thread.MAX_PRIORITY = 10
// Thread.NORM_PRIORITY = 5
// Thread.MIN_PRIORITY = 1
```

<br>

### 동기화 메소드와 동기화 블록

멀티 스레드 프로그램에서는 스레드들이 객체를 공유해서 작업해야 하는 경우가 있는데 이 경우 여러 스레들이 동시에 같은 객체를 공유하면 엉터리 값이 나올 수 있기 때문에 주의해야 한다.

<br>

#### *동기화 메소드 및 동기화 블록*

- 스레드가 사용 중인 객체를 다른 스레드가 변경할 수 없도록 하려면 스레드 작업이 끝날 때까지 객체에 잠금을 걸어서 다른 스레드가 사용할 수 없도록 해야 한다.
- **임계 영역** : 멀티 스레드 프로그램에서 단 하나의 스레드만 실행할 수 잇는 코드 영역
  - 자바는 임계 영역을 지정하기 위해 동기화(synchronized) 메소드와 동기화 블록을 제공
  - 스레드가 객체 내부의 동기화 메소드 또는 블록에 들어가면 즉시 객체에 잠금을 걸어 다른 스레드가 임계 영역 코드를 실행하지 못하게 한다.

```java
// 동기화 메소드
public synchronized void method() {
    // 임계 영역
}
```

일부 내용만 임계 영역으로 만들고 싶다면 아래와 같이 한다.

```java
public void method() {
    // 여러 스레드가 실행 가능한 영역
    synchronized(공유객체) {
        // 임계 영역 ( 단 하나의 스레드만 실행 )
    }
    // 여러 스레드가 실행 가능한 영역
}
```

<br>

### 스레드 상태

- 스레드 객체를 생성하고 `start()` 메소드를 호출하면 실행 대기 상태가 된다.

  - **실행 대기 상태** : 아직 스케줄링이 되지 않아서 실행을 기다리고 있는 상태
  - **실행 상태** : 실행 대기 상태에 있는 스레드 중에서 스레드 스케줄링으로 선택된 스레드가 `run()` 메소드를 실행하는 상태
  - **일시 정지 상태** : 스레드가 실행할 수 없는 상태 ( 스레드가 실행 상태가 되려면 일시 정지 상태에서 실행 대기 상태로 바뀌어야 함)

  - `getState()` : 스레드 상태를 리턴
    - 객체 생성 
      - `NEW` : 스레드 객체가 생성, 아직 `start()` 메소드가 호출되지 않은 상태
    - 실행대기
      - `RUNNABLE` : 실행 상태로 언제든지 갈 수 있는 상태
    - 일시정지
      - `WAITING` : 다른 스레드가 통지할 때 까지 기다리는 상태
      - `TIMED_WAITING` : 주어진 시간 동안 기다리는 상태
      - `BLOCKED` : 사용하고자 하는 객체의 락이 풀릴 때까지 기다리는 상태
    - 종료 
      - `TERMINATED` : 실행을 마친 상태

<br>

### 스레드 상태 제어

- 실행 중인 스레드의 상태를 변경하는 것
- `interrupt()` : 일시 정지 상태의 스레드에서 `InterruptedException` 예외를 발생시켜, 예외 처리 코드(`catch`)에서 실행 대기 상태로 가거나 종료 상태로 갈 수 있도록 한다.
- `notify()`, `notifyAll()` : 동기화 블록 내에서 `wait()` 메소드에 의해 일시 정지 상태에 있는 스레드를 실행 대기 상태로 만든다.
- `resume()` : `suspend()` 메소드에 의해 일시 정지 상태에 있는 스레드를 실행 대기 상태로 만든다. 
- `sleep(long mills)` : 주어진 시간 동안 스레드를 일시 정지 상태로 만든다. 주어진 시간이 지나면 자동적으로 실행 대기 상태가 된다.
- `join(long mills)` : `join()` 메소드를 호출한 스레드는 일시 정지 상태가 된다. 실행 대기 상태로 가려면 `join()` 메소드를 멤버로 가지는 스레드가 종료되거나 매개값으로 주어진 시간이 지나야 한다.
- `wait(long mills)` : 동기화 블록 내에서 스레드를 일시 정지 상태로 만든다. 매개값으로 주어진 시간이 지나면 자동적으로 실행 대기 상태가 된다. 시간이 주어지지 않으면 `notify()`, `notifyAll()` 메소드에 의해 실행 대기 상태로 갈 수 있다.
- `suspend()` : 스레드를 일시 정지 상태로 만든다. `resume()` 메소드를 호출하면 다시 실행 대기 상태가 된다.
- `yield()` : 실행 중에 우선순위가 동일한 다른 스레드에게 실행을 양보하고 실행 대기 상태가 된다.
- `stop()` : 스레드를 즉시 종료시킨다.

<br>

<br>

<br>

___

이것이 자바다 한빛 미디어 - 신용권

































