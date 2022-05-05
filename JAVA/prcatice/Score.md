> 학생의 이름, 3과목 성적을 입력받아 평균점수와 등급을 출력하는 프로그램

## Score 클래스
이름, 국어 성적, 영어 성적, 수학 성적, 합 메서드(makeSum), 평균 메서드(makeAvg), 등급 계산(makeGrade)메서드 필드로 구성

```java
public class Score {
	
	private String name;
	private int korean;
	private int english;
	private int math;
	public String getName() {
		return name;
	}
	public int getKorean() {
		return korean;
	}
	public int getEnglish() {
		return english;
	}
	public int getMath() {
		return math;
	}	

	public void setName(String name) {
		this.name = name;
	}
	public void setKorean(int korean) {
		this.korean = korean;
	}
	public void setEnglish(int english) {
		this.english = english;
	}
	public void setMath(int math) {
		this.math = math;
	}
	
	public int makeSum() {
		return korean+english+math;
	}
	public double makeAvg() {
		return makeSum()/3.0;
	}
	public String makeGrade() {
		//if(make)
		double num=makeAvg();
		if(num>=90 && num<=100) {
			return "A";
		}
		else if(num>=80 && num<90) {
			return "B";
		}
		else if(num>=70 && num<80) {
			return "C";
		}
		else if(num>=60 && num<70) {
			return "D";
		}
		else {
			return "F";
		}
	}
	public static void main(String[] args) {
		Score t =new Score();
		t.korean=90;
		t.english=80;
		t.math=90;
		System.out.println(t.makeSum());
		System.out.println(t.makeAvg());
		System.out.println(t.makeGrade());
	}
	
}
```
## ArrayListMain 클래스
- Score 객체를 생성하고, 입력 방식은 BufferedReader로 입력받아 성적입력, 성적출력 메뉴기능 구현
- 음수 값, 문자 형태의 입력 등 올바르지 않은 형식은 예외 처리
```java
package kr.s01.list;

import java.util.ArrayList;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class ArrayListMain10 {
	BufferedReader br;
	ArrayList<Score> mlist;
	Score in = new Score();
	public ArrayListMain10() {
		
		mlist = new ArrayList<Score>();
		try {
			br = new BufferedReader(new InputStreamReader(System.in));
			// 메뉴 호출
			callMenu();
		} catch (IOException e) {
			e.printStackTrace();// 예외 문구 출력
		} catch (Exception e) {
			e.printStackTrace();// 예외 문구 출력
		} finally {
			if (br != null)
				try {
					br.close();
				} catch (IOException e) {
				}

		}
	}

	// 메뉴 만들기
	public void callMenu() throws IOException {
		while(true) {
			System.out.print("1.성적입력,2성적출력,3.종료");
			System.out.print("메뉴선택:");
			try {
				int num = Integer.parseInt(br.readLine());
				if(num == 1){//성적 입력
					inputScore();
				}else if(num==2) {//성적출력
					printScore();
					
				}else if(num==3) {//종료
					System.out.println("종료 합니다");
					break;
				}else {
					System.out.println("잘못 입력했습니다");
				}
			}catch(NumberFormatException e) {
				System.out.println("숫자만 입력해주세요");
			}
		}
	}

	// 성적 입력
	public void inputScore() throws IOException {
		//Score 객체 생성
				Score s =new Score();
				//이름 입력
				System.out.print("이름 :");
				s.setName(br.readLine());

				//국어 입력
				s.setKorean(parseInputData("국어 :"));
				//영어 입력
				s.setEnglish(parseInputData("영어 :"));
			    //영어 입력
				s.setMath(parseInputData("수학 :"));
				//ArrayList에 Score 객체 저장 중요!!
				mlist.add(s);
				
	}
	//성적 입력 조건 체크
	public int parseInputData(String course) throws IOException{
		while(true) {
			System.out.print(course);
		
		try {
			int num = Integer.parseInt(br.readLine());
			
			//성적 유효 범위(0~100) 체크
			if(num<0 || num>100) {
				throw new ScoreValueException("0~100사이의 값만 인정");
			}
			return num;
		}catch(NumberFormatException e) {
			System.out.println("숫자만 입력하세요");
		}catch(ScoreValueException e) {
			System.out.println(e.getMessage());
		}
	}
	}
	// 성적 출력
	public void printScore() {
		//이름,국어,영어,수학,총점,평균,등급 출력
		System.out.println("---------------------------------------");
		System.out.println("이름\t국어\t수학\t영어\t총점\t평균\t등급");
		System.out.println("---------------------------------------");
		for(Score s : mlist) {
			System.out.print(s.getName()+"\t");
			System.out.print(s.getKorean()+"\t");
			System.out.print(s.getEnglish()+"\t");
			System.out.print(s.getMath()+"\t");
			System.out.print(s.makeSum()+"\t");
			System.out.printf("%.2f\t",s.makeAvg());
			System.out.println(s.makeGrade());
			
		}
	}

	public static void main(String[] args) {
		new ArrayListMain10();
	}
}
```
<br>

### 향상된 for문 대체


```java
// 성적 출력
	public void printScore() {
		//이름,국어,영어,수학,총점,평균,등급 출력
		System.out.println("---------------------------------------");
		System.out.println("이름\t국어\t수학\t영어\t총점\t평균\t등급");
		System.out.println("---------------------------------------");
		for(int i=0; i<mlist.size(); i++) {
			System.out.print(mlist.get(i).getName()+"\t");
			System.out.print(mlist.get(i).getKorean()+"\t");
			System.out.print(mlist.get(i).getEnglish()+"\t");
			System.out.print(mlist.get(i).getMath()+"\t");
			System.out.print(mlist.get(i).makeSum()+"\t");
			System.out.printf("%.2f\t",mlist.get(i).makeAvg());
			System.out.println(mlist.get(i).makeGrade());
			System.out.println("Arraylist size : "+mlist.size());
			
		}
	}
```
이런 방식으로 바꿔서 정의 할 수 있다






## ScoreValueException 클래스
```java
package kr.s01.list;

//성적 범위가 0~100 사이가 아니면 예외가 발생, 사용자 정의 예외클래스
public class ScoreValueException extends Exception{
	public ScoreValueException(String message) {
		super(message);
	}

}

```
### 예시 출력
```
1.성적입력,2성적출력,3.종료메뉴선택:123
잘못 입력했습니다
1.성적입력,2성적출력,3.종료메뉴선택:1
이름 :홍길동
국어 :90
영어 :80
수학 :90
1.성적입력,2성적출력,3.종료메뉴선택:1
이름 :제임스
국어 :80
영어 :70
수학 :90
1.성적입력,2성적출력,3.종료메뉴선택:2
---------------------------------------
이름	국어	수학	영어	총점	평균	등급
---------------------------------------
홍길동	90	80	90	260	86.67	B
제임스	80	70	90	240	80.00	B
```

