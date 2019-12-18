## Git 저장소 만들기(git init, git clone)

두 가지 방법으로 Git 저장소를 생성할 수 있다. 하나는 기존에 사용하던 프로젝트 디렉토리를 Git 저장소로 만드는 것이고, 다른 하나는 서버에 있는 저장소를 로컬로 복제하는 것이다.

---

#### 기존에 사용하던 디렉토리를 Git 저장소로 만들기

```bash
$ mkdir git_study
$ cd git_study
$ git init
```

- 위 명령을 실행하면 git_study 디렉토리에 .git이라는 하위 디렉토리가 생성된다.
- .git 디렉토리에는 프로젝트 저장소에 필요한 파일들이 들어 있다.
- Git은 현재 어떤 파일도 관리하지 않으며, 파일을 관리하게 하려면 저장소에 파일을 추가하거나 수정하고 commit해야 한다.

```bash
$ git add Hello.java
$ git add .gitignore
$ git commit -m "create project directory"
```

- `git add` 명령은 Stage Area(index)에 파일을 추가하고 `git commit` 명령은 Stage Area의 스냅샷을 찍어 로컬 저장소에 저장한다.
- 자세한 내용은 추후에 다룬다.

---

#### 기존 저장소를 복제하기

- 오픈소스(다른 프로젝트)에 참여해서 기여하거나 다른 저장소를 복제하고 싶을 때 `git clone`명령을 이용한다.
- 기존의 VCS와의 차이점은 원격 저장소(서버)에 있는 거의 모든 데이터를 복사한다는 점이다.
  - 서버의 저장소가 망가져도 클라이언트의 저장소를 이용해 복구할 수 있다.

```bash
$ git clone https://github.com/yh0921k/TIL.git
$ git clone https://github.com/yh0921k/TIL.git myTIL # 다른 디렉토리 이름으로 clone
```

위의 명령은 TIL이라는 디렉토리를 만들고 그 안에 .git 디렉토리를 만들며 저장소를 초기화한다. 또한 서버의 히스토리를 모두 가져와서 적용하므로 당장 작업을 시작할 수 있다.

---

