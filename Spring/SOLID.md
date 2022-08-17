## 객체 지향 설계 SOLID

> 클린코드로 유명한 로버트 마틴이 객체 지향 설계의 5가지 원칙을 정리



- SRP : 단일 책임 원칙 (single responsibilty principle)
- OCP : 개방-폐쇠 원칙 (Open/closed principle)
- LSP : 리스코프 치환 원칙 (Liskov substitution principle)
- ISP : 인터페이스 분리 원칙 (InterFace segregation principle)
- DIP : 의존관계 역전 원칙 (Dependency inversion principle)
<br>

### SRP  단일 책임 원칙
한 클래스는 하나의 책임만 가져야 한다.
<br>

### OCP : 개방-폐쇠 원칙
소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다
<br>

### LSP  리스코프 치환 원칙
프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다
<br>

### ISP  인터페이스 분리 원칙
특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다

인터페이스가 명확해지고, 대체 가능성이 높아진다.
<br>

### DIP  의존관계 역전 원칙
프로그래머는 _“추상화에 의존해야지, 구체화에 의존하면 안된다.”_ 
의존성 주입은 이 원칙을 따르는 방법 중 하나다

구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻
