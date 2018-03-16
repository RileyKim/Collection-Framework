#Collection Framework
-----------------------

자료 구조를 바탕으로 객체들을 효율적으로 추가, 삭제, 검색할 수 있도록 java.util 패키지에 컬렉션과 관련된 인터페이스와 클래스들을 총칭한 것.

주요 인터페이스 : List, Set, Map

ArrayList, Vector, LinkedList는 List 인터페이스를 구현한 클래스.

HashSet, TreeSet은 Set 인터페이스를 구현한 클래스.

HashMap, Hashtable, TreeMap, Properties는 Map인터페이스를 구현한 클래스.

**List : 순서 유지하고 저장, 중복 저장 가능**

**Set : 순서 유지하지 않고 저장, 중복 저장 안됨**

**Map : 키와 값의 쌍으로 저장, 키는 중복 저장 안됨**


#List Collection
------------------

List Collection은 객체를 일렬로 늘어놓은 구조를 가지고 있다. 객체를 인덱스로 관히라기 때문에 객체를 저장하면 자동 인덱스가 부여되고 인덱스로 객체를 검색, 삭제할 수 있는 기능을 제공한다. 

**객체추가**

- Boolean add(E e)
- void add(int index, E element)
- set(int index, E element)

**객체 검색**

- boolean contains(Object o)
- E get(int index)
- isEmpty()
- int size()

**객체 삭제**

- Void clear()
- E remove(int index)
- Boolean remove(Object o)

```
// 예시

List<String> list = ...

List.add("김택수"); // 맨 끝에 객체 추가
List.add(1, "김택수1"); // 지정된 인덱스에 객체 삽입
String str = List.get(1); // 인덱스로 객체 찾기
List.remove(0); // 인덱스로 객체 삭제

```



##ArrayList

ArrayList : List 인터페이스의 구현 클래스 

Thread(동기화)를 지원하지 않는다.

**저장 용량을 초과한 객체들이 들어오면 자동적으로 저장 용량이 늘어난다!**

- ArrayList 생성

```
List<String> list = new ArrayList<String>();

```

기본 생성자로 생성하면 내부에 10개의 객체를 저장할 수 있는 초기 용량을 가진다.

ArrayList에서 특정 인덱스의 객체를 제거하면 바로 뒤 인덱스부터 마지막 인덱스까지 모두 앞으로 1씩 당겨진다. 마찬가지로 특정 인덱스에 객체를 삽입하면 해당 인덱스부터 마지막 인덱스까지 모두 1씩 밀려난다. 따라서 빈번한 객체 삭제와 삽입이 일어나는 곳에서는 ArrayList를 사용하는 것이 바람직하지 않다. 이런 경우라면 LinkedList를 사용하는 것이 좋다. 

##vector

Thread(동기화)를 지원한다.

ArrayList와 동일한 내부 구조를 가지고 있지만 Vector는 동기화된 메소드로 구성되어 있기 때문에 멀티스레드가 동시에 이 메소드를 실행할 수 없고 하나의 스레드가 완료해야만 다른 스레드를 실행할 수 있다. 따라서 **멀티 스레드 환경에서 안전하게 객체를 추가, 삭제할 수 있다.**

##LinkedList

LinkedList는 List 구현 클래스이므로 ArrayList와 사용 방법은 똑같지만 내부 구조는 다르다. **LinkedList는 인접 참조를 링크래서 체인처럼 관리한다. LinkedList에서 특정 인덱스의 객체를 제거하면 앞뒤 링크만 변경되고 나머지 링크는 변경되지않는다.**
그렇기 때문에 빈번한 객체 삭제와 삽입이 일어나는 곳에서는 LinkedList가 좋은 성능을 발휘한다. 

- 기본 생성자

```
List list = new LinkedList();
```

#Set Collection
--------------

Set Collection에는 HashSet, LinkedHashSet, TreeSet등 이 있는데 공통적으로 사용 가능한 Set 인터페이스의 메소드들이다. 인덱스로 관리하지 않기 때문에 인덱스를 매개값으로 갖는 메소드가 없다. 


**객체 추가**

- boolean add(E e)

**객체 검색**

- boolean contains(Object o)
- isEmpty()
- iterator<E> iterator()
- int size()

**객체 삭제**

- void clear()
- boolean remove(Object o)

###Iterator

반복자는 Iterator 인터페이스를 구현한 객체

iterator()를 호출하면 얻을 수 있다. 

```
//예시
Set<String> set = ...;
Iterator it = set.iterator();
```

###iterator 메소드

- hasNext() : 가져올 객체가 있으면 true를 리턴하고 없으면 false를 리턴한다.
- next() : Collection에서 하나의 객체를 가져온다.
- remove() : Set Collection에서 객체를 삭제한다.

```
//예시
Set set = ...;
Iterator it = set.iterator();

while(it.hasNext()){
	//String 객체 하나 가져옴
	String str = it.next();
	
	//Set Collection에서 삭제
	if(str.equals("홍길동"){
	it.remove();
	}
}
```

##HashSet

HashSet은 Set 인터페이스의 구현 클래스.

- 기본 생성자

```
Set<E> set = new HashSet<E>();
```

타입 파라미터 E에는 Collection에 저장할 객체 타입을 지정하면 된다.

HashSet은 객체들을 순서 없이 저장하고 동일한 객체는 중복 저장하지 않는다. 


```
//예시
//String 객체를 중복없이 저장하는 HashSet

public class HashsetExample{
	public static void main (String[] args){
		Set<String> set = new HashSet<String>();
		
		set.add("java");
		set.add("HTML");
		
		int size = set.size();
		System.out.println(size); //2
		
		Iterator<String> it = set.iterator();
		
		while(it.hasNext()){
			String str = it.Next();
			System.out.println(str);
		}
		
		set.remove("HTML")
		System.out.println(set.size) // 1
		
		set.clear();
		
	
	}
	
}
```





