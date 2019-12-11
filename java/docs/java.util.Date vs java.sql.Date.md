## java.util.Date vs java.sql.Date

- 자바에서 Date 클래스를 사용하다 보면 java.util의 Date와 java.sql의 Date, 두 가지를 확인할 수 있다.
- 이 글에서는 두 클래스의 차이를 확인한다.

---

### java.util.Date

- 1970년 1월 1일 00:00:00 GMT(Epoch Time 또는 POSIX Time) 이후의 특정 시점을 millisecond 단위로 나타낸다. 
  - 따라서 클래스 내부에 UTC(협정 세계시)에 대한 정보를 가지고 있다.
- 자바 11 기준 생성자는 아래와 같다.

```java
Date()
Date(long date)
Date(int year, int month, int date)
Date(int year, int month, int date, int hrs, int min)
Date(int year, int month, int date, int hrs, int min, int sec)
Date(String s)
```

- Date 클래스는 더이상 사용을 권고하지 않는다.
  - Date 클래스의 객체는 mutable이며, setTime(0) 등의 메소드로 내부 값을 변경할 수 있다.
    - Immutable 객체의 대한 장점은 이 글에서 다루지 않는다.
  - 또한 Date 클래스는 UTC를 사용하기 때문에 한계를 가진다. 
    - 시스템에 따라 UTC가 다를 수 있다.
- Java 8이 도입되면서 java.time 패키지의 사용이 권고된다.

---

### java.sql.Date

- java.sql.Date 클래스는 java.util.Date 클래스를 상속한다.
  - 해당 클래스의 사용 목적은 년도, 월, 일을 유지하는 SQL 데이터를 다루기 위함이다.
  - 즉, 시간 정보는 다루지 않고 0으로 초기화된다.

```java
Date(int year, int month, int day)
Date(long date)
```

- 해당 클래스는 데이터베이스를 다룰 때 사용되어야 한다.
  - 시간 정보를 유지하지 않으므로, 로컬 환경과 데이터베이스 간의 시간 변환은 JDBC 드라이버의 구현에 따라 다르다.
  - 마지막으로 SQL TIME, SQL TIMESTAMP와 같은 SQL의 데이터 타입을 처리하기 위해 java.sql의 Time 클래스 또는 Timestamp 클래스를 사용할 수 있다.

---

### Conclusion

- java.util.Date는 Epoch Time 이후 날짜, 시간 정보를 저장한다.
- java.sql.Date는 시간 정보가 없이 날짜 정보만 저장하며, JDBC에서 일반적으로 사용된다.
- 자바 8 이후에서는 java.util.Date의 사용을 권고하지 않는다.