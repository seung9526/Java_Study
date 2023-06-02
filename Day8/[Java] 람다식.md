```
🫧 람다식
람다식(Lambda expression)은 함수형 프로그래밍 기법을 지원하는 자바의 문법 요소.

함수(function)는 기능 또는 동작을 정의한 일련의 명령 모음, 
메서드는 클래스 또는 인터페이스내에 정의된 함수를 말한다.

void abc() {
	// 기능 및 동작 : 함수 => 기능, 동작을 정의
}

class A {
	void abc(){
		// 기능 및 동작 : 메서드 => 클래스 또는 인터페이스 내부에서 정의된 함수
	}
}

- 함수형 프로그래밍에서 함수 사용
step 1. 함수 정의 및 구현
void abc() {
	// ...
}

step 2. 함수 호출
abc()

- 객체 지향형 프로그래밍에서 메서드 사용
step 1. 메서드 정의 및 구현
class A{
	void abc(){
		// ...
	}
}

step 2. 객체 생성
A a = new A();

step 3. 객체 내부 메서드 호출
a.abc();

단 하나의 추상 메서드만을 포함하는 인터페이스를 함수형 인터페이스라 하고, 
이 함수형 인터페이스의 호출 및 기능을 구현하는 방법을 새롭게 정의한 문법이 바로 람다식인 것이다. 
람다식은 기존의 객체 지향 프로그램 체계 안에서 함수형 프로그래밍을 가능하게 하는 기법.

🫧 객체 지향 구조 내에서 람다식 적용 과정

itnerface A {
	void abc();
}

class B implements A{
	@Override
	public void abc(){
		System.out.println("메서드 내용 1");
	}
}

public class OOPvsFP{
	public static void main(String[] args){
		// 1. 객체 지향 프로그래밍 문법 1
		A a1 = new B();
		a1.abc();
		
		// 2. 객체 지향 프로그래밍 문법 2(익명 이너 클래스 사용)
		A a2 = new A(){
			@Override
			public void abc() {
				System.out.println("메서드 내용 2);
			}
		};
		
		a2.abc();
		
		// 3. 함수형 프로그래밍 문법(람다식)
		A a3 = () -> {System.out.println("메서드 내용 3");};
		a3.abc();
	}
}

람다식은 익명 이너 클래스 정의 내부에 있는 메서드명을 포함해 이전 부분을 삭제한 형태다. 
즉, 람다식은 익명 이너 클래스의 축약된 형태라고 볼 수 있다.

🫧 람다식의 기본 문법 및 약식 표현
- 람다식의 기본 문법
구현된 추상 메서드를 람다식으로 표현할 때는 메서드명 이후의 소괄호와 중괄호만을 차례대로 포함하여, 
이들 사이에는 람다식 기호인 화살표(->)가 들어간다. 즉, '(소괄호) -> {중괄호}'

- 람다식의 약식 표현
1. 중괄호 안의 실행문이 1개일 때 중괄호 생략 가능
A a1 = () -> {System.out.println("테스트");}
A a2 = () -> System.out.println("테스트);

2. 매개변수 타입을 생략 가능하고, 매개변수가 1개일 때 () 생략 가능
A a1 = (int a) -> { ... };
A a2 = (a) -> { ... };
A a3 = a -> { ... };
A a4 = int a -> { ... };  // X = 소괄호가 생략 될 떄는 매개변수 타입을 반드시 생략

3. return 구문만 포함할 때 return 생략 가능
A a1 = (int a, int b) -> { return a+b;};
A a2 = (int a, int b) -> a+b;
A a3 = (int a, int b) -> {a+b;}  // X = return을 생략할 때 중괄호를 반드시 함께 생략

🫧 람다식의 활용
람다식은 익명 이너 클래스 내부 구현 메서드의 약식 표현뿐 아니라 메서드 참조와 생성자 참조에도 사용된다. 
여기서 참조한다는 의미는 함수형 인터페이스의 메서드를 구현하는 데 있어 직접 구현하는 대신, 
이미 있는 기능을 가져다 쓰겠다는 의미. 
즉, 구현 메서드의 약식 표현은 함수형 인터페이스의 추상 메서드를 직접 구현했을 때,
메서드 참조는 이미 있는 메서드로 대체했을 때다. 

생성자 참조는 구현 메서드의 내용이 객체 생성 코드만으로 거정돼 있을 때.

🫧 구현 메서드의 약식 표현
interface A {
    // 입력 X, 리턴 X
    void method1();
}
interface B {
    // 입력 O, 리턴 X
    void method2(int a);
}
interface C {
    // 입력 X, 리턴 O
    int method3();
}
interface D {
    // 입력 O, 리턴 O
    double method4(int a, double b);
}


public class FunctionToLambdaExpression {
    public static void main(String[] args) {
        // 인터페이스의 함수 구현 -> 람다식
        // 1. 익명 이너 클래스 방식
        A a1 = new A(){
            @Override
            public void method1(){
                System.out.println("입력 x 리턴 x 함수");
            }
        };

        // 람다식 표현
        A a2 = () -> {
            System.out.println("입력 x 리턴 x 함수");
        };

        A a3 = () -> System.out.println("입력 x 리턴 x 함수");
        // 2. 익명 이너 클래스 방식
        B b1 = new B(){
            @Override
            public void method2(int a){
                System.out.println("입력 O 리턴 X 함수");
            }
        };

        // 람다식 표현
        B b2 = (int a) -> {
            System.out.println("입력 O 리턴 X");
        };
        B b3 = (a) -> {System.out.println("입력 O 리턴 X");};
        B b4 = (a) -> System.out.println("입력 O 리턴 X");
        B b5 = a -> System.out.println("입력 O 리턴 X");

        // 3. 익명 이너 클래스 방식
        C c1 = new C() {
            @Override
            public int method3(){
                return 4;
            }
        };

        // 람다식 표현
        C c2 = () -> {return 4;};
        C c3 = () -> 4;

        // 4. 익명 이너 클래스 방식
        D d1 = new D(){
            @Override
            public double method4(int a, double b){
                return a + b;
            }
        };

        // 람다식 표현
        D d2 = (int a, double b) -> {return a + b;};
        D d3 = (a, b) -> {return a+b;};
        D d4 = (a, b) -> a + b;
    }
}

🫧 메서드 참조
두 번째 람다식의 활용 예는 추상 메서드를 직접 구현하는 대신, 
이미 구현이 완료된 메서드를 참조하는 것이다. 
메서드를 참조하는 방식은 다시 인스턴스 메서드를 참조할 때와 정적 메서드를 참조할 때로 나눠지며, 
인스턴스 메서드의 참조는 다시 2가지로 나뉜다.

- 저의돼 있는 인스턴스 메서드 참조
인스턴스 메서드를 참조하기 위해서는 먼저 인스턴스 메서드가 사용할 수 있는 상태가 돼야 하므로 
당연히 객체를 먼저 생성해야 할 것이다. 
객체 생성 이후 인스턴스 메서드를 참조하는 방법은 

'객체 참조 변수::인스턴스메서드명'과 같이 작성한다.

⭐ 인스턴스 멤버(필드, 메서드, 이너 클래스)는 인스턴스, 
즉 객체 내부에 존재하기 때문에 이를 사용하기 위해서는 항상 객체를 먼저 생성해야 한다.

- 정의 되어있는 인스턴스 메서드 참조
클래스 객체 :: 인스턴스 메서드명

interface A {
	void abc();
}

class B {
	void bcd() {
		System.out.println("메서드");
	}
}
public class RefOfIntanceMethod_Type1_1 {
	public static void main(String[] args){
		//	1. 익명 이너 클래스
		A a1 = new A() {
			@Override
			public void abc(){
				B b = new B();
				b.bcd();
			}
		};
		
		// 람다식으로 표현
		A a2 = () -> {
			B b = new B();
			b.bcd();
		};
		
		// 정의된 인스턴스 메서드 참조
		B b = new B();
		A a3 = b::bcd;
		
		a1.abc();
		a2.abc();
		a3.abc();
	}
}

- 정의돼 있는 정적 메서드 참조
클래스명::정적 메서드명

정적 메서드는 객체 생성 없이 클래스명으로 바로 사용할 수 있기 때문에 
객체의 생성 없이 클래스명을 바로 사용했다고 생각하면 된다. 
정적 메서드 역시 메서드의 참조를 위해서는 리턴타입과 입력매개변수 타입이 동일해야한다.

interface A {
	void abc(B b, int k);
}

class B {
	static void bcd() {
		System.out.println("메서드");
	}
}
public class RefOfIntanceMethod_Type1_1 {
	public static void main(String[] args){
		//	1. 익명 이너 클래스
		A a1 = new A() {
			@Override
			public void abc(B b, int k){
				b.bcd(k);
			}
		};
		
		// 람다식으로 표현
		A a2 = (B b, int k) -> {
			B.bcd(k);
		};
		
		// 정의된 인스턴스 메서드 참조
		B b = b::bcd;
		
		a1.abc(new B(), 3);
		a2.abc(new B(), 3);
		a3.abc(new B(), 3);
	}
}

- 자바에서 제공하는 클래스의 메서드 참조

// 익명 이너 클래스
A a = new A() {
	public int abc(String str){
		return str.length();
	}
};

// 람다식
A a = (str) -> str.length();

A a = String::length();

🫧 생성자 참조
람다식의 마지막 활용 방법은 생성자 참조다. 
생성자 참조에서 참조하는 생성자는 크게 배열 객체 생성자와 클래스 객체 생성자로 나뉜다.

- 배열 생성자 참조
함수형 인터페이스에 포함된 추상 메서드가 배열의 크기를 입력매개변수로 하여, 
특정 배열 타입을 리턴한다면 구현 메서드의 내부에는 반드시 new 자료형[]이 포함될 것이다. 
이때 인터페이스에 포함된 추상 메서드의 구현 메서드가 new 자료형[]과 같이 
배열 객체의 생성 기능만을 수행할 때는 람다식의 배열 생성자 참조 방법을 사용할 수 있다.

배열 타입::new

interface A {
	int[] abc(int len);
}

// 익명 이너 클래스
A a = new A() {
	public int[] abc(int len){
		return new int[len];
	}
}

// 람다식
A a = (len) -> new int[len];

- 배열의 new 생성자를 참조할 때
A a = int[] :: new


interface A {
	int[] abc(int len);
}

public class RefOfIntanceMethod_Type1_1 {
	public static void main(String[] args){
		//	1. 익명 이너 클래스
		A a1 = new A() {
			@Override
			public int abc(int len){
				b.bcd(k);
			}
		};
		
		// 람다식으로 표현
		A a2 = (int len) -> {
			return new int[len];
		};
		
		// 정의된 인스턴스 메서드 참조
		A a3 = int[]::new;
		
		int[] array1 = a1.abc(3);
		int[] array2 = a2.abc(3);
		int[] array3 = a3.abc(3);
		
		System.out.println(array1.length);
		System.out.println(array2.length);
		System.out.println(array3.length);
	}
}

- 클래스 생성자 참조
클래스명 :: new

배열과 완벽히 동일한 개념으로 추상 메서드를 구현할 때 new 생성자()와 같이 
객체만을 생성해 리턴하면 이러한 클래스 생성자 참조를 사용할 수 있다.

A a = B::new;

interface A {
	B abc();
}

class B {
	B() {
		System.out.println("첫 번째 생성자");
	}
	B(int k) {
		System.out.println("두 번째 생성자");
	}
}

public class RefOfClassConstructor {
	public static void main(String[] args) {
		A a1 = new A(){
			@Override
		};
		
		A a3 = B::new;
		a1.abc();
		a3.abc();
	}
}

클래스 생성자 참조에서는 고려해야 할 사하잉 있는데, 
그것은 바로 생성자가 여러 개일 수 있다는 것이다. 
즉, 클래스 B가 여러 개의 생성자를 갖고 있을 때 A a = B::new와 같이 표현하면 
클래스B의 어떤 생성자가 호출되는지의 문제가 남는다. 

이런 문제는 인터페이스 A에 포함된 추상 메서드의 매개변수에 따라 결정.

```
