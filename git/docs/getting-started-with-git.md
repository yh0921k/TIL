---

## Git 시작하기



### 설치 및 Version 확인

Ubuntu를 기준으로 `apt-get install git` 명령을 이용하면 Git을 설치할 수 있다.

버전을 확인하기 위해 `git --version` 명령을 이용할 수 있다.

---

### 최초 설정

Git을 설치하고 사용환경을 적절하게 설정해야 한다. `git config` 명령은 설정 내용을 확인하고 변경할 수 있다. Git은 아래의 세 가지 파일의 설정 내용에 따라 동작한다.

1. /etc/gitconfig
   - 시스템의 모든 저장소와 모든 사용자에게 적용되는 설정 파일
   - `git config --system` 명령으로 이 파일을 읽고 쓸 수 있다.

2. ~/.gitconfig, ~/.config/git/config
   - 현재 사용자와 해당 사용자가 사용하는 모든 저장소에 적용되는 설정 파일
   - `git config --global` 명령으로 이 파일을 읽고 쓸 수 있다. 

3. .git/config
   - git 디렉토리에 존재하며 현재 작업 중인 프로젝트에 적용되는 설정 파일
   - `--local` 옵션을 사용해 사용할 수 있다.

각 설정은 3 > 2> 1 순으로 우선순위가 높다.



#### 사용자 이름과 이메일 설정

Git을 설치하면 가장 먼저 해야하는 설정이다. Git은 commit을 할 때마다 이 정보를 사용하며, 한 번 커밋한 후에는 정보를 변경할 수 없다.

###### `git config --global user.name "User Name"`

###### `git config --global user.email "Email Address"`

위에서 말했다시피 `--global` 옵션으로 수행하는 설정은 한 버만 하면 된다. 만약 프로젝트마다 다른 이름과 이메일 주소를 사용하고 싶으면 `--global` 옵션을 빼고 명령을 실행한다.



#### 설정 확인

###### `git config --list`

Git은 설정 값을 여러 파일에서 읽기 때문에 같은 설정이 존재할 수 있다. 이 때 Git은 가장 나중 값을 사용한다. 

###### `git config <Key>` 

위의 명령으로 Git이 특정 Key에 대해 어떤 값을 사용하는지 확인할 수 있다.

---

