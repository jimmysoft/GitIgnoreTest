# GitIgnoreTest

>git 저장소에 commit 해버린 파일을 지우는 방법!

git 사용이 익숙치 않은 사람들은 일단 파일 관리에서 염려가 많을 것이다.

사실상 git은 코드 관리를 손쉽게 할 수 있도록 도와주는 도구라는 사실을 먼저 생각할 필요가 있다.

>해당 프로젝트 목적
이미 커밋해둔 파일이 있다. 사정이 생겨 해당 파일을 제거하고 싶다.
.gitignore에 해당 파일이나 해당 폴더를 추가하면 끝일 것 같지만 그렇지 않다.

2가지 작업을 모두 해줘야 한다.

.gitignore에 해당 파일을 추가해서 이후 commit 부터 해당 파일을 무시하도록 하고,
기존에 git이 바라보고 있는 파일 목록에서 해당 파일을 지워줘야 한다.

1. git rm --cached 파일명
2. .gitignore 파일에 /파일명 추가
3. 이후 커밋하고 푸시

이렇게 해주면 이후에 실수로 또 git add * 하더라도 .gitignore에 등록된 파일은 무시한다.

위 예제는 다음과 같이 진행했다.

1. 폴더 생성
2. git repository 생성
3. 해당 폴더 git init
4. 폴더내에 First.txt 파일 생성
5. 파일들 깃에 추가 git add *
6. 첫번째 커밋 git commit -m "First Commit"
7. 폴더와 remote 연결 git remote add origin 주소
8. 첫번째 푸시 git push origin master
9. 폴더내 Second.txt 파일 생성
10. 깃이그노어 생성 vi .gitignore 에 First.txt 추가
11. 파일들 깃에 추가 git add *
12. 두번째 커밋 git commit -m ".gitignore & Second Commit"
13. 두번째 푸시 git push origin master
--------------------------------------------------------
하지만 여전히 원격 저장소에 First.txt가 남아있다.

사실 한번에 처리하려면 이순서가 아니라
10. 이전에 14. 처리를 선행해주는게 좋다.

본 예시는 .gitignore만 가지고는 파일을 제거할 수 없다는 걸 알려주기 위한 구성이다.

14. 깃 캐시제거 git rm --cache First.txt
15. 세번째 커밋 git commit -m "untrack First.txt"
16. 세번째 푸시 git push origin master
-------------------------------------------------------
이제서야 원격 저장소에 Second.txt만 남아 있음을 알 수 있다.


>결론
.gitignore는 말그대로 git add * 처럼 파일을 추가하는 걸 방지해주는 기능이다.
파일이 이미 추가되어 있다면 직접 그 파일을 지워주는 작업이 별도로 수행되어야 한다.
