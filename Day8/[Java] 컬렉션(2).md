```
🫧 Set<E> 컬렉션의 특징
Set<E>는 동일한 타입의 묶음이라는 특징은 그대로 갖고 있지만, 
인덱스 정보를 포함하고 있지 않은, 즉 집합의 개념과 같은 컬렉션이다. 

✅ 즉, Set<E>는 데이터를 구분할 수 있는 유일한 방법이 데이터 그 자체인 것이며 
 따라서 동일한 데이터의 중복 저장을 허용하지 않는다.

🫧 Set<E>의 주요 메서드
- 데이터 추가
return type : boolean			method name : add(E element)
					매개면수로 입력된 원소를 리스트에 추가
								
	      boolean	 		method name : addAll(Collection<? Extends E> c)
					매개변수로 입력된 컬렉션 전체를 추가
- 데이터 삭제
return type : boolean			method name : remove(Object o)
					원소 중 매개변수 입력과 동일한 객체 삭제
								
		void			method name : clear()
					전체 원소 삭제					
-데이터 정보 추출
return type : boolean			method name : isEmpty()
					Set<E> 객체가 비어 있는지 여부를 리턴
								
		boolean			method name : contains(Object o)
					매개변수로 입력된 원소가 있는지 여부를 리턴
			
		int			method name : size()
					리스트 객체 내에 포함된 원소의 개수
								
		Iterator<E>		method name : iterator()
					Set<E> 객체 내의 데이터를 연속해 꺼내는 Iterator 객체 리턴
								
- Set<E> 객체 배열 반환
remove type : Object[]			method name : toArray()
					리스트를 Object배열로 변환
								
		T[]			method name : toArray(T[] t)
					입력매개변수로 전달한 타입의 배열로 전환

📝
contains(Object o)는 해당 Set<E> 매개변수로 넘어온 데이터가 
객체 내에 포함돼 있는지를 불리언 값으로 리턴. 

iterator() 메서드는 Iterator<E> 객체를 리턴하는데, 
이 객체는 Set<E> 객체에서 데이터를 1개씩 꺼내는 기능을 포함하고 있다.

Set<E>는 for문으로 인덱스 값을 바꿔가면서 데이터를 출력할 수 있었던 List<E>와 달리 
인덱스 정보를 가지고 있지 않아 일반적인 for문으로는 데이터를 꺼낼 수 없다.

이런 Set<E>의 모든 데이터를 1개씩 모두 꺼낼 수 있도록 하는 것이 
iterator() 메서드로 리턴되는 Iterator<E> 객체다. 
이 것이외에도 for-each 구문을 이용할 수 있다.

⭐ 인덱스 정보가 없는 Set<E>뿐 아니라 인덱스 정보를 갖고 있는 List<E>에도 
iterator() 메서드가 있지만, List<E>는 인덱스 정보를 바로 이용할 수 있기때문에 
굳이 Iterator<E>를 가져와 사용할 필요가 없음.

대표적인 Set<E> 인터페이스 구현 클래스로는 HashSet<E>, LinkedHashSet<E>, TreeSet<E> 가 있다.

🫧 HashSet<E> 구현 클래스

데이터 추가하기 - add()
HashSet<E>는 모든 데이터를 하나의 주머니에 넣어 관리하므로 입력 순서와 다르게 출력될 수 있다.

⭐ Set<E>의 모든 구현 클래스는 모든 항목을 출력하도록 toString()을 오버라이딩해 놓았기 때문에 
System.out.println() 메서드로 항목을 쉽게 확인할 수 있다.

데이터 삭제하기 - remove(), clear()

데이터 정보 추출하기 - isEmpty(), contains(), size(), iterator()

// isEmpty() hSet2 = []
System.out.println(hSet2.isEmpty())

// contains(Object o)
Set<String> hSet3 = new HashSet<String>();
hSet3.add("가");
hSet3.add("나");
hSet3.add("다");

System.out.println(hSet2.contains("나");  // true
System.out.println(hSet2.contains("라");  // false

// iterator()
Iterator<String> iterator = hSet3.iterator();
while(iterator.hasNext()){
	System.out.print(iterator.next() + " ");  // 가 다 나
}

📝
데이터가 비어 있는지의 여부는 isEmpty()로 알 수 있다. 
contains(Object o ) 메서드는 HashSet<E> 객체 안에 해당 원소가 있는지를 true/false로 리턴하고, 
size()는 저장된 데이터의 개수를 정수형으로 리턴.

iterator()는 Set<E> 객체 내부의 데이터를 1개씩 꺼내 처리하고자 할 때 사용하는 메서드.
iterator() 메서드를 호출하면 먼저 제네릭 클래스 타입인 Iterator<E>의 객체가 생성된다. 
여기서 제네릭 타입은 당연히 HashSet<E>가 저장하고 있는 원소의 타입이다. 
Iterator의 사전적 의미는 '반복한다.' 인데, 
모든 데이터를 담고 있는 것이 아니라 각각의 데티어의 위치를 번갈아가면서 가리킬 수 있다.

hasNext() : 다음으로 가리킬 원소의 존재 여부를 불리언으로 리턴
next() : 다음 원소 위치로 가서 읽은 값을 리턴

최초 Iterator<E> 객체가 생성되면 이 객체가 가리키고 있는 위치는 첫 원소 위치가 아닌 
첫 원소 바로 이전의 위칫값이라는 것이다. 
✅ 즉, 첫 번쨰 원소값을 읽으려면 iterator.next()를 실행해야 하며 for-each 구문으로 데이터를 꺼낼 수 있다.

for(String s : hSet3){
	System.out.print(s+" ");
}

배열로 반환 하기 - toArray(), toArray(T[] t)
toArray() 메서드는 HashSet<E> 내의 모든 원소를 담는 Object[]을 리턴. 
toArray(T[] t)는 특정 타입의 배열로 변환 하는 메서드로, 
HashSet<E>의 데이터 개수보다 작은 크기의 배열을 넘겨 주면 데이터의 개수만큼 확장된 배열을 리턴.

- HashSet<E>의 중복 확인 메커니즘
같은 데이터를 2개 이상 포함할 수 없다. 
여기서 중요한 것이 '데이터가 같다.' 또는 '데이터가 다르다'의 기준이다. 
먼저 객체의 해시코드는 객체가 저장된 번지와 연관된 값으로, 실제 번짓값은 아니다. 
✅ 즉, 객체가 저장된 번지를 기준으로 생성된 정수형 고유값이 바로 해시코드다.

1. hashcode() 동일한지 확인
2. equals() 결과 true 인지 확인

- 오버라이딩하지 않았을 때 객체의 hashcode(), toString()을 이용한 해시코드값 출력

class A extends Object {}
public class Test {
	public static void main(String[] args){
		A a = new A();
		System.out.printf("%x", a.hashCode());
		System.out.println(a.toString());
	}
}

- Object.hash() 메서드를 이용한 해시코드 생성
System.out.println(Object.hash(1, 2, 3,));

등가연산자(==)는 스택 메모리값을 동등 비교한다. 
그런데 기본 자료형과 참조 자료형은 스택 메모리에 각각 실제값과 위치값을 저장하고 있다. 
따라서 기본 자료형의 등가연산은 실제값, 참조 자료형의 등가연산은 위치값을 비교한다. 
Object의 equals() 메서드는 등가연산과 완벽하게 동일.

- Object 클래스의 equals() 메서드
public boolean equals(Object obj){
	return (this == obj);
}

⭐ HashMap<K, V>, HashTree<K, V> 등 과 같이 Hash가 포함된 모든 컬렉션은 
이와 같은 중복 확인 매커니즘으로 데이터의 저장 가능여부를 결정한다.

🫧 LinkedHashSet<E> 구현 클래스
LinkedHashSet<E>는 출력 순서가 항상 입력 순서와 동일한 특징을 갖고 있다. 
입력 순서의 정보를 갖고 있지만, 
List<E> 처럼 중간에 데이터를 추가하거나 특정 순서에 저장된 값을 가져오는 것은 불가능하다.

🫧 TreeSet<E> 구현 클래스
TreeSet<E>는 공통적인 Set<E>의 기능에 크기에 따른 정렬 및 검색 기능이 추가된 컬렉션이다. 
저장된 데이터를 출력할 때 HashSet<E>는 입력 순서와 다를 수 있고, 
LinkedHashSet<E>는 항상 입력 순서와 동일.

TreeSet<E>는 데이터를 입력 순서와 상관없이 크기순으로 출력한다. 
따라서 HashSet<E>에서는 단지 두 객체가 같은지, 
다른지를 비교했다면 TreeSet<E>에서는 두 객체의 크기를 비교해야 한다.

- Set<E>로 객체 타입을 선언할 때
Set<String> treeSet = new TreeSet<String>();
treeSet.example();  // Set<E> 메서드만 사용가능

- TreeSet<E>로 객체 타입을 선언할 때
TreeSet<String treeSet = new TreeSet<String>();
treeSet.example(); 	// Set<E> 메서드와 정렬/검색 기능 메서드도 사용 가능

📝 TreeSet<E>의 주요 메서드
- 데이터 검색
return type : E					method name : first()
					Set 원소 중 가장 작은 원소값 리턴
							
	: E					method name : last()
						Set 원소 중 가장 큰 원소값 리턴
							
	: E					method name : lower(E element)
						매개변수로 입력된 원소보다 작은, 가장 큰 수
							
	: E					method name : higher(E element)
						매개변수로 입력된 원소보다 큰, 가장 작은 수
							
	: E					method name : floor(E element)
						매개변수로 입력된 원소보다 같거나 작은 가장 큰수
			
	: E					method name : ceiling(E element)
						매개변수로 입력된 원소보다 같거나 큰 가장 작은 수
- 데이터 꺼내기
return type : E					method name : pollFirst()
						Set 원소들 중 가장 작은 원소값을 꺼내 리턴
							
	: E					method name : pollLast()
						Set 원소들 중 가장 큰 원소값을 꺼내 리턴

- 데이터 부분 집합 생성
return type : SortedSet<E>  	method name : headSet(E toElement)
				toElement 미만인 모든 원소로 구성된 Set을 리턴(toElement 미포함)
			
	: NavigableSet<E>	method name : headSet(E toElement, boolean inclusive)
				toElement 미만/이하인 모든 원소로 구성된 Set을 리턴
        (inclusive=true 이면 toElement 포함, inclusive=false 이면 toElement 미포함)
								
	: SortedSet<E>		method name : tailSet(E fromElement)
				toElement 이상인 모든 원소로 구성된 Set을 리턴
        (fromElement 포함)
								
	: NavigableSet<E>	method name : tailSet(E fromElement, boolean inclusive)
				fromElement 초과/이상인 모든 원소로 구성된 Set을 리턴
        (inclusive=true 이면 fromElement 포함, inclusive=false이면 fromElement 미포함)
			
	: SortedSet<E>		method name : subSet(E fromElement, boolean inclusive)
				fromElement 이상 toElement 미만인 원소들로 이뤄진 Set을 리턴
        (fromElement 포함, toElement 미포함)
								
	: NavigableSet<E>	method name : subSet(E fromElement, boolean inclusive, E toElement, boolean toinclusive)
				fromElement 초과/이상 toElement 미만/이하인 원소들로 이뤄진 Set을 리턴
        (fromclusive=true/false이면 fromElement 포함/미포함, toinclusive=true/false이면 toElement 포함/미포함)

- 데이터 정렬
return type : NavigableSet<E>	method name : descendingSet()
				내림차순의 의미가 아닌 현재 정렬 기준을 반대로 변환
								
📝 정리하면
first()와 last()는 각각 첫 번째 값과 마지막 값을 리턴
lower()는 입력 매개변수 원소보다 작으면서 가장 가까운 수를 말하고, higher()는 이와 반대.
floor(), ceiling()은 lower(), higher()와 비슷하지만, 값이 매개변수와 같을 때도 함께 고려.

pollFirst()와 pollLast()는 TreeSet<E>에서 각각 처음과 마지막 값을 꺼내 리턴. 
따라서 검색 메서드오와 달리 수행한 후 데이터의 개수가 줄어든다.

메서드의 매개변수에 따라 SortedSet<E> 또는 NavigableSet<E> 타입을 리턴. 
매서드에 매개변수 불리언 타입이 들어가지 않으면 SortedSet<E>를 리턴하고, 
불리언 타입이 들어가면 NavigableSet<E> 타입을 리턴한다고 생각하면 이해하기 쉬움.

headSet()은 입력매개변수보다 작은 원소로 구성된 Set<E>를 리턴하는데, 
불리언값을 이용해 입력매개변수값의 포함 여부를 설정 할 수 있으며 tailSet()은 이와 반대로 종작

subSet()은 전달 되는 2개의 원소값을 최소값과 최대값으로 하는 Set<E>을 구성하는 메서드로, 
불리언 값으로 시작과 끝 값의 포함 여부를 설정할 수 있다.

descendingSet()은 현재의 정렬 기준을 반대로 변환하는 메서드.

⭐ descending의 사전적인 의미가 내림차순이라고 해서 내림차순으로 정렬하는 것이 아님.

- TreeSet<E>에서 데이터 크기 비교
treeSet<E>에 저장되는 모든 객체는 크기 비교의 기준이 제공되야 하며 
크기 비교의 기준을 제공하는 방법은 2가지가 있으며 
첫 번째 방법은 Comparable<T> 제제릭 인터페이스르 구현하는 것이고, 
TreeSet<E> 객체를 생성하면서 생성자 매개변수로 Comparable<T> 객체를 제공하는 것이다.

1. Comparable<T> 인터페이스 구현
class MyComparableClass implements Comparable<MyComparableClass> {
	int data1;
	int data2;
	
	public MyComparableClass(int data1, int data2) {
		this.data1 = data1;
		this.data2 = data2;
	}
	
	@Override
	public int compareTo(MyComparableClass m) {
		if(data1 < m.data1) {
			return -1;
		} else if (data1 == m.data1) {
			return 0;
		} else {
			return 1;
		}
	}
}

2. TreeSet 생성자 매개변수로 Comparable<T> 인터페이스 객체 제공
TreeSet<MyClass> treeSet5 = new TreeSet<MyClass>(new Comparable<MyClass>(){
	@Override
	public int compare(MyClass o1, MyClass o2){
		if(o1.data1 < o2.data1){
			return -1;
		} else if(o1.data1 == o2.data1){
			return 0;
		} else {
			return 1;
		}
	}
});

MyClass myClass1 = new MyClass(2, 5);
MyClass myClass2 = new MyClass(3, 3);

treeSet5.add(myClass1);
treeSet5.add(myClass2);

for (MyClass mc : treeSet5) {
	System.out.println(mc.data1);
}
```
