# π SQL λ¬Έλ² μ€μ΅_#4 

1)λ μ«μλ₯Ό μ κ³΅νλ©΄ λ§μμ ν΄μ κ²°κ³Όκ°μ λ°ννλ ν¨μλ₯Ό μ μνμμ€.
ν¨μλͺ : add_num
```sql
create or replace function add_num(num1 integer,
                                   num2 integer)
  return integer
is
begin
  return num1 + num2;
end;
```
```sql
SELECT ADD_NUM(2,5) FROM dual;
SELECT ename, ADD_NUM(sal,NVL(comm,0)) μ€κΈμ¬ FROM emp;
```
2)λΆμλ²νΈλ₯Ό μλ ₯νλ©΄ ν΄λΉ λΆμμμ κ·Όλ¬΄νλ μ¬μμλ₯Ό λ°ννλ ν¨μλ₯Ό
μ μνμμ€.
ν¨μλͺ : get_emp_count
```sql
create or replace function get_emp_count(
                                 dept_no emp.deptno%type)
  return integer
is
  emp_count integer;
begin
  SELECT COUNT(empno)
  INTO emp_count
  FROM emp WHERE deptno=dept_no;
  
  return emp_count;
end;
```
```sql
SELECT deptno, dname, GET_EMP_COUNT(deptno) μ¬μμ FROM dept;
```
3)empνμ΄λΈμ μμ¬μμ μλ ₯νλ©΄ κ·Όλ¬΄μ°μ°¨λ₯Ό κ΅¬νλ ν¨μλ₯Ό μ μνμμ€.
(μμμ  μλ¦¬ μ μ­)
ν¨μλͺ : get_info_hiredate
```sql
create or replace function get_info_hiredate(
                                  hire_date emp.hiredate%type)
  return number
is
begin
  return TRUNC(MONTHS_BETWEEN(SYSDATE,hire_date)/12);
end;
```
```sql
SELECT ename, GET_INFO_HIREDATE(hiredate) κ·Όλ¬΄μ°μ°¨ FROM emp;
```


4)empνμ΄λΈμ μ΄μ©ν΄μ μ¬μλ²νΈλ₯Ό μλ ₯νλ©΄ ν΄λΉ μ¬μμ κ΄λ¦¬μ μ΄λ¦μ
κ΅¬νλ ν¨μλ₯Ό μ μνμμ€.

ν¨μλͺ : get_mgr_name
```sql
create or replace function get_mgr_name(emp_no emp.empno%type)
  return varchar2
is
  m_name varchar2(10);
begin
  SELECT ename
  INTO m_name
  FROM emp WHERE empno = (SELECT mgr FROM emp 
                          WHERE empno=emp_no);
  return m_name;                        
end;

------------------------------------------------

create or replace function get_mgr_name(emp_no emp.empno%type)
  return varchar2
is
  m_name varchar2(10);
begin
  SELECT m.ename
  INTO m_name
  FROM emp e, emp m
  WHERE e.mgr = m.empno
  AND e.empno = emp_no;
  
  return m_name;
end;
```
```sql
SELECT GET_MGR_NAME(7369) FROM dual;
SELECT empno,ename,GET_MGR_NAME(empno) FROM emp;
```
5)empνμ΄λΈμ μ΄μ©ν΄μ μ¬μλ²νΈλ₯Ό μλ ₯νλ©΄ κΈμ¬λ±κΈμ κ΅¬νλ ν¨μλ₯Ό
μ μνμμ€.(caseλ¬Έ μ΄μ©, 4000μ΄μ(A),3000μ΄μ4000λ―Έλ§(B),
        2000μ΄μ3000λ―Έλ§(C),1000μ΄μ2000λ―Έλ§(D) λλ¨Έμ§ F)
ν¨μλͺ : get_sal_grade      
```sql
create or replace function get_sal_grade(emp_no emp.empno%type)
  return char
is
  sgrade char(1);
begin
  SELECT CASE WHEN sal>=4000 THEN 'A'
              WHEN sal>=3000 AND sal<4000 THEN 'B'
              WHEN sal>=2000 AND sal<3000 THEN 'C'
              WHEN sal>=1000 AND sal<2000 THEN 'D'
              ELSE 'F'
        END grade -- SQLλ¬Έμ₯ μμμλ END CASE X, END O
  INTO sgrade
  FROM emp
  WHERE empno = emp_no;
  return sgrade;
end;

SELECT ename, sal, GET_SAL_GRADE(empno) κΈμ¬λ±κΈ FROM emp;

-----------------------------

create or replace function get_sal_grade2(emp_no emp.empno%type)
  return number
is
  sgrade number;
begin
  SELECT s.grade
  INTO sgrade
  FROM emp e, salgrade s
  WHERE e.sal BETWEEN s.losal AND S.hisal
  AND e.empno = emp_no;
  
  return sgrade; 
end;
```
```sql
SELECT ename, sal, GET_SAL_GRADE2(empno) κΈμ¬λ±κΈ FROM emp;
```
6)μ¬μλ²νΈλ₯Ό μλ ₯νλ©΄ κ·Όλ¬΄μ§λ₯Ό κ΅¬νλ ν¨μ
ν¨μλͺ : find_loc
```sql
create or replace function find_loc(emp_no emp.empno%type)
  return varchar2
is
  dept_loc varchar2(14);
begin
  SELECT d.loc
  INTO dept_loc
  FROM emp e INNER JOIN dept d
  ON e.deptno = d.deptno
  WHERE e.empno = emp_no;
  
  return dept_loc;
end;
```
```sql
SELECT FIND_LOC(7698) FROM dual;
SELECT empno, ename, FIND_LOC(empno) FROM emp;
```
