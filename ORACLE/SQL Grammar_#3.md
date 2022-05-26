# SQL 문법 실습_#3 📌
[실습]
1)student라는 이름으로 테이블 생성
컬럼명)    id           name         age        score
데이터타입) varchar2(10) varchar2(30) number(3)  number(3)
제약조건) primary key | not null | not null | not null
```sql
CREATE TABLE student(
 id varchar2(10) primary key,
 name varchar2(30) not null,
 age number(3) not null,
 score number(3) not null
);
```
2)student 테이블에 데이터를 아래와 같이 입력

|id|name|age|score|
|---|---|---|---|
|dragon|홍길동|21|100|
|sky | 장영실|22 |99|
|blue|박문수|34|88|
   
             
```sql
INSERT INTO student (id,name,age,score) 
VALUES ('dragon','홍길동',21,100);

INSERT INTO student (id,name,age,score) 
VALUES ('sky','장영실',22,99);

INSERT INTO student (id,name,age,score) 
VALUES ('blue','박문수',34,88);
COMMIT;
```

3)student 테이블에서 데이터 읽기
성적 합계 구하기
```sql
SELECT SUM(score) FROM student;
```
<br>

---
<br>

1)emp테이블에서 커미션 항목이 입력된 사원들의 이름과 급여,커미션을
출력하시오.
```
SELECT ename,sal,comm FROM emp WHERE comm IS NOT NULL;
```
2)커미션 계약을 맺은 모든 사원의 이름,급여,커미션을 출력하는데 커미션을 기준으로 내림차순 정렬하시오.
```
SELECT ename,sal,comm FROM emp 
WHERE comm IS NOT NULL ORDER BY comm DESC;
```
3)월급과 커미션을 합친 금액이 2,000이상인 급여를 받는 사원의 이름,업무,월급,커미션,고용날짜를 출력하시오.(단, 고용날짜는 1980-12-17 형태로 출력하시오)
```
SELECT ename,job,sal,comm,
       TO_CHAR(hiredate,'YYYY-MM-DD') hiredate
FROM emp WHERE sal+NVL(comm,0) >= 2000;
```
4)CASE~WHEN~THEN 를 이용해서 다음 데이터에 따라 JOB 열의 값을 기준으로 모든 사원의 등급을 표시하시오.

|업무 | 등급|
|:---:|:---:|
|PRESIDENT | A|
|ANALYST|  B|
|MANAGER|  C|
|SALESMAN| D|
|CLERK|  E|
|기타  | 0|

```sql
SELECT ename,job, 
       CASE job WHEN 'PRESIDENT' THEN 'A'
                WHEN 'ANALYST' THEN 'B'
                WHEN 'MANAGER' THEN 'C'
                WHEN 'SALESMAN' THEN 'D'
                WHEN 'CLERK' THEN 'E'
                ELSE '0'
        END "Grade"
FROM emp ORDER BY "Grade" ASC;
```
       
5)30번 부서에서 근무하는 사원들의 부서번호, 부서이름, 사원이름,월급,급여등급을 출력하시오.
```sql
SELECT e.deptno, d.dname, e.ename, e.sal, s.grade
FROM emp e INNER JOIN dept d
ON e.deptno=d.deptno
INNER JOIN salgrade s
ON e.sal BETWEEN s.losal AND s.hisal
WHERE e.deptno=30;
```
6)ALLEN보다 급여를 많이 받는 사람 중에서 입사일이 가장 빠른 사원과 동일한 날짜에 입사한 사원의 이름과 입사일,급여를 출력하시오.
```sql
SELECT ename,hiredate, sal FROM emp
WHERE hiredate = (SELECT MIN(hiredate) FROM emp 
WHERE sal >(SELECT sal FROM emp WHERE ename='ALLEN'));
```