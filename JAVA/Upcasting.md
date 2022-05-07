# 업캐스팅 (Upcasting)
## 업캐스팅 이란
자식클래스에서 부모클래스로 형변환 하는 것 
- 부모 클래스에 선언된 필드 혹은 메서드만 접근 가능
- 자동 형변환
## 업캐스팅 하는 이유
자식클래스 -> 부모클래스로 업캐스팅하면 사실상 범위가 좁아짐 에도 불구하고 업캐스팅 하는 이유에는 공통된 부분을 처리하기 위해서 이다
<br>
다음 예시를 보자

```java
//부모클래스
class Product{
	int price; //제품의 가격
	
	public Product(int price) {
		this.price=price;
	}
	
	public String getName() {
		return "제품";
	}
}
class Tv extends Product{
	public Tv() {
		super(1000);
	}
	
	@Override
	public String getName() {
		return "Tv";
	}
}
class Computer extends Product{
	public Computer() {
		super(2000);
	}
	
	
	public String getName() {
		return "Computer";
	}
	
}
class Audio extends Product{
	public Audio() {
	super(3000);
	}
	public String getName() {
		return "Audio";
	}
}

class Buyer{
	private int money;	
	public int getMoney() {
		return money;
	}
	public void setMoney(int money) {
		this.money = money;
	}
	//구매하기
	public void buy(tv v) {
		money-=p.price;
		System.out.println("구매한 제품은 : "+v.getName());
		System.out.println("남은 잔돈 : "+money);
				
	}

}
```
<br>
<br>
소비자가 잔돈을 입력하면 구매 제품 이름, 남은 잔돈이 출력되는 프로그램이다. 이 중 소비자 부분인 Buyer 클래스의 buy메서드를 살펴보자 
<br>
<br>

```java
//구매하기
	public void buy(tv v) {
		money-=p.price;
		System.out.println("구매한 제품은 : "+v.getName());
		System.out.println("남은 잔돈 : "+money);
				
	}
```
<br>
<br>
입력된 객체의 정보를 출력하는 역할을 수행기능 
<br>

_다른 제품도 출력을 해야 하는 상황이라면 어떨까?_
<br>
<br>

```
     public void buy(Tv v) {
		money-=v.price;
		System.out.println("구매한 제품은 : "+v.getName());
		System.out.println("남은 잔돈 : "+money);
				
	}
    public void buy(Computer c) {
		money -= c.price;
		System.out.println("구매한 제품은 : " + c.getName());
		System.out.println("남은 잔돈 : " + money);

	}
    public void buy(Audio a) {
		money -= a.price;
		System.out.println("구매한 제품은 : " + a.getName());
		System.out.println("남은 잔돈 : " + money);

	}
    
    
   // ...........           생략         ................

```
<br>
<br>
이런식으로 제품 객체별로 생성하여 코드가 중복되는 부분이 상당히 많아지게 되고, 상당히 지저분해진다.
<br>
<br>
그래서 공통 부분이 있는 Product 부모 클래스로 형변환하여 나타내보면

<br>
<br>

```java

import java.util.*;

//부모클래스
class Product {
	int price; // 제품의 가격

	public Product(int price) {
		this.price = price;
	}

	public String getName() {
		return "제품";
	}
}

class Tv extends Product {
	public Tv() {
		super(1000);
	}

	@Override
	public String getName() {
		return "Tv";
	}
}

class Computer extends Product {
	public Computer() {
		super(2000);
	}

	public String getName() {
		return "Computer";
	}

}

class Audio extends Product {
	public Audio() {
		super(3000);
	}

	public String getName() {
		return "Audio";
	}
}

class Buyer {
	private int money;

	public int getMoney() {
		return money;
	}

	public void setMoney(int money) {
		this.money = money;
	}

	// 구매하기
	public void buy(Product p) {
		money -= p.price;
		System.out.println("구매한 제품은 : " + p.getName());
		System.out.println("남은 잔돈 : " + money);

	}

}

public class Main {
	public static void main(String[] args) {
		Buyer b = new Buyer();
		Tv tv = new Tv();
		Audio ad = new Audio();
		Computer com = new Computer();
		Scanner in = new Scanner(System.in);

		System.out.print("소비자의 잔돈 입력 = ");
		int buyer = in.nextInt();
		b.setMoney(buyer); // setter를 통함
		// 구매하기
		while (true) {
			System.out.println("=========================================");
			System.out.println("구매 하려는 제품은? ( 1.tv 2.컴퓨터 3.오디오 )");
			System.out.println("==========================================");
			System.out.println("Tv : 1000원 | 컴퓨터 : 2000원 | 오디오 : 3000원 ");
			int num = in.nextInt();

			if (num == 1)
				b.buy(tv); // Tv -> Product타입으로 형변환됨
			else if (num == 2)
				b.buy(com);
			else if (num == 3)
				b.buy(ad);
			else if (num == 4) {
				System.out.println("프로그램을 종료 합니다.");
				break;
			}

		}
	}
}
```
<br>
<br>
이런 식으로 부모의 업캐스팅을 통해 공통적인 부분을 한번에 해결하였다
<br>
<br>


#### 출력 결과
```
소비자의 잔돈 입력 = 15000
=========================================
구매 하려는 제품은? ( 1.tv 2.컴퓨터 3.오디오 )
==========================================
Tv : 1000원 | 컴퓨터 : 2000원 | 오디오 : 3000원 
1
구매한 제품은 : Tv
남은 잔돈 : 14000


=========================================
구매 하려는 제품은? ( 1.tv 2.컴퓨터 3.오디오 )
==========================================
Tv : 1000원 | 컴퓨터 : 2000원 | 오디오 : 3000원 
2
구매한 제품은 : Computer
남은 잔돈 : 12000


=========================================
구매 하려는 제품은? ( 1.tv 2.컴퓨터 3.오디오 )
==========================================
Tv : 1000원 | 컴퓨터 : 2000원 | 오디오 : 3000원 
3
구매한 제품은 : Audio
남은 잔돈 : 9000


=========================================
구매 하려는 제품은? ( 1.tv 2.컴퓨터 3.오디오 )
==========================================
Tv : 1000원 | 컴퓨터 : 2000원 | 오디오 : 3000원 
4
프로그램을 종료 합니다.

```
