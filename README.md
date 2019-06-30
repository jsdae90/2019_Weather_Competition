# 2019_Weather_Competition

Description
- 날씨 빅데이터 콘테스트


### 1. Data load - (encoding='UTF-8')

### Data1. korea_hnb (Shape : 820274, 7)
## Column 설명
* korea_hnb.pvm_nm : 지역명(서울특별시, 인천광역시, 경기도) 총 3개
* korea_hnb.bor_nm : 지역명 세부(강남구, 강북구, 강서구, 계양구, 고양시, 관악구, … ) 총 36개
* korea_hnb_sale.dt : 기간(20160101 - 20181231) 총 1096개
* korea_hnb.gen_cd : 성별(F, M) 총 2개
* korea_hnb.age_cd : 나이대(00~19, 20~39, 40~59, 60~99) 총 4개
* korea_hnb.category : 아이템 카테고리(네일, 립컬러, 립케어, 마스크팩, 바디로션, 선케어, 제모제, 체중조절, 크림로션, 훼이셜클렌저) 총 10개
* korea_hnb.qty : 판매개수

### Data2. korea_cvs (Shape :2707786, 7)
## Column 설명
* korea_cvs.pvm_nm : 지역명(서울특별시, 인천광역시, 경기도) 총 3개
* korea_cvs.sale_dt : 기간(20160101 - 20181231) 총 1096개
* korea_hnb.gen_cd : 성별(F, M) 총 2개
* korea_hnb.age_cd : 나이대(00~19, 20~39, 40~59, 60~99) 총 4개
* korea_hnb.category : 아이템 카테고리 ['라면', '과자', '마스크', '맥주', '생리대', '생수', '숙취해소제', '스타킹', '아이스크림',
       '탄산음료', '면도기', '우산'] 총 12개
* korea_hnb.qty : 판매개수 min 7 - max 49938 (left skew)
* korea_cvs.bor_nm : 지역명 세부(강남구, 강북구, 강서구, 계양구, 고양시, 관악구, … ) 총 60개


