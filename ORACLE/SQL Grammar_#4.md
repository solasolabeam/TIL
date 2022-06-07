# 📌 SQL 문법 실습_#4 

1)두 숫자를 제공하면 덧셈을 해서 결과값을 반환하는 함수를 정의하시오.
함수명 : add_num
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
SELECT ename, ADD_NUM(sal,NVL(comm,0)) 실급여 FROM emp;
```
2)부서번호를 입력하면 해당 부서에서 근무하는 사원수를 반환하는 함수를
정의하시오.
함수명 : get_emp_count
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
SELECT deptno, dname, GET_EMP_COUNT(deptno) 사원수 FROM dept;
```
3)emp테이블의 입사입을 입력하면 근무연차를 구하는 함수를 정의하시오.
(소수점 자리 절삭)
함수명 : get_info_hiredate
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
SELECT ename, GET_INFO_HIREDATE(hiredate) 근무연차 FROM emp;
```


4)emp테이블을 이용해서 사원번호를 입력하면 해당 사원의 관리자 이름을
구하는 함수를 정의하시오.

함수명 : get_mgr_name
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
5)emp테이블을 이용해서 사원번호를 입력하면 급여등급을 구하는 함수를
정의하시오.(case문 이용, 4000이상(A),3000이상4000미만(B),
        2000이상3000미만(C),1000이상2000미만(D) 나머지 F)
함수명 : get_sal_grade      
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
        END grade -- SQL문장 안에서는 END CASE X, END O
  INTO sgrade
  FROM emp
  WHERE empno = emp_no;
  return sgrade;
end;

SELECT ename, sal, GET_SAL_GRADE(empno) 급여등급 FROM emp;

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
SELECT ename, sal, GET_SAL_GRADE2(empno) 급여등급 FROM emp;
```
6)사원번호를 입력하면 근무지를 구하는 함수
함수명 : find_loc
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
