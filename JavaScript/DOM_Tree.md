## **DOM 트리** <p>
- 문서 객체 모델 (Document Object Model)에 따르면, 모든 HTML 태그는 객체다. 태그 하나가 감싸고 있는 자식태그는 중첩태그(nested tag)라고 부른다. 태그 내 문자 역시 객체다. 모든 객체는 자바스크립트를 통해 접근할 수 있고, 페이지를 조작할 때 이 객체를 사용한다. 

<br/>

### **1. DOM 구조** <p>
  ```html
  <!DOCTYPE HTML>
  <html>
  <head>
    <title>사슴에 관하여</title>
  </head>
  <body>
    사슴에 관한 진실.
  </body>
  </html>
  ```
![dom_node.png](../Images/dom_node.png)

- 트리 안의 노드는 모두 객체다. 태그는 요소노드(element node)이며 트리 구조를 구성한다. <html>은 루트 노드가 되고, <head>와 <body>는 루트 노드의 자식이 되는 것이다.
- 요소 내 문자는 텍스트 노드 (text node)가 된다. 위 그림에서 #text는 문자열만 담으며, 자식 노드를 가질 수 없고, 트리 끝에서 잎 노드(leaf node)가 된다. 
- 텍스트 노드에 있는 특수문자는 항상 유효한 문자처럼 취급되므로, 아래 두 특수문자는 텍스트 노드가 되고, DOM의 일부가 된다. 
  - 새 줄(newline): ↵ (자바스크립트에서는 \n로 표시)
  - 공백(space): ␣
- 하지만 텍스트 노드 생성에는 두 가지 예외가 있다.
  - 역사적인 이유로, <head> 이전의 공백과 새 줄은 무시된다.
  - HTML 명세서에서 모든 컨텐츠는 body 안쪽에 있어야 하므로, </body> 뒤에 무언가를 넣더라도 그 컨텐츠는 자동으로 body 안쪽으로 옮겨진다. 따라서 </body> 뒤에는 공백이 있을 수 없다. 

<br/>

### **2. 자동 교정** <p>
- 기형적인 HTML을 만나면 브라우저는 DOM 생성 과정에서 HTML을 자동으로 교정한다. (e.g.최상위 태그는 항상 <html>이어야 하는데 없다든가, 닫는 태그가 없다든가)
- cf. 테이블 사용시, DOM에서는 <tbody>가 있어야 한다고 하지만, HTML에서는 이를 생략하므로 브라우저가 자동으로 DOM에 <tbody>를 생성한다. 

<br/>

### **3. 기타 노드 타입** <p>
- 주석도 노드가 된다. 아래와 같이 주석 노드 (comment node) 타입은 화면 출력물에 영향을 주지 않더라도 DOM에 추가된다. HTML 안의 모든 것은 주석이더라도 DOM을 구성하기 때문이다.

  ```html
  <!-- comment -->
  ```
  ↪️ #comment comment

- 비슷하게 HTML 문서 최상단의 <!DOCTYPE>도 DOM 노드로 된다. 문서 전체를 나타내는 document 객체 또한 DOM 노드다. 

<br/>

### **4. 콘솔을 사용해 DOM 다루기** <p>
- 개발자도구 console 창에 document.body를 입력해 DOM 노드를 탐색해 볼 수도 있으며, 이는 디버깅 용도로 사용된다. 

  ![dom_console.png](../Images/dom_console.png)

<br/>


