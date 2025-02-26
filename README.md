# 항해 플러스 프론트엔드 4기 과제 10주차 <br/>: Chapter 4-2. 성능 최적화 (2)

[1. 개요](#1-개요)

[2. 프로젝트 배포](#2-프로젝트-배포)

[3. 초기 성능 측정](#3-초기-성능-측정)

[4. 성능 개선 방법 및 과정](#4-성능-개선-방법-및-과정)

[5. 성능 개선 결과 및 분석](#5-성능-개선-결과-및-분석)

## 1. 개요

- 지난 과제에서 인프라 구성 및 개선을 통해 실제로 인프라를 구축하고 배포를 해보며 인프라 레벨에서 웹 성능을 최적화하는 방법을 학습해보았습니다.
- 이번 과제에서는 프론트엔드 개발자가 주요 쓰는 기술 스택을 사용하여 코드 레벨에서 웹 성능을 최적화 하는 기법을 이해할 수 있습니다.
- 프론트엔드 성능 측정 도구를 통해 측정 항목을 알아보고, 측정 방법을 통해 코드 성능 개선 작업을 수행할 수 있습니다.
- 성능 개선 후 성능 보고서를 작성하여 개선된 결과를 수치화하여 분석 및 평가를 진행할 수 있습니다.
- 실무에서 CSS 또는 JavaScript를 최적화 하는 방법을 실제로 적용해 볼 수 있습니다.

## 2. 프로젝트 배포

![vercel 배포과정](https://github.com/user-attachments/assets/0b4393de-ba31-49c5-95a1-93f1acb6935d)

1. 로컬 환경에서 코드를 Github 저장소에 푸시합니다.
2. main 브랜치에 푸시되면, Github은 Vercel에 웹훅 알림을 보냅니다.
3. Vercel은 웹훅 알림을 감지해 main 브랜치에 최신 코드를 가져와 자동으로 빌드 및 배포 프로세스를 시작합니다.
4. Vercel은 해당 프로젝트의 설정에 맞는 의존성을 설치하고, 정적 파일을 생성합니다.
5. 빌드된 파일을 Vercel CDN 및 Edge Network에 배포하고, 프로젝트 배포 URL을 생성합니다.

🔗 링크: https://front-4th-chapter4-2-basic.vercel.app/

## 3. 초기 성능 측정

|측정 항목|lighthouse|core web vitals|
|------|---|---|
||![before-lighthouse](https://github.com/user-attachments/assets/886fed0d-002b-44aa-b198-ff4b6791e7f9)|![before-pageSpeed Insights](https://github.com/user-attachments/assets/9410a37b-00ad-48fa-bef6-11b363f27858)|
|성능 점수|🟧 60|🟧 67|
|FCP|🟧 2.4s|🟧 2.4s|
|LCP|🔺 4.9s|🔺 15.3s|
|TBT|🟢 20ms|🟢 150ms|
|CLS|🔺 0.42|🟢 0.018|
|Speed Index|🟢 2.4s|🟧 4.6s|

- FCP (First Contentful Paint)
  - 사용자가 페이지로 처음 이동한 시점부터 페이지 콘텐츠의 일부가 화면에 렌더링되는 시점까지의 시간을 측정
  - 목표: 1.8s
- LCP (Largest Contentful Paint)
  - 사용자가 페이지로 처음 이동한 시점을 기준으로 표시 영역에 표시되는 가장 큰 콘텐츠(이미지, 텍스트 블록 또는 동영상 등)의 렌더링 시간
  - 목표: 2.5s
- TBT (Total Blocking Time)
  - FCP 이후 입력 응답성을 방지하기에 충분한 시간 동안 기본 스레드가 차단되었던 총 지연 시간을 측정
  - 목표: 200ms
- CLS (Cumulative Layout Shift)
  - 페이지가 로드되는 동안 예기치 않은 레이아웃 변경에 대한 레이아웃 변경 점수 중 가장 큰 버스트를 측정하는 측정항목
  - 목표: 0.1 미만
- Speed Index
  - 페이지 로드 중에 콘텐츠가 시각적으로 표시되는 속도를 측정
  - 목표: 0.34s 미만
 
보시다시피 측정 도구에 따라 결과가 조금씩 다르지만, 전반적으로 FCP와 LCP 개선이 작업의 주요 목표가 될 것 같습니다. <br />
FCP와 LCP를 개선하기 위해 사용하지 않는 CSS 삭제, 서버 응답 시간 단축, 리소스 로드 지연 제거 등의 방향으로 서비스 성능을 개선해나갈 예정입니다.

## 4. 성능 개선 방법 및 과정

## 5. 성능 개선 결과 및 분석

|측정 항목|lighthouse|core web vitals|
|------|---|---|
||![after-lighthouse](https://github.com/user-attachments/assets/2057aa32-ffaf-402f-8863-439e015af7cc)|![after-pageSpeed Insights](https://github.com/user-attachments/assets/3ebfe0ee-719f-429f-ae0d-b5b1ec5c59c0)|
|성능 점수|🟧 88|🟢 97|
|FCP|🟧 2.1s|🟢 0.8s|
|LCP|🟧 3.7s|🟢 2s|
|TBT|🟢 10ms|🟢 170ms|
|CLS|🟢 0.01|🟢 0.001|
|Speed Index|🟢 2.1s|🟢 1.4s|
