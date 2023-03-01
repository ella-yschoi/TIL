### ****Chapter2-1. 객체 기초****

1. **객체 개념**
    1. 공통적인 속성을 가지는 경우 객체를 사용해야 함
    2. 회원 주소록을 만든다고 가정해보기
        
        ```jsx
        // 매번 이런 식으로 여러 개의 변수를 선언해 주어야 할까?
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
        	firstName: 'Ella', // 키, 값, 쌍은 쉼표로 구분
        	lastName: 'Choi', // lastName: 키(key), 'Choi': 값(value)
        	email:'ella@gmail.com',
        	city: 'Seoul'
        ```
        

### ****Chapter2-2. 객체 조회하기****

1. **객체의 값을 사용하는 방법 두 가지**
    1. Dot notation
        
        ```jsx
        let user = { // 객체의 속성을 가져옴
        	firstName: 'Ella', 
        	lastName: 'Choi', 
        	email:'ella@gmail.com',
        	city: 'Seoul'
        };
        
        user.firstName; // 'Ella'
        user.city; // 'Seoul'
        ```
        
    2. Bracket notation
        
        ```jsx
        let user = { // 객체의 속성을 가져옴
        	firstName: 'Ella', 
        	lastName: 'Choi', 
        	email:'ella@gmail.com',
        	city: 'Seoul'
        };
        
        user['firstName']; // 'Ella': 키 값이 대괄호 안에 문자열로 들어감
        user['city']; // 'Seoul'
        ```
        

### ****Chapter2-3. 객체 다루기****

1. **흔히 하는 실수**
    1. 문자열 작성 시
        
        ```jsx
        user['firstName']; // 'Ella'
        user[firstName]; // ReferenceError: firstName is not defined -> 키 값이 아니라 변수처럼 취급되고 있는 것임
        ```
        
        ```jsx
        user // {firstName: 'Ella', lastName: 'Choi', email: 'ella@gmail.com', city: 'Seoul'}
        let keyname = 'firstName'; // undefined
        user[keyname] // 'Ella'
        user[keyname] === user['firstName'] // true
        
        let firstName = 'Ella' // undefined
        user[firstName] === user['firstName'] // false
        user[keyname] === user['firstName'] // true
        
        user['firstName'] === user.firstName // true
        user[firstName] === user.firstName // false
        user[firstName] === user['firstName'] // false
        ```
        
2. **객체를 다루는 다양한 방법**
    1. Bracket notation: 키 값이 동적으로 변할 때 반드시 사용 
        
        ```jsx
        let person = {
        	name: 'Steve',
        	age: 16
        };
        function getProperty(obj, propertyName) {
        	return obj[propertyName]; // obj['name'] 
        // [propertyName]가 아닌 .name을 넣으면 계속 Steve만 나올 것
        // .propertyName을 넣으면 안됨. propertyName이라는 키 이름이 있어야 넣을 수 있음
        }
        
        //1
        let output = getProperty(person, 'name');
        console.log(output); // -> 'Steve'
        
        //2
        let output = getProperty(person, 'age');
        console.log(output2); // -> 16
        ```
        
    2. dot/bracket notation으로 값을 추가할 수도 있음
        
        ```jsx
        let tweet = {
        	writer: 'Stevelee',
        	createdAt: '2022-02-28 12:03:33',
        	content: '프리코스 재밌어요'
        };
        
        tweet['category'] = '잡담';
        tweet.isPublic = true;
        tweet.tags = ['#코드스테이츠', '#프리코스']
        ```
        
    3. delete 키워드로 속성 삭제도 가능
        
        ```jsx
        let tweet = {
        	writer: 'Stevelee',
        	createdAt: '2022-02-28 12:03:33',
        	content: '프리코스 재밌어요'
        };
        
        delete tweet.createdAt; // createAt 키-값 쌍을 지웁니다
        tweet.createdAt // 지워졌으니 undefined로 나옴
        
        // tweet은 다음과 같게 됨
        // {writer: 'stevelee', content: '프리코스 재밌어요'}
        ```
        
    4. in 연산자로 해당하는 키가 있는지 확인 가능