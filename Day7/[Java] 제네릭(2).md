```
🫧 제네릭 타입 범위 제한의 필요성
제네릭 타입의 범위 제한으로 얻을 수 있는 또 하나의 장점은 
입력매개변수로 제네릭 타입의 객체 t가 전달됐을 때 메서드 내부에서 사용할 수 있는 객체 t의 메서드 종류다.

즉, 제네릭 타입 변수가 이후에 어떤 타입으로 지정될지 모르기 때문에 
제네릭 입력매개변수를 갖는 메서드의 내부에서는 Object 클래스의 메서드만 사용할 수 있었다. 

만일 입력매개변수의 제네릭 타입 변수가 Number 클래스로 한정된다면 
실제 제네릭 타입으로는 Number 또는 Number 클래스의 자식 클래스인 Integer, Long, Float, Double 등과 
같은 타입만 지정될 수 있을 것이다.

⭐ Number 클래스는 8개의 기본 자료형 중 숫자를 저장하는 
6개의 기본 자료형(byte, short, int, long, float, double)을 
클래스로 포장(wrapping)한 클래스를(Byte, Short, Integer, Long, Float, Double)의 
공통된 특성을 뽑아 정의한 부모 클래스.

🫧 제네릭 타입 범위 제한의 종류와 타입 범위 제한 방법
- 제네릭 클래스의 타입 제한
접근 지정자 class 클래스명 < T extends 최상위 클래스/인터페이스명> {
}

이때 주의해야 할 점은 여기서 사용한 extends 키워드는 상속에서 사용한 것처럼 '상속하라'. 
의미가 아니라 '최상위 클래스/인터페이스로 지정한다'의 의미를 갖는다는 것이다. 
그래서 뒤에 나오는 요고사 클래스인든, 인터페이스이든 항상 extends 키워드를 사용해야 한다.

- 제네릭 메서드의 타입 제한
제네릭 클래스와 마찬가지로 <제네릭 타입 변수 extends 상위 클래스>와 같이 올 수 있는 
최상위 타입을 정의하며, 클래스와 인터페이스 모두 extends 키워드를 사용한다. 
즉, 제네릭 클래스일 때와 동일한 타입 제한 방식이 적용되는 것이다.

접근 지정자 <T extends 최상위 클래스/인터페이스명> T 메서드명(T t){
	// 최상위 클래스의 메서드 사용 가능
}

제네릭 메서드에서 중요한 것은 메서드 내부에서 사용할 수 있는 메서드의 종류이다. 
타입을 제한 하지 않을 때는 모든 타입의 최상위 클래스인 Object 메서드만 사용할 수 있다. 
하지만 같은 원리로 <T extends String>과 같이 표현하면 올 수 있는 모든 타입의 
최상위 타입이 String이기 때문에 해당 제네릭 메서드의 내부에서는 
String 객체의 멤버(필드/메서드)를 사용할 수 있는 것이다.

⭐ chatAt(int index) 메서드는 String 클래스의 매서드로, 
문자열에서 index 위치의 문자를 char 타입으로 리턴하는 메서드다.

class GenericMethods{

	// Object 메서드만 사용 가능
	public <T> void method1(T t) {
		char c = t.charAt(0);
		System.out.println(c);
	}
	
	// String의 메서드 사용 가능
	public <T extends String> void method2(T t){
		char c = t.charAt(0);
		System.out.println(c);
	}
}

String은 자식 클래스를 생성할 수 없는 final 클래스이기 때문에 
<T extends String>과 같이 표현하면 실제 제네릭 타입으로 올 수 있는 타입은 String 밖에 없다.

class A{
	public <T extends Number> void method1(T t){
		// 값을 정수로 리턴하는 Number 클래스의 메서드
		System.out.println(t.intValue());
	}
}

interface MyInterface{
	public abstract void print();
}

class B {
	public <T extends MyInterface> void method1(T t) {
		t.print();
	}
}

public class BoundedTypeOfGenericMethod {
	public static void main(String[] args){
		A a = new A90;
		// = a.<Double>method1(5.8)
		a.method1(5.8);
		
		B b = new B();
		b.method1(new MyInterface(){
		@Override
		public void print(){
				System.out.println("print() 구현");
			}
		});
	}
}

- 메서드 배개변수일 때 제네릭 클래스의 타입 제한
입력 매개변수에 입력되는 제네릭 클래스 객체의 제네릭 타입은 크게 4가지 형태로 제한할 수 있다.

1.
리턴 타입 메서드명(제네릭 클래스명<제네릭 타입명> 참조 변수명) {
	// ...
}

2.
리턴타입 메서드명(제네릭 클래스명<?> 참조 변수명) {
	// ...
}

3.
리턴 타입 메서드명(제네릭 클래스명<? extends 상위 클래스/인터페이스> 참조 변수명) {
	// ...
}

4.
리턴 타입 메서드명(제네릭 클래스명<? extends 하위 클래스/인터페이스> 참조 변수명) {
	// ...
}


ex)
//	제네릭 타입 = A인 객체만 가능
method(Goods<A> v)	

//	제네릭 타입 = 모든 타입인 객체 가능
method(Goods<?> v)	

//	제네릭 타입 = B 또는 B의 자식 클래스인 객체만 가능
method(Goods<? extends B> v)

//	제네릭 타입 = B 또는 B의 부모 클래스인 객체만 가능
method(Goods<? super B> v)

첫 번째 객체의 제네릭 타입을 특정 타입으로 확정하는 방법이며 
이때 해당 타입을 제네릭타입으로 갖는 제네릭 객체만 입력매개변수로 전달할 수 있다.

두 번째는 제네릭 타입변수에<?>를 사용할 때로, 
이때는 제네릭 타입으로 어떤 것이 대입됐든 
해당 제네릭 객체이기만 하면 매개변수로 사용할 수 있다는 것을 의미한다. 

세 번째는 <? extends 상위 클래스 / 인터페이스>와 같이 표기하는 방법으로, 
이때 상위 클래스 또는 상위 클래스의 자식 클래스 타입이 
제네릭 타입으로 대입된 객체가 매개변수로 올 수 있다.

마지막으로 <? super 하위 클래스 / 인터페이스>는 extends와 반대 개념으로, 
제니릭 타입으로 하위 클래스 또는 하위 클래스의 부모 클래스 타입이 올 수 있다는 것을 의미.

class A {}
class B extends A {}
class C extends B {}
class D extends C {}

class Goods<T> {
	private T t;
	public T get(){
		return t;
	}
	
	public void set(T t){
		this.t = t;
	}
}

class Test {
	void method1(Goods<A> g) {}	  // case1
	void method2(Goods<?> g) {}	  // case2
	void method3(Goods<? extends B> g) {}	// case3
	void method4<Goods<? super B> g) {}	  // case4
}

public class BoundedTypeOfInputArguments {
	public static void main(String[] args){
		Test t = new Test();
		
		// case1
		t.method1(new Goods<A>());
		// t.method1(new Goods<B>());
		// t.method1(new Goods<C>());
		// t.method1(new Goods<D>());
		
		// case2
		t.method2(new Goods<A>());
		t.method2(new Goods<B>());
		t.method2(new Goods<C>());
		t.method2(new Goods<D>());
		
		// case3
		// t.method3(new Goods<A>());
		t.method3(new Goods<B>());
		t.method3(new Goods<C>());
		t.method3(new Goods<D>());
		
		// case4
		t.method4(new Goods<A>());
		t.method4(new Goods<B>());
		// t.method4(new Goods<C>());
		// t.method4(new Goods<D>());
	}
}

🫧 제네릭 클래스의 상속
부모 클래스가 제네릭 클래스일 때, 이를 상속한 자식 클래스도 제네릭 클래스가 된다. 
또한 자식 클래스는 제네릭 타입 변수를 추가해 정의할 수도 있다.

- 부모 클래스와 제네릭 타입 변수의 개수가 동일할 때
class Parent<K, V> {
	// ...
}

class Child<K, V> extends Parent<K, V> {
	// ...
}

- 부모 클래스보다 제네릭 타입 변수의 개수가 많을 때
class Parent<K> {
	// ...
}

class Child<K, V> extends Parent<K> Parent {
	// ...
}

class Parent<T> {
	T t;
	public T getT(0{
		return t;
	}
	
	public void setT(T t) {
		this.t = t;
	}
}

class Child1<T> extends Parent<T> {
}

class Child2<T, V> extends Parent<T> {
	V v;
	public V getV(){
		return v;
	}
	
	public void setV(V v){
		this.v = v;
	}
}

public class InheritanceGenericClass {
	public static void main(String[] args) {
		// 부모 제네릭 클래스
		Parent<String> p = new Parent<>();
		p.setT("부모 제네릭 클래스");
		System.out.println(p.getT());
		
		// 자식 클래스1
		Child1<String> c1 = new Child1<>();
		c1.setT("자식 1 제네릭 클래스");
		System.out.println(c1.getT());
		
		// 자식 클래스2
		Child2<String, Integer> c2 = new Child2<>();
		c2.setT("자식 2 제네릭 클래스");
		c2.setV(100);
		System.out.println(c2.getT());
		System.out.println(c2.getV());
	}
}

🫧 제네릭 메서드의 상속
제네릭 메서드를 포함한 일반 클래스를 상속해 자식 클래스를 생성할 때도 
부모 클래스 내의 제네릭 메서드는 그대로 자식 클래스로 상속된다.

- 부모 클래스의 제네릭 메서드를 상속받아 사용하는 예
class Parent {
	public <T> void print(T t) {
		System.out.println(t);
	}
}

class Child extends Parent {
}

Parent p = new Parent();
p.<String>print("안녕");

Child c = new Child();
c.<String>print("안녕");


```
