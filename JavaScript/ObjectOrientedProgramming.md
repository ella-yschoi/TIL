## **1. 객체 지향 프로그래밍 ** ##
- 객체지향 프로그래밍은 절차지향 프로그래밍과는 다르게 데이터를 한 곳에 묶어 처리함
- 속성과 메서드가 하나의 '객체' 라는 개념에 포함되며, 이는 JavaScript 내장 타입은 object와는 다르게, class라는 이름으로 부름
- 객체 지향 프로그래밍은 하나의 모델이 되는 청사진(blueprint)을 만들고 → class
- 그 청사진을 바탕으로 한 객체(object)를 만드는 프로그래밍 패턴 → instance
<br/><p>

## **2. 클래스 모듈 패턴** ##
  
  a. 매소드 호출

  ```jsx
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
  
  ```jsx
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