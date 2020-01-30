# Git Command

---

### 설정

##### 사용자 이름과 이메일 설정

- git config --global user.name "UserName" 
- git config --global user.email "UserEmail"



##### 텍스트 편집기 설정

- git config --global core.editor vim



##### Line Ending 설정

- git config --global core.autocrlf [ true | input | false ]
  - windows 에서는 true로 설정하고 linux, mac, unix에서는 input을 사용한다.

---

### Local Repository를 위한 Git Command

- git init
  - git 저장소 초기화



- git add [ filename | . | * ]
  - untracked 파일을 tracked로 만들거나 unstaged 파일을 staged로 만들 때 사용
  - 즉, 추적하지 않은 파일을 추적하거나 수정된 파일을 commit하기 위해 staging area에 등록하는데 사용하는 명령어



- git commit 
  - staged 상태의 내역을 최종적으로 저장소에 반영하는 명령
  - -a 옵션은 add를 동시에 수행하며, -m 옵션은 간단한 commit 메시지 작성을 위해 사용한다.



- git commit --amend
  - git status가 clean한 상태에서 최신 커밋(마지막 커밋) 내용을 수정한다.
    - 부가적으로 설명하면, 마지막 커밋 내용을 수정하는 것이 아니라 새로운 커밋으로 대체하는 것이다.
    - 커밋의 체크섬 값이 변한다.
  - 이미 remote repository에 push한 경우 주의해서 사용한다.



- git status
  - 현재 저장소의 상태 확인을 위한 명령
  - 추적되지 않은 파일이 있거나 변경되었는데 commit되지 않은 내역 등을 알려준다.



- git branch
  - 해당 명령 자체로는 어떠한 branch가 존재하는지 확인할 수 있다.
  - -a 옵션 또는 -r 옵션을 이용하여 원격 저장소의 연결된 브랜치를 확인할 수 있다.



- git branch [ BranchName ]
  - 해당 브랜치를 생성한다.



- git checkout [ BranchName ]
  - 해당 브랜치로 체크아웃한다.
  - -b 옵션을 통해 브랜치를 생성하면서 동시에 체크아웃할 수 있다.



- git merge [ BranchName ]
  - 현재 작업중인 branch에 명시한 branch를 병합한다.



- git log
  - -5와 같이 옵션을 사용해 해당 개수 만큼 로그를 확인할 수 있다.

---

### Remote Repository를 위한 Git Command

- git clone https://github.com/user-name/repository-name.git
  - 위의 형태로 원격 저장소의 내용을 로컬 저장소로 가져올 수 있다.
  - clone한 저장소의 별칭은 따로 명시하지 않으면 origin으로 지어진다.



- git remote add origin https://github.com/user-name/repository-name.git
  - 원격 저장소와 로컬 저장소를 연결한다.
  - 위의 경우는 origin이라는 별칭으로 현재 로컬 저장소와 링크로 명시한 원격 저장소를 연결한다.



- git remote -v
  - 원격 저장소와의 연결을 확인할 수 있다.



- git push
  - 기본적으로 commit을 원격 저장소의 master branch에 업로드한다.
  - 또한, 다양한 옵션을 통해 특정 branch를 가져오거나 업로드할 수 있으며 tag를 업로드할 수 있다.



- git push origin [ --all | BranchName ]
  - 현재 로컬 저장소의 모든 branch를 별칭에 해당하는 원격 저장소에 업로드한다.
  - 만약 원격 저장소에 로컬 저장소에서 업로드하는 이름의 branch가 없다면 새로 생성한다.



- git pull & git fetch
  - 원격 저장소의 정보를 가져와 로컬 branch에 merge까지 수행한다.
  - 즉, fetch + merge의 형태이다.
  - pull을 사용하면 병합되면서 변경된 프로젝트의 세세한 부분을 파악할 수 없다.
  - 따라서 팀 프로젝트에서 권고되지 않으며, fetch를 이용해 원격 저장소의 커밋을 가져오고 로컬 저장소에서는 이를 수동으로 merge 하는 방법이 권고된다.

---

### 기타 명령어

- git tag [태그 내용] [commit checksum]
  - 특정 커밋을 참조하는 태그를 붙인다.
  - 간단하게 이름만 붙이는 light weight tag와 보다 많은 정보 전달을 위한 annotated tag가 있다.
  - 보통 배포 버전을 명시하는데 활용된다.

- git tag -l
  - 현재 저장소에 존재하는 태그의 리스트를 출력한다.

- git show-ref --tags
  - 태그와 함께 태그가 붙은 commit의 체크섬 값을 같이 출력한다.

- git tag -a [태그 내용] [commit checksum]
  - annotated 태그를 붙인다.
  - 해당 명령을 수행하면 에디터가 실행된다.
    - 보통 언제, 누가, 왜 이 태그를 붙였는지 입력한다.

- git show [tag]
  - 태그를 확인한다.

- git push [remote repository] [branch] --tags
  - 로컬의 특정 branch의 모든 태그를 명시한 별칭의 원격 저장소에 push
  - oriigin master가 기본값

---

