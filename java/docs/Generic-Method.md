## JAVA - 제너릭 메소드(Generic Method) 설명 및 예제

- 이 포스팅은 이미 제너릭을 학습했고, 제너릭 메소드의 개념이 모호하신 분들이 읽으시길 추천드립니다.

---

#### 제너릭 메소드

- 제너릭 메소드는 파라미터 타입과 반환 타입으로 타입 파라미터를 가지는 메소드를 말한다.

- 아래와 같이 메소드의 반환타입 앞에 "<T>" 형태로 명시한다.

  `public static <T> int add(T a, T b) { ... } `

- 해당 타입 파라미터는 메소드 내에서만 유효하다.
  - 제너릭 클래스에서 명시한 타입 파라미터와 메소드에서 명시한 타입 파라미터는 다르다.

---

이미 제너릭을 학습한 개발자라면 위의 내용을 이해하는데 무리가 없을 것이다. 본격적으로 예제로 살펴본다.

```java
public static void main(String[] args) {
    
    /* add1 */
    List<String> stringList = add1(new LinkedList<>(), "AAA");
    System.out.println(stringList);
    //List<Integer> integerList = add1(new LinkedList<>(), 123); // Error
    System.out.println("--------------------");
  }  
  private static List<String> add1(List<String> list, String element) {
    list.add(element); 
    return list;
  }
```

위와 같이 하나의 List와 문자열을 인자로 받아 리스트에 해당 문자열을 추가한 뒤 새로운 List를 반환하는 함수가 있다고 가정한다. 위 코드는 객체지향 프로그램에 적합하지 않는 코드이다. 만약 Integer 형태의 요소를 추가하고 싶다면 메소드를 오버로딩 해야하는가? 우린 조금전에 제너릭 메소드를 학습했다. 바로 적용해본다.

```java
public static void main(String[] args) {    
    /* add2 */
    List<String> stringList2 = add2(new LinkedList<>(), "AAA");
    System.out.println(stringList2);
    List<Integer> integerList2 = add2(new LinkedList<>(), 123); // Good
    System.out.println(integerList2);
    // LinkedList<Double> doubleList2 = add2(new LinkedList<>(), 3.1415); // Error    
    System.out.println("--------------------");
  }
  private static <T> List<T> add2(List<T> list, T element) {
    list.add(element);
    return list;
  }
```

제너릭 메소드의 형태로 바꾸고 모든 레퍼런스 타입이 사용 가능해졌다. 하지만 파라미터의 타입과 반환 타입이 List에 한정되어 있다. 예를들어, Collection의 형태로 파라미터를 전달할 수 없다. 

- 이 문제에서 Collection을 전달하고 싶다면? 
- 더하여 반환 타입을 Collection이 아니라 인자로 전달되는 타입(Collection의 하위 클래스가 될 수 있음)으로 지정하고 싶다면? 

제너릭 메소드의 작은 변형이 이를 가능하게 해준다.

```java
  public static void main(String[] args) {
    /* add3 */
    Collection<String> stringList3 = add3(new LinkedList<>(), "AAA");
    System.out.println(stringList3);
    //List<Integer> integerList3 = add3(new LinkedList<>(), 123); // Error
    System.out.println("--------------------");
  }
  private static <T> Collection<T> add3(Collection<T> list, T element) {
    list.add(element);
    return list;
  }
```

위 코드는 다형성을 이용해 Collection의 하위 클래스들을 파라미터로 전달 가능하게 만들었다. 하지만 이전 메소드인 add2에서 명시한 두 번째 요구사항을 충족하지 못했다. 즉, main 메소드에서 `List<String> stringList = add(new LinkedList<>(), "AAA")` 라는 명령을 수행할 경우 Collection 타입이 반환되기 때문에 에러가 발생하고, 이를 해결하기 위해 아래와 같이 명시적으로 형변환해야 한다.

- `List<String> stringList = (List<String>)add3(new LinkedList<>(), "AAA")`

위의 문제를 해결하기 위해 마지막으로 조금 복잡한 형태의 제너릭 메소드를 사용한다.

```java
    public static void main(String[] args) {
    /* add4 */
    Collection<String> stringList4 = add4(new LinkedList<>(), "AAA");
    System.out.println(stringList4);
    LinkedList<Integer> integerList4 = add4(new LinkedList<>(), 123);
    System.out.println(integerList4);
    List<Double> doubleList4 = add4(new ArrayList<>(), 3.1415);
    System.out.println(doubleList4);
  }
  private static <T, R extends Collection<T>> R add4(R collection, T element) {
    collection.add(element);
    return collection;
  }
```

최종적으로 위에서 발생한 문제들을 모두 해결한 형태가 add4 메소드이다. 이 메소드에서 타입 파라미터는 T, R이 사용되는데 T 타입의 인자를 강제했으므로 Collection에는 T 타입의 요소들만 사용 가능하다. 따라서 두 번째 인자로 전달되는 element의 타입과 충돌할 이유가 없다. 또한 나머지 타입 파라미터인 R을 보면 Collection 클래스로 상한 제한이므로 Collection을 포함한 하위 클래스에서만 사용 가능하다.

main 메소드의 예시들을 보면, add4의 결과로 Collection, LinkedList, ArrayList를 사용했을 때 문제가 없음을 확인할 수 있고 두 번째 인자로 넘어가는 element의 타입과도 충돌이 발생하지 않음을 확인할 수 있다.

---

