## 클래스와 구조체의 차이

클래스
- 참조형식(Reference Type)
- 인스턴스 데이터는 힙(Heap)에 저장, 해당 힙을 가르키는 변수는 스택에 저장하고 메모리 주소는 힙(Heap)을 가르킴
- (복사시) 값을 전달하는것이 아니고 저장된 주소를 전달
- 힙(Heap)의 공간에 저장, ARC시스템을 통해 메모리 관리(주의)

구조체
- 값 형식(Value Type)
- 인스턴스 데이터를 모두 스택(Stak)에 저장 
- (복사시) 값을 전달할때마다 복사본을 생성(다른 메모리 공간 생성)
- 스택(Stack)의 공간에 저장, 스택 프레임 종료시 메모리에서 자동 제거



-----------



클래스를 사용하는 경우
- 데이터에서 상속의 구조가 필요할때
- 해당 모델을 serialize해서 전송하거나 파일로 저장할 경우

구조체를 사용하는 경우
- 연관된 데이터들을 단순히 캡슐화(묶는)하는 것이 목적일때
- 캡슐화한 데이터를 참조하는것보다 복사해서 사용하는 것이 효율적일때
- 구조체에 저장된 저장 속성들이 값 타입이며 참조하는것보다 복사하는것이 합당할때

클래스가 구조체보다 무겁기때문에 구조체를 주로 사용하고 필요한경우에만 클래스를 사용한다.

## 메모리 저장방식의 차이
```swift
class personClass {
    var name = "이름"
    var age = 0
}
struct personStruct {
    var name = "이름"
    var age = 0
}

var personClassA = personClass()
personClassA.name = "Any"

var personClassB = personClassA // 같은 메모리 주소가 복사됨
personClassB.name = "Annei"

personClassA.name // "Annie"
personClassB.name // "Annie" 


var personStructA = personStruct()
personStructA.name = "Any"

var personStructB = personStructA
personStructB.name = "Annei"

personStructA.name // "Any"
personStructB.name // "Annie"
```

클래스의 경우 값을 다른 변수에 복사해도 같은 메모리 주소값을 가르키기 때문에 두 인스턴스가 동일한 `"Annie"` 라는 이름을 갖게 된다.

구조체는 값을 다른 변수에 복사하면 서로 다른 데이터가 스택에 생성되기 때문에(다른 메모리 공간 생성) `"Any", "Annie"` 처럼 다른 이름을 갖게 된다.


## 클래스와 구조체의 let과 var 키워드

```swift
class personClass {
    var name = "이름"
    var age = 0
}
struct personStruct {
    var name = "이름"
    var age = 0
}

// 인스턴스 생성
let personA = personClass()
let personB = personStruct()

// 인스턴스 속성값 변경
personA.name = "Any"
personB.name = "Any" // Error
```

구조체는 `let`으로 인스턴스 생성시 내부의 속성 변수들이 `let`으로 상수화 되기 때문에 값을 변경 할 수 없다.

반대로 클래스는 `let`으로 인스턴스 생성을 해도 내부 속성에 접근해서 값을 변경할 수 있다.

