1. ### **객체란?** <p>
   JavaScript에서의 객체는 게임 캐릭터와 비슷하다고 할 수 있다. 사용자들의 캐릭터는 동일하게 직업과 능력을 가지고 있지만, 각각 세부적인 내용은 다르다. 누군가는 Ella라는 ID와 마법사라는 직업을 가지고 있지만, 다른 누군가는 Chloe라는 ID와 전사라는 직업을 가지고 있다.
   
   마찬가지로 사용자가 웹사이트에 가입할 때 입력할 항목은 모두 같지만, 입력하는 정보는 사용자마다 다르다. 이렇게 각기 다른 값을 가질 수 있지만, 입력해야 하는 데이터의 종류가 동일한 경우 객체를 사용하면 손쉽게 데이터를 관리할 수 있다.
   
   이렇듯, 공통적인 속성을 가지는 경우 객체를 사용해야 한다. 웹사이트에 가입한 회원 주소록을 만든다고 가정해 보자.

     ```jsx
     // 위와 같이 매번 여러 개의 변수를 선언해 주어야 할까?
     let userFirstName = 'Ella';
     let userLastName = 'Choi';
     let userEmail = 'ella@gmail.com';
     let userCity = 'Seoul';
     
     let userFirstName = 'Chloe';
     let userLastName = 'Kim';
     let userEmail = 'chloe@gmail.com';
     let userCity = 'Seoul';
     ```
     
     ```jsx
     let user = { // 중괄호로 객체 만듬
      firstName: 'Ella', // 한 쌍의 이름과 값은 ',' 로 구분, 이름과 값은 ':' 으로 분리
      lastName: 'Choi', // 여기서 lastName는 키(key), 'Choi'는 값(value)
      email:'ella@gmail.com',
      city: 'Seoul'
     ```


2. ### **객체의 값을 조회하는 방법 두 가지** <p>
    a. Dot notation: 객체 + .(점) + 키 값의 형태로 작성한다.
        
     ```jsx
     let user = { 
      firstName: 'Ella', 
      lastName: 'Choi', 
      email:'ella@gmail.com',
      city: 'Seoul'
     };

     // 형식: 객체 + .(점) + 키 값
     user.firstName; // 'Ella'
     user.city; // 'Seoul'
     ```
        
    b. Bracket notation: 키 값이 대괄호 안에 '문자열'로 들어간다. 이 점을 주의하자.
        
     ```jsx
     let user = {
     	firstName: 'Ella', 
     	lastName: 'Choi', 
     	email:'ella@gmail.com',
     	city: 'Seoul'
     };
     
     // 형식: 키 값이 대괄호 안에 '문자열'로 들어감
     user['firstName']; // 'Ella'
     user['city']; // 'Seoul'
     ```

       
3. ### **객체를 다루는 다양한 방법** <p>

   a. Bracket notation: 키 값이 동적으로 변할 때 반드시 사용 
        
     ```jsx
        let person = {
        name: 'Ella',
        age: 16 
    }; // 키 값이 계속 변하는 상황

    // name 값 조회
    let output = getProperty(person, 'name');
    console.log(output); // -> 'Ella'

    // name 값 조회 방법
    function getProperty(obj, propertyName) {
        return obj[propertyName]; // obj['name']   
    }

    // 주의1: return person.name (X) Ella만 나오기에 -> obj[propertyName]를 넣어야 함
    // 주의2: return.propertyName (X) -> propertyName 라는 키 이름이 별도로 있어야 넣을 수 있음


    // age 값 조회
    let output = getProperty(person, 'age');
    console.log(output2); // -> 16

    // age 값 조회 방법
    function getProperty(obj, propertyName) {
        return obj[propertyName]; // obj['age']   
    }
     ```
        
    b. dot/bracket notation으로 값을 추가할 수도 있음
        
     ```jsx
     let tweet = {
     writer: 'Ella Choi',
     createdAt: '2022-02-28 12:03:33',
     content: '코딩은 재밌어'
    };

    // 다양한 값을 넣을 수 있음
    tweet['category'] = '이야기'; // Bracket notation으로 이야기 라는 문자열을 추가
    tweet.isPublic = true; // Dot notation으로 Boolean값을 추가
    tweet.tags = ['#코딩', '#개발자'] // Dot notation으로 배열을 추가
     ```
        
    c. delete 키워드로 속성 삭제도 가능
     ```jsx   
    let tweet = {
        writer: 'Ella Choi',
        createdAt: '2022-02-28 12:03:33',
        content: '코딩은 재밌어'
    };

    delete tweet.createdAt; // createAt 키-값 쌍을 지움
    tweet.createdAt // 지워졌으니 콘솔에 찍으면 undefined로 나옴

    // tweet은 다음과 같게 됨
    // {writer: 'Ella Choi', content: '코딩은 재밌어'}
     ```
        
    d. in 연산자로 해당하는 키가 있는지 확인 가능
     ```jsx 
    let tweet = {
	writer: 'Stevelee',
	createdAt: '2022-02-28 12:03:33',
	content: '코딩은 재밌어'
    };

    'content' in tweet; // true
    'updatedAt' in tweet; // false
    ```

4. ### **문자열 작성 시 흔히 하는 실수** <p>
   Bracket notation 사용 시 대괄호를 빼먹는다거나, 변수 선언을 하지 않았다거나 등등 사소한 실수를 막기 위해 아래 내용을 하나씩 이해하며 눈에 익혀보자!

   ```jsx
   let user = {
	firstName: 'Ella', 
	lastName: 'Choi', 
	email:'ella@gmail.com',
	city: 'Seoul'
    };
    user['firstName']; // 'Ella' : Bracket notation으로 객체의 값 조회
    user[firstName]; // ReferenceError: firstName is not defined : firstName이 변수취급 되고 있는 것임

    let keyname = 'firstName'; // keyname에 'firstName'라는 문자열을 담아봄
    user[keyname] // 'Ella' : 'firstName' 문자열 값이 keyname로 들어갔기 때문에
    user[keyname] === user['firstName'] // true : 사실상 Bracket notation으로 객체 값 조회한 결과와 같음

    let firstName = 'Ella'
    user[firstName] === user['firstName'] // false : Bracket notation 사용 시 대괄호 안에 문자열이 들어가야 함
    user[keyname] === user['firstName'] // true

    user['firstName'] === user.firstName // true :Dot notation === Bracket notation
    user[firstName] === user.firstName // false : Bracket notation 사용 시 대괄호 안에 문자열이 들어가야 함
    user[firstName] === user['firstName'] // false
   ```
