# mangoPlate_test_Server_Mango

## 2021.08.14
- 망고플레이트 기획서 작성(개발범위, 우선순위, 1주차 계획 등)
- aws를 이용한 서버 구축(dev, prod)

## 2021.08.15
- dev, prod에 ssl 적용
- dev에 템플릿 적용
* erd 설계 90% 완료
  * https://aquerytool.com/aquerymain/index/?rurl=fdd39719-b384-4641-aa57-9ce097b2527f (비밀번호 : 4488t8)
  * 추가로 만들어야할 테이블 
    1. Top 리스트   
    2. Top 리스트 북마크   
    3. 리뷰 댓글의 답글    
  * issue:  
    1. 지역 필터링 -> 지역테이블을 따로 만들어서 가게가 지역테이블을 참조하도록 하는게 맞나?   
    2. 식당상세정보 구성이 가게마다 다 다름 -> 상세정보 테이블 따로 -> 식당테이블에 넣을지 상세정보 테이블에 넣을지 기준을 어떻게? (일단 필터링 기능이 필요한 것은 식당테이블에 넣음)   
    3. 메뉴 사진은 리뷰에서 끌고 오는구조 -> 사진을 몇개 넣을 수 있는건지 모르겠음(일단 별로 없을거같아서 메뉴 테이블에 세개만 구현) -> 많으면 이미지 테이블 따로 뺄 예정   
    4. 알림은 어떻게 구현? n:n or 1:n ?

## 2021.08.16
- rds 구축
- erd 수정
- 회원가입/로그인 api 구현(회원가입할 때 이메일 인증 api 추가해야함)

## 2021.08.17
- 서버 수정
- 회원가입/로그인 api URI, validation 수정
- 카카오로그인, 지역별 가게조회, 특정가게 조회(+조회수 올리기) API 구현
- 1차 피드백
  - 리뷰댓글의 대댓글 erd로 구현하는법 : 리뷰댓글 테이블에 parentsId컬럼을 넣어서 리뷰댓글 id참조
  - 이미지 데이터 넣는 법 : aws s3사용
  - 알람은 나중에 구현

## 2021.08.18
- erd 수정
  - RestaurantMenu, DetailInformation 테이블 name, price등 없애고 RestaurantInformation테이블로 합침, content를 html로 받음, informationType으로 메뉴정보인지 편의정보인지 구분
  - 식당 메뉴에 보이는 사진을 위해 ReviewImage에 isMenu컬럼추가 ->isMenu가 1이면 식당메뉴 이미지에 나타나도록
- API 구현
  - 특정 가게 전체 사진 보기 API
  - 가게 메뉴 조회 API

## 2021.08.19
- API 구현
  - 전체리뷰조회(소식탭) API
  - 전체 리뷰조회(소식-팔로잉탭)
  - 이벤트 조회 API
  - 특정 리뷰 조회 API
  - 가게 리뷰 조회 API
  - 가게 편의정보 조회 API
  
- API 수정
  - 클라이언트 요청에 따라 변수명 모두 영어로 변경, id나 조건걸어야하는 변수를 제외한 int자료형 모두 string자료형으로 변경

## 2021.08.20
- API 구현
  - 리뷰 댓글 보기 API
  - 리뷰 댓글 달기 API
  - 랜덤 유저 조회 API
  - 팔로잉 목록 조회 API
  - 팔로워 목록 조회 API
  - EAT딜 목록 조회 API
- API 수정
  - 클라이언트 요청에 따라 지역, 거리 합쳐줌, 조회수 정보 추가

## 2021.08.21
- API 구현
  - 특정 EAT딜 조회 API
  - 리뷰 댓글 언급 유저 목록 조회 API
  - 회원 정보 수정(이름) API
  - 회원 정보 수정(이메일) API
  - 회원 탈퇴 API
- API 수정
  - 지역별 가게조회(메인화면) 필터링 구현(거리뺴고) + 회원용 API 따로 만듦(가고싶다, 가봤어요 필터때문에)
  - 클라이언트가 페이징 기능 구현하기가 벅차다고 없애달라고 요청해서 페이징기능 주석처리
  - 이미지가 null이면 기본이미지가 출력되도록 수정

## 2021.08.22
- API 구현
  - 특정 유저 조회 API
  - 마이리스트 조회 API
  - 특정리스트 조회 API
  - 마이리스트 생성 API
  - 마이리스트에 식당 추가 API
- 테이블 수정
  - 식당 정보 html이 아닌 데이터로 변경(메뉴는 고민중)
- API 수정
  - 특정가게 조회 : 한 화면에 있는 정보가 한 api를 사용할 때 다 나오도록 하기위해 데이터베이스에 {multipleStatements : true} 추가 후 여러개의 쿼리 사용
  - 클라이언트가 null처리를 할 수 없다고 해서 이미지가 없는 리뷰, 리뷰가 없는 가게의 평점 등을 해결할 방법 

## 2021.08.23
- API 구현
  - 마이리스트 수정 API
  - 마이리스트 삭제 API
  - 마이리스트 식당 추가할 때 검색 API
  - 마이리스트 식당 삭제 API
  - 특정 유저 가고싶다 리스트 조회 API
  - 프로필 사진 설정 API
- 테이블 수정
  - 탑리스트 관련 테이블 없애고 마이리스트에 탑리스트여부 컬럼을 줌(조회수가 100이상이면 탑리스트) -> 마이리스트 조회할 때 조회수가 100이 넘으면 탑리스트로 바뀜
- API 수정
  - 특정 가게 API : 클라이언트 요구에 따라 result안의 여러배열을 각각 restaurant, countPerReview, reviewList 배열로 나누어 결과를 줌
  - 리스트 관련 uri 변경 : User파일에서 ist파일로 옮김

## 2021.08.24
- API 구현
  - 팔로우 버튼 API
  - 식당 등록하기 API
  - 지역 보기 API
  - 리뷰 좋아요 버튼 API
  - 가고싶다 버튼 API
  - 내가 등록한 식당 조회 API
  - 리뷰 작성 API
- API 수정
  - 클라이언트 요구에 따라 특정가게 조회에서 가게정보 부분 api와 리뷰수, 리뷰부분 api를 따로 나누어서 전달

## 2021.08.25
- API 구현
  - 위치정보 허용 API
- API 수정
  - 식당등록할 때 도로명, 지번을 좌표만으로 가져올 수 있게 하기 위해 카카오 로컬 api 사용
- 테이블 수정
  - 위치정보를 위해 user, restaurant 테이블에 위도, 경도 컬럼 추가
  - 메뉴 테이블 생성하고 RestaurantInformation 테이블 삭제
- 더미데이터 30% 

## 2021.08.26
- API 구현
  - 휴대폰 인증 + 인증완료시 회원정보 수정 API
- 더미데이터 모두 넣음
- 명세서, 포스트맨 정리 