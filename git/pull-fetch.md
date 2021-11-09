# Pull, Fetch

### **pull**

* 원격 저장소 (Remote Repository)로부터 최신의 파일 내용을 로컬 저장소에 **가져오고 병합(Merge)**한다. (git fetch + git merge)
* 브랜치의 최근 커밋 스냅샷을 가리키는 **HEAD **포인터가 '**origin/브랜치명**'을 가리킨다.

#### &#x20;

### **fetch**

* 원격 저장소 (Remote Repository)로부터 최신의 파일 내용을 로컬 저장소에 **가져오기만** 한다. (병합 X)
* 로컬 브랜치의 **HEAD** 포인터가 가리키는 곳은 변하지 않고, 원격 저장소에서 가져온 '**origin/브랜치명**'는 해당 브랜치의 최신 커밋을 가리킨다.
* '**git diff HEAD origin/브랜치명**' 명령어를 통해 로컬과 원격 저장소의 차이를 알 수 있다.
* '**git merge origin/브랜치명**' 명령어를 실행하면 **git pull**을 실행한 상태와 같아진다.\
