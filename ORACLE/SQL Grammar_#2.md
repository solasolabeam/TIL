# SQL λ¬Έλ² μ€μ΅_#2 π

1)λͺ¨λ  μ¬μμ κΈμ¬ μ΅κ³ μ‘,μ΅μ μ‘,μ΄μ‘ λ° νκ· μ‘μ νμνκ³  μ΄ λ μ΄λΈμ κ°κ° maximum,minimum,sum λ° averageλ‘ μ§μ νκ³  κ²°κ³Όλ₯Ό μ μλ‘ λ°μ¬λ¦Όνκ³  μΈμλ¦¬ λ¨μλ‘ ,λ₯Ό λͺμνμμ€.
```sql
SELECT 
MAX(sal)maximum,
MIN(sal)minimum,
TO_CHAR(ROUND(AVG(sal)),'9,999')average 
FROM emp;
```
<br>

2)empνμ΄λΈμμ κΈμ¬μ μ»€λ―Έμμ λν κΈμ‘μ μ΅κ³ ,μ΅μ ,νκ· κΈμ‘μ κ΅¬νμμ€.
νκ· κΈμ‘μ μμμ  μ²«μ§Έμλ¦¬κΉμ§ νμνμμ€.
```sql
SELECT MAX(sal+NVL(comm,0)),MIN(sal+NVL(comm,0)),
ROUND(AVG(sal+NVL(comm,0)),1)FROM emp;
```
<br>

3)μλ¬΄κ° λμΌν(μλ¬΄λ³) μ¬μμλ₯Ό νμνμμ€.
```sql
SELECT job,COUNT(*) FROM emp GROUP BY job;
```
<br>

4)empνμ΄λΈμμ 30λ²λΆμμ μ¬μμλ₯Ό κ΅¬νμμ€.
```sql
SELECT COUNT(*) FROM emp WHERE deptno=30;
```
<br>


5)empνμ΄λΈμμ μλ¬΄λ³ μ΅κ³  μκΈμ κ΅¬νκ³  μλ¬΄,μ΅κ³  μκΈμ μΆλ ₯νμμ€.
```sql
SELECT job,MAX(sal) FROM emp GROUP BY job ;
```
<br>


6)empνμ΄λΈμμ λΆμλ³λ‘ μ§κΈλλ μ΄μκΈμμ κΈμ‘μ΄ 9,000μ΄μμΈ μ΄μκΈμ λ°λ λΆμλ²νΈ,μ΄μκΈμ μΆλ ₯νμμ€
```sql
SELECT deptno, SUM(sal) FROM emp 
GROUP BY deptno HAVING SUM(sal)>=9000;
```
<br>

7)empνμ΄λΈμμ μλ¬΄λ³λ‘ μ¬λ²μ΄ μ μΌ λ¦μ μ¬λμ κ΅¬νκ³  κ·Έ κ²°κ³Όλ΄μμ
μ¬λ²μ΄ 79λ‘ μμνλ κ²°κ³Όλ§ μΆλ ₯νμμ€.
```sql
SELECT job, MAX(empno) FROM emp 
GROUP BY job HAVING MAX(empno) LIKE '79%';
```
<br>

8)empνμ΄λΈμμ μλ¬΄λ³ μ΄μκΈμ μΆλ ₯νλλ° μλ¬΄κ° 'MANAGER'μΈ μ¬μλ€μ
μ μΈνκ³  μ΄μκΈμ΄ 5,000λ³΄λ€ λ§μ μλ¬΄μ μ΄μκΈμ μΆλ ₯νμμ€.
```sql
SELECT job,SUM(sal) FROM emp 
WHERE job!='MANAGER' GROUP BY job HAVING SUM(sal)>5000;
```
<br>

9)empνμ΄λΈμμ μλ¬΄λ³ μ¬μμ μκ° 4λͺ μ΄μμΈ μλ¬΄μ μΈμμλ₯Ό μΆλ ₯νμμ€.
```sql
SELECT job,COUNT(*) FROM emp 
GROUP BY job HAVING COUNT(*)>=4;
```
<br>


10)empνμ΄λΈμμ λΆκΈ°λ³λ‘ μμ¬ν μ¬μμλ₯Ό κ΅¬νλλ° 2λΆκΈ°μ μμ¬ν μ¬μμλ§ κ΅¬νμμ€.(TO_CHAR()μ¬μ©νκΈ°)
```sql
SELECT TO_CHAR(HIREDATE,'Q')λΆκΈ°,COUNT(*) μ¬μμ FROM emp 
GROUP BY TO_CHAR(HIREDATE,'Q') HAVING TO_CHAR(HIREDATE,'Q')=2;
```
<br>

---
<br>

1)λͺ¨λ  μ¬μμ μ΄λ¦, λΆμλ²νΈ, λΆμμ΄λ¦μ νμνμμ€.(emp,dept)
```sql
SELECT e.ename,e.job,d.dname,d.loc
FROM emp e, dept d
WHERE e.deptno=d.deptno;
```

2)μλ¬΄κ° MANAGER μΈ μ¬μμ μ λ³΄λ₯Ό μ΄λ¦,μλ¬΄,λΆμλͺ,κ·Όλ¬΄μ§ μμΌλ‘ μΆλ ₯νμμ€.(emp,dept)
```sql
SELECT e.ename,e.job,d.dname,d.loc
FROM emp e, dept d
WHERE e.deptno=d.deptno AND e.job='MANAGER';
```
<br>


3)μ»€λ―Έμμ λ°κ³  κΈμ¬κ° 1,600μ΄μμΈ μ¬μμ μ¬μμ΄λ¦,κΈμ¬,λΆμλͺ,κ·Όλ¬΄μ§λ₯Ό μΆλ ₯νμμ€.(emp,dept)
```sql
SELECT e.ename,e.sal,d.dname,d.loc
FROM emp e, dept d
WHERE e.deptno=d.deptno AND comm IS NOT NULL AND e.sal>=1600;
```
<br>

4)κ·Όλ¬΄μ§κ° CHICAGOμΈ λͺ¨λ  μ¬μμ μ΄λ¦,μλ¬΄,λΆμλ²νΈ λ° λΆμμ΄λ¦μ νμνμμ€
```sql
SELECT e.ename,e.job,e.deptno,d.dname
FROM emp e, dept d
WHERE e.deptno=d.deptno AND d.loc='CHICAGO';
```
<br>


5)κ·Όλ¬΄μ§(loc)λ³λ‘ κ·Όλ¬΄νλ μ¬μμ μκ° 5λͺ μ΄νμΈ κ²½μ°, μΈμμ΄ μ μΈ λμ μμΌλ‘ μ λ ¬νμμ€.(κ·Όλ¬΄ μΈμμ΄ 0λͺμΈ κ³³λ νμ)
```sql
SELECT d.loc,COUNT(e.ename) 
FROM emp e, dept d
WHERE e.deptno(+) = d.deptno 
GROUP BY d.loc HAVING COUNT(e.ename)<=5 
ORDER BY d.loc ASC;
```
