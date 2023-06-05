### SELECT 문장 실행 순서
- FROM
- WHERE
- GROUP BY
- HAVING
- SELECT
- ORDER BY

#### 윈도우 함수
> `윈도우 함수()` `OVER` ( `partion by` 컬럼 `order by` 컬럼 ASC or DESC )
- 윈도우 함수(): 순위함수, 집계함수, 행순서 함수, 비율함수
- OVER :윈도우 함수에서 **꼭** 들어가야하며 OVER 내부에 `partion by`와 `order by`이 온다/.
- partion by : 전체 집합을 어떤 기준(컬럼)에 따라 나눌지 결정
- order by : 어떤 항목(컬럼)을 기준으로 순위를 정할 지 결정하는 부분