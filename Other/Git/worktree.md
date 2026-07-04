# Git Worktree(워크트리)란?
AI 에이전트를 병렬로 사용하다 보면 Git `worktree` 라는 기능을 자주 접하게 된다.

그동안 개발하면서 사용해본 적은 없었지만, 최근 AI 개발 워크플로우에서 자주 사용하게 되어 정리해본다.

워크트리는 **하나의 Git 저장소를 여러 작업 공간에서 동시에 사용**할 수 있는 기능이다.

> 쉽게 말하면 **하나의 프로젝트를 여러 폴더에서 동시에 작업**할 수 있게 해주는 기능이다.
## 왜 필요할까?
아래와 같은 상황을 한 번 생각해보자.

기능을 개발하고 있는데 갑자기 운영 서버에서 문제가 발생했다.

급하게 `main` 브랜치로 이동하려고 했더니 아래와 같은 메시지를 만났다.
```
Please commit or stash your changes before switching branches.
```
Git은 현재 브랜치에서 수정중인 내용이 다른 브랜치에 영향을 줄 수 있다고 판단하면 브랜치 변경을 막는다.

<img width="2720" height="2160" alt="branch_switch_friction_flow" src="https://github.com/user-attachments/assets/0905cf24-874e-4068-b35b-c96280b459f5" />

그래서 먼저 작업중인 내용을 `stash` 로 임시 보관하거나, 임시 커밋을 만든 뒤 브랜치를 변경해야 한다.

운영 서버 문제만 빠르게 수정하려고 해도 현재 작업을 잠시 정리해야하는 번거로움이 발생한다.

Git은 이런 불편함을 해결하기 위해 `worktree` 라는 기능을 만들었다.

## 워크트리는 어떻게 동작할까?
워크트리를 만들면 기존 프로젝트와 동일한 Git 저장소를 사용하는 새로운 작업 폴더가 생성된다.

각 작업 폴더는 서로 다른 브랜치를 사용할 수 있고, 작업 내용도 독립적으로 유지된다.

<img width="2720" height="1200" alt="worktree_tree_topdown" src="https://github.com/user-attachments/assets/22bf8410-ad71-4994-9ab8-e5c98dbf5332" />

즉, 브랜치를 계속 변경하는 것이 아니라 브랜치마다 작업 공간을 하나씩 가지는 방식이다.

## 실제로 어떻게 사용할 수 있을까?
기존 프로젝트에서 `feature/login` 브랜치를 위한 워크트리를 만들어보자.
```
git worktree add ../project-login feature/login
```

명령어를 실행하면 새로운 폴더가 생성된다.

```
project
project-login
```

<img width="1360" height="600" alt="finder" src="https://github.com/user-attachments/assets/3ecd6865-0590-4e94-b16b-7e33b81386b8" />

이제 `project`에서는 기존 작업을 그대로 이어가고, `project-login` 폴더에서는 `feature/login` 브랜치 작업을 바로 시작할 수 있다.

<img width="1360" height="640" alt="vscode" src="https://github.com/user-attachments/assets/2d2b4497-baa1-439f-825d-af0aac5b7845" />


그리고 브랜치를 변경하거나 `stash` 할 필요가 없다.

## 정리
워크트리는 브랜치를 여러 개 만드는 기능이 아니라, **브랜치마다 독립된 작업 공간을 만드는 기능**이다.

AI 에이전트를 여러 개 실행하거나 여러 기능을 동시에 개발할 때 기존보다 효율적으로 작업할 수 있다.
