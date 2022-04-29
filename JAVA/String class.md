# String
## String
-  문자열 객체
- 문자열 수정 불가능(불변적 특징)
- -,+ 연산자를 이용하여 새로운 문자열 객체 생성
```java
        int a=2;
		char b='A';
		
        String str=a+"";
		str+=b;
		
```
## String의 명시적 생성과 암시적 생성
```java
//암시적으로 문자열 생성
		String str1 ="abc";
		String str2 ="abc";
		
		//객체 비교
		if(str1 == str2) {
			System.out.println("str1과 str2는 같은 객체");			
		}
		else {
			System.out.println("str1과 str2는 다른 객체");	
		}
		
		//문자열 비교
		if(str1.equals(str2))
			System.out.println("str1과 str2는 같은 문자열.");
		else
			System.out.println("str1과 str2는 다른 문자열.");
		
		//명시적 문자열 생성
		String str3 = new String("Hello");
		String str4 = new String("Hello");
		
		//객체 비교
		if(str3 == str4) {
			System.out.println("str3과 str4는 같은 객체");			
		}
		else {
			System.out.println("str3과 str4는 다른 객체");	
		}
```
#### 출력 결과
```java
str1과 str2는 같은 객체
str1과 str2는 같은 문자열.
str3과 str4는 다른 객체
str3과 str4는 같은 문자열.
```
명시적 생성한 문자열 str1과 str2는 서로 같은 객체를 가르키고 (주소값 공유)
암시적 생성한 문자열 str3과 str4는 개별의 주소값을 가지고 있기 때문이다
# StringBuffer
## StringBuffer
- 문자열 버퍼 객체
- 문자열 추가 변경 가능
- append() 메서드를 이용하여 문자(열) 추가
```java
StringBuffer sb = new StringBuffer("여름 덥다!!");
		System.out.println("1:" + sb);
		
		//문자를 지정한 인덱스 삽입
		sb.insert(2, '이');
		System.out.println("2:" + sb);
		
		//문자열 뒤에 지정한 문자열을 연결(저장)
		sb.append("가을은 ");
		System.out.println("3:" + sb);
		
		sb.append("시원하다");
		System.out.println("4:" + sb);
		
		//지정한 인덱스 범위(시작 인덱스부터 끝 인덱스전까지)의 문자열을 지정한 문자열로 대체
		sb.replace(0,3, "여행가자!!");
		System.out.println("5:" + sb);
		
		//인덱스를 지정해서 문자 삭제
		sb.deleteCharAt(0);
		System.out.println("6:" + sb);
		
		//시작 인덱스부터 끝 인덱스전까지의 문자열 삭제
		sb.delete(0, 3);
		System.out.println("7:" + sb);
		             //StringBuffer-> String
		String str = sb.toString();
		System.out.println("str:" + str);
```
#### 출력 결과
```java
1:여름 덥다!!
2:여름이 덥다!!
3:여름이 덥다!!가을은 
4:여름이 덥다!!가을은 시원하다
5:여행가자!! 덥다!!가을은 시원하다
6:행가자!! 덥다!!가을은 시원하다
7:!! 덥다!!가을은 시원하다
str:!! 덥다!!가을은 시원하다
```
# indexOf()
```java
String s1 = "Kwon Sun Ae";
		// 012345678910, 문자열길이 11

		// indexOf : 문자 또는 문자열의 index 반환
		int index = s1.indexOf('n');
		System.out.println("맨 처음 문자 n의 위치 : " + index);

		index = s1.indexOf("Sun");
		System.out.println("문자열 Sun의 위치 : " + index);
```
#### 출력 결과
```java
맨 처음 문자 n의 위치 : 3
문자열 Sun의 위치 : 5
```
# charAt()
```java
String s1 = "Kwon Sun Ae";
		// 012345678910, 문자열길이 11


		// charAt : 인덱스를 이용해서 문자를 추출
		char c = s1.charAt(2);
		System.out.println("추출한 문자 : " + c);
```
#### 출력 결과
```java
추출한 문자 : o
```
# substring()
```java
String s1 = "Kwon Sun Ae";
		// 012345678910, 문자열길이 11

		String str = s1.substring(1);
		System.out.println("인덱스 1 부터 끝가지 문자열 추출 : " + str);

		// substring : 시작 인덱스부터 끝 인덱스전까지 마지막 인덱스까지
		str = s1.substring(5, 7);
		System.out.println("인덱스 5부터 7까지 문자열 추출 : " + str);
```
#### 출력 결과
```java
인덱스 1 부터 끝가지 문자열 추출 : won Sun Ae
인덱스 5부터 7까지 문자열 추출 : Su
```
# length()
```java
String s1 = "Kwon Sun Ae";
		// 012345678910, 문자열길이 11
		
		// 문자열의 길이
		int length = s1.length();
		System.out.println("s1의 길이 : " + length);
```
#### 출력 결과
```java
s1의 길이 : 11
```
# split()
```java
String s1 = "Kwon Sun Ae";
		// 012345678910, 문자열길이 11
		
		// 구분자를 이용해서 문자열을 잘라내기
		String[] array = s1.split("");
		for (int i = 0; i < array.length; i++) {
			System.out.println("array[" + i + "]" + array[i]);
```
#### 출력 결과
```java
array[0]K
array[1]w
array[2]o
array[3]n
array[4] 
array[5]S
array[6]u
array[7]n
array[8] 
array[9]A
array[10]e
```
# toUpperCase()
```java
String s1 = "  aBa  ";

		String msg = null;
		
		//소문자를 대문자로 변경
		msg = s1.toUpperCase();
		System.out.println("msg:" + msg);
```
#### 출력 결과
```java
msg:  ABA 
```
# toLowerCase()
```java
String s1 = "  aBa  ";

		String msg = null;
		
		//대문자를 소문자 변경
		msg = s1.toLowerCase();
		System.out.println("msg:" + msg);
```
#### 출력 결과
```java
msg:  aba  
```
# replace()
```java
String s1 = "  aBa  ";

		String msg = null;
				
		//특정 문자를 원하는 문자를 변경
		msg = s1.replace("aB","b");
		System.out.println("msg:" + msg);
```
#### 출력 결과
```java
msg:  ba  
```
# trim()
```java
String s1 = "  aBa  ";

		String msg = null;
						
		//앞뒤 공백 제거
		msg = s1.trim();
		System.out.println("msg:" + msg);
```
#### 출력 결과
```java
msg:aBa
```
# contains()
```java
String s1 = "  aBa  ";

		String msg = null;
						
		//문자열에서 특정 문자열이 포함되어 있는지 여부 확인
		boolean f = s1.contains("aB");
		System.out.println("f: " + f);
```
#### 출력 결과
```java
f: true
```
# startsWith()
```java
String s1 = "aBa";

		String msg = null;
								
		//문자열이 특정 문자열로 시작하는지 여부 확인
		boolean f;
		f = s1.startsWith("aB");
		System.out.println("f: " + f);
```
#### 출력 결과
```java
f: true
```
# endsWith()
```java
String s1 = "aBa";

		String msg = null;
								
		//문자열이 특정 문자열로 끝나는지 여부 확인
		boolean f;
		f = s1.endsWith("Ba");
		System.out.println("f: " + f);
```
#### 출력 결과
```java
f: true
```
# valueOf()
```java
        int a =100;

		String msg = null;
    
		//int -> String
		msg = String.valueOf(a); //100 -> "100"
		msg = a + "";//""는 빈문자열, 100 -> "100"
```

