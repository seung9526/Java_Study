```
🫧 자바 소스 코드의 실행 과정

1. .java 소스 파일 생성 (파일 저장 시 자동 컴파일)
2. .class 바이트 코드 파일 생성 (실행)
3. JVM은 메모리 할당 (메서드 영역에 클래스 로딩)
4. main() 메서드 실행


🛠️ 자바 가상 머신이 할당한 메모리 영역은?

자바 가상 머신은 메모리를 효율적으로 관리하기 위해 메모리를 크게 메서드(method) 영역, 스택(stack) 영역, 힙(heap) 영역으로 나눠 사용. 특히 메모리의 메서드 영역은 클래스(class)영역, 정적(static) 영역, 상수(final) 영역이라고도 부른다.
메모리 할당 이후 실행 파일인 바이트 코드는 메모리의 메서드 영역에 로딩되며, 이후 클래스 내에 포함돼 있는 main() 메서드를 실행하는 것이 자바 가상 머신의 역할이다. 즉 main() 메서드가 자바 프로그램의 시작 지점이자 끝 지점인 것이다.


🫧 클래스 선언부

public class Test{
	class : 클래스라는 것을 알려 주는 자바 키워드
	Test : 클래스명
}

public은 이 클래스를 다른 패키지에서도 사용할 수 있다는 의미를 지닌 접근 지정자이다.
여기에서 클래스의 내부에 포함될 수 있는 내부 구성 요소가 위치하며 내부 구성 요소는 필드(field), 메서드(method), 생성자(constructor), 이너 클래스(inner class) 이다.


🫧 main()메서드

'리턴 타입 메서드명(...) {}'의 형태를 띠낟. 리턴(반환) 타입은 void, 메서드명은 main이다.

ex)
public static void main(String[] args){
	void : 리턴 타입
	main : 메서드명
}

메서드 원형 앞에 위치한 public은 접근 지정자, static은 정적 메서드를 나타내는 키워드이다.
여기서 public static한 메서드 바이트 코드(.class)가 메서드 영역에 로딩되면 자바 가상 머신은 main() 부터 찾는다.
따라서 실행 이후 가장 먼저 실행되는 메서드가 main() 메서드 이다. 

📝 자료형

데이터를 저장하려면 메모리에 값을 저장할 공간을 생성하고 이름을 부여해야 한다. 이때 공간에 부여하는 이름을 '변수'라고 하며 메모리 공간은 목적에 따라 크기와 특징이 다른데, 이를 자료형이라고 한다. 즉 메모리 공간의 자료형에 따라 저장할 수 있는 값의 종류와 특징이 결정

🫧 이름 짓기
영문 소문자로 시작, 영문 단어를 2개 이상 결합할 때는 새로운 단어의 첫 글자를 대문자로 한다.(카멜케이스)

상수명을 지을 때 권장 사항으로는 상수는 변수와 구분하기 위해 모두 대문자로 표기하며 단어가 여러개로 결합되면 가독성이 떨어지므로 각각 밑줄(_)을 사용해 분리

🫧 변수의 생존기간
자바에서는 개발자가 직접 변수를 생성한다. 하지만 메모리에서 변수를 삭제하는 작업은 자바 가상 머신이 알아서 한다. 삭제를 하는 주체가 개발자가 아니므로 사라진 변숫값을 읽거나 값을 대입하려고하면 문법 오류가 발생하기 때문이다. 

변수는 선언된 시점에서 생성 디며 이후 생성된 변수는 자신이 선언된 열린 중괄호의 쌍인 닫힌 중괄호를 만나면 메모리에서 삭제

🫧 자바 메모리 구조
|-------------------------------|------------------------------|------------------------------|
|	클래스 영역		|			       |			      |
|	정적 영역		|	   스택 영역	       |	힙 영역	              |
|	상수 영역		|			       |			      |
|	메서드 영역		|			       |			      |
|-------------------------------|------------------------------|------------------------------|

 실제 데이터 값의 저장 위치 : 기본 자료형은 스택 메모리에 생성된 공간에 실제 변수값을 저장하는 반면, 참조 자료형은 실제 데이터 값은 힙 메모리에 저장하고, 스택 메모리의 변수 공간에 실제 변수값이 저장된 힙 메모리의 위치값을 저장한다.

🫧 기본 자료형 간의 타입 변환
boolean을 제외한 기본 자료형 7개는 자료형을 서로 변환할 수 있는데 이를 타입 변환(type casting)이라고 한다. 타입 변환 방법은 단순히 변환 대상 앞에(자료형)만 표기하면 된다.

그리고 자동타입 변환과 수동 타입 변환이 존재하며 컴파일러가 자동으로 수행하는 '자동 타입 변환'과 개발자가 직접 타입 변환을 수행해야 하는 '수동 타입 변환'이 있다. 작은 자료형을 큰 자료형에 담으면 개발자가 타입 변환 코드를 넣어 주지 않더라도 컴파일러가 자동으로 타입변환을 실행하는데, 이를 '업케스팅(up-casting)'이라고 한다.

큰 자료형을 작은 자료형에 대입하는 행위를 '다운캐스팅(down-casting)'이라고 한다. 이때 데이터 손실이 발생할 수 있으므로 컴파일러에 따른 자동 타입 변환은 일어자니 않으며 개발자가 직접 명시적으로 타입 변환을 수행해야 한다. 크기는 'byte < short/char < int < long < float < double'의 순서로 커진다.

```
