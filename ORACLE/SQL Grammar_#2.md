# SQL 문법 실습_#2 📌

1)모든 사원의 급여 최고액,최저액,총액 및 평균액을 표시하고 열 레이블은 각각 maximum,minimum,sum 및 average로 지정하고 결과를 정수로 반올림하고 세자리 단위로 ,를 명시하시오.
```sql
SELECT 
MAX(sal)maximum,
MIN(sal)minimum,
TO_CHAR(ROUND(AVG(sal)),'9,999')average 
FROM emp;
```
<br>

2)emp테이블에서 급여와 커미션을 더한 금액의 최고,최저,평균금액을 구하시오.
평균금액은 소수점 첫째자리까지 표시하시오.
```sql
SELECT MAX(sal+NVL(comm,0)),MIN(sal+NVL(comm,0)),
ROUND(AVG(sal+NVL(comm,0)),1)FROM emp;
```
<br>

3)업무가 동일한(업무별) 사원수를 표시하시오.
```sql
SELECT job,COUNT(*) FROM emp GROUP BY job;
```
<br>

4)emp테이블에서 30번부서의 사원수를 구하시오.
```sql
SELECT COUNT(*) FROM emp WHERE deptno=30;
```
<br>


5)emp테이블에서 업무별 최고 월급을 구하고 업무,최고 월급을 출력하시오.
```sql
SELECT job,MAX(sal) FROM emp GROUP BY job ;
```
<br>


6)emp테이블에서 부서별로 지급되는 총월급에서 금액이 9,000이상인 총월급을 받는 부서번호,총월급을 출력하시오
```sql
SELECT deptno, SUM(sal) FROM emp 
GROUP BY deptno HAVING SUM(sal)>=9000;
```
<br>

7)emp테이블에서 업무별로 사번이 제일 늦은 사람을 구하고 그 결과내에서
사번이 79로 시작하는 결과만 출력하시오.
```sql
SELECT job, MAX(empno) FROM emp 
GROUP BY job HAVING MAX(empno) LIKE '79%';
```
<br>

8)emp테이블에서 업무별 총월급을 출력하는데 업무가 'MANAGER'인 사원들은
제외하고 총월급이 5,000보다 많은 업무와 총월급을 출력하시오.
```sql
SELECT job,SUM(sal) FROM emp 
WHERE job!='MANAGER' GROUP BY job HAVING SUM(sal)>5000;
```
<br>

9)emp테이블에서 업무별 사원의 수가 4명 이상인 업무와 인원수를 출력하시오.
```sql
SELECT job,COUNT(*) FROM emp 
GROUP BY job HAVING COUNT(*)>=4;
```
<br>


10)emp테이블에서 분기별로 입사한 사원수를 구하는데 2분기에 입사한 사원수만 구하시오.(TO_CHAR()사용하기)
```sql
SELECT TO_CHAR(HIREDATE,'Q')분기,COUNT(*) 사원수 FROM emp 
GROUP BY TO_CHAR(HIREDATE,'Q') HAVING TO_CHAR(HIREDATE,'Q')=2;
```
<br>

---
<br>

1)모든 사원의 이름, 부서번호, 부서이름을 표시하시오.(emp,dept)
```sql
SELECT e.ename,e.job,d.dname,d.loc
FROM emp e, dept d
WHERE e.deptno=d.deptno;
```

2)업무가 MANAGER 인 사원의 정보를 이름,업무,부서명,근무지 순으로 출력하시오.(emp,dept)
```sql
SELECT e.ename,e.job,d.dname,d.loc
FROM emp e, dept d
WHERE e.deptno=d.deptno AND e.job='MANAGER';
```
<br>


3)커미션을 받고 급여가 1,600이상인 사원의 사원이름,급여,부서명,근무지를 출력하시오.(emp,dept)
```sql
SELECT e.ename,e.sal,d.dname,d.loc
FROM emp e, dept d
WHERE e.deptno=d.deptno AND comm IS NOT NULL AND e.sal>=1600;
```
<br>

4)근무지가 CHICAGO인 모든 사원의 이름,업무,부서번호 및 부서이름을 표시하시오
```sql
SELECT e.ename,e.job,e.deptno,d.dname
FROM emp e, dept d
WHERE e.deptno=d.deptno AND d.loc='CHICAGO';
```
<br>


5)근무지(loc)별로 근무하는 사원의 수가 5명 이하인 경우, 인원이 적인 도시 순으로 정렬하시오.(근무 인원이 0명인 곳도 표시)
```sql
SELECT d.loc,COUNT(e.ename) 
FROM emp e, dept d
WHERE e.deptno(+) = d.deptno 
GROUP BY d.loc HAVING COUNT(e.ename)<=5 
ORDER BY d.loc ASC;
```
