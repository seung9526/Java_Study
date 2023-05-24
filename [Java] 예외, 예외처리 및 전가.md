```
🫧 예외와 에러의 차이점
예외(exception) : 연산 오류, 숫자 포맷 오류 등과 같이 상황에 따라 개발자가 해결할 수 있는 오류. 
해결할 수 있는 오류라는 것은 차선책을 선택하는 것을 말함.

에러(error) : 자바 가상 머신 자체에서 발생하는 오류로 '개발자가 해결할 수 없는 오류'를 말함

⭐ 오류가 발생했을 때 차선책을 제시함으로써 오류를 피하는 과정을 '예외 처리'라고 한다.

자바에서 예외의 최상위 클래스는 Exception 클래스, 
에러의 최상의 클래스는 Error 클래스이다. 
이 2개의 클래스는 모두 Throwable 클래스를 상혹하고 있으며 
따라서 에러와 예외 모두 Throwable 클래스의 모든 기능을 포함한다.

🫧 예외 클래스의 상속 구조
Throwable 클래스를 상속받은 Exception 클래스는 다시 일반 예외(checked exception) 
클래스와 실행예외(unchecked(runtime) exception)으로 나뉨

일반 예외 : 컴파일 전에 체크
	ClassNotFountException
	InterruptedException
	IOException
	FileNotFoundException
	CloneNotSupportedExcption

실행 예외 : 실행할 때 체크
	ArithmeticException
	ClassCastException
	ArrayIndexOutOfBoundsException
	NumberFormatException
	NullPointerException
	
🫧 일반 예외 클래스
- InterruptedException
Thread.sleep(시간) 메서드는 일정 시간 동안 해당 쓰레드를 
일시정지 상태로 만드는 Thread 클래스의 정적 메서드다. 
이 메서드는 일반 예외가 발생할 수 있기 때문에 반드시 예외 처리를 해야한다. 
이를 생략하면 문법 오류가 발생해 컴파일 자체가 불가능

⭐ 쓰레드는 프로그램 실행 과정에서 cpu를 사용하는 최소 단위로, 프로세스 내에 존재

public class A{
	public static void main(String[] args){
		Thread.sleep(1000);
	}
}

- ClassNotFountException
클래스를 동적으로 메모리에 로딩하는 메서드로, 
해당 클래스의 정보를 담고 있는 Class 타입의 객체를 리턴. 
만약 동적으로 로딩하는 과정에서 해당 클래스가 존재하지 않을 때는 ClassNotFountException이 발생

⭐ 실제 java.lang.Object 클래스가 존재하더라도 예외 처리를 하지 않으면 문법오류가 발생. 
즉, 실제 클래스의 조냊 유무와 상관없이 예외가 발생할 수 있는 코드인지가 중요.

public class A{
	public static void main(String[] args){
		Class cls = Class.forName("java.lang.Object");
	}
}

- IOException
콘솔이나 파일에 데이터를 쓰거나(write()) 읽을(read()) 때 발생하며, 
반드시 IOException에 대한 예외 처리를 해야한다.

public class A{
	public static void main(String[] args){
		InputStreamReader isr = new InputStreamReader(System.in);
		isr.read();
	}
}

- FileNotFoundException
파일을 읽을 때 해당 경로에 파일이 없으면 FileNotFoundException이 발생

public class A{
	public static void main(String[] args){
		FileInputStream fis = new FileInputStream("test.txt");
	}
}

- CloneNotSupportedExcption
Object클래스의 메서드 중 clone()은 자신의 객체를 복사한 클론 객체를 생성해 리턴하는 메서드.
이를 위해 복사의 대상이 되는 클래스는 반드시 Cloneable 인터페이스를 상속해야한다.

⭐ Cloneable는 내부에 추상 메서드를 포함하고 있지 않으며, 
단순히 해당 클래스가 복사 기능을 제공함을 나타내는 마커(marker)의 기능만을 수행하는 인터페이스다.

🫧 실행 예외

- ArithmeticException
'산술','연산'이다. 즉, ArithmeticException은 연산 자체가 불가능할 때 발생하는 실행 예외

public class A{
	public static void main(String[] args){
		System.out.print(3/0);
	}
}

- ClassCastException
다운캐스팅이 불가능한 상황에서 다운캐스팅을 시도할 때 발생

class A {}
class B extends A {}

public class Test{
	public static void main(String[] args){
		A a = new A();
		B b = (B) a;
	}
}	

- ArrayIndexOutOfBoundsException
배열의 인덱스를 잘 못 사용했을 때 발생한다.
배열의 인덱스는 항상 0 ~ (배열의 길이 -1) 까지의 값만 사용할 수 있다.

public class A{
	public static void main(String[] args){
		int [] a = {1,2,3};
		System.out.print(a[3]);
	}
}

- NumberFormatException
public class A{
	public static void main(String[] args){
		int num = Integer.parseInt("10!");
	}
}

- NullPointerException
참조 변수가 실제 객체를 가리키고 있지 않은 상황에서 필드나 메서드를 호출할 때 발생. 
여기서 null은 위칫값을 저장하는 참조 변수의 초깃값으로만 사용할 수 있으며, 
현재 가리키고(pointing)있는 객체가 없다는 것을 의미.

public class A{
	public static void main(String[] args){
		String a = null;
		System.out.print(a.charAt(2));
	}
}

🫧 예외 처리 문법
3가지 요소 (try, catch, finally)로 구성

try{
	// 일반 예외, 실행 예외 발생 가능 코드
}
catch(){
	// 예외가 발생했을 때 처리
}
finally{
	// 예외 발생 여부에 상관없이 무조건 실행
}

⭐ 예외 처리 구문이 있으면 자바 가상 머신은 적절히 예외가 처리됐다고 
판단하기 때문에 프로그램을 강제종료 하지 않는다. 
심지어 예외 처리 구문 내에 아무런 코드를 작성하지 않아도 예외가 처리된 것으로 간주.

🫧 예외 처리 과정
먼저 try{} 구문이 실행. 
만일 예외가 발생하지 않는다면 catch(){} 블록은 실행되지 않을 것이고, 
finally{} 블록이 있다면 이 블록을 실행할 것이다.

🫧 다중 예외 처리
try{
}
catch(예외 타입 e1){
}
catch(예외 타입 e2){
}
finally{
}

이런 다중 예외 처리 구문을 작성할 때 주의 할 사항은 여러개의 catch(){} 블록이있을 때 
실행할 catch(){} 블록의 선택 과정은 항상 위에서부터 확인

- 다중 예외를 한 블록에서 처리
try{
}
catch(예외 타입 A | 예외 타입 B 참조 변수명){
}
finally{
}

🫧 리소스 자동 해제 예외 처리
finally{} 블록의 가장 대표적인 기능은 리소스를 해제하는 것이다. 

try(리소스 자동 해애제 필요한 객체 생성){
	// 예외 발생 가능 코드
}
catch(예외 클래스명 참조 변수명) {
	// 해당 예외가 발생했을 때 처리하는 블록
}
finally{
	// 예외 발생 여부에 상관없이 무조건 생항하는 블록
}

AutoCloseable 자동해제를 위해 구현해야 한다. 
이 인터페이스 내부에는 close() 추상 메서드가 포함돼 있기 때문에 
이 인터페이스를 구현한 모든 클래스의 객체는 내부에 close() 
메서드를 포함하고 있다는 것을 보장받을 수 있는 것이다.

즉, 리소스 자동 해제 객체는 
반드시 close 메서드를 로함 해야 함 = 리소스 자동 해제 객체는 AutoCloseable 인터페이스를 구현해야 함

class A implements AutoCloseable {
	String resource;
	A(String resource) {
		this.resource = resource;
	}
	
	@Override
	public voide close() throws Exception {
	resource = null;
	System.out.print("리소스 해제");
	}
}

🫧 예외 전가
자신을 호출한 지점으로 예외를 전가(throws) 할 수도 있다. 
예외를 전가하면 예외 처리의 의무를 호출한 메서드가 갖게 된다. 
상위의 메서드도 자신을 호출한 지점으로 예외를 전가 할 수 있음.

🫧 예외 전가 문법
리턴 타입 메서드명(입력매개변수) throws 예외 클래스명 {
	// 예외 발생 코드
}

void abc() {
	try {
		bcd();
	} catch (InterruptedException e){
		// 예외 처리 구문
	}
}

void bcd() throws InterruptedException {
	Thread.sleep(1000);
}

- 다중 예외 전가 구조
리턴 타입 메서드명(입력매개변수) throws 예외 클래스 A, 예외 클래스 B ... {
	// 여러 개의 예외 종류가 발생할 수 있는 블록
}

🫧 사용자 정의 예외 클래스 생성 방법
1. 예외 클래스를 사용자가 직접 정의
2. 작성한 예외 클래스를 이용해 객체를 생성
3. 고려하는 예외 상황에서 예외 객체를 던진다.

- 사용자 정의 예외 클래스 작성
사용자 예외 클래스를 정의하는 방법은 Exception을 바로 상속해 
일반 예외 클래스로 만드는 방법과 RuntimeException을 상속해 실행 예외 클래스로 만드는 방법

- 사용자 정의 예외 객체 생성
사용자 정의 예외 클래스 객체 생성해
MyException me1 = new MyException();
MyException me2 = new MyException("예외 메시지");

- 예외 상황에서 예외 객체 던지기
예외 객체를 '던진다'는 것은 '실제 자바 가상 머신에게 예외 객체를 만들어 전달한다' 는 의미. 
예외 객체를 던지면 곧바로 예외가 발생 그러면 자바 가상 머신은 그 예외를 처리할 수 있는 
catch(){} 블록에게 받았던 예외 객체를 전달

예외를 해당 메서드 안에서 직접 처리
void abc(int age) {
	try {
		if (age>=0)
			System.out.print("정상값");
		else
			throw new MyException();
	} catch (MyException e) {
		System.out.print("예외 처리");
	}
}

void bcd() {
	abc(-2);
}

예외를 사위 메서드로 전가해 예외 처리
void abc(int age) throws MyException {
	if(age>=0)
		System.out.print("정상값");
	else
		throw new MyException();
}

void bcd(){
	try {
		abc(-2);
	} catch (MyException e) {
		System.out.print("예외 처리");
	}
}

// 1. 사용자 일반 예외
class MyException extends Exception {
	public MyException() {
		super();
	}
	
	public MyException(String message) {
		super(message);
	}
}

// 2. 사용자 실행 예외
class MyRTException extends RuntimeException {
	public MyRTException() {
		super();
	}
	
	public MyException(String message) {
		super(message);
	}
}

class A {
// 3. 사용자 정의 예외 객체 생성
	MyException me1 = new MyException();
	MyException me2 = new MyException("예외 메세지 : MyException");
	
	MyRTException mre1 = new MyRTException();
	MyRTException mre2 = new MyRTException("예외 메시지: MyException");
	
	// 4. 예외 던지기(throw) : 던진 시점에서 예외 발생
	// 방법 1. 예외를 직접 처리
	void abc_1(int num) {
		try {
			if(num > 70)
				System.out.print("정상 작동");
			else
				throw me1;
		} catch (MyException e) {
			System.out.print("예외 처리 1");
		}
	}
	
	void bcd_1() {
		abc_1(65);
	}
	
	// 방법 2. 예외 전가
	void abc_2(int num) throws MyException {
		if(num > 70)
			System.out.print("정상 작동");
		else
			throw me1;
	}
	
	void bcd_2{
		try {
			abc_2(65);
		} catch (MyException e) {
			System.out.print("예외 처리 2");
		}
	}
}

public class CreateUserException {
	public static void main(String[] args){
		A a = new A();
		a.bcd_1();
		a.bcd_2();
	}
}

🫧 예외 클래스의 메서드
- getMessage() 메서드
public String getMessage()

예외 객체를 생성했을 때 메시지를 전하지 않았을 경우
try{
	throw new Exception();
} catch (Exception e) {
	System.out.print(e.getMessage());	// null
}

예외 객체를 생성했을 때 메시지를 전달했을 경우
try {
	throw new Exception("예외 메시지");
} catch (Exception e) {
	System.out.print(e.getMessage));	// 예외 메시지
}

- printStactTrace() 메서드
public String printStactTrace()

class A{
	void abc() throws NumberFormatException {
		bcd();
	 }
	 
	void bcd() throws NumberFormatException {
		cde();
	}
	void cde() throw NullPointerException {
		int num = Integer.parseInt("10A");
	}
}

public static void main(String[] args){
	// 객체 생성
	A a = new A();
	
	// 메서드 호출 + 예외 처리
	try {
		a.abc();
	} catch (NumberFormatException e) {
		e.printStactTrace();
	}
}

```
