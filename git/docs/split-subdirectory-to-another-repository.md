## [Git] subtree를 이용해 프로젝트 분리하기

- 프로젝트가 커지면서 하위 디렉토리를 별도의 프로젝트로 분리해야하는 상황이 발생했다.
- subtree 명령을 이용하여 쉽게 작업을 진행할 수 있다.
- **분할된 각각의 프로젝트가 commit 내역을 유지하므로 Github에서 잔디를 유지할 수 있다.**

---

#### 예시) 아래의 경우는 필자가 실제로 직면한 상황이다.

###### 		Original_Project/

###### 						.git

###### 						SubDirectory01/

###### 						SubDirectory02/

###### 						docs/

- 대략적으로 위와 같은 상황이 발생했으며, SubDirectory02가 너무 커져서 다른 프로젝트로 분리해야하는 상황이다. 
- 명령을 이해하며 따라가면 손쉽게 아래와 같은 구조를 만들 수 있다.

---

### 결과

###### 		new_project_name01/

###### 						.git/

###### 						docs/

###### 						// 기존 폴더 내용 유지

###### 		new_project_name02/

###### 						.git

###### 						docs/

###### 						// 기존 폴더 내용 유지

> 

- 즉 SubDirectory01과 SubDirectory02가 하나의 프로젝트였지만, 각각의 프로젝트 디렉토리로 분리하고 필요한 파일들을 해당 프로젝트에 맞게 옮겨주는 작업이다. 
- 필요에 따라 Original_Project에 SubDirectory01을 남기고 SubDirectory02만 다른 프로젝트로 분리할 수 있다.

---

### 과정

```bash
# Original_Project/ 위치에서 아래의 명령을 수행한다.
# Original_Project의 경로는 /home/user/git/Original_Project 로 가정한다.
$ git subtree split -P SubDirectory02 -b copybranch
$ mkdir ../new_project_name02
$ cd ../new_project_name02
$ git init
$ git pull /home/user/git/Original_Project/ copybranch
$ git remote add origin https://github.com/user_id/new_project_name02
$ git remote -v
$ git push origin -u master
```

- user_id와 new_project_name은 본인에 맞게 입력한다. 
- 위의 작업 이후 commit 내역은 유지되면서 SubDirectory02가 다른 프로젝트 폴더로 분리됐음을 확인할 수 있다. 
- **또한 가장 중요한 잔디가 살아있음을 확인할 수 있다.**



- ##### SubDirectory01을 Original_Directory에 유지하고 싶다면** 아래와 같은 작업을 수행한다. 

```bash
# Original_Project/ 위치에서 아래의 명령을 수행한다.
# Original_Project의 경로는 /home/user/git/Original_Project 로 가정한다.
git rm -r SubDirectory02
git commit -m "split SubDirectory02 and remove SubDirectory02 in Original_Directory"
git branch -D copybranch
```



- SubDirectory01 또한 다른 프로젝트 디렉토리로 구성해야 하는 상황이라면 위의 작업 대신 SubDirectory02에 진행한 작업을 수행한 후 기존의 Original_Directory를 로컬과 원격 저장소에서 제거한다.

- ###### 단, 삭제하기 전에 docs/ 와 같은 추가적으로 옮겨줘야 할 파일이 있다면 신경쓰도록 한다.

---

