## Git의 세 가지 상태



##### Git은 파일을 Committed, Modified, Staged의 세 가지 상태로 관리한다.

- Committed란 데이터가 로컬 데이터베이스에 안전하게 저장됐음을 의미한다.
- Modified는 수정한 파일을 아직 로컬 데이터베이스에 commit하지 않은 상태를 말한다.
- Staged란 현재 수정한 파일을 곧 commit할 것이라고 표시한 상태를 의미한다.

---

위의 세 가지 상태는 Git 프로젝트의 세 가지 단계와 연결된다. 

- Git 디렉토리,  워킹 트리, Staging Area를 이해해야 한다.

![ThreeStatusOfGit](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbeCcS8%2FbtqAyyU72Wi%2FfbeZoxZ6t5IRsJAY0lCWu1%2Fimg.jpg)

##### Git 디렉토리는 Git이 프로젝트의 메타데이터와 객체 데이터베이스를 저장하는 곳을 말한다.

- .git 디렉토리가 Git의 핵심이다.
- 다른 컴퓨터에 있는 저장소를 복제할 때 해당 디렉토리가 만들어진다.

##### 워킹 트리는 프로젝트의 특정 버전을 Checkout 한 것이다.

- Git 디렉토리는 지금 작업하는 디스크에 있고 디렉토리 안에 압축된 데이터베이스에서 파일을 가져와서 워킹 트리를 만든다.

##### Staging Area는 Git 디렉토리에 있다.

- 단순한 파일이며, 곧 commit할 파일에 대한 정보를 저장한다.
- "index"라는 이름으로 불리기도 하지만 Staging Area라는 명칭이 표준이 되어가고 있다.

---

##### Git에서 하는 일은 기본적으로 아래와 같다.

1. 워킹 트리에서 파일을 수정한다.
2. Staging Area에서 파일을 Stage 해서 commit할 스냅샷을 만든다.
3. Staging Area에 있는 파일들을 commit해서 Git 디렉토리에 영구적인 스냅샷으로 저장한다.

즉, Git 디렉토리에 있는 파일들은 Committed 상태이다. 파일을 수정하고 Staging Area에 추가했다면 Staged이다. 그리고 Checkout 하고 나서 수정했지만, 아직 Staging Area에 추가하지 않았다면 Modified 이다.

---

