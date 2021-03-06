# RStudio를 이용한 데이터 가공

학교 논문 제출용으로 RStudio를 이용하여 데이터를 가공하는 경험을 하였다. '코로나 사태 이후 서울권 유동인구를 분석' 하는 것을 제목로 하였고, 주제는 서울시 유동인구를 분석하여 COVID-19의 확산을 방지하기 위하여 각 서울시 행정 구의 유동인구에 따른 방역의 강화와  가급적 그 구역을 피하도록 유도하기 위한 (인구 확산) 서비스에 기초자료로 활용되도록 분석하는 것으로 하였다.



![image](https://user-images.githubusercontent.com/68289543/102897483-69335400-44ab-11eb-9405-5858a3c90101.png)



데이터는SKT Big Data Hub (https://www.bigdatahub.co.kr/product/view.do?pid=1002338) 에서 '서울시 유동인구 데이터 20년 11월' 을 이용하였다.

```R
dat <- read.csv(file="C:/Floating_population_2011.csv")
```

명령어를 통해 데이터를 열고 dat이라는 변수에 저장하였다. 처음에 오류가 자꾸 떠서 안되다가 인코딩을 UTF-8로 변경하니 됐다.



![image](https://user-images.githubusercontent.com/68289543/102897902-160dd100-44ac-11eb-9f51-a767e942cf6a.png)

처음 데이터는 이런 모습이었다.  약 216000개의 행이 있었고 열은 총 7개였다. 이 데이터를 시간, 지역별로 나눈다음 유동인구수의 평균을 내어 특정 시간에 특정 지역의 인구수를 파악 하고자 하였다.



![image](https://user-images.githubusercontent.com/68289543/102899278-04c5c400-44ae-11eb-86d1-b019b341622e.png)

위 명령어를 통해 1열 (일자), 3열(연령대), 4열(성별)을 삭제하고 그 삭제된 데이터를 delete_column에 저장하였다.

![image](https://user-images.githubusercontent.com/68289543/102899938-fe841780-44ae-11eb-8940-2054b75fd78e.png)

위와 같이 원하는 데이터만 추출한 후 여기서 우선 군구로 정렬한 다음 맨 위에 나오는 구부터 차례로 새로운 데이터 프레임을 만들어 집어 넣었다. 가장 처음엔 강남역 부터 하였다.



![image](https://user-images.githubusercontent.com/68289543/102900412-9255e380-44af-11eb-92aa-35b71c005ea8.png)

gangam 이란 변수를 만들어 subset 함수를 이용하여 delete_column에 군구열이 "강남구" 인 열만 추출해여 gangnam 에 집어 넣었다.

![image](https://user-images.githubusercontent.com/68289543/102900522-bdd8ce00-44af-11eb-8cdf-30b539c50b8f.png)

데이터는 위와 같고 여기서 시간별로 유동인구수의 평균을 구해야 했기 때문에 tapply 함수를 이용하였는데, tapply 함수는 인자로 (평균을 구할 변수, 그룹 변수, 평균을 구할 함수) 를 갖는 함수인데, 데이터가 아닌 값으로 반환한다. 



![image](https://user-images.githubusercontent.com/68289543/102900794-29bb3680-44b0-11eb-9d1c-36fa633f5e11.png)

위와 같이 gangnam_mean 이라는 변수를 만들어 tapply함수를 이용하여 시간에 따른 유동인구수의 평균 값(value) 를 저장하였다.



![image](https://user-images.githubusercontent.com/68289543/102901750-54f25580-44b1-11eb-9fa3-5cf2dc51cdf2.png)

그 후에는 데이터프레임으로 다음과 같이 값을 만들기를 원했기 때문에 열이 군구 이고 값이 강동구로만 되어있는 값과 열이 시간이고 값이 0~23으로 되어 있는 갑과 내가 방금 tapply 함수를 통해 구한 구의 평균 유동인구수 값을 합치기로 하였다.

![image](https://user-images.githubusercontent.com/68289543/102900957-5a02d500-44b0-11eb-9574-f0afc52cd8fb.png)

그 코드가 위의 코드이다. data.frame함수를 이용하여 행의 수가 같은 세 값을 하나의 테이블로 합쳤다. 여기서 rep은 특정 문자를 반복하여 값으로 만들어주는 함수로 rep(값, 반복횟수) 를 입력하여 값을 반복횟수 만큼 반복하여 값을 생성한다. 그리고 sep 함수는 인자로 (시작 값, 끝 값, 간격 값) 을 갖는 함수인데, 말 그대로 시작 값부터 시작하여 끝 값까지 간격 값을 기준으로 증감시키는 값을 저장하는 함수이다. ~~하지만 이 방식으로 하지 말고 mean 값을 구했을 때에서 멈췄어야했다.~~ 결과적으로 gangnam_fin 변수에 군구, 시간, gangnam_min ( 강남구의 평균 유동인구) 를 열로 갖는 데이터프레임이 완성되었다.



![image](https://user-images.githubusercontent.com/68289543/102902072-c6ca9f00-44b1-11eb-8cbc-6902ed24b546.png)

위와 같이 과정을 모든 구에 반복하여, 결과 적으로 다음과 같이 데이터 프레임을 만들었다.

![image](https://user-images.githubusercontent.com/68289543/102902145-e5c93100-44b1-11eb-9b1e-9cd3531e2237.png)

더 길었지만 화면에 들어오지 않아 다 담지는 못했다. 

하지만 여기서 나는 이 데이터들을 열로 합쳐서 한 데이터 프레임으로 만들고자 하였다. 그렇게 해야 각 구 별, 시간대 별로 평균 유동인구수를 한 테이블로 확인할 수 있기 때문이다. 하지만 여기서 아까 내가  (군구,시간,평균) 값을 합쳐서 구_fin 이라는 변수에 데이터 프레임으로 만들던게 생각이났다. 그래서 cbind 함수를 이용하여 floation_population 이라는 변수에 모든 구의 시간별 유동인구 값을 저장하였다.

![image](https://user-images.githubusercontent.com/68289543/102903006-15c50400-44b3-11eb-88a2-92cc461c824c.png)

<br>

![image](https://user-images.githubusercontent.com/68289543/102903260-6b99ac00-44b3-11eb-9d62-f4f8a328e367.png)

그리고 flaotion_population 을 데이터 프레임으로 만들었다.

![image](https://user-images.githubusercontent.com/68289543/102903449-b4e9fb80-44b3-11eb-8029-66cd62d1b0d3.png)

마지막으로 열의 이름을 영어에서 한글로 다 바꿔주었다.



![image](https://user-images.githubusercontent.com/68289543/102903559-da770500-44b3-11eb-9b33-aca4b22045b3.png)

결과적으로 시간대별 구의 평균 유동인구수에 관한 데이터를 얻는데 성공하였다. 처음 데이터를 가공해보는 거라 어떤 식으로 해야할 지 감도 안잡히고 data, value 값에 대해서도 혼동도 오고 많이 힘들었지만 하루 종일 차근차근 하며 조금씩 건들여 보고 힘들게 구한 값이 혹여나 없어질까 새로운 변수에 계속 저장해가면서 해결하는 과정이 나름 재미있었다. 다음에는 조금 익숙한 언어인 python을 이용하여 가공해보는 시간을 가져봐야겠다.
