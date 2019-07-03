# 2019_Weather_Competition

Description
- 날씨 빅데이터 콘테스트

1. Data load - (encoding='UTF-8')

2. 기존 수상작들을 볼 때, 주로 연구원 및 현직자들이 회사의 데이터와 결합하여 사용함(https://blog.naver.com/PostView.nhn?blogId=kma_131&logNo=221356151838). 기껏해야 장려상으로 공공데이가 메인으로 사용된 느낌. 기획이 매우 중요하며 메인으로 사용될 별도의 데이터를 모색함이 가장 중요한 시점으로 보인다.

3. 유통분야로 진행 시, 필수로 사용해야 하는 korean_hnb와 korean_cvs의 데이터가 서울특별시, 인천광역시, 경기도 로 나뉘어있기에 이 중 한 곳으로 집중하는것도 좋아보임.

3-1. 데이터 추가의 필요성 증대
 - 생활기상지수 (https://www.data.go.kr/dataset/15000232/openapi.do) :  체감온도, 불쾌지수, 더위체감지수 등 날씨 보조자료로 사용가능
 - 뉴스빅데이터 분석 정보 (https://www.data.go.kr/dataset/15012945/fileData.do) : 가뭄, 미세먼지, 오존 등의 기사 메타 데이터 -> 인트로로 사용가능
 - 랄라블라 매장 위치 데이터 (slack general에 업로드함) : 수도권 107개 매장 대상


4. 참고해볼 사이트 및 데이터 (주기적으로 업데이트 부탁합니다)
 - 서울시열린데이터광장(https://data.seoul.go.kr/)
 - 공공데이터포털 (https://www.data.go.kr/)
 - SKT Data Hub(http://www.bigdatahub.co.kr/index.do)
 
 


## Data1. korea_hnb (Shape : 820274, 7)
### Column 설명
* korea_hnb.pvm_nm : 지역명(서울특별시, 인천광역시, 경기도) 총 3개
* korea_hnb.bor_nm : 지역명 세부(강남구, 강북구, 강서구, 계양구, 고양시, 관악구, … ) 총 36개
* korea_hnb_sale.dt : 기간(20160101 - 20181231) 총 1096개
* korea_hnb.gen_cd : 성별(F, M) 총 2개
* korea_hnb.age_cd : 나이대(00~19, 20~39, 40~59, 60~99) 총 4개
* korea_hnb.category : 아이템 카테고리(네일, 립컬러, 립케어, 마스크팩, 바디로션, 선케어, 제모제, 체중조절, 크림로션, 훼이셜클렌저) 총 10개
* korea_hnb.qty : 판매개수

## Data2. korea_cvs (Shape :2707786, 7)
### Column 설명
* korea_cvs.pvm_nm : 지역명(서울특별시, 인천광역시, 경기도) 총 3개
* korea_cvs.sale_dt : 기간(20160101 - 20181231) 총 1096개
* korea_hnb.gen_cd : 성별(F, M) 총 2개
* korea_hnb.age_cd : 나이대(00~19, 20~39, 40~59, 60~99) 총 4개
* korea_hnb.category : 아이템 카테고리 ['라면', '과자', '마스크', '맥주', '생리대', '생수', '숙취해소제', '스타킹', '아이스크림',
       '탄산음료', '면도기', '우산'] 총 12개
* korea_hnb.qty : 판매개수 min 7 - max 49938 (left skew)
* korea_cvs.bor_nm : 지역명 세부(강남구, 강북구, 강서구, 계양구, 고양시, 관악구, … ) 총 60개

## Data3. bigcon_weather (Shape : 70072, 11)
### Column 설명
* bigcon_weather.tm        : 	관측일 (20160101 - 20181231)
* bigcon_weather.stn_id    : 	관측지점번호 (bor_nm의 id)  총 54개
* bigcon_weather.pvn_nm    : 	법정동코드 - 도 ('경기도', '서울특별시', '인천광역시') - 총 3개 
* bigcon_weather.bor_nm    : 	법정동코드 - 시,군 ('동두천시', '파주시', '종로구', '수원시권선구' 등) 총 54개
* bigcon_weather.max_ta    : 	최고기온 min -24.4 - max 41.8
* bigcon_weather.max_ws    : 	최대풍속 min 0.0 - max 15.7
* bigcon_weather.min_ta    : 	최소기온 min -24.4 - max 31.8
* bigcon_weather.avg_ta    : 	평균기온 min -18.1 - max 34.4
* bigcon_weather.avg_rhm   : 	평균상대습도 min 0.0 - max 100.0
* bigcon_weather.avg_wa    : 	평균풍속 min 0.0 - max 9.5
* bigcon_weather.sum_rn    : 	합계강수 min 0.0 - max 327.5

**!! Problem 발생 = 결측치**
* bigcon_weather.tm        : 	관측일		10959개
* bigcon_weather.stn_id    : 	관측지점번호		10959개
* bigcon_weather.pvn_nm    : 	법정동코드(도)		10959개
* bigcon_weather.bor_nm    : 	법정동코드(시,군)		10959개
* bigcon_weather.max_ta    : 	최고기온		11246개
* bigcon_weather.max_ws    : 	최대풍속		11294개
* bigcon_weather.min_ta    : 	최소기온		11246개
* bigcon_weather.avg_ta    : 	평균기온		11258개
* bigcon_weather.avg_rhm   : 	평균상대습도		26159개
* bigcon_weather.avg_wa    : 	평균풍속		11244개
* bigcon_weather.sum_rn    : 	합계강수		11013개

해결 if 1.법정동코드(도)로 지역 나눠서 (관측일 기준)
 - 경기도 : 26264개 중 결측치 max 151 (상대습도)
 - 서울특별시 : 27395개 중 결측치 max 11068 (상대습도)
 - 인천광역시 : 5454개 중 결측치 max 3981 (상대습도)
 
---
<주제>  대형 화재 방지를 위한 분류 모형과 지표 개발
1. 화재 발생 위험 지역 분류
2. 대형 화재로 발현 가능성
3. 소방 취약 지역을 점수화
4. 피크 시즌의 차량 및 인원 배치 (위험 지역에 있어서)

==> 전국 데이터
- 화재 데이터
- 건축물 노후도
- 도로 교통 현황
- 소방서 위치
- 소방차 진입 불가 구간
- 날씨데이터

---

<IDEA 2>  미세먼지 정화 차량 배치 최적화 모델

<IDEA 3>  가설 검증. 날씨와 상권에 따른 소비패턴 분석

<IDEA 4>  지역 별 날씨에 따른 성장 지표 예측

<IDEA 5> 날씨에 따른 지역별 음식물 쓰레기 배출량 예측 - 음식물 쓰레기 배차량 배치

<IDEA 6> 날씨에 따른 작업 오류 분류

<IDEA 7> 날씨 지표 개발

<IDEA 8> 날씨와 범죄
1. 화재 발생 위험 지역 분류
2. 위험 지역을 점수화
3. 차량 및 인원 배치 (위험 지역에 있어서)~

