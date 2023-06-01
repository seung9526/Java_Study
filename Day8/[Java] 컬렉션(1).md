```
🫧 컬렉션이란?
컬렉션(collection)은 동일한 타입을 묶어 관리하는 자료구조를 말한다. 
배열도 동일한 타입을 묶어 관리하는 것이지만, 
배열을 컬렉션이라 부르지 않는다. 

컬렉션이 배열과 구분되는 가장 큰 특징은 바로 데이터의 저장 용랑(capacity)을 
동적으로 관리 할 수 있다는 것이다. 

배열은 생성 시점에 저장 공간의 크기를 확정해야 하고, 
나중에 변경할 수 없는 반면, 
컬렉션의 저장 공간은 데이터의 개수에 따라 얼마든지 동적으로 변화할 수 있다.

따라서 컬렉션은 메모리 공간이 허용하는 한 저장 데이터의 개수에 제약이 없다.

⭐ 저장 용량은 저장할 수 있는 최대 데이터의 개수를 말한다.

🫧 컬렉션 프레임워크란?
일반적으로 단순히 연관된 클래스와 인터페이스들의 묶음을 '라이브러리'라고 한다. 
반면 프레임워크는 클래스 또는 인터페이스를 생성하는 과정에서 설계의 원칙 또는 구조에 따라 
클래스 또는 인터페이스를 설계하고, 이렇게 설계된 클래스와 인터페이스를 묶어 놓은 개념

컬렉션 프레임워크는 이러한 컬렉션과 프레임워크가 조합된 개념으로, 
리스트, 스택, 큐, 트리 등의 자료구조에 정렬, 탐색 등의 알고리즘을 구조화해 놓은 프레임워크다. 

쉽게 말해 여러 개의 데이터 묶음 자료를 효과적으로 처리하기 위해 구조화된 클래스 또는 인터페이스의 모음

📝 정리

- 컬렉션 
동일한 타입을 묶어 관리하는 자료구조
저장 용량을 동적으로 관리

- 프레임워크
클래스와 인터페이스의 모임(라이브러리)
클래스의 정의에 설계 원칙 또는 구조가 존재

- 컬렉션 프레임워크
리스트, 스택, 큐, 트리 등의 자료구조에 정렬, 탐색 등의 알고리즘을 구조화해 놓은 프레임워크

컬렉션 특성에 따라 구분
List<E>
Set<E>
Map<K, V>

메모리의 입출력 특성에 따라 기존의 컬렉션 기능을 확장 또는 조합한
Stack<E>
Queue<E>

🫧 List<E> 컬렉션 인터페이스
- 배열과 리스트의 차이점
저장 공간의 크기가 고정적이냐, 동적으로 변화하느냐

- 배열의 특징
// 이 코드의 array는 저장 공간의 크기가 7인 배열 참조 객체
String[] array = new String[]{"가","나","다","라","마","바","사"};
array[2] = null;
array[5] = null;
System.out.println(array.length);	// 7

- 리스트의 특징
List<String> aList = new ArrayList<>();	// 저장 공간의 크기가 0인 리스트 참조 객체
aList.add("가");
aList.add("나");
aList.add("다");
aList.add("라");
aList.add("마");
aList.add("바");
aList.add("사");

System.out.println(aList.size());	// 저장 공간의 크기가 7인 리스트 참조 객체

aList.remove("다");
aList.remove("바");

System.out.println(aList.size());	// 저장 공간의 크기가 5인 리스트 참조 객체

🫧 List<E> 객체 생성하기
List<E>는 인터페이스이기 때문에 객체를 스스로 생성할 수 없다. 
따라서 객체를 생성하기 위해서는 List<E>를 상속받아 자식 클래스를 생성하고, 
생성한 자식 클래스를 이용해 객체를 생성해야 한다.

하지만 컬렉션 프레임워크를 이용할 때는 직접 인터레이스를 구현하지 않아도 되며, 
컬렉션 프레임워크 안에 이미 각각의 특성 및 목적에 따른 클래스가 구현돼 있기 때문이다. 

List<E> 인터페이스를 구현한 대표적인 클래스로는 크게 ArrayList<E>, Vector<E>, LinkedList<E>를 들 수 있다.

⭐ List<E>는 제네릭 인터페이스다. 
따라서 이후 객체를 생성하는 시점에 제네릭 변수의 타입, 
즉 내부에 어떤 타입의 데이터를 저장할 것이지를 저장해 줘야한다.

- List<E> 인터페이스 구현 클래스 생성자로 동적 컬렉션 객체 생성
객체를 생성할 때 제네릭의 실제 타입을 지정해야 한다. 
객체를 생성할 때는 일반적으로 기본 생성자를 사용하지만, 
초기 저장용량을 매개변수로 포함하고 있는 생성자를 사용할 수도 있다.

⭐ 단, List<E>의 대표적인 구현 클래스 중 LinkedList<E>는 기본 생성자만 존재한다.

저장 용량은 실제 데이터의 개수를 나타내는 저장 공간의 크기(size())와는 다른 개념으로, 
데이터를 저장하기 위해 미리 할당해 놓은 메모리의 크기라고 생각하면된다. 

자식 클래스로 객체를 생성할 때는 각각의 클래스 타입으로 선언할 수 있지만, 
당연히 다형적 표현에 따라 부모 타입인 List<E> 타입으로 선언할 수도 있다.

📝 List<E> 인터페이스의 구현 클래스 생성자로 동적 컬렉션 생성

List<제네릭 타입 지정> 참조 변수 = new ArrayList<제네릭 타입 지정>();
List<제네릭 타입 지정> 참조 변수 = new Vector<제네릭 타입 지정>();
List<제네릭 타입 지정> 참조 변수 = new LinkedList<제네릭 타입 지정>();

ArrayList<제네릭 타입 지정> 참조 변수 = new ArrayList<제네릭 타입 지정>();
Vector<제네릭 타입 지정> 참조 변수 = new Vector<제네릭 타입 지정>();
LinkedList<제네릭 타입 지정> 참조 변수 = new LinkedList<제네릭 타입 지정>();

📝 Arrays.asList() 메서드를 이용해 정적 컬렉션 객체 생성
List<E> 객체를 생성하는 또 다른 방법은 Arrays 클래스의 asList(T...) 정적 메서드를 사용하는 것이다. 
내부적으로 배열을 먼저 생성하고, 이를 List<E>로 래핑, 즉 포장만 해 놓은 것이다. 

따라서 내부 구조는 배열과 동일하므로 컬렉션 객체인데도 저장 공간의 크기를 변경 할 수 없다.

- ArrayList.asList() 메서드로 정적 컬렉션 객체 생성
List<제네릭 타입 지정> 참조 변수 = Arrays.asList(제네릭 타입 저장 데이터);

즉, 구현 클래스로 객체를 생성했을 떄와 달리 데이터의 추가(add()) 및 삭제(remove())가 불가능한다. 
다만 저장 공간의 크기를 변경하지 않는 데이터의 변경(set())은 가능하다. 
따라서 고정된 개수의 데이터를 저장하거나 활용할 때 주로 사용한다.

⭐ 고정된 개수의 데이터를 사용하는 대표적인 예로는 요일(월, 화, 수, 목, 금, 토, 일) 등을 들 수 있다.

🫧 List<E>의 주요 메서드
- 데이터 추가
return type : boolean		method name : add(E element)
							매개면수로 입력된 원소를 리스트 마지막에 추가
			
	    : void	    method name : add(int index, E element)
							index 위치에 입력된 원소 추가
			
	   : boolean		method name : addAll(Collection<? Extends E> c)
							매개변수로 입력된 컬렉션 전체를 마지막에 추가
			
	   : boolean		method name : addAll(int index, Collection<? Extends E> c)
							index 위치에 입력된 컬렉션 전체를 추가
- 데이터 변경
return type : E		method name : set(int index, E element)
							index 위치의 원소값을 입력된 원소로 변경
- 데이터 삭제
return type : E		method name : remove(int index)
							index 위치의 원소값을 삭제
							
			: boolean		method name : remove(Object o)
							원소 중 매개변수 입력과 동일한 객체 삭제
							
			: void 			method name : clear()
							전체 원소 삭제

- 리스트 데이터 정보 추출
return type : E		method name : get(int index)
							index 위치의 원소값을 꺼내 리턴

			: int 			method name : size()
							리스트 객체 내에 포함된 원소의 개수
							
			: boolean		method name : isEmpty()
							리스트의 원소가 하나도 없는지 여부를 리턴
							
- 리스트 배열 변환
return type : Object[]		method name : toArray()
							리스트를 Object 배열로 변환

	: T[]			method name : toArray(T[] t)
							입력매개변수로 전달한 타입의 배열로 변환

📝
여기서 리스트를 배열 객체로 변환하는 메서드 중 
첫 번째인 toArray()는 리스트를 원소의 자료형과 상관없이 Object[]로 변환한다. 
따라서 특정 타입으로 변환하기 위해서는 다운캐스팅이 필요하다. 

애초에 특정 타입의 배열로 리턴받기 위해서는 
toArray(T[] t)를 사용해 매개변수로 특정 타입의 배열 객체를 만들어 넘겨 주면 되는데, 
이때 만일 리스트의 데이터 개수가 배열 객체의 크기보다 작을 때는 
입력된 배열 크기가 그대로 리턴되지만, 
리스트 데이터의 개수가 더 많을 때는 배열 크기가 데이터의 개수만큼 확장돼 리턴된다.

List<E>에 있는 메서드는 추상 메서드이므로 List<E>의 자식 클래스들은 반드시 이 메서드를 구현해야 한다.

🫧 ArrayList<E> 구현 클래스
ArrayList<E>는 대표적인 List<E> 구현 클래스로, 
List<E>가 지니고 있는 대표적인 특징인 데이터를 인덱스로 관리하는 기능, 
저장 공간을 동적으로 관리하는 기능 등을 그대로 지니고 있다.

ArrayList<E>의 특징
- List<E> 인터페이스를 구현한 구현 클래스
- 배열처럼 수집(collect)한 원소(element)를 인덱스(index)로 관리하며 저장 용량(capacity)을 동적 관리

데이터 추가하기 - add()
- 단일 데이터 추가
List<Integer> aList1 = new ArrayList<Integer>();
// add (E element)
aList1.add(3);
aList1.add(4);
aList1.add(5);

System.out.println(aList1.toString());

// add(int index, E element)
aList1.add(1,6);
System.out.println(aList1.toString());

- 컬렉션 객체 추가
// addAll(Collection<? extends E> c)
List<Integer> aList2 = new ArrayList<Integer>();
aList2.add(1);
aList2.add(2);
aList2.addAll(aList1);
System.out.println(aList2.toString());

// addAll(int index, Collection<? extends E> c)
List<Integer> aList3 = new ArrayList<Integer>();
aList3.add(1);
aList3.add(2);
aList3.addAll(1, aList3);
System.out.println(aList3.toString());

데이터 변경하기 - set()
- 데이터의 변경
// set(int index, E element) : aList3 = [1, 1, 2, 2]
aList3.set(1, 5);
aList3.set(3, 6);

System.out.println(aList3.toString());

기존의 데이터를 변경할 때는 set(int index, E element) 메서드가 사용된다.

⭐ 배열에서 잘못된 위칫값에 값을 대입하거나 변경하면 ArrayIndexOutOfBoundsException이 발생.

데이터 삭제하기 - remove(), clear()
⭐ 모든 컬렉션의 원소에는 객체만 올 수 있다. 
즉, remove(1)과 같이 기본 자료형의 값으로 숫자를 직접 넣으면 숫자 1은 인덱스값을 의미한다.

데이터 정보 추출하기 - isEmpty(), size(), get(int index)
// isEmpty() aList3 = []
System.out.println(aList3.isEmpty());	// true

// size()
aList3.add(1);
aList3.add(2);
aList3.add(3);
System.out.println(aList3.toString());
System.out.println("size: " + aList3.size());

// get(int index)
System.out.println("0번째 : " + aList3.get(0));
System.out.println("1번째 : " + aList3.get(1));
System.out.println("2번째 : " + aList3.get(2));

for(int i=0 ; i<aList3.size(); i++){
	System.out.println(i+"번째 : " + aList3.get(i));
}

List<E> 객체를 사용할 떄 주로 사용되는 정보의 대표적인 예로는 
데이터의 존재 여부(isEmpty()), 저장 데이터의 개수(size()), 
특정 위치의 데이터값(get(int index))을 들 수 있다. 

isEmpty()는 말 그대로 데이터가 하나도 없을 때만 true 값을 리턴. 
size()는 실제 데이터의 개수를 리턴하며, 데이터가 추가 및 삭제될 때마다 그 값은 변하게 될 것이다.
특정 위치의 값을 가여졸 때는 get(int index)를 사용.

배열로 변환하기 - toArray(), toArray(T[] t)
toArray() 메서드는 원소의 타입과 관계없이 모든 데이터를 Object[]에 담아 리턴하지만, 
저장 원소 타입으로 다운캐스팅해 사용해야 할 수도 있다. 

이렇게 특정 타입의 배열로 바로 변환하기 위해서는 toArray(T[] t)메서드를 이용해 
매개변수로 특정 타입의 배열 객체를 만들어 넣어 주면 된다.

toArray(T[] t)메서드를 이용할 떄 주의점은 매개변수로 전달되는 배열의 크기이다. 
리스트가 갖고 있는 데이터의 개수보다 작은 크기의 배열을 넘겨 주면 
리스트 데이터의 개수만큼 크기가 확장된 배열을 리턴한다. 

하지만 배열의 리스트 데이터의 개수보다 더 큰 배열을 입력하면 
해당 배열의 앞부분부터 데이터를 넣어 리턴.

🫧 Vector<E> 구현 클래스
List<E>를 상속했으므로 당연히 동일한 타입의 객체를 수집할 수 있고, 
메모리를 동적 할당할 수 있으며, 데이터의 추가, 변경, 삭제 등이 가능하다는
List<E>의 공통적인 특성을 모두 갖고 있을 것이다. 

또한 ArrayList<E>와 메서드 기능 및 사용법 또한 완벽히 동일

ArrayList<E> 와의 차의점은 바로 Vector<E>의 주요 메서드는 동기화 메서드로 구현돼 있으므로 
멀티 쓰레드에 적합하도록 설계돼있다는 것이다.

public synchronized E remove(int index){
	// ...
}

public synchronized E get(int index) {
	// ...
}

정리하면 Vector<E>는 ArrayList<E>와 동일한 기능을 수행하지만, 
멀티 쓰레드에서 사용할 수 있도록 기능이 추가된 것이다. 
물론 하나의 쓰레드로만 구성된 싱글 쓰레드에서도 사용할 수 있지만, 
싱글 쓰레드에서는 굳이 무겁고 많은 리소스를 차지하는 Vector<E>를 쓰는 대신 ArrayList<E>를 쓰는 것이 효율적.

🫧 LinkedList<E> 구현 클래스
List<E>의 모든 공통적인 특징(동질 타입 수집, 메모리 동적 할당, 데이터 추가/변경/삭제 메서드)을 지니고 있다. 
ArrayList<E> 처럼 메서드를 동기화하지 않았기 때문에 싱글 쓰레드에서 사용하기에 적합

- LinkedList<E>와 ArrayList<E> 차이
1. LinkedList<E>는 저장 용량을 매개변수로 갖는 생성자가 없기 때문에 
객체를 생성할 떄 저장 용량을 지정할 수 없다.

List<E> aLinkedList1 = new LinkedList<Integer>();

2. 내부적으로 데이터를 저장하는 방식이 서로 다르다는 것. 
말 그래도 모든 데이터가 서로 연결된 형태로 관리 되는 것

🫧 ArrayList<E>와 LinkedList<E>의 성능 비교
중간에 데이터를 추가할 때 속도 차이가 남. 
이와 마찬가지로 중간에 데이터를 삭제할 때도.

LinkedList에서는 각 원소가 자신의 인덱스 정보를 따로 갖고 있지 않다. 
특정 인덱스 위치의 값을 가져오기 위해서는 
앞에서부터 차례대로 번호를 세어가면서 인덱스의 위치를 찾아야 한다. 

반면 ArrayList는 데이터 자체가 인덱스 번호를 갖고 있으므로 
특정 인덱스 위치의 데이터를 빠르게 찾을 수 있음.

✅ 즉, 데이터를 추가 또는 삭제할 때는 LinkedList<E>의 속도가 빠르며, 
데이터를 검색할 때는 ArrayList<E>의 속도가 빠름

⭐ currentTimeMillis() 메서드와 nanoTime() 메서드
currentTimeMillis() 는 1970년 1월 1일 00시 00분과 현재 시간의 차이를 
ms(밀리초, 1/1000초) 단위로 리턴(long형)하는 메서드다. 

반면 System.nanoTime()은 현재 시간 정보와는 관계 없으며, 
상대적인 시간 차이를 나노초 단위로 구하는 데 사용되는 메서드다.

// 시간 측정 대상 모듈
long startTime = System.nanoTime();

// 측정 시간(ns) = endTime - startTime;
long endTime = System.nanoTime();
```
