## **1. 객체 지향 프로그래밍** ##
- 객체지향 프로그래밍은 절차지향 프로그래밍과는 다르게 데이터를 한 곳에 묶어 처리함
- 속성과 메서드가 하나의 '객체' 라는 개념에 포함되며, 이는 JavaScript 내장 타입은 object와는 다르게, class라는 이름으로 부름
- 객체 지향 프로그래밍은 하나의 모델이 되는 청사진(blueprint)을 만들고 → class
- 이때 모델의 청사진을 만들 때 쓰는 원형객체(original form)는 → prototype
- 그 청사진을 바탕으로 한 객체(object)를 만드는 프로그래밍 패턴 → instance

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
  - new 키워드로 인스턴스를 생성했을 때는 해당 인스턴스가 바로 this 값이 됨 <br/><p>

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

<br/><p>

## **2. 클래스 모듈 패턴** ##
  
  a. 매소드 호출

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

  b. 클로저를 이용해 매번 새로운 객체 생성하기
  
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
<br/><p>

## **3. 클래스와 인스턴스** ##
- 