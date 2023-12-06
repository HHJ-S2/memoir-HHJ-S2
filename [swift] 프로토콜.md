### 프로토콜 - 선택적 요구사항의 구현
```swift
@objc protocol MyProtocol {
	var name: String { get }
	
	@objc optional var isOn: Bool { get set }
	@objc optional var doSomething()
}
```

- 프로토콜에서 요구사항 구현시, 선택적인 멤버로 구현가능 하도록 한다.
- objectiveC 에서 지원하는 기능이다.
- `@objc` 키워드를 프로토콜 선언 앞에 표기한다.(objectiveC에서 읽을 수 있는 코드라는 의미)
- `@objc optional`을 멤버 앞에 선언하면 해당 멤버는 선택적으로 구현할 수 있다.
- 클래스 전용 프로토콜이기 때문에 구조체, 열거형에서는 채택할 수 없다.



-----------



### 프로토콜 - 확장
```swift
protocol 커피 {
	func 에스프레소넣기()
	func 액체넣기()
}

// 커피 프로토콜을 확장
extension 커피 {
	func 에스프레소넣기() { print('에스프레소를 컵에 부었다.') }
	func 액체넣기() { print('물을 컵에 부었다.') }
	func 납품하기() { print('손님에게 주었다.') }
}

// 커피 프로토콜을 채택
class 라떼: 커피 {
	func 액체넣기() { print('우유를 컵에 부었다.') }
	func 납품하기() { print('손님에게 주지 않고 내가 마셨다.') }
}

let 음료A:커피 = 라떼()
음료A.에스프레소넣기() // 에스프레소를 컵에 부었다. -> 확장으로 미리 구현된 메서드이다.
음료A.액체넣기() // 우유를 컵에 부었다. -> 직접 구현한 내용이 우선순위가 더 높다.
음료A.납품하기() // 손님에게 주었다. -> 타입에 따라 우선순위가 달라진다.

let 음료B:라떼 = 라떼() // 타입을 프로토콜 타입으로 채택
음료B.에스프레소넣기() // 에스프레소를 컵에 부었다.
음료B.액체넣기() // 우유를 컵에 부었다.
음료B.납품하기() // 손님에게 주지 않고 내가 마셨다.
```

- 프로토콜의 멤버를 확장 키워드를 사용해서 메서드 중복구현을 방지한다.
- 클래스로 정의할때 같은 이름의 메서드는 직접 구현했을때 우선순위가 더 높다.
- 인스턴스를 생성하면 해당 인스턴스의 타입에 따라 메서드 구현내용이 달라질 수 있다.



-----------



### 프로토콜 - 확장의 적용 제한
```swift
protocol Bluetooth {
	func on() {}
	func off() {}
}

protocol Remote {
	// ...
}

extension Bluetooth where Self: Remote {
	func blueOn() { print('블루투스 켜가') }
	func blueOff() { print('블루투스 끄기') }
}

class Phone: Remote, Bluetooth {
	// Remote 프로토콜을 채택한 타입만 BlueTooth 확장을 적용할 수 있다.
	// Remote 프로토콜을 채택하지 않으면 확장이 적용되지 않기 때문에 직접 구현해야 한다.
}

```