# Calendar 클래스
> - Date 클래스와 마찬가지로 날짜와 시간을 다루는 클래스이다
- 추상 클래스 라 객체 생성 불가 
- Calendar.getInstance() 메소드를 이용하거나 Calendar 클래스를 상속받는 GregorianCalendar 클래스를 이용하여 객체를 생성

### 예시 코드
```java
package kr.s05.date;

import java.util.Calendar;

public class CalendarMain01 {
	public static void main(String[] args) {
		Calendar today = Calendar.getInstance();
		System.out.println(today);
		
		int year = today.get(Calendar.YEAR);//연도
		int month = today.get(Calendar.MONTH) + 1;//월 0~11
		int date = today.get(Calendar.DATE);//일
		
		System.out.printf("%d년%d월%d일 ",year,month,date);
		
		int day = today.get(Calendar.DAY_OF_WEEK);//요일 1~7
		
		String nday = "";
		switch(day) {
		case 1: nday = "일";break;
		case 2: nday = "월";break;
		case 3: nday = "화";break;
		case 4: nday = "수";break;
		case 5: nday = "목";break;
		case 6: nday = "금";break;
		case 7: nday = "토";break;
		}
		System.out.print(nday+"요일 ");
		
		int amPm = today.get(Calendar.AM_PM);//오전 0, 오후 1
		int hour = today.get(Calendar.HOUR);//시(12시 표기), HOUR_OF_DAY (24시 표기)
		int min = today.get(Calendar.MINUTE);//분
		int sec = today.get(Calendar.SECOND);//초
		
		String str = amPm == Calendar.AM ? "오전" : "오후";
		System.out.printf("%s %d시%d분%d초",str,hour,min,sec);
		
	}
}
```
#### 출력 결과
```
java.util.GregorianCalendar[time=1651320633844,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Seoul",offset=32400000,dstSavings=0,useDaylight=false,transitions=30,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2022,MONTH=3,WEEK_OF_YEAR=18,WEEK_OF_MONTH=5,DAY_OF_MONTH=30,DAY_OF_YEAR=120,DAY_OF_WEEK=7,DAY_OF_WEEK_IN_MONTH=5,AM_PM=1,HOUR=9,HOUR_OF_DAY=21,MINUTE=10,SECOND=33,MILLISECOND=844,ZONE_OFFSET=32400000,DST_OFFSET=0]
2022년4월30일 토요일 오후 9시10분33초
```
# 달력 프로그램
```java
package kr.s05.date;

import java.util.Calendar;
import java.util.Scanner;

public class CalendarMain02 {
	public static void main(String[] args) {
		Scanner input = new Scanner(System.in);
		
		//현재 날짜와 시간을 구함
		Calendar cal = Calendar.getInstance();
		System.out.println("희망 연도와 월을 입력하세요!!(ex 연도:2022,월:4)");
		System.out.print("연도:");
		int year = input.nextInt();
		System.out.print("월:");
		int month = input.nextInt();
		
		System.out.println("    [ " + year + "년 " + month + "월]");
		System.out.println("===========================");
		System.out.println("  일  월 화 수  목 금  토");
		
		//희망 연도,월,일 셋팅(월의 범위는 0~11이기 때문에 입력월-1)
		cal.set(year, month-1,1);
		
		//달력은 1일부터 시작하기 때문에 1일의 요일을 구함
		int week = cal.get(Calendar.DAY_OF_WEEK);//일(1) ~ 토(7)
		//마지막 날짜 구하기
		int lastOfDate = cal.getActualMaximum(Calendar.DATE);
		
		//1일전에 공백 만들기
		for(int i=1;i<week;i++) {
			System.out.printf("%3s", " ");
		}
		
		//1일부터 말일까지 반복하면서 숫자를 출력
		for(int i=1;i<=lastOfDate;i++) {
			System.out.printf("%3d", i);
			if(week%7==0) System.out.println();
			week++;
		}
		System.out.println("\n=========================");
		
		input.close();
	}
}
```
#### 출력 결과
```
희망 연도와 월을 입력하세요!!(ex 연도:2022,월:4)
연도:2022
월:4
    [ 2022년 4월]
===========================
  일  월 화 수  목 금  토
                 1  2
  3  4  5  6  7  8  9
 10 11 12 13 14 15 16
 17 18 19 20 21 22 23
 24 25 26 27 28 29 30

=========================
```



