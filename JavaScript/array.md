### ****Chapter1-1. 배열 기초****

1. **배열은 순서(index)가 있는 값(element)**
    1. 순서: 1이 아닌 0부터 번호를 매김
    2. 대괄호를 이용해 배열을 만들고, 각각의 원소(element)에는 쉼표로 구분해줌 
2. **예시 코드**
    1. 인덱스 값 구하기
        
        ```jsx
        let myNumber = [73, 98, 86, 61, 96];
        // myNumber 라는 배열의 3번째 인덱스 값은?
        myNumber[3]; // 61
        
        let myNumber = [73, 98, 86, 61, 96];
        // myNumber 라는 배열의 5번째 인덱스 값은?
        myNumber[5]; // undefined
        
        let myNumber = [[13, 30], [73, 8], [44, 17]];
        // myNumber 라는 배열의 1번째 인덱스 값은?
        myNumber[1]; // [73, 8]
        // myNumber 라는 배열의 1번째 인덱스값의 0번째 인덱스의 값은?
        myNumber[1]; // 73
        
        let myNumber = [[13, 30],[73, 8],[44, 17] ]; // undefined
        myNumber // (3) [Array(2), Array(2), Array(2)]
        myNumber[1] // (2) [73, 8]
        myNumber[1][0] // 73
        ```
        
    2. 배열로 길이 알아내기
        
        ```jsx
        let myNumber = [73, 98, 86, 61];
        // myNumber 배열의 길이는?
        myNumber.length; // 4: 온점을 활용해 변수가 가지고 있는 속성에 접근 가능
        ```
        
    3. 배열로 **맨 뒤에** 요소 추가/삭제 하기
        
        ```jsx
        ley myNumber = [73, 98, 86, 61];
        
        // myNumber 배열 **끝에** 96 이라는 값을 추가하려면
        myNumber.push(96); // 온점을 활용해 관련된 명령(method)도 실행 가능하며, 명령 실행 시 함수를 실행하듯 괄호 열고 닫기 형태로 실행
        
        // myNumber 배열 **마지막 값**을 삭제하려면
        myNumber.pop();
        ```
        

### ****Chapter1-2. 배열의 반복****

1. **예시 코드**
    1. 반복문을 이용해 배열의 요소를 한번씩 출력하기
        
        ```jsx
        let myNum = [73, 98, 86, 61];
        for (let n = 0; n < myNum.length; n++) {
        	console.log(myNum[n]);
        }
        ```
        
    2. 배열의 모든 요소를 누적해서 더하기
        
        ```jsx
        let myNum = [10, 20, 40, 10];
        let sum = 0; // 0 할당 안하면 undefined 되고 초기값 안 넣어준 상태로 계산하면 NaN 나옴
        
        for(let n = 0; n < **myNum.length**; n++) {
        // sum = **0** + 10 -> sum + myNum[0]
        // sum = 10 + 20 -> sum + myNum[1]
        // sum = 30 + 40 -> sum + myNum[2]
        // sum = 70 + 10 -> sum + myNum[3]
        **sum = sum + myNum[n]**;
        }
        console.log(sum); // 80
        ```
        

### ****Chapter1-3. 배열 메소드****

1. **메소드 종류와 예시 코드**
    1. 특정 값이 배열인지 아닌지 판별할 수 있는 `Array.isArray`
        
        ```jsx
        let words = ['피', '땀', '눈물'];
        typeof [1, 2, 3] // object
        
        Array.isArray('문자열') // false
        Array.isArray(123) // false
        
        Array.isArray(words) // true
        Array.isArray([]) // true
        ```
        
    2. 배열의 요소를 push, pop 활용해 추가 및 삭제하기
        
        ```jsx
        let arr = ['code', 'states'];
        console.table(arr) // Array(2)
        
        arr.push('pre') // **맨 뒤**에 요소 추가
        console.table(arr) // Array(3)
        
        arr.pop() // **맨 뒤**의 요소 제외
        console.table(arr) // Array(2)
        
        arr.shift() // **맨 앞**의 요소 제외
        console.table(arr) // Array(1)
        
        arr.unshift('creative') // **맨 앞에** 요소 추가
        console.table(arr) // Array(2)
        ```
        
        ![array.png](../Images/array.png)
        
    3. 특정 값이 배열에 포함되어 있는지, 인덱스 값이 무엇인지 알 수 있는 `indexOf`
        
        ```jsx
        let word = ['Hello', 'world', 'everyone'];
        
        word.indexOf('world') // 1 : 해당 elemment가 들어있는 **인덱스 값**
        word.indexOf('everyone') // 2
        word.indexOf('what') // -1 : 없는 단어
        
        word.indexOf('world') !== -1 // true: 단어가 있다는 뜻
        word.indexOf('what') !== -1 // false: 단어가 없다는 뜻, -1이랑 같으니까
        
        word.indexOf('WORLD') // -1 : 대소문자를 구분하니 주의
        ```
        
    4. 특정 값이 배열에 포함되어 있는지 확인할 수 있는 `inclundes`