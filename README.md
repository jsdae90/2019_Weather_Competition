# 2019_Weather_Competition

Description
- 날씨 빅데이터 콘테스트

1. Data load - (encoding='UTF-8')

2. 기존 수상작들을 볼 때, 주로 연구원 및 현직자들이 회사의 데이터와 결합하여 사용함(https://blog.naver.com/PostView.nhn?blogId=kma_131&logNo=221356151838). 기껏해야 장려상으로 공공데이가 메인으로 사용된 느낌. 기획이 매우 중요하며 메인으로 사용될 별도의 데이터를 모색함이 가장 중요한 시점으로 보인다.

3. 유통분야로 진행 시, 필수로 사용해야 하는 korean_hnb와 korean_cvs의 데이터가 서울특별시, 인천광역시, 경기도 로 나뉘어있기에 이 중 한 곳으로 집중하는것도 좋아보임.

4. 참고해볼 사이트 (주기적으로 업데이트 부탁합니다)
 - 서울시열린데이터광장(https://data.seoul.go.kr/)
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
 
 
