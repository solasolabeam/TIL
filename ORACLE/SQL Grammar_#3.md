# SQL ๋ฌธ๋ฒ ์ค์ต_#3 ๐
[์ค์ต]
1)student๋ผ๋ ์ด๋ฆ์ผ๋ก ํ์ด๋ธ ์์ฑ<br>
์ปฌ๋ผ๋ช)    id           name         age        score<br>
๋ฐ์ดํฐํ์) varchar2(10) varchar2(30) number(3)  number(3)<br>
์ ์ฝ์กฐ๊ฑด) primary key | not null | not null | not null
```sql
CREATE TABLE student(
 id varchar2(10) primary key,
 name varchar2(30) not null,
 age number(3) not null,
 score number(3) not null
);
```
2)student ํ์ด๋ธ์ ๋ฐ์ดํฐ๋ฅผ ์๋์ ๊ฐ์ด ์๋ ฅ

|id|name|age|score|
|---|---|---|---|
|dragon|ํ๊ธธ๋|21|100|
|sky | ์ฅ์์ค|22 |99|
|blue|๋ฐ๋ฌธ์|34|88|
   
             
```sql
INSERT INTO student (id,name,age,score) 
VALUES ('dragon','ํ๊ธธ๋',21,100);

INSERT INTO student (id,name,age,score) 
VALUES ('sky','์ฅ์์ค',22,99);

INSERT INTO student (id,name,age,score) 
VALUES ('blue','๋ฐ๋ฌธ์',34,88);
COMMIT;
```

3)student ํ์ด๋ธ์์ ๋ฐ์ดํฐ ์ฝ๊ธฐ
์ฑ์  ํฉ๊ณ ๊ตฌํ๊ธฐ
```sql
SELECT SUM(score) FROM student;
```
<br>

---
<br>

1)empํ์ด๋ธ์์ ์ปค๋ฏธ์ ํญ๋ชฉ์ด ์๋ ฅ๋ ์ฌ์๋ค์ ์ด๋ฆ๊ณผ ๊ธ์ฌ,์ปค๋ฏธ์์
์ถ๋ ฅํ์์ค.
```sql
SELECT ename,sal,comm FROM emp WHERE comm IS NOT NULL;
```
2)์ปค๋ฏธ์ ๊ณ์ฝ์ ๋งบ์ ๋ชจ๋  ์ฌ์์ ์ด๋ฆ,๊ธ์ฌ,์ปค๋ฏธ์์ ์ถ๋ ฅํ๋๋ฐ ์ปค๋ฏธ์์ ๊ธฐ์ค์ผ๋ก ๋ด๋ฆผ์ฐจ์ ์ ๋ ฌํ์์ค.
```sql
SELECT ename,sal,comm FROM emp 
WHERE comm IS NOT NULL ORDER BY comm DESC;
```
3)์๊ธ๊ณผ ์ปค๋ฏธ์์ ํฉ์น ๊ธ์ก์ด 2,000์ด์์ธ ๊ธ์ฌ๋ฅผ ๋ฐ๋ ์ฌ์์ ์ด๋ฆ,์๋ฌด,์๊ธ,์ปค๋ฏธ์,๊ณ ์ฉ๋ ์ง๋ฅผ ์ถ๋ ฅํ์์ค.(๋จ, ๊ณ ์ฉ๋ ์ง๋ 1980-12-17 ํํ๋ก ์ถ๋ ฅํ์์ค)
```sql
SELECT ename,job,sal,comm,
       TO_CHAR(hiredate,'YYYY-MM-DD') hiredate
FROM emp WHERE sal+NVL(comm,0) >= 2000;
```
4)CASE ~ WHEN ~ THEN ๋ฅผ ์ด์ฉํด์ ๋ค์ ๋ฐ์ดํฐ์ ๋ฐ๋ผ JOB ์ด์ ๊ฐ์ ๊ธฐ์ค์ผ๋ก ๋ชจ๋  ์ฌ์์ ๋ฑ๊ธ์ ํ์ํ์์ค.

|์๋ฌด | ๋ฑ๊ธ|
|:---:|:---:|
|PRESIDENT | A|
|ANALYST|  B|
|MANAGER|  C|
|SALESMAN| D|
|CLERK|  E|
|๊ธฐํ  | 0|

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
       
5)30๋ฒ ๋ถ์์์ ๊ทผ๋ฌดํ๋ ์ฌ์๋ค์ ๋ถ์๋ฒํธ, ๋ถ์์ด๋ฆ, ์ฌ์์ด๋ฆ,์๊ธ,๊ธ์ฌ๋ฑ๊ธ์ ์ถ๋ ฅํ์์ค.
```sql
SELECT e.deptno, d.dname, e.ename, e.sal, s.grade
FROM emp e INNER JOIN dept d
ON e.deptno=d.deptno
INNER JOIN salgrade s
ON e.sal BETWEEN s.losal AND s.hisal
WHERE e.deptno=30;
```
6)ALLEN๋ณด๋ค ๊ธ์ฌ๋ฅผ ๋ง์ด ๋ฐ๋ ์ฌ๋ ์ค์์ ์์ฌ์ผ์ด ๊ฐ์ฅ ๋น ๋ฅธ ์ฌ์๊ณผ ๋์ผํ ๋ ์ง์ ์์ฌํ ์ฌ์์ ์ด๋ฆ๊ณผ ์์ฌ์ผ,๊ธ์ฌ๋ฅผ ์ถ๋ ฅํ์์ค.
```sql
SELECT ename,hiredate, sal FROM emp
WHERE hiredate = (SELECT MIN(hiredate) FROM emp 
WHERE sal >(SELECT sal FROM emp WHERE ename='ALLEN'));
```
