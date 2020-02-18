## [Git] 여러 저장소를 단일 저장소로 병합하기(합치기)

- 따로 관리하던 프로젝트를 병합해야 하는 상황이 발생했다.
- **`git merge --allow-unrelated-histories`** 옵션을 통해 비교적 간단히 이 작업을 수행할 수 있다.
- 합쳐진 단일 프로젝트에서 기존의 다수 프로젝트의 commit history를 모두 유지할 수 있다.

---

#### 예시) 아래의 경우는 필자가 실제로 직면한 상황이다.		

```bash
Original-Project/
         .git/
         .gitignore
         README.md
         App.java
         
Original-Server/
		.git/
		.gitignore
		README.md
		ServerApp.java
		
Original-Client/
		.git/
		.gitignore
		README.md
		ClientApp.java
```

- 대략적으로 위와 같은 상황이 발생했으며, 하나의 저장소에 세 개의 프로젝트를 모두 병합해야 한다.
- 위의 상황에서 각 프로젝트는 git 프로젝트이며, 간략화 했지만 다수의 파일이 존재한다.
- 명령을 이해하며 따라가면 손쉽게 아래와 같은 구조를 만들 수 있다.

---

### 결과

```bash
Original-Project/
         .git/
         .gitignore
         Original-Project/
         			README.md
         			App.java
         			
         Original-server/
         			README.md
         			ServerApp.java
         			
         Original-Client/
         			README.md
         			ClientApp.java       

```

- 기존의 프로젝트와 서버, 클라이언트로 세 개의 저장소가 존재했고, 각 저장소는 git으로 관리되고 있었다.
- 이를 하나의 저장소에 합치며 단일 git 프로젝트로 만든다.

---

### 과정

```bash
# 먼저 각 프로젝트 폴더를 아래와 같이 구성한다.
# git과 관련된 파일 및 폴더를 제외하고 나머지 파일을 모두 현재의 프로젝트 폴더 이름과 동일한 폴더에 위치시킨다.
Original-Project/
         .git/
         .gitignore
         Original-Project/
         			README.md
         			App.java
         
Original-Server/
		.git/
		.gitignore
		Original-Server/
					README.md
					ServerApp.java
		
Original-Client/
		.git/
		.gitignore
		Origianl-Client/
					README.md
					ClientApp.java
```



```bash
# Original-Project의 경로는 /home/user/git/Original-Project 로 가정한다.
# 또한 Original-Server와 Original-Client의 위치는 Original-Project의 위치와 동일하다고 가정한다.
# Original-Project/ 위치에서 아래의 명령을 수행한다.

$ git remote add server ../Original-Server
$ git fetch server
$ git merge --allow-unrelated-histories server/master
$ git remote remove server
$ git add .
$ git commit -m "Merge server project into original-project"

$ git remote add client ../Original-Client
$ git fetch client
$ git merge --allow-unrelated-histories client/master
$ git remote remove client
$ git add .
$ git commit -m "Merge client project into original-project"

```

- 원격 저장소를 연결할 때 별칭이나 폴더명은 본인에 맞게 적절히 적용한다.

- **병합시에 `.gitignore` 파일이 충돌할 수 있다. **

  - 충돌은 파일을 열어 적절히 수정하고 commit하여 해결한다.

  

- commit history가 유지되는 것을 확인하고, 추가적으로 필요하다면 github에 새로운 remote repository를 만들어 push할 수 있다.

- **`--allow-unrelated-histories`** 옵션은 세 개의 프로젝트의 commit history의 조상이 같지 않기 때문에 사용한다.

  - 커밋 조상이 같지 않은 프로젝트를 병합하는 것을 허용하겠다는 의미이다.

---

