# Vue-VideoSearch-App
## 메인 페이지
![메인 페이지](https://user-images.githubusercontent.com/94600999/160776935-53f9c1de-ad3b-43bf-99c1-f472ed232d6a.png)
## 핸드폰 화면
![핸드폰 화면](https://user-images.githubusercontent.com/94600999/160777331-dc19b65f-fca4-4da3-9847-06fb58c17d63.png)
- Demo [VideoFinder](https://fluffy-cocada-5de093.netlify.app)

# 목차
- 프로젝트 소개
- Vue를 선택한 이유
- 발생한 에러
- Api를 사용하면서 느낀점
- 문제점
- 마치며

# 1. 프로젝트 소개
## 1.1 프로젝트 목적
- Vue 공부하기 위함
- Api 활용하는 연습

## 1.2 사용한 라이브러리
- [reset.css](https://www.jsdelivr.com/package/npm/reset-css)
- [Font Awesome](https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.13.0/css/all.min.css)

## 1.3 사용한 Api
- [YTS.MX](https://yts.mx/api)    
Api를 고를 때 어떤 데이터를 들고올 수 있는지 다른 Api와 다른 점은 무엇인지를 비교했습니다.
네이버Api, OMDB.Api, YTS.Api를 비교해서 YTS.Api를 사용했습니다.   
YTS.Api를 선택한 이유는 인기순으로 데이터를 받아올 수 있기에 처음 페이지가 로딩되었을 때 인기순으로 비디오를 보여주기 위해서 YTS.Api를 선택했습니다.

# 2. Vue를 선택한 이유
## 1. React보다 쉬워 보임
아직 React를 제대로 다루어보지 않았지만 조사를 해보니 Vue가 더 쉽다는 느낌을 받았습니다. 처음에는 React를 공부해볼까 생각을 했는데 Vue가 더 쉬워보이고 Vue가 React와 비슷한 구조를 가지고 있다는 느낌을 받아 Vue 선택하게 되었습니다.

## 2. Right-way가 있음
React와 Vue를 비교해보니 React는 정말 선택지가 많다고 느꼈습니다.   
- React for문   
  - map
  - forEach
  - for in
  - for of

- Vue for 문
  - v-for

for문만해도 React는 정말 많은 선택지가 있고 개발자의 능력에 따라 차이가 속도가 더 빨라지지 않을까라는 생각이 듭니다.    
Vue를 배우는 입장에서 선택상황이 많은 거 보다 작은 것이 더 프레임워크에 대한 이해를 하기 쉬울 것이라고 생각이 됩니다.

# 3. 발생한 에러
## [Vue warn]: Extraneous non-emits event listeners...
- 발생 원인   
프로퍼티와 같이, 컴퍼넌트가 발행하는 이벤트는 emits옵션으로 정의할 수 있게 되었습니다.    

- 해결 방안
1. 위의 공식 문서처럼 emits를 설정
2. 문제있는 부분 div로 감싸기

※ 참고    
[Vue 공식 문서](https://v3.ja.vuejs.org/guide/migration/emits-option.html#_3-x-%E3%81%AE%E6%8C%99%E5%8B%95)   
[coding apple 커뮤니티](https://codingapple.com/forums/topic/emit-listener-%EA%B2%BD%EA%B3%A0/)

# 4. Api를 사용하면서 느낀점
검색 Api를 고르는 데에 어떤 Api가 있는 지 검색해보고 각각의 Api를 비교하면서 Api를 선택했지만 Api를 고르기 전에 어떤 데이터를 가져오고 제대로 값을 가져오는 지 내가 원하는 것을 구현할 수 있는 지에 대해 확인을 하고 골라야겠다는 느낌이 들었습니다.   
YTS를 활용하면서 2가지 문제가 발생했습니다.
## 1. 제대로 값을 가져오지 못함
YTS를 활용하여 최근에 업데이트 된 목록을 출력하는 기능을 만들고 싶었으나 홈페이지에 가서 출력을 해보니 값을 가져오지 못하는 상황이 발생하였습니다. 만약 실전에서 이런 상황이었다면... Api를 선택하기 전에 한 번 사용해보고 골라야겠다고 느꼈습니다.

## 2. 장르 검색 2개 이상 안됨
장르를 선택하여 그 장르에 대한 목록을 출력하는 기능을 만려고 했습니다. 원래는 다수의 장르를 선택해도 검색이 되는 것을 만들고 싶었습니다.    
하지만 2개 이상의 장르를 넣으면 WWE TLC Tables, Ladders & Chairs 이 영화가 나오는 것이 확인됬습니다. 그래서 장르 검색을 1개만 되는 걸로 제한을 걸었습니다.

# 5. 문제점
## 1. 이미지 로딩이 느림
[티비나누기](https://tvnng.com/), [JustWatch](https://www.justwatch.com/kr) 같은 플랫폼에 있는 영상 검색사이트가 더 많은 트래픽이 왔다갔다 할껀데 내가 만든 것보다 빨라서 어떻게하면 속도를 줄일 수 있을 지 찾아봐야겠다고 느꼈습니다.

# 6. 마치며
이번 프로젝트를 진행하면서 프로그램을 어떻게 만들지에 대해 더 신중하게 생각을 해야겠다는 생각이 들었습니다. 머리 속에서 이거는 만들어지겠지?라고 생각했던 것이 안되니 난감했습니다. 이런 경험을 하니 많은 생각이 들었습니다.    
기본기의 중요성도 많이 느꼈지만 프로그램을 어떻게 만들지부터 생각을 많이 해봐야겠다고 많이 느꼈습니다. 내가 원하는 기능을 구현을 할 수 있는지, 어떤 Api를 사용할 것인지 등등 **그냥 단순히 코딩을 하는 프로그래머가 되지 말자**는 생각이 들었습니다.    
정말 **프로같은 프로그래머가 될 수 있도록 더욱 노력**해야겠다고 느꼈습니다.
