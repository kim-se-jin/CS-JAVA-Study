###  쿼리 수행 순서
FROM -> WHERE -> SELECT -> GROUP BY -> HAVING -> ORDER BY -> LIMIT 순으로이루어 져 있다. GROUP BY 의 위치는 무조건 FROM, WHERE 뒤에 위치해야 한다.

        
### HAVING과 WHERE의 차이를 설명해주세요.

- 그룹을 나타내는 결과 집합의 행에만 적용된다는 점에서 차이가 있다.
- WHERE 절은 개별 행에 적용됩니다. 쿼리에는 WHERE 절과 HAVING 절이 모두 포함될 수 있다.

### group by의 역할에 대해 설명해주세요
테이블에서 특정 구조로 그룹을 지어주는 역할을 하는 구문

### DELETE, TRUNCATE, DROP의 차이를 설명해주세요

DELETE는 테이블의 컬럼을 삭제할수있고 테이블 용량은 줄어들지않는다.삭제후 되돌릴수없다.
TRUNCATE는 테이블을 용량이 줄어들고 인덱스도 삭제된다. 삭제후 되돌릴수없다.
DROP은 테이블을 삭제한다. 삭제후 되돌릴수없다.

### INSERT/ UPDATE/ DELETE/ LIKE/ null

```sql
INSERT INTO table_name (column1, column2, column3,...) VALUES (value1, value2, value3,...)

UPDATE 테이블명 SET 컬럼1=컬럼1의 값, 컬럼2=컬럼2의 값 WHERE 대상이 될 컬럼명=컬럼의 값

DELETE FROM 테이블명 [WHERE 삭제하려는 칼럼 명=값]

아디다스로 시작하는 데이터 검색

select * from tbl_board where title like '아디다스%';

아디다스로 끝나는 데이터 검색

select * from tbl_board where title like '%아디다스';

아디다스가 들어가는 데이터 검색

select * from tbl_board where title like '%아디다스%';
```

#### 평균, 합계, 최고, 최저
```sql
합 : select sum(컬럼이름) from 테이블 where 조건

평균 : select avg(컬럼이름) from 테이블 where 조건

최고 : select max(컬럼이름) from 테이블 where 조건

최저 : select min(컬럼이름) from 테이블 where 조건

```

#### 테이블 정보
```sql
SHOW TABLE STATUS;
```
#### 중복 제거
distinct

### **IN, NOT IN 설명**
IN : where 절에서 찾으려는 모든값을 SELECT해준다
NOT IN: 입력한 값을 제외한 값을 SELECT해줄수있게 해준다.

mysql 기준
### **숫자에서 문자로**
```sql
select cast(2 as char(1));
````
### **문자에서 숫자로**
```sql
SELECT CAST('123' AS UNSIGNED);
// 문자열을 부호없는 정수형으로
```
### **문자에서 날짜로**
```sql
STR_TO_DATE('2000-01-31', '%Y-%m-%d') 
```
### **날짜 관련 함수**
너무많아서..
https://jang8584.tistory.com/7

### **분석 함수**
ROW_NUMBER(): 결과에 순번, 순위를 매기는 함수 
```sql
SUM(sal) OVER(PARTITION BY job ORDER BY empno)
```

- **누적 함수**
```sql
SUM(sal) OVER(PARTITION BY job ORDER BY empno)
```
합을구할때는 SUM만쓰면되는데 조회순서대로 누적할때는 OVER까지 사용한다. 
