# 상대 경로

상대경로(Relative path)란 현재 파일의 위치를 기준으로 다른 파일의 위치를 표시 하는 방법이다.

## 상대경로 기호

1. .: 현재 디렉토리
2. ..:현재 디렉토리의 상위 디렉토리를 나타낸다.
3. /(슬래시) : 디렉토리의 구분자 역할을 한다.

## 경로 파악하기

```md
src/
├── components/
│ └── Header/
│ └── Header.jsx
└── assets/
└── react_icon.png
```

react_icon.png 의 이미지를 Header.jsx에서 파일 참조하려면

1. ../: 현재 디겍토리(Header)의 한 단계로 이동(components/로 이동)
2. ../: 다시 한 단계 위로 이동(src/ 로 이동)
3. assets.react_icon.pns:src/ 안의 assets 디렉토리 내의 react-icon.png 파일

- 상대 경로는 현재 파일의 위치를 기준으로 다른 파일의 위치를 표현하는 방법이다.
- 프로젝트의 구조가 변경되어도 파일간의 상대적 위치만 유지된다면 경로를 수정할 필요가 없어 편리하다.

## 절대경로

절대경로(Absolute path)는 파일 시스템의 루트 디렉토리부터 전체 경로를 모두 표시하는 방법이다.
프로젝트 구조가 변경되면 경로도 함께 수정해야 한다.

```
C:\Users\John\Documents\project\src\components\Header\Header.jsx
```

## 정리

웹개발에서는 주로 상대 경로로 사용 하는 편이다.
