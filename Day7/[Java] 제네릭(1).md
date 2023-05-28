```
🫧 제네릭 클래스의 문법
잘못된 캐스팅을 할 때 문법 오류를 발생시켜 잘못된 캐스팅으로 발생할 수 있는 문제를 사전에 예방할 수 있다. 
이를 강한 타입 체크라고 한다.

🫧 제네릭 클래스와 제네릭 인터페이스 정의하기
- 제네릭 타입 변수명이 1개일 때
접근지정자 class 클래스명 <T> {
	// 타입 T를 사용한 코드
}

접근 지정자 interface 클래스명<T> {
	// 타입 T를 사용한 코드
}

- 제네릭 타입 변수명이 2개일 때
접근지정자 class 클래스명 <K, V> {
	// 타입 K, V 를 사용한 코드
}

접근 지정자 interface 클래스명<K, V> {
	// 타입 K, V 를 사용한 코드
}

제네릭 타입 변수             의미
T                     타입(Type)
K                     키(Key)
V                     값(Value)
N                     숫자(Number)
E                     원소(Element)

🫧 제네릭 클래스의 객체 생성
객체를 생성할 때 제네릭 타입 변수에 실제 타입을 대입하는 것이다.

클래스명 <실제 제네릭 타입> 참조 변수명 = new 클래스명<실제 제네릭 타입>();
또는
클래스명 <실제 제네릭 타입> 참조 변수명 = new 클래스명<>();

즉, 제네릭 클래스는 클래스를 정의하는 시점에 타입을 지정하는 것이 아니라 
객체를 생성하는 시점에 타입을 지정하기 때문에 하나의 제네릭 클래스로 
다양한 타입의 값을 저장 및 관리할 수 있는 객체를 생성할 수 있는 것이다.

// 제네릭 타입 변수 1개를 가진 제네릭 클래스의 선언 및 활용

class MyClass<T> {
    private T t;
    public T get(){
        return t;
    }
    public void set(T t){
        this.t = t;
    }
}

public class SingleGenericArgument {
    public static void main(String[] args) {
        // String 타입을 저장하거나 꺼내 올 수 있는 객체로 지정
        MyClass<String> mc1 = new MyClass<>();
        mc1.set("안녕");

        System.out.println(mc1.get());

        // Integer 타입을 저장하거나 꺼내 올 수 있는 객체로 지정
        MyClass<Integer> mc2 = new MyClass<>();
        mc2.set(100);

        System.out.println(mc2.get());
    }
}

// 제네릭 타입 변수 2개를 가진 제네릭 클래스의 선언 및 활용
class KeyValue<K, V> {
    private K key;
    private V value;
    public K getKey(){
        return key;
    }
    public void setKey(K key){
        this.key = key;
    }
    public V getValue(){
        return value;
    }
    public void setValue(V value) {
        this.value = value;
    }
}

public class TwoGenericArguments {
    public static void main(String[] args) {
        // 제네릭 타입 변수 K, V가 각각 String, Integer 타입으로 결정
        KeyValue<String, Integer> kv1 = new KeyValue<>();
        kv1.setKey("사과");
        kv1.setValue(1000);

        String key1 = kv1.getKey();
        int value1 = kv1.getValue();

        System.out.println("key : "+key1+" value : "+ value1);

        // 제네릭 타입 변수 K, V가 각각 Integer, String 타입으로 결정
        KeyValue<Integer, String> kv2 = new KeyValue<>();
        kv2.setKey(404);
        kv2.setValue("Not found");

        int key2 = kv2.getKey();
        String value2 = kv2.getValue();

        System.out.println("key : "+key2+" value : "+ value2);

        // 해당 제네릭 타입 변수와 필드를 사용하지 않는다는 것을 의미
        KeyValue<String, Void> kv3 = new KeyValue<>();
        kv3.setKey("키 값만 사용");

        String key3 = kv3.getKey();
        System.out.println("key : "+ key3);
    }
}

🫧 제네릭 메서드의 정의와 호출
제네릭 클래스가 객체를 생성하는 시점에 실제 타입을 지정하는 것과 달리 
제네릭 메서드는 호출되는 시점에 실제 제네릭 타입을 지정한다.

- 제네릭 타입 변수명이 1개일 때
접근 지정자 <T> T 메서드명 (T t) {
	// 타입 T를 사용한 코드
}

- 제네릭 타입 변수명이 2개일 때
접근 지정자 <T, V> T 메서드명 (T t, V v){
	// 타입 T, V 를 사용한 코드
}

- 매개변수에만 제네릭이 사용됐을 때
접근 지정자 <T> void 메서드명 (T t) {
	// 타입 T를 사용한 코드
}

- 리턴 타입에만 제네릭이 사용됐을 때
접근 지정자 <T> T 메서드명 (int a){
	// 타입 T를 사용한 코드
}

- 제네릭 메서드 호출의 문법 구조
참조 객체.<실제 제네릭 타입> 메서드명 (입력매개변수);

public <T> method1(T t) {
	return t;
}

// 일반 클래스 안에 제네릭 메서드
class GenericMethods {
    public <T> T method1 (T t){
        return t;
    }

    public <T> boolean method2(T t1, T t2){
        return t1.equals(t2);
    }

    public <K, V> void method3(K k, V v){
        System.out.println(k+" : "+v);
    }
}

public class GenericMethod {
    public static void main(String[] args) {
        GenericMethods gm = new GenericMethods();

        String str1 = gm.<String>method1("안녕");
        String str2 = gm.method1("안녕");

        System.out.println(str1);
        System.out.println(str2);

        boolean bool1 = gm.<Double>method2(2.5, 2.5);
        boolean bool2 = gm.method2(2.5, 2.5);

        System.out.println(bool1);
        System.out.println(bool2);

        gm.<String, Integer> method3("국어", 80);
        gm.method3("국어", 80);
    }
}

🫧 제네릭 메서드 내에서 사용할 수 있는 메서드
특정 타입에 포함돼 있는 메서드(String 객체의 length() 등)는 메서드를 정의하는 시점에 사용할 수 없다.
아직 결정되지 않은 제네릭 타입 T 객체의 내부에서는 Object에서 물려받은 메서드만 사용할 수 있다. 
즉, 나중에 어떤 타입이 제네릭 타입 변수로 확정되더라도 
항상 사용할 수 있는 메서드만 제네릭 메서드 내부에서 사용할 수 있는 것이다.

class A {
	// 정의 시점에서는 어떤 타입이 들어올지 모름
	public <T> void method1(T t){
		// 제네릭 메서드의 내부에서는 참조 변수 t의 메서드로 Object 클래스의 메서스만 사용 가능
	}
}

// 제네릭 메서드 내부에서 사용할 수 있는 메서드
class A{
    public <T> void method(T t){
        System.out.println(t.equals("안녕"));
    }
}

public class AvailableMethodInGenericMethod {
    public static void main(String[] args) {
        A a = new A();
        a.<String>method("안녕");
    }
}
```
