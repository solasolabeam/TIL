# SQL 문법 실습 📌 
1)emp 테이블에서 사원번호, 사원이름, 월급을 출력하시오.
```sql
SELECT empno, ename, sal FROM emp;
```
2)emp 테이블에서 사원이름과 월급을 출력하는데 컬럼명은 "이 름","월 급"으로 바꿔서 출력하시오.
```sql
SELECT ename "이 름",sal "월 급" FROM emp;
```
3)emp 테이블에서 사원번호,사원이름,월급,연봉을 구하고 각각 컬럼명은
"사원번호","사원이름","월급","연봉"으로 출력하시오.
```sql
SELECT empno "사원번호" ,ename "사원이름" ,sal "월급" ,sal*12"연봉" FROM emp; 
```
4)emp 테이블에서 업무를 중복되지 않게 표시하시오.
```sql
SELECT DISTINCT job FROM emp;
```
<br>

---

<br>

5)emp테이블에서 사원번호가 7698인 사원의 이름,업무,급여를 출력하시오.
```sql
SELECT ename, job, sal FROM emp WHERE empno=7698;
```

6)emp테이블에서 사원이름이 SMITH인 사람의 이름과 월급, 부서번호를 구하시오.
```sql
SELECT ename,sal,deptno FROM emp WHERE ename='SMITH';
```

7)월급이 2500이상 3500미만인 사원의 이름,입사일,월급을 구하시오.
```sql
SELECT ename, hiredate, sal FROM emp WHERE sal>=2500 AND sal<3500;
```

8)급여가 2000에서 3000사이에 포함되지 않는 사원의 이름,업무,급여를 
출력하시오.
```sql
SELECT ename, job, sal FROM emp WHERE sal BETWEEN 2000 AND 3000;
```

9)81년05월01일과 81년12월03일 사이에 입사한 사원의 이름,급여,입사일을 출력하시오.
```sql
SELECT ename, sal, hiredate FROM emp 
WHERE hiredate BETWEEN '81-05-01' AND '81-12-03';
```
<br>

---

<br>

10)emp테이블에서 사원번호가 7566,7782,7934인 사원을 제외한 사람들의
사원번호,이름,월급을 출력하시오.
```sql
SELECT empno,ename,sal FROM emp 
WHERE empno NOT IN(7566,7782,7934);
```

11)부서번호 30에서 근무하며 월2,000달러 이하를 받는 81년05월01일 이전에 입사한 사원의 이름,급여,부서번호,입사일을 출력하시오.
```sql
SELECT ename,sal,deptno,hiredate FROM emp
WHERE deptno=30 AND sal<=2000 AND hiredate<'81-05-01';
```

12)emp테이블에서 급여가 $2,000와 $5,000사이고 부서번호가 10 또는 30인 사원의 이름과 급여,부서번호를 나열하시오.
```sql
SELECT ename,sal,deptno FROM emp
WHERE sal BETWEEN 2000 AND 5000 AND deptno IN(10,30);
```

13)업무가 SALESMAN 또는 MANAGER이면서 급여가 $1,600,$2,975,$2,850이 아닌 모든 사원의 이름, 업무 및 급여를 표시하시오.
```sql
SELECT ename,job,sal FROM emp 
WHERE job IN('SALESMAN','MANAGER') AND sal 
NOT IN(1600,2975,2850);
```

14)emp테이블에서 사원이름 중 S가 포함되지 않은 사람들 중 부서번호가 20인 사원들의 이름과 부서번호를 출력하시오
```sql
SELECT ename,deptno FROM emp 
WHERE deptno=20 AND ename NOT LIKE '%S%';
```
<br>

---

<br>

15)emp테이블에서 사원번호,사원이름,입사일을 출력하는데 입사일이 빠른 사람순 으로 정렬하시오.
```sql
SELECT empno,ename,hiredate FROM emp ORDER BY hiredate ASC;
```

16)emp테이블에서 사원이름,급여,연봉을 구하고 연봉이 많은 순으로 정렬하시오.
```sql
SELECT ename,sal,sal*12 FROM emp ORDER BY sal*12 DESC;
```

17)10번 부서 또는 20번 부서에서 근무하고 있는 사원의 이름과 부서번호를 출력하는데 이름을 영문자순으로 표시하시오.
```sql
SELECT ename,deptno FROM emp 
WHERE deptno IN(10,20) ORDER BY ename ASC;
```

18)커미션 계약을 맺은 모든 사원의 이름,급여,커미션을 출력하는데 커미션을 기준으로 내림차순 정렬하시오.
```sql
SELECT ename,sal,comm FROM emp 
WHERE comm IS NOT NULL ORDER BY comm DESC;
```
<br>

---

<br>

19)emp 테이블의 업무(job)을 첫글자는 대문자, 나머지는 소문자로 출력하시오.
```sql
SELECT INITCAP(job) FROM emp; 
```

20)emp 테이블에서 사원이름 중 A가 포함된 사원이름을 구하고 그 이름 중
앞에서 3자만 추출하여 출력하시오.
```sql
SELECT SUBSTR(ename,1,3) FROM emp WHERE ename LIKE '%A%';
```

21)emp 테이블에서 이름의 세번째 문자가 A인 모든 사원의 이름을 표시하시오.
```sql
SELECT ename FROM emp WHERE ename LIKE '__A%';
```

22)emp 테이블에서 이름이 J,A 또는 M으로 시작하는 모든 사원의 이름
(첫 글자는 대문자로, 나머지 글자는 소문자로 표시) 및 이름의 길이를
표시하시오
```sql
SELECT INTITCAP(ename), LENGTH(ename) FROM emp; 
```
23)emp 테이블에서 이름의 글자수가 6자 이상인 사원의 이름을 소문자로 이름만
출력하시오.
```sql
SELECT LOWER(ename) FROM emp WHERE LENGTH(ename)>=6;
```
<br>

---

<br>

24)모든 사원의 이름과 급여를 표시하시오. 급여는 15자 길이로 왼쪽에
$기호가 채워진 형식으로 표기하고 열 레이블을 SALARY로 지정하시오.
```sql
SELECT LPAD(ename,15,'*'),sal SALARY FROM emp;
```

25)오늘부터 이번달의 마지막 날까지의 남은 날 수를 구하시오.
```sql
SELECT TRUNC(LAST_DAY(SYSDATE) -SYSDATE) FROM dual;
```

26)emp 테이블에서 각 사원에 대해 사원번호,이름,급여 및 15% 인상된 급여를 정수(반올림)로 표시하시오. 인상된 급여명의 레이블은 New Salary로 지정하시오.
```sql
SELECT empno,ename,sal,ROUND(sal*0.15) "New Salary" FROM emp; 
```

27)각 사원의 이름을 표시하고 근무 월 수(입사일로부터 현재까지의 월 수)를 계산하여 열레이블은 "근무월수"로 지정하시오. 결과는 정수로 반올림하여 표시하고 근무 월 수를 기준으로 오름차순으로 정렬하시오.
```sql
SELECT ename,ROUND(MONTHS_BETWEEN(SYSDATE,hiredate)) 
근무월수 FROM emp ORDER BY 근무월수 ASC;
```


28)emp테이블에서 이름(소문자로 표시),업무, 근무연차를 출력하시오.
```sql
SELECT LOWER(ename),job,TRUNC((SYSDATE-hiredate)/365) 
근무연차 FROM emp;
```

