# Movie Site Portfolio ✨

## 제작 기간

2022년 7월 27일 ~ 8월 14일

## 프로젝트 목표

JavaScript와 Vue.js 공부한 내용 복습 및 TMDB API를 활용하여 영화 소개 사이트 제작

## Skills

- HTML5
- CSS
- JavaScript
- Vue.js

## 프로젝트 URL

[movify](https://superb-entremet-0f24f9.netlify.app/)

![page](https://user-images.githubusercontent.com/82078896/184534702-52819ff5-fbfb-4276-b2c3-54b3af2ef744.png)

## 프로젝트 부분별 기능 소개

### 메인 페이지

- 검색기능

  - TMDB API 중 Search Movies를 이용해 원하는 키워드의 영화 목록을 불러왔습니다.

- 카운트 업 기능

  - TMDB API 중 Discover Movie를 이용해 영화 토탈 개수를 불러왔습니다.
  - RAF(RequestAnimationFrame)을 이용하여 기능을 구현했습니다.

- 최신 영화

  - TMDB API 중 Now Playing을 이용해 현재 개봉중인 영화 목록을 불러왔습니다.
  - vue-owl-carousel을 이용하여 슬라이드로 구현했습니다.
  - 영화 포스터, 제목, 평점, 장르, 영화 내용, 예고편 영상을 보여줍니다.
  - 상세보기를 클릭하면 영화 상세 페이지로 이동합니다.

- 개봉 예정인 영화
  - TMDB API 중 UpComing을 이용해 개봉 예정인 영화 목록을 불러왔습니다.
  - 새로 고침할 때마다 영화 목록이 바뀌도록 구현했습니다.
  - 영화 포스터, 예고편 영상, 제목, 개봉일자를 보여줍니다.
  - 영화 제목을 클릭하면 상세 페이지로 이동합니다.

### 영화 상세 페이지

해당 영화에 관련된 정보들을 소개해주는 페이지입니다.

- TMDB API 중 Movie Detail을 이용해 해당 영화에 대한 정보를 불러왔습니다.
- 포스터와 동영상은 모달로 창을 띄우도록 구현했습니다.
- 동영상과 다른 추천 영화는 vue-owl-carousel을 이용하여 슬라이드로 구현했습니다.
- 출연진을 클릭하면 해당 출연진 상세 페이지로 이동하며 더보기를 클릭하면 출연진 리스트 페이지로 이동합니다.

### 해당 영화 출연진 목록 페이지

영화에 출연한 배우의 목록을 보여주는 페이지입니다.

- TMDB API 중 Movie credits을 이용해 해당 영화 출연진 목록을 불러왔습니다.
- 배우 사진 또는 이름을 클릭하면 해당 배우의 상세 페이지로 이동합니다.
- 목록 나열을 list와 grid 두 가지 방법으로 구현했습니다.
- 한 페이지당 6개를 보여주며 6개가 넘을 경우 페이징 처리를 했습니다.

### 배우 상세 페이지

배우의 biography와 filmography를 보여주는 페이지입니다.

- TMDB API 중 credit을 이용해 해당 배우에 대한 정보를 불러왔습니다.

### 헤더

- 로고를 클릭하면 메인 페이지로 이동합니다.
- 영화메뉴 드롭다운 된 현재 상영중인 영화를 클릭하면 목록을 보여줍니다.
- 검색은 어느 페이지에서 하든 상관없이 해당 키워드에 대한 영화 목록을 보여줍니다.
- Login을 클릭하면 로그인 모달창을 보여줍니다.
