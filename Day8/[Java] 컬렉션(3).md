```
🫧 Map<K, V> 컬렉션 인터페이스
Map<K, V> 컬렉션은 상속 구조상 List<E>, Set<E>와 분리돼 있다. 
즉, List<E>와 Set<E>가 Collection<E> 인터페이스를 상속받는 반면, 
Map<K, V>는 별도의 인터페이스로 존재.

🫧 Map<K, V> 컬렉션의 특징
- Key와 Value 한 쌍으로 데이터를 저장
이때 한 쌍의 데이터를 '엔트리(entry)'라고 하며, 
Map.Entry 타입으로 정의. 즉, Map<K, V>는 데이터를 엔트리 단위로 입력

- Key는 중복 저장 불가, Value는 중복 가능
List<E>의 인덱스는 고정적인 반면, 
Map<K, V>의 Key 값으로는 무엇이든 올 수 있다. 
데이터를 구분하는 기준이 바로 이 Key 값이기 떄문에 
List<E>에서 인덱스가 중복되지 않았던 것처럼 Key 값도 중복될 수 없다. 
하지만 Value 값은 Key 값으로 구분해 가져올 수 있으므로 중복이 허용.

🫧 Map<K, V> 인터페이스 주요 메서드
- 데이터 추가 
return type : V					method name : put(K key, V value)
						입력매개변수의 (key, value)를 Map 객체에 추가
								
		: void				method name : putAll(Map<? extends K, ? extends V > m)
						입력 매개변수의 Map 객체를 통째로 추가

- 데이터 변경
return type : V					method name : replace(K key, V value)
						Key에 해당하는 값을 Value 값으로 변경(old 값 리턴)
					  	(단, 해당 Key가 없으면 null 리턴)
								
		: boolean			method name : replace(K key, V oldValue, V newValue)
						(key, oldValue)의 쌍을 갖는 엔트리에서 oldValue를 newValue로 변경
            					(단, 해당 엔트리가 없으면 false를 리턴)
								
- 데이터 정보 추출
return type : V					method name : get(Object key)
						매개변수의 Key 값에 해당하는 oldValue를 리턴
								
		: boolean			method name : containsKey(Object key)
						매개변수의 key 값이 포함돼 있는지 여부
								
		: boolean			method name : containsValue(Object value)
						매개변수의 Value 값이 포함돼 있는지 여부
								
		: Set<K>			method name : keySet()
						Map 데이터들 중 Key들만 뽑아 Set 객체로 리턴
									
		: Set<Entry<K, V>>  method name : keySet()
						Map의 각 엔트리들을 Set 객체로 담아 리턴
								
		: int 				method name : size()
						Map에 포함된 엔트리의 개수
								
- 데이터 삭제
return type : V					method name : remove(Object key)
						입력매개변수의 Key를 갖는 엔트리 삭제
              					(단, 해당 Key가 없으면 아무런 동작을 하지 않음)
								
			: boolean			method name : remove(Object key, Object value)
						입력매개변수의 (key, value)를 갖는 엔트리 삭제
              					(단, 해당 엔트리가 없으면 아무런 동작을 하지 않음)
								
			: void				method name : clear()
						Map 객체 내의 모든 데이터 삭제

📝 정리하면
데이터를 추가할 때는 put(K key, V value)와 같이 (Key, Value)의 쌍으로 전달하며,
putAll()을 이용해 다른 Map<K, V> 객체를 통째로 추가할 수도 있다. 

데이터를 변경할 때는 replace() 메서드를 사용하며, 
해당 엔트리(Key와 Value의 쌍)가 없을 때는 매개변수에 따라 null 또는 false를 리턴 한다.

데이터의 값을 꺼낼 때는 다른 컬렉션처럼 get() 메서드를 사용하며, 
매개변수로는 Key 값을 사용한다. 
즉, 해당 Key 값을 갖는 Value 값이 리턴된다. 
containKey()와 containValue()는 각각 매개변수로 들어오는 Key와 Value의 객체가 
Map<K, V> 객체 내에 존재하는지를 불리언으로 리턴한다. 
KeySet()은 Map<K, V> 데이터 쌍들 중에서 Key만을 뽑아 Set<E>로 리턴한다.

Map 데이터를 1개씩 꺼낼 때 일반적으로 이 KeySet()로 전체 Key를 추출하고, 
각 Key 값에 따라 Value 값을 읽는다. 
Key의 집합이 아니라 엔트리를 Set<Entry<K, V>>로 바로 가져올 수도 있는데, 
이때 사용하는 메서드가 entrySet()이다. 

전체 엔트리의 개수는 size()로 구할 수 있다.

데이터를 삭제할 때는 remove() 메서드를 사용하는데, 
매개변수로 Key만 넘길 떄는 해당 Key와 Value를 함께 매개변수로 전달하면, 
Key와 Value가 정확히 일치하는 엔트리가 있을 때만 데이터의 삭제가 이뤄진다. 
claer()는 Map<K, V> 객체의 전체 엔트리를 삭제하는 메서드다.

Map<K, V> 역시 인터페이스이기 때문에 객체를 생성하기 위해서는 
하위 클래스에서 위의 모든 메서드를 구현해야 하며 대표적인 구현 클래스로는 
HashMap<K, V>, LinkedHashMap<K, V>, Hashtable<K, V>, TreeMap<K, V>를 들 수 있다.

⭐ HashMap<K, V>와 Hashtable<K, V>는 Key 값을 HashSet<E>로 관리하고, 
LinkedHashMap<K, V>와 TreeMap<K, V>는 Key 값을 각각 LinkedHashSet<E> 및 TreeSet<E>로 관리한다.

🫧 HashMap<K, V>
HashMap<K, V>는 Map<K, V>의 대표적인 구현 클래스로, key 값의 중복을 허용하지 않는다. 
Key 값의 중복 여부를 확인하는 메커니즘은 HashSet<E> 때와 완벽히 동일.

🫧 Hashtable<K, V>
HashMap<K, V> 구현 클래스가 단일 쓰레드에 적합한 반면, 
Hashtable은 멀티 쓰레드에 안정성을 가진다. 이는 
ArrayList<E>가 단일 쓰레드에 적합한 반면, 
Vector<E> 클래스가 멀티 쓰레드에 안전하도록 설계한 것과 비슷한 관계.

🫧 LinkedHashMap<K, V>
LinkedHashMap<K, V>는 HashMap<K, V>의 기본적인 특성에 
입력 데이터의 순서 정보를 추가로 갖고 있는 컬렉션이다. 
따라서 저장 데이터를 출력하면 항상 입력된 순서대로 출력.

🫧 TreeMap<K, V>
TreeMap<K, V>는 Map<K, V>의 기본 기능에 정렬 및 검색 기능이 추가된 컬렉션으로, 
입력 순서와 관계없이 데이터를 Key 값의 크기 순으로 저장. 
따라서 반드시 Key 객체는 크기 비교의 기준을 갖고 있어야 한다.
또한, TreeMap<K, V>로 선언해야 SortedMap<K, V>와 
NavigableMap<K, V>에서 추가된 정렬 및 추가 메서드를 호출할 수 있다.

- Map<K, V>로 객체 타입을 선언할 때
Map<Integer, String> treeMap = TreeMap<Integer, String>();
treeMap.example();	// Map<K, V> 메서드만 사용 가능

- TreeMap<K, V>로 객체 타입을 선언할 때
TreeMap<Integer, String> treeMap = new TreeMap<Integer, String>();
treeMap.example();	// Map<K, V> 메서드와 추가된 정렬/검색 메서드 사용 가능

📝 Tree<K, V>의 주요 메서드
데이터의 검색은 firstKey()와 firestEntry()는 각각 첫 번째 검색 데이터의 Key 값과 엔트리를 가져온다. 
모든 데이터가 Key 값의 오름차순으로 저장돼 있으므로 
리턴되는 첫 번째 값은 가장 작은 key 값을 갖는 엔트리를 의미하며 
엔트리는 Map의 이너 인터페이스로 정의돼 있으므로 Map.Entry<K, V>와 같이 타입을 표현.

lastKey()와 lastEntry()는 반대 역할 수행.

lowerKey()와 lowerEntry()는 각각 입력된 매개변수보다 작은 가장 인접한 값을 의미하고, 
higherKey()와 higherEntry()는 반대 역할 수행.

pollFirstEntry()와 pollLastEntry()는 각각 가장 작은 Key 값의 엔트리와 
가장 큰 Key 값의 엔트리를 꺼내오는 메서드로, 
실제 TreeMap<K, V> 객체에서 데이터를 꺼내기 때문에 데이터의 개수는 꺼낸 만큼 줄어든다.

TreeMap<K, V> 객체 내에 저장된 데이터의 일부분을 가져와 
새로운 Map<K, V> 객체를 구성할 수도 있는데, 이는 TreeSet<E>와 비슷함 

매개변수에 불리언이 포함되지 않을 때는 SortedMap<K, V> 타입을 리턴하고, 
불리언이 포함될 때는 NavigableMap<K, V> 타입을 리턴.

데이터의 정렬에 관한 메서드인 descendingKeySet()은 
Map에 포함된 모든 Key 값의 정렬 순서를 반대로 변환한 NavigableSet<E> 객체를 리넡하는 메서드다. 
이와 비슷하게 descendingMap()은 현재의 TreeMap<K, V>에 포함된 모든 Key 값의 정렬을 반대로 변환한 
NavigableMap<K, V> 객체를 리턴.

- TreeMap<K, V>의 객체 생성 및 데이터 추가와 출력
TreeMap<Integer, String> treeMap = new TreeMap<Integer, String>();
for(int i=20; i>0; i-=2){
	treeMap.put(i, i+" 번째 데이터 ");
}
System.out.println(treeMap.toString());


🫧 Stack<E> 컬렉션의 특징
Stack<E> 컬렉션은 5개의 컬렉션 중 유일하게 클래스다. 
즉, 자체적으로 객체를 생성할 수 있다. 
상속 구조를 살펴보면 List<E> 컬렉션의 구현 클래스인 Vector<E> 클래스의 자식 클래스로 
후입선출(LIFO) 자료구조를 구현한 컬렉션이다.

⭐ 스택 메모리 영역도 데이터를 LIFO 방식으로 입출력한다.

🫧 Stack<E>의 주요메서드
Stack<E>에 추가하는 push(), 위에서부터 데이터를 꺼내는 pop(), 가장 위의 데이터를 읽는 peek(), 
현재 데이터의 위치값(맨 위의 값이 1, 아래로 갈수록 1씩 증가, 
해당 데이터가 없을 때 -1을 리턴)을 리턴하는 search(), 
마지막으로 Stack<E> 객체의 데이터가 비어 있는지를 알아보는 empty()가 있다.

🫧 Queue<E> 컬렉션의 특징
LinkedList<E>가 Queue<E> 인터페이스의 구현 클래스이다.
Queue<E>의 가장 큰 특징은 Stack<E>의 LIFO와 반대되는 개념인 
선입선출(FIFO : first in first out) 구조를 가진다는 것이다. 
즉, 먼저 지정된 데이터가 먼저 출력.

출력 데이터를 확인하기 위해서는 add(), remove(), element() 
메서드나 offer(), poll(), peek() 메서드를 사용할 수 있다.

🫧 Queue<E>의 주요 메서드
⭐ 사실 기본값이라고 해 봐야 데이터가 없을 때 null을 리넡하는 것이 전부다. 
하지만 적절한 예외 처리 없이 예외가 발생하면 프로그램이 강제 종료되기 
때문에 예외 발생 여부는 매우 중요한 차이를 가진다.

6개의 메서드 중 add() 메서드만 컬렉션 인터페이스에 정의돼 있고, 
나머지는 모두 큐 인터페이스에 정의돼 있다.

예외 처리 기능이 포함되지 않은 메서드셋에는 데이터를 추가하는 add(), 
데이터를 꺼내는 remove(), 가장 상위(다음 출력 대상)의 요소 값을 읽는 element() 메서드가 있다.

각각의 동일한 기능을 수행하면서 예외 처리기능이 초함된 메서드셋에는 데이터를 추가하는 offer(), 
데이터를 꺼내는 poll(), 가상 상위의 요소 값을 읽는 peek()가 있다. 

⭐ 실제 자바 API 문서에서 peek()와 poll() 메서드의 정의를 확인해 보면, 
예외 처리를 하는 대신 if 조건문을 사용해 데이터가 없을 때 null을 리턴하도록 작성돼 있다.

- Queue<E> 컬렉션의 주요 메서드 활용 방법
public static void main(String[] args) {
        // 1. 예외 처리 기능 미포함 메서드
        Queue<Integer> queue1 = new LinkedList<>();

        // System.out.println(queue1.element()); NoSuchElementException
        queue1.add(3);
        queue1.add(4);
        queue1.add(5);

        System.out.println(queue1.element());

        System.out.println(queue1.remove());
        System.out.println(queue1.remove());
        System.out.println(queue1.remove());
        //System.out.println(queue1.remove()); NoSuchElementException

        // 2. 예외 처리 기능 포함 메서드
        Queue<Integer> queue2 = new LinkedList<>();
        System.out.println(queue1.peek());

        queue2.offer(3);
        queue2.offer(4);
        queue2.offer(5);

        System.out.println(queue2.peek());

        System.out.println(queue2.poll());
        System.out.println(queue2.poll());
        System.out.println(queue2.poll());
        System.out.println(queue2.poll());
    }

```
