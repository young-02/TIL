# package manager

패키지 매니저는 **소프트웨어 패키지(라이브러리,프라임워크 도구등)를 쉽게 설치 업데이트, 삭제 관리 할수 있도록 도와주는 도구**이다.

## 패키지 매니저가 필요한 경우

1. 손쉬운 패키지 설치

- `npm install react` 한 줄로 React 패키지를 설치할 수 있다.

2. 의존성 관리

- 프로젝트에서 사용하는 패키지들이 서로 의존하는 다른 패키지들도 자동으로 설치해 준다.

3. 업데이트 및 버전 관리

- 특정 버전을 고정하거나 최신 버전으로 업데이트할 수 있다. 4. 일관된 환경유니
  - package.json과 lock 파일(package-lock.json, yarn.lock)덕분에 팀원들과 동일한 환경을 유지 할 수 있다.

## 대표적인 패키지 매니저

| 패키지 매니저            | 특징                                                    |
| ------------------------ | ------------------------------------------------------- |
| npm                      | node.js의 기본 패키지 매니저                            |
| yarn                     | npm 보다 속도가 빠르고 안정적인 패키지 관리 기능 추가   |
| yarn berry(yarn v2 이상) | zero-install(설치 없이 실행)지원, 더 강력한 성능 제공   |
| pnpm                     | 중복 패키지를 최소화하여 더 빠르고 효율적인 패키지 관리 |

## 기본 명령어 예시(npm)

```bash
npm  init -y #프로젝트 초기화(package.json 생성)
npm install # package.json에 있는 모든 패키지 설치
npm install lodash # lodash 패키지 설치
npm uninstall lodash # lodash 패키지 삭제
npm update # 모든 패키지를 최신 버전으로 업데이트
npm list # 설치된 패키지 목록 확인
```
