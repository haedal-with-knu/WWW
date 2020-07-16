# 파이참 설치 및 세팅

## 파이참 설치
[다운로드는 여기](https://www.jetbrains.com/ko-kr/pycharm/)

먼저 위의 Jetbrains 페이지에 접속하게 되면

![파이참메인](../statics/pycharm/pycharm_main.png)  
위와 같은 화면이 나오게 되는데, 여기서 화면 중간에 있는 다운로드 클릭

![파이참다운로드](../statics/pycharm/pycharm_download.png)  
우리는 프로페셔널하지 않기 때문에 Community 아래 검은 동그라미 다운로드 클릭

![다운로드를누르면](../statics/pycharm/pycharm_clicked_download.png)  
누르고 기다리면 다운로드가 시작된다.

![파이참설치세팅](../statics/pycharm/pycharmsetup1.png)
PATH만 추가해주면 된다.

## 파이참 세팅
### Git Bash와 command
#### Git Bash
![gitbash](../statics/pycharm/git_bash.PNG)
#### Windows command
![command](../statics/pycharm/command.png)

윈도우는 cmd를 사용하는데, git bash로 리눅스체제의 명령어를 윈도우에서도 사용할 수 있다.
따라서 mac이나 리눅스를 사용하는 사람은 따로 설치하지 않고 기존의 터미널을 사용해도 된다.

[다운로드는 여기](https://git-scm.com/) 에서!

중간에 다운로드 누르고 계속 진행진행 하면 된다. 모두 설치가 완료되었다면, 파이참을 열고 File-Settings-Tools-Terminal-Shell Path에 들어가주자.
거기에서 아래 사진과 같이 경로를 설정해주고, 파이참 화면에서 Terminal을 눌러주면 아래쪽의 터미널이 command에서 Git bash로 바뀌게 된다.

![GitBashSetting](../statics/pycharm/git_bash_setting.png)  

처음 파이참을 설치하고 터미널을 바꿔 줬으면, 본인의 깃헙 계정과 연동해야 한다. 계정이 없다면, 계정 생성부터 하고, 계정이 있다면, 파이참 터미널에서 다음과 같이 치면 된다.  
```
git config --global user.name 계정명
git config --global user.email 이메일명
```
이렇게 두개를 쳐 줘야 본인의 깃헙 계정과 연동이 되고, 자유롭게 레포를 클론해 와서 자신의 문서를 관리할 수 있다.

### 깃헙 사용법
크게 네 가지 정도만 알면 되는데,
```
git clone
git add .
git commit -m "할말"
git push
```
이렇게 네 가지를 앞으로 가장 많이 사용하게 될 것이다. `git clone`은 자신의 github repository와 똑같은 파일을 자기 로컬에 생성하는 것이고, 수정할 부분을 수정한 뒤에  
```
git add .
git commit -m "할말"
git push
```
이렇게 세 단계를 거쳐주면 본인의 github repository에 수정사항이 반영되게 된다.

### [돌아가기](../11st.md)

