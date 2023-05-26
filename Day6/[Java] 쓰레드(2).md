```
🫧 동기화의 개념

동기화(synchronized) : 하나의 작업이 완전히 완료된 후 다른 작업을 수행하는 것을 말함. 
비동기(asynchronous) : 하나의 작업 명령 이후 완료 여뷰 상관없이 바로 다른 작업 명령을 수행

🫧 동기화의 필요성
// 동기화를 사용하지 않았을 때 문제 발생
class MyData {
	int data = 3;
	
	public void plusData() {
		int mydata = data;
		try {Thread.sleep(2000);} catch (InterruptedException e) {}
		data = mydata + 1;
	}
}

// 공유 객체를 사용하는 쓰레드
class PlusThread extends Thread {
	MyData myData;
	public PlusThread(MyData myData){
		this.myData = myData
	}
	
	@Override
	public void run(){
		myData.plusData();
		System.out.println(getName() + "실행 결과: " + myData.data);
	}
}

public class TheNeedsForSynchronized {
	public static void main(String[] args){
		// 공유 객체 생성
		MyData myData = new MyData();
		
		// plusThread 1
		Thread plusThread1 = new PlusThread(myData);
		plusThread1.setName("plusThread1");
		plusThread1.start();
		
		try {Thread.sleep(1000);} catch (InterruptedException e){}
		
		// plusThread 2
		Thread plusThread2 = new PlusTread(myData);
		plusThread2.setName("plusThread2");
		plusThread2.start();
	}
}

2개의 쓰레드가 각각 MyData 객체의 data 필드값을 1씩 증가시켰는데도 두 결과 값은 4의 결과값을 가진다. 
이유는 두 번째 쓰레드가 data 필드를 증가시키는 시점에 아직 첫 번째 쓰레드의 실행이 끝나지 않았기 때문에 
즉, 이 시점에서 데이터값은 여전히 3이다.

5의 값을 나오게 하려면 하나의 쓰레드가 MyData 객체 내의 data 필드값을 완전히 증가시키고난 후 
다음 쓰레드가 동일한 작업을 수행하면 data 필드값은 5의 결과를 가질 것이다.

이렇게 한 쓰레드가 객체를 모두 사용해야 다음 쓰레드가 사용할 수 있도록 설정하는 것을 '동기화' 라고 한다.

🫧 동기화 방법
동기화 방법은 크게 메서드 동기화와 블록 동기화로 나눌 수 있다.

동기화는 '하나의 쓰레드가 객체를 사용한 후 다른 객체가 사용할 수 있도록 하는 설정'
한 객체를 두 쓰레드가 동시에 사용할 수 없다는것, 

블록 동기화는 2개의 쓰레드가 동시에 해당 블록을 실행할 수 없다는 것을 의미
즉 하나의 쓰레드가 메서드 또는 블록 사용을 완전히 종료한 후 
잠금이 풀리면 다른 쓰레드가 사용할 수 있다는 것이다.

⭐ 하나의 쓰레드가 공유 객체를 사용할 때 다른 쓰레드가 해당 객체를 사용할 수 없도록 하는 것을 
  '객체를 잠근다(lock)' 라고 표현한다. 
  사용을 완료한 후 객체의 잠금을 풀면(unlock)다른 쓰레드가 사용할 수 있게 된다.

- 메서드 동기화
메서드를 동기화 할 때는 동기화하고자 하는 메서드의 리턴 타입 앞에 synchronized 키워드 만 넣으면 된다.

접근 지정자 synchronized 리턴 타입 메서드명(입력매개변수) {
	// 동기화가 필요한 코드
}

class MyData {
	int data = 3;
	public synchronized void plusData(){
		// data 필드의 값을 +1 수행
	}
}

이렇게 해야 위에서 작성한 plusData 메서드의 결과 값이 4가 나오는 문제를 해결할 수 있게 된다.

- 블록 동기화
멀티 쓰레드를 사용하는 프로그램이라 하더라도 동기화 영역에서는 하나의 쓰레드만 실행할 수 있기 때문에 
성능 면에서 손해를 보게 되며 따라서 동기화 영역은 꼭 필요한 부분에 한정해 적용하는 것이 좋음. 
만일 메서드 전체 중에 동기화가 필요한 부분이 일부라면 굳이 전체 메서드를 동기화 할 필요 없이 
해당 부분만 동기화 할수 있는데 이것이 '블록 동기화' 이다.

synchronized (임의의 객체) {
	// 동기화가 필요한 코드
}

여기서 임의의 객체 : Key를 가진 객체(모든 객체는 저마다의 Key 하나를 갖고 있음) 
일반적으로 클래스 내부에서 바로 사용할 수 있는 객체인 this를 사용 
왜냐하면 this로 자기 객체를 가르키기 때문에.

class MyData{
	int data = 3;
	public void plusData(){
		synchronized (this) {
			// data 필드의 값을 +1 수행
		}
	}
}

🫧 동기화의 원리
모든 객체는 자신만의 열쇠(Key)를 하나씩 갖고 있다. 
동기화를 사용하면 처음 사용하는 쓰레드가 Key 객체의 열쇠를 가짐.

동기화 메서드 : 자기 자신의 객체(this)
동기화 블록 : synchronized(Key 객체){}에ㅔ서 사용한 Key 객체

다른 쓰레드는 먼저 사용 중인 쓰레드가 작업을 완료하고 열쇠를 반납할 때까지 대기(blocked)

- Key 값에 따른 동시 사용 여부
class MyData {
	Object keyObject = new Object();
	synchronized void abc() {
		// 동기화 메서드
	}
	
	synchronized void bcd() {
		// 동기화 메서드
	}
	
	void cde() {
		synchronized (keyObject) {
			// 동기화 블록
		}
	}
	
	void efg() {
		synchronized (keyObject) {
			// 동기화 블록
		}
	}
}

결국 어떤 열쇠를 사용하느냐에 따라 동시 사용 여부가 정해지는 것이다.

🫧 쓰레드의 상태
쓰레드는 객체가 생성, 실행, 종료되기까지 다양한 상태를 가짐. 
각 쓰레드의 상태는 Thread.State 타입으로 정의돼 있으며 
Thread의 인스턴스 메서드인 getState()로 가져올수 있다. 
이 메서드는 쓰레드의 상태를 Thread.State 타입에 저장된 문자열 상수값중 하나로 리턴

- 쓰레드의 상태 값 가져오기
Thread.State getState()

Thread.State는 enum 타입이며 내부에는 
6개의 문자열 상수(NEW, RUNNABLE, TERMINATED, TIMED_WAITING, BLOCKED, WAITING)가 저장.

⭐ enum 타입은 자바에서 상수의 집합을 표현하기 위한 문법 체계로 문자열 상수들을 모아 놓은 자료형

- 쓰레드 상태에 따른 동작 수행
Thread.State state = myTread.getState();

switch (state) {
case Thread.State.NEW:
	// ...
case Thread.State.RUNNABLE:
	// ...
}

🫧 쓰레드의 6가지 상태
- NEW, RUNNABLE, TERMINATED
처음 객체가 생성되면 NEW의 상태를 가지며, 
이후 start() 메서드로 실행하면 RUNNABLE 상태가 된다. 
이 상태에서는 실행과 실행 대기를 반복하면서 cpu를 다른 쓰레드들과 나눠 사용한다. 
이후 run() 메서드가 종료되면 TERMINATED 상태가 된다. 
RUNNABLE 상태에서는 상황에 따라 TIMED_WAITING, BLOCKED, WAITING라는 일시정지 상태로 전환될 수 있다.

- TIMED_WAITING
정적 메서드인 Thread.sleep(long millis) 또는 인스턴스 메서드인 join(long millis)가 호출되면 
쓰레드는 TIMED_WAITING 상태가 된다.

RUNNABLE -> TIMED_WAITING 상태로 전환하기
static void Thread.sleep(long millis)
synchronized void join(long millis)

말 그대로 일정 시간 동안 일시정지되는 것. 
만일 설정한 일시정지 시간이 지나거나 중간에 interrupt() 메서드가 호출되면 다시 RUNNABLE 상태가 된다.

TIMED_WAITING -> RUNNABLE 상태로 전환하기
일시정지 시간이 종료
void interrupt()

Thread.sleep(long millis) 메서드와 join(long.millis) 메서드의 호출로 일시정지되는 대상은 
메서드를 호출한 쓰레드라는 점에서 동일하다.

차이점은 
Ex) 쓰레드 A에서 Thread.sleep(1000)을 실행했다면 
쓰레드 A는 외부에서 interrupt() 메서드가 호출되지 않는한 1초동안 일시정지 상태가 된다. 

하지만 '쓰레드 B 객체.join(1000)'과 같이 호출하면 
이는 '나는 일지성지할 테니 쓰레드 B에게 cpu를 할당하라'라는 의미를 가짐. 
따라서 만일 쓰레드 B가 0.5초 만에 실행이 완료된다면 
외부 interrupt() 메서드의 호출 없이도 다시 쓰레드 A는 RUNNABLE 상태가 된다.

- BLOCKED
두 번째 일시정지 상태는 BLOCKED 상태로 동기화 메서드 또는 동기화 블록을 실행하기 위해 
먼저 실행 중인 쓰레드의 실행 완료를 기다리는 상태

- WAITING
시간 정보가 없는 join() 메서드가 호출되거나 wait()메서드가 호출되면 WAITING상태가 된다. 
wait()는 Object 클래스로부터 상속받은 메서드

RUNNABLE -> WAITING 상태로 전환
synchronized void join()
void wait()

WAITING 상태로 전환되는 과정에서 일시정지하는 시간을 정한 바가 없으므로 
한없이 일시정지 상태에 빠져 있을 것이다. 
이 상태에서 다시 RUNNABLE 상태로 돌아가는 방법은 어떤 메서드를 인해 WAITING 상태가 됐는지에 따라 다름

join() 메서드로 WAITING 상태가 됐을 때 WAITING -> RUNNABLE 상태 전환
join()의 대상 쓰레드가 종료
void interrupt()

wait()메서드의 호출로 WAITING 상태가 됐을 때는 
Object 클래스의 notify() 또는 notifyAll()메서드를 이용해 다시 RUNNABLE 상태로 돌아갈 수 있다.

void notify()
void notifyAll()

notify는 하나의 쓰레드를 notifyAll은 모든 쓰레드를 RUNNABLE 상태로 전환. 
주의 할점 wait(), notify(), notifyAll()은 동기화 블록 내에서만 사용할 수 있다.

🫧 NEW, RUNNABLE, TERMINATED
NEW 상태는 Thread 객체를 new 키워드를 이용해 생성한 시점으로 아직 start() 메서드 호출 이전 상태, 
즉 실행 이전 상태. 이후 start() 메서드를 호출하면 RUNNABLE 상태가 된다. 
이후 run() 메서드가 완전히 종료되면 쓰레드는 TERMINATED 상태가 된다.

NEW, RUNNABLE, TERMINATED 상태의 특징
new : new 키워드로 쓰레드의 객체가 생성된 상태(start() 전)
->
Thread.yield() : 다른 쓰레드에게 cpu 사용을 양보하고 자신은 실행 대기 상태로 전환
-> 
RUNNABLE : start() 이후 cpu를 사용할 수 있는 상태, 
          다른 쓰레드들과 동시성에 따라 실행과 실행대기를 교차함
->
TERMINATED : run() 메서드의 작업 내용이 모두 완료돼 쓰레드가 종료된 상태 
      한 번 실행(start())된 쓰레드는 재실행이 불가능하며 객체를 새롭게 생성해야함.

- 쓰레드 상태(NEW, RUNNABLE, TERMINATED)
public class NewRunnableTerminated {
	public static void main(String[] args) {
		// 쓰레드 상태 저장 클래스
		Thread.State state;
		
		// 1. 객체 생성(NEW)
		Thread myThread = new Thread(){
			@Override
			public void run(){
				for(long i=0; i< 10000000: ; i++) {} //	시간 지연
			}
		}
		
		state = myThread.getState();
		System.out.println("myThread state = " + state);
		
		// 2. myThread 시작
		myThread.start();
		state = myThread.getState();
		System.out.println("myThread state = " + state);
		
		// 3. myThread 종료
		try{
			// myThread 실행이 완료될 때까지 main 쓰레드 일시 정지
			myThread.join();
		} catch ( InterruptedException e) {}
		state = myThread.getState();
		System.out.println("myThread state = " + state);
	}
}

Thread의 정적 메서드인 yield()를 호출하면 다른 쓰레드에게 cpu 사용을 인위적으로 양보하고, 
자신은 실행 대기 상태로 전환할 수도 있다.

static void Thread.yield();

yield() 메서드로 영영 cpu 사용을 양보하는 것은 아님. 
자신의 차례를 딱 한 번 양보하는 메서드로 자신의 차례가 돌아오면 다시 cpu를 사용할 수 있다.

⭐ 실행이 끝난 쓰레드 객체는 내부에서 정의한 필드 또는 메스드를 호출하는 용도로만 사용할 수 있다.

🫧 TIMED_WAITING
RUNNABLE 상태에서 TIMED_WAITING 상태가 됐을 때는 
Thread의 정적 메서드인 sleep(long millis)를 호출하거나 
인스턴스 메서드인 join(long millis)가 호출됐을 때다.

sleep와 join을 명확히 구분할 필요가 있다. 
하나는 정적 메서드, 다른 하나는 인스턴스 메서드라는 점 이외에 메서드의 의미 또한 다르다. 
join메서드는 특정 쓰레드 객체에게 일정 시간 동안 cpu를 할당하라는 의미. 
일반적으로 다른 쓰레드의 겨로가가 먼저 나와야 이후의 작업을 진행할 때 join을 사용할 수 있다.
Thread.sleep은 호출한 쓰레드를 일시정지하라는 의미.

TIMED_WAITING 상태에서 지정된 시간이 다 되거나 
일시정지된 쓰레드 객체의 interrupt() 메서드가 호출되면 다시 RUNNABLE상태가 된다. 
Thread.sleep와 join은 모두 필수적으로 InterruptedException을 처리해 줘야하는데, 
interrupt() 메서드가 호출되면 이 예외가 발생해 일시정지가 종료

- Thread.sleep을 이용한 일시정지 및 RUNNABLE 상태 전환
class MyThread extends Thread {
	@Override
	public void run(){
		try{
			Thread.sleep(3000);
		} catch (InterruptedException e) {
			System.out.println(" -- sleep() 진행 중 interrupt() 발생");
			for(long i=0; i< 10000000L; i++){}	// 시간 지연
		}
	}
}

public class TimeWaiting_Sleep{
	public static void main(String[] args){
		
		MyThread myThread = new MyData();
		myThread.start();
		
		try{Thread.sleep(100);} catch (InterruptedException e) {}
		System.out.println("MyThread State = " + myThread.getState());
		
		// TIMED_WAITING
		myThread.interrupt();	// TIMED_WAITING -> RUNNABLE 전환
		try {Thread.sleep(100);} catch (InterruptedException e) {}
		System.out.println("MyThread State = " + myThread.getState());
	}
}

쓰레드의 상태를 출력할 때 내부적인 동작으로 조금은 까다롭고 번거로운 처리를 해 줘야 하지만, 
시간지연코드를 통해 자바 가상머신이 cpu를 독립적으로 사용하기 위한 
메모리 할당 등의 준비과정 및 interrupt() 메서드에도 
시간지연 코드를 통해 InterruptedException 객체를 생성해 
해당 쓰레드의 catch(){} 블록에 전달해야되 기 때문에 사용.

- join를 이용한 일시정지 및 RUNNABLE 상태 전환

// join() 메서드를 이용한 TIMED_WAITING과 interrupt()

class MyThread1 extends Thread {
	@Override
	public void run(){
		for (long i=0; i< 1000000000L; i++) {}
	}
}

class MyThread2 extends Thread {
	MyThread1 myThread1;
	public MyThread2(MyThread1 myThread1){
		this.myThread1 = myThread1;
	}
	
	@Override
	public void run() {
		try {
			myThread1.join(3000);
		} catch (InterruptedException e) {
			System.out.println(" -- join(...) 진행 중 interrupt() 발생")'
			for(long i=0; i<1000000000L; i++){}
		}
	}
}

public class TIMED_WAITING_Join{
	public static void main(String[] args) {
		// 객체 생성
		MyThread1 myThread1 = new MyThread1();
		MyThread2 myThread2 = new MyThread2(myThread1);
		myThread1.start();
		myThread2.start();
		
		// 쓰레드 시작 준비 시간
		try {Thread.sleep(100);} catch (InterruptedException e ) {}	
		System.out.println("MyThread1 State = " + myThread1.getState());
		System.out.println("MyThread2 State = " + myThread2.getState());
		
		//	TIMED_WAITING
		myThread2.interrupt();
		
		// 인터럽트 준비시간
		try{Thread.sleep(100);} catch (InterruptedException e ) {}	
		System.out.println("MyThread1 State = " + myThread1.getState());
		System.out.println("MyThread2 State = " + myThread2.getState());
	}
}

🫧 BLOCKED
동기화 메서드 또는 동기화 블록을 실행하고자 할 때 
이미 다른 쓰레드가 해당 영역을 실행하고 있는 경우 발생. 
해당 동기화 여역이 잠겨 있을 때는 이미 실행하고 있는 쓰레드가 실행을 완료하고, 
해당 동기화 영역의 열쇠를 반납할 때 까지 기다려야 하는데, 이것이 바로 BLOCKED 상태이다.

🫧 WAITING
wait() 메서드의 호출로 WAITING 상태가 됐을 때 주의해야 할 점은 2가지이다.
1. wait() 메서드로 WAITING이 된 쓰레드는 다른 쓰레드에서 
notify() 또는 notifyAll()을 호출해야만 RUNNABLE상태가 될 수 있다는 점. 
즉, 스스로는 WAITING 상태를 벗어 날 수 없다는 것이다. 
쓰레드는 실행 중에 wait() 메서드를 만나면 그 자리에서 WAITING 상태가 된다. 
이후 다른 쓰레드에서 notify() 또는 notifyAll() 메서드가 호출되면 
일시정지됐던 지점인 wait()의 다음 줄부터 다시 이어서 실행

2. wait(), notify(), notifyAll() 메서드는 반드시 동기화 블록에서만 사용할 수 있다.

class DataBox{
    boolean isEmpty = true;
    int data;
    synchronized void inputData(int data){
        if(!isEmpty){
            try{wait();} catch (InterruptedException e){}
        }
        this.data = data;
        isEmpty = false;
        System.out.println("입력 데이터 : "+ data);
        notify();
    }

    synchronized void outputData(){
        if(isEmpty){
            try{ wait();} catch (InterruptedException e) {}
        }
        isEmpty = true;
        System.out.println("출력 데이터 : "+data);
        notify();
    }
}

public class Waiting_WaitNotify {
    public static void main(String[] args) {
        DataBox dataBox = new DataBox();
        Thread t1 = new Thread(){
            public void run(){
                for(int i=1; i<9;i++){
                    dataBox.inputData(i);
                }
            }
        };

        Thread t2 = new Thread(){
            public void run(){
                for(int i=1; i<9; i++){
                    dataBox.outputData();
                }
            }
        };

        t1.start();
        t2.start();
    }
}

쓰기 -> 읽기 -> 쓰기 -> 읽기 ... 와 같이 쓰기와 읽기가 번갈아가며 한 번씩 실행. 
이를 가능하게 하는 것이 바로 wait(), notify() 메서드다.

inputData() 메서드에서 isEmpty 불리언값을 이용데 데이터가 비어 있는지를 검사. 
만일 isEmpty = true 이면 데이터값이 비어있는 것으로 판단해 
매개변수로 넘어온 데이터값을 필드에 복사한 후 isEmpty = true로 변경 하고, 
WAITING 상태의 읽기 쓰레드를 RUNNABLE 상태로 바꾸기 위한 notify() 메서드를 호출

반대로 isEmpty = false이면 쓰기를 완료한 데이터를 아직 읽기 쓰레드가 읽지 않은 것으로 간주해 
wait() 메서드를 실행함으로써 자신은 WAITING 상태가 된다. 
WAITING 상태가 되면 당연히 열쇠는 반납하게 되며, 
이 열쇠를 차지한 읽기 쓰레드가 동기화 영역을 실행할 것이다.

읽기 쓰레드는 쓰기 쓰레드와 반대로 isEmpty = true 이면 아직 읽을 데티어가 없는 것이므로 
자신은 열쇠를 반납하고 WAITING 상태가 된다. 
이와 반대로 isEmpty = false 이면 읽을 데이터가 있다는 것으로 
해당 데이터를 출력한 후 isEmpty = true 반환하고, 
쓰기 쓰레드를 RUNNABLE 상태로 변환시키기 위한 notify() 메서드를 호출

```
