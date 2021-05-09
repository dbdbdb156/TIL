# DB 기본상식

## CRUD

### INSERT
INSERT INTO T1 (A,B) VALUES (1,’김대중’)

### UPDATE
UPDATE 테이블 SET 컬렴명=값 where id=20000;

### DELETE
DELETE FROM 테이블 where where id=20000;

### SELECT


## JOIN(조인)

### 1. inner 조인 : 두 테이블간 교집합
SELECT T1.A, T1.B, T2.C
FROM T1 INNER JOIN T2 ON T1.A=T2.A

### 2. LEFT OUTER 조인 
: left 테이블의 값이 있으면 right 테이블에 데이터가 없어도 null 로 출력
SELECT T1.A,T1.B, T2.C
FROM T1 LEFT  OUTER JOIN T2 ON T1.A=T2.A
ex)
<ORACLE>
SELECT *
FROM EMPLOYEE E, DEPARTMENT D
WHERE E.DepartmentID = D.DepartmentID(+);


### 3. RIGHT 아우터 조인
: right 테이블의 값이 있으면 left 테이블에 데이터가 없어도 null 로 출력
SELECT T1.A,T1.B, T2.C
FROM T1 RIGHT OUTER JOIN T2 ON T1.A=T2.A

### 4. FULL OUTER 조인 
: XOR 연산이라 생각하면 편함
SELECT T1.A,T1.B, T2.C
FROM T1 FULL OUTER JOIN T2 ON T1.A=T2.A

*참고
<MySQL> full outer join 이 없음
SELECT *
FROM EMPLOYEE E LEFT OUTER JOIN department D
ON E.DepartmentID = D.DepartmentID
UNION
SELECT *
FROM EMPLOYEE E RIGHT OUTER JOIN DEPARTMENT D
ON E.DEPARTMENTID = D.DEPARTMENTID;

### 5. CROSS 조인 - 카디션 곱
SELECT *
FROM EMPLOYEE CROSS JOIN DEPARTMENT;

### 6. 셀프조인
SELECT
A.NAME, --A테이블의 NAME조회
B.AGE --B테이블의 AGE조회
FROM EX_TABLE A,EX_TABLE B


## 이외 정보들

### 1. 서브쿼리

1) SELECT 에서 서브쿼리
SELECT
CD_PLANT,
NM_PLANT,
(SELECT AVG(UM) FROM TABLE_ITEM) AS UM
FROM TABLE_PLANT

2) FROM 에서 서브쿼리
SELECT
CD_PLANT,
NM_PLANT,
AM
FROM
(SELECT * FROM  TABLE_PLANT)

3) where 에서 서브쿼리
Select
CD_PLANT
FROM TABLE_PLANT
WHERE CD_PLANT IN(SELECT CD_PLANT FROM  TABLE_PLANT WHERE PLANT ='1000' AND COMPANY = '0327')


### 2. rename : 테이블 재 명명
SELECT gg._id, gg.name, s.title
FROM girl_group as gg
join song as s
on s._id = gg.hit_song_id;

### 3. 내장함수 & group by, order by , DESC(올림차순) <_> ASC
SELECT '2005년' year, deptno 부서번호, COUNT(*) 사원수
  FROM emp
 GROUP BY deptno
 ORDER BY COUNT(*) DESC;

### 4. distinct
SELECT COUNT(DISTINCT d.deptno) "중복제거 수", 
       COUNT(d.deptno) "전체 수"
  FROM emp e, dept d
 WHERE e.deptno = d.deptno;
 
-> SELECT DISTINCT 컬럼 FROM 테이블

### 5. having <- group by 의 조건문
SELECT b.dname, COUNT(a.empno) "사원수"
  FROM emp a, dept b
 WHERE a.deptno = b.deptno
 GROUP BY dname
HAVING COUNT(a.empno) > 5;





