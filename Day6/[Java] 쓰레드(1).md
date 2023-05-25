```
🫧 프로그램과 프로세스의 개념
프로그램 : 하드디스크에 저장된 파일들의 모임
프로세스 : 메모리상의 로딩된 프로그램을 의미

멀티 프로세스 : 동일 프로그램을 메모리에 2번 로딩하면 2개의 프로세스가 동작하는 경우

🫧 쓰레드의 개념
'cpu를 사용하는 최소단위' : cpu를 사용하는 것은 프로세스 내부의 쓰레드라는 것을 알 수 있음

🫧 자바 프로그램에서의 쓰레드
.class 파일을 실행하면 자바 가상 머신은 main 쓰레드를 생성. 
프로그램이 처음 실행되면 시작 시점에서는 main 쓰레드 1개만이 존재. 
main() 메서드에서 작성한 내용이 바로 이 main 쓰레드에서 동작 함.
만일 main 쓰레드의 내부에서 2개의 쓰레드를 생성해 실행하면 
동시에 2개 이상의 쓰레드가 동작하게 되는데, 
이를 멀티 쓰레드 프로세스라고 한다.

🫧 쓰레드는 정말 동시에 수행 될까?
이를 이해하기 위해서는 쓰레드의 동시성과 병렬성을 이해해야함.

쓰레드는 동시성(Concurrency)과 병렬성(Parallelism)을 갖고 수행 : 이런 동시성과 병렬성 때문에 
                                                  사용자는 동시에 동작하는 것으로 인식 한다.

단일 쓰레드로 2개의 작업을 처리할 떄 각 작업은 순차적(sequential)으로 처리
멀티 쓰레드는 동시성 또는 병렬성을 가지고 처리

- 동시성
동시성은 처리할 작업의 수가 cpu의 코어 수 보다 많을 때.

ex) cpu 코어는 1개인데 동시에 처리해야 할 작업이 2개일 때. 
    이때 cpu는 각 작업 쓰레드의 요청 작업을 번갈아가면서 실행하며 
    매우 짧은 간격으로 교차 실행하기 때문에 사용자는 두 작업이 마치 
    동시에 실행되는 것처럼 보이는 것이다. 
    이것이 바로 쓰레드이 동시성이다.

- 병렬성
cpu의 코어 수가 작업 수보다 많을 때 이때는 각가의 작업을 
각각의 코어에 할당해 동시에 실행할 수 있기 때문에 이를 쓰레드의 병렬성이라 한다.

🫧 쓰레드의 생성 및 실행
1. Thread 클래스를 상속받아 run()메서드를 오버라이딩(재정의)하는 것으로 
이 메서드의 내부에서 작성된 내용이 바로 cpu를 독립적으로 사용하면서 동시에 실행되는 것이다. 

2. Thread 객체를 생성할 때 앞 단계에서 생성한 Runnable 객체를 생성자로 전달하는 것이다. 
즉 2가지 생성 방법 모두 run() 메서드를 재정의하고 있고, 
결과적으로 Thread 객체를 생성한다.

이렇게 생성한 쓰레드를 실행하는 방법으로는 Thread 객체 내의 start() 메서드를 호출하는 것이다. 
그리고 start() 메서드로 한 번 실행된 Thread 객체는 재사용할 수 없다는 것이다. 
만일 다시 실행하고 싶다면 객체를 다시 생성해야한다.

🫧 쓰레드 생성 및 실행 방법
- 1. Thread 클래스를 상속받아 run() 메서드 재정의

step 1. 클래스 정의
Thread 클래스를 상속받아 run() 메서드를 오버라이딩한 클래스(또는 익명 이너 클래스) 정의

class MyTread extends Thread {
	@Override
	public void run(){
		// 쓰레드 작업 내용
	}
}

step 2. 객체 생성
Thread 객체 생성

Thread myTread = new MyTread();
또는
MyTread myThread = new MyThread();

step 3. 쓰레드 실행
start() 메서드를 이용해 쓰레드 실행

myThread.start();

run() 메서드와 start() 메서드의 차이점은 무엇일까?
쓰레드는 cpu를 사용하는 최소 단위라고 했는데, 
실제 cpu와 이야기하기 위해서는 자신만의 스택메모리를 포함해 준비해야 할 것이 많다. 
start()메서드는 바로 '새로운 쓰레드 생성/ 추가를 위한 모든 준비', 
'새로운 쓰레드 위에서 run()실행' 이라는 2가지 작업을 연속으로 실행하는 메서드인 것이다.

⭐ 쓰레드 내부에 run() 메서드가 있기 때문에 run()을 직업 호출해도 오류는 발생하지 않는다. 
  다만 이때 별도의 쓰레드가 아닌 현재의 쓰레드에서 일반 메서드처럼 실행된다.

start() = 새로운 쓰레드 생성/추가하기 위한 모든 준비 + 새로운 쓰레드 위에 run() 실행

방법 1. 2개의 쓰레드 활용 (main, SMIFile Thread)
// Thread 클래스를 상속해 클래스를 생성한 후 쓰레드 2개 생성

class SMIFileThread extends Thread {
	@Override
	public void run() {
		// 자막 번호 하나~다섯
		String[] strArray = {"하나", "둘", "셋", "넷", "다섯"};
		try {Thread.sleep(10);} catch (InterruptedException e) {}
		// 자막 번호 출력
		for( int i=0; i<strArray.length; i++){
			System.out.println("- (자막번호) " + strArray[i]);
			try {Thread.sleep(200);} catch (InterruptedException e) {}
		}
	}
}

public class CreateAndStartThread_M1C1{
	public static void main(String[] args){
		//SMIFileThread 객체 생성 및 시작
		Thread smiFileThread = new SMIFileThread();
		smiFileThread.start();
		
		// 비디오 프레임 번호 1~5
		int[] intArray = {1,2,3,4,5};
		
		// 비디오 프레인 번호 출력
		for(int i=0; i<intArray.length;i++){
			System.out.println("(비디오 프레임) " + intArray[i]);
			try {Thread.sleep(200);} catch (InterruptedException e) {}
		}
	}
}

방법 1. 3개의 쓰레드 활용 (main, SMIFile Thread, VideoFileThread)
// Thread 클래스를 상속해 클래스를 생성한 후 쓰레드 3개 생성

class SMIFileThread extends Thread {
	@Override
	public void run() {
		// 자막 번호 하나~다섯
		String[] strArray = {"하나", "둘", "셋", "넷", "다섯"};
		try {Thread.sleep(10);} catch (InterruptedException e) {}
		// 자막 번호 출력
		for( int i=0; i<strArray.length; i++){
			System.out.println("- (자막번호) " + strArray[i]);
			try {Thread.sleep(200);} catch (InterruptedException e) {}
		}
	}
}

class VideoFileThread extends Thread {
	@Override
	public void run(){
		// 비디오 프레임 번호 1~5
		int[] intArray = {1,2,3,4,5};
		
		// 비디오 프레인 번호 출력
		for(int i=0; i<intArray.length;i++){
			System.out.println("(비디오 프레임) " + intArray[i]);
			try {Thread.sleep(200);} catch (InterruptedException e) {}
		}
	}
}

public class CreateAndStartThread_M1C2 {
	public start void main(String[] args){
		
		// SMIFileThread 객체 생성 및 시작
		Thread smiFileThread = new SMIFileThread();
		smiFileThread.start();
		
		// VideoFileThread 객체 생성 및 시작
		Thread videoFileThread = new VideoFileThread();
		videoFileThread.start();
	}
}

방법 2. Runnable 인터페이스 구현 객체를 생성한 후 Thread 생성자로 Runnable 객체 전달
⭐ Runnable 인터페이스를 구현한 클래스를 직접 정의하는 대신 
   익명 이너 클래스 정의 방법을 이용해 바로 객체를 생성할 수도 있다.

step 1. 클래스 정의
Runnable 인터페이스를 구현한 클래스 정의(추상 메서드 run() 구현)
class MyRunnable implements Runnable {
	@Override
	public void run(){
		// 쓰레드 작업 내용
	}
}

step 2. 객체 생성
- Runnable 객체 생성
- Thread 객체 생성 (생성자에 Runnable 객체 전달)

Runnable r = new MyRunnable();
또는
MyRunnable r = new MyRunnable();
Thread myThread = new Thread(r);

step 3. 쓰레드 실행
start() 메서드를 이용해 쓰레드 실행
myThread.start();

// Runnable 인터페이스를 상속해 클래스를 생성한 후 쓰레드 2개 생성

class SMIFileRunnable implements Runnable {
	@Override
	public void run(){
		// 비디오 프레임 번호 1~5
		int[] intArray = {1,2,3,4,5};
		
		// 비디오 프레인 번호 출력
		for(int i=0; i<intArray.length;i++){
			System.out.println("(비디오 프레임) " + intArray[i]);
			try {Thread.sleep(200);} catch (InterruptedException e) {}
		}
	}
}
	
public class CreateAndStartThread_M2C1 {
	public static void main(String[] args){
		// SMIFileRunnable 객체 생성
		Runnable smiFileRunnable = new SMIFileRunnable();
		
		// smiFileThread.start();
		Thread thread = new Thread(smiFileRunnable);
		thread.start();
		
		// 비디오 프레임 번호 1~5
		int[] intArray = {1,2,3,4,5};
		
		// 비디오 프레인 번호 출력
		for(int i=0; i<intArray.length;i++){
			System.out.println("(비디오 프레임) " + intArray[i]);
			try {Thread.sleep(200);} catch (InterruptedException e) {}
		}
	}
}

// Runnable 인터페이스 상속 클래스를 생성한 후 쓰레드 3개 생성

class SMIFileThread implements Thread {
	@Override
	public void run() {
		// 자막 번호 하나~다섯
		String[] strArray = {"하나", "둘", "셋", "넷", "다섯"};
		try {Thread.sleep(10);} catch (InterruptedException e) {}
		// 자막 번호 출력
		for( int i=0; i<strArray.length; i++){
			System.out.println("- (자막번호) " + strArray[i]);
			try {Thread.sleep(200);} catch (InterruptedException e) {}
		}
	}
}

class VideoFileThread implements Thread {
	@Override
	public void run(){
		// 비디오 프레임 번호 1~5
		int[] intArray = {1,2,3,4,5};
		
		// 비디오 프레인 번호 출력
		for(int i=0; i<intArray.length;i++){
			System.out.println("(비디오 프레임) " + intArray[i]);
			try {Thread.sleep(200);} catch (InterruptedException e) {}
		}
	}
}

public class CreateAndStartThread_M1C2 {
	public start void main(String[] args){
		
		// SMIFileThread 객체 생성 및 시작
		Runnable smiFileRunnable = new SMIFileRunnable();
		// smiFileRunnable.start();
		Thread thread1 = new Thread(smiFileRunnable);
		thread1.start();
		
		// VideoFileThread 객체 생성 및 시작
		Runnable videoFileRunnable = new VideoFileRunnable();
		
		Thread thread2 = new Thread(videoFileRunnable);
		thread2.start();
	}
}

// 이너 클래스를 활용한 객체 생성 및 실행

public class CreateAndStartThread_M2C3{
	public static void main(String[] args){
		// 자막 번호를 출력하는 쓰레드의 익명 이너 클래스 정의하는
		Thread thread1 = new Thread(new Runnable(){
			@Override
			public void run(){
			// 자막 번호 하나~다섯
				String[] strArray = {"하나", "둘", "셋", "넷", "다섯"};
				try {Thread.sleep(10);} catch (InterruptedException e) {}
				// 자막 번호 출력
				for( int i=0; i<strArray.length; i++){
					System.out.println("- (자막번호) " + strArray[i]);
				try {Thread.sleep(200);} catch (InterruptedException e) {}
				}
			}
		});
		
		// 비디오 프레임 번호를 출력하는 쓰레드의 익명 이너 클래스 정의
		Thread thread2 = new Thread(new Runnable(){
		@Override
		public void run() {
			// 비디오 프레임 번호 1~5
			int[] intArray = {1,2,3,4,5};
		
			// 비디오 프레인 번호 출력
			for(int i=0; i<intArray.length;i++){
				System.out.println("(비디오 프레임) " + intArray[i]);
				try {Thread.sleep(200);} catch (InterruptedException e) {}
				}
			}
		});
		
		// Thread 실행
		thread1.start();
		thread2.start();
	}
}

🫧 현재 쓰레드 객체 참조값 얻어오기
쓰레드 객체를 참조할 수 없을 때 Thread 클래스의 정적 메서드인 
currentThread()메서드를 이용해 현재 쓰레드 객체의 참조값을 얻어올 수 있다.

- 현재 쓰레드 객체 참조값 얻어오기
static Thread Thread.currentThread()

🫧 실행 중인 쓰레드의 개수 가져오기
여러 개의 쓰레드가 실행되고 있을 때 현재 실행중인 쓰레드의 개수를 알고자 한다면, 
Thread 클래스 내의 정적 메서드인 activeCount()를 사용

- 실행 중인 쓰레드의 개수 가져오기
static int Thread.activeCount()

activeCount()는 동일한 쓰레드 그룹 내에서 실행 중인 쓰레드의 개수를 리턴.

🫧 쓰레드의 이름 지정 및 가져오기
직접 이름을 부여하려면 Thread 클래스의 인스턴스 메서드인 setName() 메서드를 사용

String setName(String name)

쓰레드의 이름을 직접 지정하지 않으면 컴파일러가 대신해서 자동으로 부여. 
자동으로 부여한 이름은 thread-0, thread-1, ... 과 같이 'thread-숫자' 의 형태로 부여한다.

setName() 메서드는 인스턴스 메서드이므로 일단 쓰레드 객체를 생성한 후에 작용할 수 있음. 
직접 지정했거나 자동으로 부여된 쓰레드의 이름을 가져올 때는 인스턴스 메서드인 getName()을 사용.

String getName()

- 쓰레드 객체의 속성 다루기
public class ThreasProperties_1{
	public static void main(String[] args){
		// 객체 참조하기, 쓰레드의 개수 가져오기
		Thread curThread = Thread.currentThread();
		System.out.println("현재 쓰레드의 이름 = " + curThread.getName());
		System.out.println("동작하는 쓰레드의 개수 = " + Thread.activeCount());
		
		// 쓰레드 이름 자동 지정
		for(int i=0; i<3; i++){
			Thread thread = new Thread();
			System.out.println(thread.getName());
			thread.start();
		}
		
		// 쓰레드 이름 직접 지정
		for(int i = 0; i<3; i++){
			Thread thread = new Thread();
			thread.setName(i+"번째 쓰레드");
			System.out.println(thread.getName());
			thread.start();
		}
		
		// 쓰레드 이름 자동 지정
		for(int i = 0; i<3; i++) {
			Thread thread = new Thread();
			System.out.println(thread.getName());
			thread.start();
		}
		
		// 쓰레드의 개수 가져오기
		System.out.println("동작하는 쓰레드의 개수 = " + Thread.activeCount());
	}
}

🫧 쓰레드의 우선순위
대표적으로 우선순위가 1, 5, 10일 때는 각각 
정적 상수 Thread.MIN_PRIORITY, Thread.NORM_PRIORITY, Thread.MAX_PRIORITY

이 우선순위는 쓰레드의 동시성과 관계가 있다. 
만일 2개의 쓰레드가 2개의 cpu 코어에 각각 할당돼 
동작하는 쓰레드 병렬성일 때 우선순위는 의미가 없다. 
2개의 작업이 하나의 cpu코어에서 동작할 때 쓰레드의 동시성에 따라 
2개의 작업은 일정 시간 간격으로 번갈아가면서 실행.

쓰레드의 우선순위를 지정하거나 지정된 우선순위 값을 가져오는 메서드는 
Thread 클래스의 인스턴스 메서드인 setPriority()와 getPriority()이다.

- 쓰레드 객체의 우선순위 정하기
void setPriority(int priority)

- 쓰레드 객체의 우선순위 가져오기
int getPriority()

🫧 쓰레드의 데몬 설정
일반 쓰레드가 모두 종료되면 함께 종료되는 쓰레드를 데몬 쓰레드 라고한다.

일반 쓰레드 : 다른 쓰레드 종료 여부와 상관업이 자신의 작업이 종료될 때까지 계속 수행
데몬 쓰레드 : 일반 쓰레드(사용자 쓰레드)가 모두 종료되면 작업이 완료되지 않더라도 함께 종료

- 데몬 쓰레드 설정
Thread 클래스의 인스턴스 메서드인 setDeamon() 메서드를 사용하며, 기본 값은 false다.
void setDeamon(boolean on)

- 데몬 쓰레드 설정 확인
isDaemon() 메서들 이용해 확인 할 수 있음
boolean isDaemon()

주의 할 점은 데몬 설정은 반드시 쓰레드를 실행하기 전, 
즉 start() 메서드 호출전에 설정해야 한다는 것이다.

// 일반 쓰레드와 데몬 쓰레드
class MyThread extends Thread {
	@Override
	public void run(){
		System.out.println(getName() + ": " + (isDaemon()? "데몬 쓰레드":"일반 쓰레드"));
		for(int i=0; i< 6; i++){
			System.out.println(getName() + ": " + i + "초");
			try {Thread.sleep(1000);} catch(InterruptedException e) {}
		}
	}
}

public class ThreasProperties_3_3{
	public static void main(String[] args){
		
		// 일반 쓰레드
		Thread thread1 = new MyThread();
		thread1.setDeamon(false);	// 일반 쓰레드로 설정
		thread1.setName("thread1");
		thread1.start();
		
		// 데몬 쓰레드
		Thread thread2 = new MyThread();	// 모든 일반 쓰레드가 중지돼야 종료됨
		thread2.setDeamon(true);	// 데본 쓰레드로 설정
		thread2.setName("thread2");
		thread2.start();
		
		// 3.5초 후 main 쓰레드 종료
		try{Thread.sleep(3500);} catch (InterruptedException e){}
		System.out.println("main Thread 종료");
	}
}
```
