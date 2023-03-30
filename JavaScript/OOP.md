## **1. 객체 지향** ##
### 1. 정의
   - 객체지향 프로그래밍은 절차지향 프로그래밍과는 다르게 데이터를 한 곳에 묶어 처리함
   - 속성과 메서드가 하나의 '객체' 라는 개념에 포함되며, 이는 JavaScript 내장 타입은 object와는 다르게, class라는 이름으로 부름
   - 객체 지향 프로그래밍은 하나의 모델이 되는 청사진(blueprint)을 만들고 → class
   - 이때 모델의 청사진을 만들 때 쓰는 원형객체(original form)는 → prototype
   - 그 청사진을 바탕으로 한 객체(object)를 만드는 프로그래밍 패턴 → instance

<br/><br/>

### **2. 클래스 모듈 패턴** ##
- 매소드 호출
  ```javascript
  let counter1 = {
    value: 0;
    increase: function() {
        this.value++ // 메소드 호출을 할 경우, this는 counter1을 가리킴
    },
    decrease: function() {
        this.value--
    },
    getValue: function() {
        return this.value
    }
  }

  counter1.increase()
  counter1.decrease()
  counter1.increase()
  counter1.decrease()
  counter1.getValue() // 2
  ```

- 클로저를 이용해 매번 새로운 객체 생성하기
  ```javascript
  function makeCounter() {
    let value = 0;
    return {
        increase: function () {
            value++;
        },
        decrease: function () {
            value--;
        },
        getValue: function () {
            return value;
        }
    }
  }

  let counter1 = makeCounter()
  counter1.increase()
  counter1.getValue() // 1

  let counter2 = makeCounter()
  counter2.decrease()
  counter2.decrease()
  counter2.getValue() // -2
  ```

### 2. 클래스와 인스턴스
  - 클래스를 만드는 문법: class 키워드
    
    ```javascript
    class Car {
      constructor (brand, name, color) {
          // 인스턴스가 만들어질 때(=초기화될 때) 실행되는 코드: constructor(생성자)
          // 참고로 생성자 함수는 return 값을 만들지 않음
      }
    }
    ```

  - 클래스의 인스턴스 만들기
    ```javascript
    let avante = new Car('hyundai', 'avante', 'black');
    // 인스턴스를 만들 때는 new 키워드 사용
    // 각각의 인스턴스는 Car 라는 클래스의 고유한 속성과, 메소드를 가짐
    ```

  - this: 인스턴스 객체
    - parameter로 넘어온 브랜드, 이름, 색상 등은 인스턴스 생성 시 지정하는 값
    - this에 할당한다는 것은 만들어진 인스턴스에 해당 해당 브랜드, 이름, 색상을 '부여'하겠다는 의미 
    - 함수가 실행될 때 해당 scope마다 생성되는 고유한 실행 context 
    - new 키워드로 인스턴스를 생성했을 때는 해당 인스턴스가 바로 this 값이 됨 <br/><br/>

  - 메소드 정의
    - 생성자 함수와 함께 class 키워드 안쪽에 묶어서 정의
      ```javascript
      class Car {
        constructor(brand, name, color) {/* 생략 */}
        refuel() {
        }
        drive() {
        }
      }
      ```

  - 인스턴스에서의 사용: 위에서 설정한 속성과 메소드를 인스턴스에서 사용하는 방법
    ```javascript
    let avante = new Car('hyundai', 'avnante', 'black');
    avante.color; // 'black'
    avante.drive(); // 아반떼가 운전을 시작합니다

    let mini = new Car('bmw', 'mini', 'white');
    mini.brand; // 'bmw'
    mini.refuel(); // 미니에 연료를 공급합니다
    ```

  - 정리
    ```javascript
    // constructor(생성자) 함수
    function Car (brand, name, color) { // Car는 class
      this.brand = brand; // 여기서 avante === this
      this.name = name;
      this.color = color;
    }
    
    // Car.prototype 객체: 여기에 속성이나 메소드를 정의할 수 있음
    Car.prototype.drive = function() {
      console.log(this.name + '가 운전을 시작합니다');
    }

    let avante = new Car('hyundai', 'avante', 'black'); // avante: instance
    avante.color; // 'black'
    avante.drive(); // 'avante가 운전을 시작합니다'
    ```
  <br/><br/>

### **3. 객체 지향 프로그래밍** ##
- 절차적 언어 > 객체 지향 언어
  - 절차적 언어: 순차적인 명령의 조합
  - 객체 지향 언어: class 라는 데이터 모델의 청사진을 이용해 코드를 작성하며, 데이터와 기능이 한번에 묶여서 처리됨.
  - JavaScript는 객체 지향 언어는 아니지만, 객체 지향 패턴으로 작성 가능
- OOP(객체 지향 프로그래밍)의 네 가지 기본 개념
  - (1) Encapsulation(캡슐화)
    - 데이터와 기능을 하나의 단위로 묶는 것
    - 은닉(Hiding): 구현은 숨기고, 동작은 노출
    - 느슨한 결합(Loose Coupling)에 유리: 코드 실행 순서에 따라 절차적으로 코드를 작성하는 것이 아니라, 코드가 상징하는 실제 모습과 닮게 코드를 모아 결합, 언제든 구현 수정 가능
    - 코드가 복잡하지 않고 재사용성을 높임
  - (2) Inheritance(상속)
    - 부모, 즉 기본 클래스(base class)의 특징을 자식, 즉 파생 클래스(derived class)가 상속받는 것
    - 코드가 단순하고 재사용성을 높임
  - (3) Abstraction(추상화)
    - 내부 구현은 복잡 but 실제 노출되는 부분은 단순하게 만들어, 예기치 못한 사용상의 변화 방지
    - 캡슐화는 데이터의 은닉에 중심을 맞추고, 추상화는 클래스를 사용하는 사람이 불필요한 메소드 등을 노출시키지 않고, 단순한 이름으로 정의하는 것에 중심.
    - 코드가 복잡하지 않고 변화에 대한 영향 최소화
  - (4) Polymorphism(다형성)
    - ex) 같은 이름을 가진 메소드라도 각 요소에 조금씩 다르게 적용됨
    - 동일한 메소드에 대해 if/else와 같은 조건문 대신 각 객체의 특성에 맞게 다르게 작성 가능