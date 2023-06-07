#### 식별자 분류

- 대표성 여부
    - 주식별자
    - 보조식별자
- 스스로 생성 여부
    - 내부식별자
    - 외부식별자
- 속성 수
    - 단일식별자
    - 복합식별자
- 대체여부
    - 본질식별자
    - 인조식별자

#### 데이터 모델링의 특징
- 단순화, 추상화, 명확화

#### 데이터 모델링의 기능
- 가구 명문 관표
- 가시화
- 구조화
- 명세화
- 문서화
- 다양한 관점
- 표현 방법 제공

#### SQL
- DML (데이터 조작 언어)
    - SELECT, INSERT, UPDATE, DELETE
- DDL (데이터 정의 언어)
    - ALTER, CREATE, MODIFY, DROP
- TCL (트랜잭션 제어 언어)
    - ROLLBACK, COMMIT
- DCL (데이터 제어 언어)
    - GRANT, REVOKE

#### SELECT 문장 실행 순서
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


#### SQL 연산 순서
- FROM
- WHERE
- GROUP BY
- HAVING
- SELECT
- ORDER BY

#### CONCAT
``` sql
Select col1 + col2 + col3 from table; (SQL Server)
Select col1 || col2 || col3 from table; (oracle)
Select concat(col1, col2) from table; 
```
    
#### ROWNUM, TOP

ORACLE에선 WHERE절에 ROWNUM 을 사용
SQL Server에선 SELECT 옆에 TOP

#### 날짜 함수
To_char – 날짜형 데이터를 문자로 출력
``` sql
# To_date – 문자형 데이터를 날짜형으로 출력
Select to_char(sysdate, ‘YYYY-MM-DD’) from dual;

# sysdate (oracle), getdate() (SQL Server)
Select to_date('2022-09-22') from dual;
```

#### GROUP BY
집약기능을 가지고 있음 (다수의 행을 하나로 합침)
Group by 절에 온 컬럼만 select 절에 올 수 있음

#### 집합연산자
- Union 정렬O 중복제거O 느리다
- Intersect 정렬O 교집합 느리다
- Minus (except) 정렬O 차집합 느리다
- Union all 정렬X 중복제거X 빠르다

#### 그룹함수
- roll up
    - (GROUP BY에 있는 컬럼들을 오른쪽에서 왼쪽순으로 그룹 생성)
    - a, b 로 묶이는 그룹의 값
    - a 로 묶이는 그룹의 소계
    - 전체합계
- cube
    - (나올 수 있는 모든 경우의 수로 그룹 생성)
    - a, b 로 묶이는 그룹의 값
    - a 로 묶이는 그룹의 소계
    - b 로 묶이는 그룹의 소계
    - 전체합계
- groupingsets
- grouping
어떤 결과가 나오고 어떤 함수를 사용 했는지에 대한 문제 기출
- rollup(A,B) != rollup(B,A), cube(A,B) = cube(B,A)

#### Entity

관리해야 할 대상이 엔터티가 될 수 있다.
인스턴스 2개이상
업무에서 사용해야 함 (프로세스)
관계를 하나이상 가져야 한다
- 유형 엔터티
- 개념 엔터티
- 사건 엔터티
- 기본 엔터티
- 중심 엔터티
- 행위 엔터티

#### ERD

그리는방법

- 좌상에서 우하로
- 관계명 반드시 표기 하지 않아도 됨
- UML은 객체지향에서만 쓰인다

#### 이상현상
1. 삽입 이상 (insertion anomaly) : 새 데이터를 삽입하기 위해서 불필요한 데이터도 함께 삽입해
야 하는 이상 문제.
2. 갱신 이상(update anomaly) : 중복 튜플 중 일부만 변경하여 데이터가 불일치하게 되는 이상
문제.
3. 삭제 이상(delete anomaly) : 튜플을 삭제하면 필요한 데이터까지 함께 삭제되는 이상 문제.

#### 논리연산자
1. AND – A 그리고 B (둘다 만족)
2. NOT - ~가 아니다
3. OR – A 또는 B (둘중 하나만 만족해도 OK!)

#### 문자 함수

Lower, upper – 소문자로, 대문자로
Trim, ltrim, rtrim – 양쪽공백제거, 왼쪽, 오른쪽 공백제거
Lpad, rpad – 특정 자리를 정하고, 왼쪽 / 오른쪽 의 공백을 채워주는 함수

- Select lpad(‘A’, 5, ‘0’) from dual;
- 0000A, rpad면 A0000
- Substr – SELECT SUBSTR(‘korea’, 2, 2) FROM DUAL; or 이 출력
- Instr - SELECT INSTR('CORPORATE FLOOR','PO') AS idx FROM DUAL; 4 가 출력

#### 조건문
- Decode
    - select decode(col1,’A’,1,’B’,2,3) from dual;
    - col이 A면 1, B면 2, 아니면 3
- case
    - case when col = ‘A’ then 1
    - when col = ‘B’ then 2
    - else 3 end; 서로 같다
    - case col when ‘A’ then 1
    - when ‘B’ then 2
    - else 3 end

#### 서브쿼리
- Select – 스칼라 서브쿼리
- From – 인라인뷰 (메인 쿼리의 컬럼 사용 가능)
- Where – 중첩 서브쿼리
- Group by – 사용 불가
- Having – 중첩 서브쿼리
- Order by – 스칼라 서브쿼리
- In – 서브쿼리 출력값들 or 조건
- Any/some – 서브쿼리 출력값들중 가장 작거나 큰 값과 비교
- All – any/some과 반대 개념
- Exists – 서브쿼리내 select 절엔 뭐가 와도 상관 없다. Row가 있으면 true, 없으면 false

#### 제약조건
- 기본키(PK) – not null + unique
- 테이블당 하나의 PK를 가질 수 있음 (하나라는게 컬럼이 아님, 복합키 가능)
Not null – 해당 컬럼에 null이 올 수 없음
Unique – 해당 컬럼에 중복값이 올 수 없음

#### 윈도우 함수
- rows between and 값이 증가한다.
rows between UNBOUNDED PRECEDING and CURRENT ROW) as "직업별 합계"
rows between 1 PRECEDING and 1 FOLLOWING) as "위아래합계"
- range between and 값이 동일하다
1. UNBOUNDED PRECEDING: 최종 출력될 값의 맨 처음 row의 값(Partition by 고려)
2. CURRENT ROW: 현재 row의 값
3. UNBOUNDED FOLLOWING: 최종 출력될 값의 맨 마지막 row의 값(Partition by 고려)
- Rank 1,1,3,4….
- Dense_rank 1,1,2,3…
- Partition by, order by
Row_number() over (partition by col1 order by col2)…

#### 속성
기본 속성
설계 속성
파생 속성

#### 식별자
유일성 – 유일하게 인스턴스를 구분
최소성 – 최소 컬럼으로
불변성 – 값이 바뀌지 않아야 함
존재성 – not null

- 위 4개를 만족하면 후보키가 될 수 있으며, 그중 하나, 대표하는 것이 기본키 이다.

#### 성능 데이터 모델링
- 아키텍쳐 모델링 (우선순위 1)
    - 테이블, 파티션, 컬럼등의 정규화 및 반정규화
- SQL 튜닝 (우선순위 2)
    - Join 수행 원리
        - Hash join
            - 등가 join만 사용 함
            - Hash 함수를 사용하여 select, join 컬럼 저장 (선행 테이블)
            - 선행 테이블이 작다
            - Hash 처리를 위한 별도 공간 필요
        - NL join
            - 랜덤 엑세스
            - 대용량 sort 작업
            - 선행 테이블이 작을수록 유리
        - Sort Merge
            - Join 키를 기준으로 정렬
            - 등가/비등가 join 가능
        - Optimizer
            - CBO 제일 경제적인걸 정함
            - RBO 규칙에 의해서 정함

#### 성능 데이터 모델링 절차
- 정용 트반 구검
    - 정규화
    - 용량산정
    - 트랜잭션 유형 파악
    - 반정규화
    - 데이터 구조 조정
    - 데이터 모델 검증

#### 반정규화
데이터의 무결성을 해칠 수 있음

- 절차
    - 대량범위처리 빈도수 조사
    - 범위처리 빈도수
    - 통계처리 여부
- 종류
    - 테이블 병합 1:1/1:M
    - 슈퍼/서브 타입 병합
    - 부분테이블 분할
    - 통계테이블 분할
    - 중복테이블 분할
    - 부분테이블 분할
    - 이력 컬럼 추가
    - 중복 컬럼 추가
    - PK를 일반 컬럼으로 병합
    - 파생 컬럼 추가
    - 응용 시스템 오작동을 피하기 위한 임시값 컬럼 추가
    - 중복 관계 추가

#### ESCAPE

and email like '@_%' escape '@'
*아무 문자나 가능

#### 숫자 함수

- Round(222.45, 1) : 소수점 둘째자리에서 반올림하여 첫째자리까지 출력
- Round(225.67, 0) : 소수점 첫째자리에서 반올림하여 정수만 출력
- -1 파라미터는 1의 자리에서 반올림하여 정수를 출력
- Ceil(oracle) / ceiling(SQL Server) : 올림함수, 파라미터 사용법은 - round와 같음
- Floor : 버림 함수, 파라미터 사용법은 round와 같음 (Ceil의 반대)
- TRUNC : 소수점 버림
- ABS : 절대값

#### 집계 함수
Count, min, sum, max 등

- null은 포함되지 않는다
- (1, null, 2, 3, null) 의 데이터를 기준으로 결과는 다음과 같다.
◼ Count() – 3
◼ Sum() – 6
◼ Avg() – 2
◼ Min() – 1
◼ Max() – 3

| Col1  | Col2  | Col3 |
| --- | --- | --- |
| null  | null  | 1 |
| 2 | 3 | 2 |
| 1 | null  | null  |

``` sql
Select sum(col1 + col2 + col3) from dual;
```
여기에서 먼저 sum을 생각하지말고 col1 + col2 + col3 을 먼저 생각해보면 첫번째 행은 null +
null + 1이기에 null이 반환되고, 마지막 세번째 행도 마찬가지다.
그러므로, 두번째 행의 2 + 3 + 2의 값인 7이 결과가 된다.
반대로, sum(col1) + sum(col2) + sum(col3)의 값은 3 + 3 + 3 이므로 9가 출력이 된다.
이 차이를 알아야 한다

#### JOIN
- Natural join
    - 반드시 두 테이블 간의 동일한 이름, 타입을 가진 컬럼이 필요하다.
    - 조인에 이용되는 컬럼은 명시하지 않아도 자동으로 조인에 사용된다.
    - 동일한 이름을 갖는 컬럼이 있지만 데이터 타입이 다르면 에러가 발생한다.
    - 조인하는 테이블 간의 동일 컬럼이 SELECT 절에 기술 되도 테이블 이름을 생략해야 한
    다.
    ``` sql
    select department_id 부서, department_name 부서이름, location_id 지역번호, city 도시
    from departments
    natural join locations
    where city = 'Seattle';
    ```
- Using
    - USING 절은 조인에 사용될 컬럼을 지정한다.
    - NATURAL 절과 USING 절은 함께 사용할 수 없다.
    - 조인에 이용되지 않은 동일 이름을 가진 컬럼은 컬럼명 앞에 테이블명을 기술한다.
    - 조인 컬럼은 괄호로 묶어서 기술해야 한다.
    ``` sql
    select department_id 부서번호, department_name 부서, location_id 지역번호, city 도시
    from departments
    join locations using (location_id);
    ```
- left outer join
    - from table a left outer join table b on a.col = b.col 이것과 같은 오라클 sql 문법은
    - from table a, table b where a.col = b.col(+)
- join 순서
    - from a,b,c a와 b가 join 되고, 그리고 c와 join 된다.

#### VIEW
- 가상 테이블
- 독립성, 편의성, 보안성
- SQL을 저장하는 개념

#### PL/SQL
- exception (생략가능)
- procedule 반드시 값이 안나옴
- trigger 커밋, 롤백 안됨
Before, after별로 Insert, update, delete 가 있음
- function 반드시 반환값이 있음

#### 계층형 함수
prior 자식데이터 = 부모데이터
부모데이터에서 자식데이터로 가면 순방향
``` sql
SELECT LEVEL, *순방향
LPAD(' ', 4 * (LEVEL-1)) || 사원 사원,
관리자,
CONNECT_BY_ISLEAF ISLEAF
FROM 사원
START WITH 관리자 IS NULL
CONNECT BY PRIOR 사원 = 관리자;
SELECT LEVEL, *역방향
LPAD(' ', 4 * (LEVEL-1)) || 사원 사원,
관리자,
CONNECT_BY_ISLEAF ISLEAF
FROM 사원
START WITH 사원 = 'D'
CONNECT BY PRIOR 관리자 = 사원;
```

#### 도메인
- 데이터유형
- 크기
- 제약조건
- Check,
- primary key,
- Foreign key,
- not null,
- unique

#### 식별자 & 비식별자
- 식별자
    - 강한관계,
    - PK가 많아진다 (조인시)
    - SQL이 복잡해짐
- 비식별자
    - 약한관계
    - SQL이 느려짐

#### 정규화
1차. 원자성
2차. 부분함수종속성 제거
3차. 이행함수종속성 제거
BCNF. 정의

Select시 join 때문에 느려질 수 있다. (테이블이 늘어나서)
Insert, update는 빨라질 수 있다. (테이블 사이즈가 작아져서)

#### 데이터에 따른 성능
- 행 이전(Row migration)
    - Update로 인해 행 길이가 증가했을 때, 저장 공간이 부족한 경우 발생
    - 원래 정보를 기존 블록에 남겨두고 실제 데이터는 다른 블록에 저장
        - → 검색 시, 원래 블록에서 주소를 먼저 읽고 다른 블록을 찾아야 하므로 성능 감소
    - 해결책 : PCTFREE 영역을 충분히 할당한다.
        - → PCTTREE가 너무 큰 경우 데이터 저장 공간 부족으로 공간 효율성 감소
- 행 연결(Chaing)
    - 데이터가 커서, 여러 블록에 나누어 저장하는 현상
        - → 2개 이상의 데이터 블록을 검색해야 하므로 성능 감소
    - Initial Row Piece(행 조각)와 Row Pointer로 블록 내에 저장
    - 해결책 : DB_BLOCK_SIZE를 크게 하여 최소화 가능
        - → 사이즈 변경이 어렵고, 무조건 크게 할 수 없음
- List partition
    - 특정 값을 기준으로
    - 관리 쉬움
    - 데이터가 치우칠 수 있음
- Range partition
    - 특정 값의 범위
    - 관리 쉬움
    - 가장 많이 씀
- Hash partition
    - 관리 어려움

#### 인덱스
- 사용 못하는 경우
    - 부정형
    - Like
    - 형변환(묵시적)
- 악영향
    - DML 사용시 성능이 저하됨