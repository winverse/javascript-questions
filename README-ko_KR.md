# (고급) JavaScript 질문 목록

JavaScript 에 관한 객관식 문제를 [Instagram](https://www.instagram.com/theavocoder)에 매일 게시하고 있어요, 물론 여기에도 게시할 거예요!

초급부터 고급까지: JavaScript를 얼마나 잘 알고 있는지 테스트하거나, 지식을 조금 깊게 하거나, 코딩 면접을 준비하세요! :muscle: :rocket: 이 기록을 매주 새로운 질문으로 업데이트해요. 마지막 업데이트: <b>6월 21일</b>

정답은 질문 아래 접힌 부분에 있어요, 그냥 클릭하면 펼칠 수 있어요. 행운을 빌어요 :heart:

[中文版本](./README-zh_CN.md)  
[Русский](./README_ru-RU.md)  
[Western Balkan](./README-bs_BS.md)  
[Deutsch](./README-de_DE.md)  
[Tiếng Việt](./README-vi.md)  
[日本語](./README-ja_JA.md)  
[Українська мова](./README-ua_UA.md)  
[한국어](./README-ko_KR.md)

---

###### 1. 무엇이 출력 될까요?

```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  var name = "Lydia";
  let age = 21;
}

sayHi();
```

- A: `Lydia` 와 `undefined`
- B: `Lydia` 와 `ReferenceError`
- C: `ReferenceError` 와 `21`
- D: `undefined` 와 `ReferenceError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: D

함수내에서, 우선 `var`키워드를 사용해 `name`변수를 선언해요. 이것은 변수가 정의되어 있는 행에 실제로 도달할 때까지, 변수는 `undefined`을 기본값으로 호이스팅 된(생성단계에 메모리 공간이 설정됨)는 것을 의미해요. `name`변수를 출력 하려는 줄에서 아직 변수를 정의하고 있지 않았기 때문에, `undefined`값을 유지하고 있어요.

`let`키워드(그리고 `const`)를 가지는 변수들은, `var`와는 달리, 호이스팅되지만 <i>초기화</i>되지 않아요. 그것들을 선언(초기화)하는 줄 전에는 접근 할 수 없어요. 이것은 "일시적 사각지대"라고 불려요. 선언되기 전에 변수에 접근하려고 하면, JavaScript는 `ReferenceError`를 던져요.

</p>
</details>

---

###### 2. 무엇이 출력 될까요?

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```

- A: `0 1 2` 와 `0 1 2`
- B: `0 1 2` 와 `3 3 3`
- C: `3 3 3` 와 `0 1 2`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

JavaScript의 이벤트 큐 때문에, `setTimeout`의 콜백함수는 루프가 실행된 _후에_ 호출되요. 첫번째의 루프 변수 `i`는 `var`키워드를 사용해 선언되어 있으므로, 이 값은 전역변수가 되요. 루프 동안, 단항 연산자 `++`를 사용하여, 매번 `i`의 값을 `1`씩 증가했어요. `setTimeout`콜백 함수가 호출되기까지, 첫번째 예에서 `i`는 `3`과 같아요.

두번째 루프에서, 변수 `i`는 `let`키워드를 사용해 선언되었어요: `let` (그리고 `const`)키워드로 선언된 변수는 블록 범위에요(블록은 `{ }` 사이의 모든것). 각각의 반복동안, `i`는 새로운 값을 가지고, 각각의 값은 루프 안쪽 범위에 있어요.

</p>
</details>

---

###### 3. 무엇이 출력 될까요?

```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius
};

shape.diameter();
shape.perimeter();
```

- A: `20` 과 `62.83185307179586`
- B: `20` 과 `NaN`
- C: `20` 과 `63`
- D: `NaN` 과 `63`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

`diameter`의 값은 정규 함수인 반면, `perimeter`의 값은 화살표 함수라는 점에 유의해요.

화살표 함수에서는, 통상적인 함수와는 달리, `this`키워드는 현재 주위의 범위를 참조해요! 이것은 `perimeter`를 부르면, shape 객체가 아닌, 그 주위의 범위(예를 들면 window)를 참조하는 것을 의미해요.

그 객체에는 `radius`라는 값은 없고, `undefined`를 리턴해요.

</p>
</details>

---

###### 4. 무엇이 출력 될까요?

```javascript
+true;
!"Lydia";
```

- A: `1` 과 `false`
- B: `false` 와 `NaN`
- C: `false` 와 `false`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

단항 더하기는 피연산자를 숫자로 변환하려 해요. `true`는 `1`, `false`은 `0`.

문자열 `'Lydia'`는 참 같은 값이에요. 실제로 묻고 있는 것은, "이 참 같은 값이 거짓 같은 값인가?"에요. 이것은 `false`을 리턴해요.

</p>
</details>

---

###### 5. 정답은 어느 것일까요?

```javascript
const bird = {
  size: "small"
};

const mouse = {
  name: "Mickey",
  small: true
};
```

- A: `mouse.bird.size` 은 유효하지 않아요
- B: `mouse[bird.size]` 은 유효하지 않아요
- C: `mouse[bird["size"]]` 은 유효하지 않아요
- D: 이 모든 것들은 유효해요.

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

JavaScript에서, 모든 객체 키는 문자열이에요 (Symbol이 아닌 한). 비록 그것을 문자열 _타입_ 으로 입력하지 않아도, 항상 밑바닥에서 문자열로 변환되요.

JavaScript는 문장을 해석(또는 박스해제)해요. 대괄호 표기를 사용하면, 첫 번째 좌대괄호 `[`를 보고 오른쪽 대괄호 `]`를 찾을 때까지 진행해요. 그때, 그 문장을 평가할거에요.

`mouse[bird.size]`: 먼저 `bird.size`를 평가해요, 이것은 `"small"`이에요. `mouse["small"]` 은 `true`를 리턴해요.

그러나, 닷 표기에서는, 이것은 발생하지 않아요, `mouse`는 `bird`라고 불리는 키를 가지고 있지 않아요 즉, `mouse.bird`는 `undefined`를 의미해요.

또, 닷 표기를 사용해 `size`를 물어봐요. `mouse.bird.size`. `mouse.bird`는 `undefined`로, 실제로는 `undefined.size`를 물어보고 있어요. 이것은 유효하지 않기 때문에, `Cannot read property "size" of undefined`와 비슷한 에러를 던질거에요.

</p>
</details>

---

###### 6. 무엇이 출력 될까요?

```javascript
let c = { greeting: "Hey!" };
let d;

d = c;
c.greeting = "Hello";
console.log(d.greeting);
```

- A: `Hello`
- B: `Hey`
- C: `undefined`
- D: `ReferenceError`
- E: `TypeError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

JavaScript에서, 모든 객체는 서로 동일하게 설정하면 _참조_ 에 따라 상호작용 해요.

우선 변수 `c`는 객체에 대한 값을 유지해요. 그 후, `c`와 동일한 객체 참조를 `d`에 할당해요.

<img src="https://i.imgur.com/ko5k0fs.png" width="200">

한개의 객체를 변경하면, 그것들 모두 변경해요.

</p>
</details>

---

###### 7. 무엇이 출력 될까요?

```javascript
let a = 3;
let b = new Number(3);
let c = 3;

console.log(a == b);
console.log(a === b);
console.log(b === c);
```

- A: `true` `false` `true`
- B: `false` `false` `true`
- C: `true` `false` `false`
- D: `false` `true` `true`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

`new Number()`는, 내장 함수 생성자에요. 숫자처럼 보이지만, 실제로는 숫자가 아니에요: 많은 추가 특징이 있고 그것은 객체에요.

`==`연산자를 사용할 때, 그건 같은 _값_ 을 가지고 있는지 여부만 확인해요. 그것들은 모두`3`의 값을 가지고 있으므로, `true`를 리턴해요.

그러나, `===`연산자를 사용할 때, 값 _과_ 타입 둘다 같아야 해요. 이건 아니에요: `new Number()`는 숫자가 아니에요. **객체**에요. 그래서 둘다 `false`를 리턴해요.

</p>
</details>

---

###### 8. 무엇이 출력 될까요?

```javascript
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor;
    return this.newColor;
  }

  constructor({ newColor = "green" } = {}) {
    this.newColor = newColor;
  }
}

const freddie = new Chameleon({ newColor: "purple" });
freddie.colorChange("orange");
```

- A: `orange`
- B: `purple`
- C: `green`
- D: `TypeError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: D

`colorChange`함수는 정적이에요. 정적 메소드는 그것들이 만들어지는 생성자 상에서만 살아있도록 설계되어 있어, 어떤 자식들도 상속 받을 수 없어요. `freddie`는 자식이기 때문에, 이 함수는 상속되지 않고, `freddie`인스턴스에서는 이용할 수 없어요: `TypeError`가 던져져요.

</p>
</details>

---

###### 9. 무엇이 출력 될까요?

```javascript
let greeting;
greetign = {}; // Typo!
console.log(greetign);
```

- A: `{}`
- B: `ReferenceError: greetign is not defined`
- C: `undefined`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

객체는 출력되요, 전역객체에 빈 객체를 방금 만들었기 때문이에요. `greeting`을 `greettign`으로 잘못 입력했을 경우, JS 터프리터는 실제로 이것을 `global.greettign = {}` (또는 브라우저의 `window.greetign = {}`) 라고 간주해요.

이것을 피하기 위해서, `"use strict"`를 사용할 수 있어요. 이렇게 하면 변수를 어떤 것과 동일하게 설정하기 전에 변수를 선언했는지 확인할 수 있어요.

</p>
</details>

---

###### 10. 이것을 하면 어떻게 될까요?

```javascript
function bark() {
  console.log("Woof!");
}

bark.animal = "dog";
```

- A: 아무 일도 일어나지 않아요, 이건 완전히 괜찮아요!
- B: `SyntaxError` 이 방법으로 함수에 속성을 추가할 수 없어요.
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

JavaScript에서는 가능해요, 함수는 객체이기 때문이에요!
(프리미티브형 이외는 모두 객체에요)

함수는 특별한 종류의 객체에요. 자신이 쓴 코드는 실제 함수가 아니에요. 함수는 속성을 가진 객체에요. 이 속성은 호출이 가능해요.

</p>
</details>

---

###### 11. 무엇이 출력 될까요?

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person("Lydia", "Hallie");
Person.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());
```

- A: `TypeError`
- B: `SyntaxError`
- C: `Lydia Hallie`
- D: `undefined` `undefined`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

You can't add properties to a constructor like you can with regular objects. If you want to add a feature to all objects at once, you have to use the prototype instead. So in this case,

```js
Person.prototype.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};
```

would have made `member.getFullName()` work. Why is this beneficial? Say that we added this method to the constructor itself. Maybe not every `Person` instance needed this method. This would waste a lot of memory space, since they would still have that property, which takes of memory space for each instance. Instead, if we only add it to the prototype, we just have it at one spot in memory, yet they all have access to it!

</p>
</details>

---

###### 12. 무엇이 출력 될까요?

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const lydia = new Person("Lydia", "Hallie");
const sarah = Person("Sarah", "Smith");

console.log(lydia);
console.log(sarah);
```

- A: `Person {firstName: "Lydia", lastName: "Hallie"}` and `undefined`
- B: `Person {firstName: "Lydia", lastName: "Hallie"}` and `Person {firstName: "Sarah", lastName: "Smith"}`
- C: `Person {firstName: "Lydia", lastName: "Hallie"}` and `{}`
- D:`Person {firstName: "Lydia", lastName: "Hallie"}` and `ReferenceError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

For `sarah`, we didn't use the `new` keyword. When using `new`, it refers to the new empty object we create. However, if you don't add `new` it refers to the **global object**!

We said that `this.firstName` equals `"Sarah"` and `this.lastName` equals `"Smith"`. What we actually did, is defining `global.firstName = 'Sarah'` and `global.lastName = 'Smith'`. `sarah` itself is left `undefined`.

</p>
</details>

---

###### 13. What are the three phases of event propagation?

- A: Target > Capturing > Bubbling
- B: Bubbling > Target > Capturing
- C: Target > Bubbling > Capturing
- D: Capturing > Target > Bubbling

<details><summary><b>정답</b></summary>
<p>

#### 정답: D

During the **capturing** phase, the event goes through the ancestor elements down to the target element. It then reaches the **target** element, and **bubbling** begins.

<img src="https://i.imgur.com/N18oRgd.png" width="200">

</p>
</details>

---

###### 14. All object have prototypes.

- A: true
- B: false

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

All objects have prototypes, except for the **base object**. The base object has access to some methods and properties, such as `.toString`. This is the reason why you can use built-in JavaScript methods! All of such methods are available on the prototype. Although JavaScript can't find it directly on your object, it goes down the prototype chain and finds it there, which makes it accessible for you.

</p>
</details>

---

###### 15. 무엇이 출력 될까요?

```javascript
function sum(a, b) {
  return a + b;
}

sum(1, "2");
```

- A: `NaN`
- B: `TypeError`
- C: `"12"`
- D: `3`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

JavaScript is a **dynamically typed language**: we don't specify what types certain variables are. Values can automatically be converted into another type without you knowing, which is called _implicit type coercion_. **Coercion** is converting from one type into another.

In this example, JavaScript converts the number `1` into a string, in order for the function to make sense and return a value. During the addition of a numeric type (`1`) and a string type (`'2'`), the number is treated as a string. We can concatenate strings like `"Hello" + "World"`, so what's happening here is `"1" + "2"` which returns `"12"`.

</p>
</details>

---

###### 16. 무엇이 출력 될까요?

```javascript
let number = 0;
console.log(number++);
console.log(++number);
console.log(number);
```

- A: `1` `1` `2`
- B: `1` `2` `2`
- C: `0` `2` `2`
- D: `0` `1` `2`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

The **postfix** unary operator `++`:

1. Returns the value (this returns `0`)
2. Increments the value (number is now `1`)

The **prefix** unary operator `++`:

1. Increments the value (number is now `2`)
2. Returns the value (this returns `2`)

This returns `0 2 2`.

</p>
</details>

---

###### 17. 무엇이 출력 될까요?

```javascript
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}

const person = "Lydia";
const age = 21;

getPersonInfo`${person} is ${age} years old`;
```

- A: `"Lydia"` `21` `["", " is ", " years old"]`
- B: `["", " is ", " years old"]` `"Lydia"` `21`
- C: `"Lydia"` `["", " is ", " years old"]` `21`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

If you use tagged template literals, the value of the first argument is always an array of the string values. The remaining arguments get the values of the passed expressions!

</p>
</details>

---

###### 18. 무엇이 출력 될까요?

```javascript
function checkAge(data) {
  if (data === { age: 18 }) {
    console.log("You are an adult!");
  } else if (data == { age: 18 }) {
    console.log("You are still an adult.");
  } else {
    console.log(`Hmm.. You don't have an age I guess`);
  }
}

checkAge({ age: 18 });
```

- A: `You are an adult!`
- B: `You are still an adult.`
- C: `Hmm.. You don't have an age I guess`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

When testing equality, primitives are compared by their _value_, while objects are compared by their _reference_. JavaScript checks if the objects have a reference to the same location in memory.

The two objects that we are comparing don't have that: the object we passed as a parameter refers to a different location in memory than the object we used in order to check equality.

This is why both `{ age: 18 } === { age: 18 }` and `{ age: 18 } == { age: 18 }` return `false`.

</p>
</details>

---

###### 19. 무엇이 출력 될까요?

```javascript
function getAge(...args) {
  console.log(typeof args);
}

getAge(21);
```

- A: `"number"`
- B: `"array"`
- C: `"object"`
- D: `"NaN"`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

The spread operator (`...args`.) returns an array with arguments. An array is an object, so `typeof args` returns `"object"`

</p>
</details>

---

###### 20. 무엇이 출력 될까요?

```javascript
function getAge() {
  "use strict";
  age = 21;
  console.log(age);
}

getAge();
```

- A: `21`
- B: `undefined`
- C: `ReferenceError`
- D: `TypeError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

With `"use strict"`, you can make sure that you don't accidentally declare global variables. We never declared the variable `age`, and since we use `"use strict"`, it will throw a reference error. If we didn't use `"use strict"`, it would have worked, since the property `age` would have gotten added to the global object.

</p>
</details>

---

###### 21. What's value of `sum`?

```javascript
const sum = eval("10*10+5");
```

- A: `105`
- B: `"105"`
- C: `TypeError`
- D: `"10*10+5"`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

`eval` evaluates codes that's passed as a string. If it's an expression, like in this case, it evaluates the expression. The expression is `10 * 10 + 5`. This returns the number `105`.

</p>
</details>

---

###### 22. How long is cool_secret accessible?

```javascript
sessionStorage.setItem("cool_secret", 123);
```

- A: Forever, the data doesn't get lost.
- B: When the user closes the tab.
- C: When the user closes the entire browser, not only the tab.
- D: When the user shuts off their computer.

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

The data stored in `sessionStorage` is removed after closing the _tab_.

If you used `localStorage`, the data would've been there forever, unless for example `localStorage.clear()` is invoked.

</p>
</details>

---

###### 23. 무엇이 출력 될까요?

```javascript
var num = 8;
var num = 10;

console.log(num);
```

- A: `8`
- B: `10`
- C: `SyntaxError`
- D: `ReferenceError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

With the `var` keyword, you can declare multiple variables with the same name. The variable will then hold the latest value.

You cannot do this with `let` or `const` since they're block-scoped.

</p>
</details>

---

###### 24. 무엇이 출력 될까요?

```javascript
const obj = { 1: "a", 2: "b", 3: "c" };
const set = new Set([1, 2, 3, 4, 5]);

obj.hasOwnProperty("1");
obj.hasOwnProperty(1);
set.has("1");
set.has(1);
```

- A: `false` `true` `false` `true`
- B: `false` `true` `true` `true`
- C: `true` `true` `false` `true`
- D: `true` `true` `true` `true`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

All object keys (excluding Symbols) are strings under the hood, even if you don't type it yourself as a string. This is why `obj.hasOwnProperty('1')` also returns true.

It doesn't work that way for a set. There is no `'1'` in our set: `set.has('1')` returns `false`. It has the numeric type `1`, `set.has(1)` returns `true`.

</p>
</details>

---

###### 25. 무엇이 출력 될까요?

```javascript
const obj = { a: "one", b: "two", a: "three" };
console.log(obj);
```

- A: `{ a: "one", b: "two" }`
- B: `{ b: "two", a: "three" }`
- C: `{ a: "three", b: "two" }`
- D: `SyntaxError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

If you have two keys with the same name, the key will be replaced. It will still be in its first position, but with the last specified value.

</p>
</details>

---

###### 26. The JavaScript global execution context creates two things for you: the global object, and the "this" keyword.

- A: true
- B: false
- C: it depends

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

The base execution context is the global execution context: it's what's accessible everywhere in your code.

</p>
</details>

---

###### 27. 무엇이 출력 될까요?

```javascript
for (let i = 1; i < 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```

- A: `1` `2`
- B: `1` `2` `3`
- C: `1` `2` `4`
- D: `1` `3` `4`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

The `continue` statement skips an iteration if a certain condition returns `true`.

</p>
</details>

---

###### 28. 무엇이 출력 될까요?

```javascript
String.prototype.giveLydiaPizza = () => {
  return "Just give Lydia pizza already!";
};

const name = "Lydia";

name.giveLydiaPizza();
```

- A: `"Just give Lydia pizza already!"`
- B: `TypeError: not a function`
- C: `SyntaxError`
- D: `undefined`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

`String` is a built-in constructor, which we can add properties to. I just added a method to its prototype. Primitive strings are automatically converted into a string object, generated by the string prototype function. So, all strings (string objects) have access to that method!

</p>
</details>

---

###### 29. 무엇이 출력 될까요?

```javascript
const a = {};
const b = { key: "b" };
const c = { key: "c" };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

- A: `123`
- B: `456`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

Object keys are automatically converted into strings. We are trying to set an object as a key to object `a`, with the value of `123`.

However, when we stringify an object, it becomes `"[Object object]"`. So what we are saying here, is that `a["Object object"] = 123`. Then, we can try to do the same again. `c` is another object that we are implicitly stringifying. So then, `a["Object object"] = 456`.

Then, we log `a[b]`, which is actually `a["Object object"]`. We just set that to `456`, so it returns `456`.

</p>
</details>

---

###### 30. 무엇이 출력 될까요?

```javascript
const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"));
const baz = () => console.log("Third");

bar();
foo();
baz();
```

- A: `First` `Second` `Third`
- B: `First` `Third` `Second`
- C: `Second` `First` `Third`
- D: `Second` `Third` `First`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

We have a `setTimeout` function and invoked it first. Yet, it was logged last.

This is because in browsers, we don't just have the runtime engine, we also have something called a `WebAPI`. The `WebAPI` gives us the `setTimeout` function to start with, and for example the DOM.

After the _callback_ is pushed to the WebAPI, the `setTimeout` function itself (but not the callback!) is popped off the stack.

<img src="https://i.imgur.com/X5wsHOg.png" width="200">

Now, `foo` gets invoked, and `"First"` is being logged.

<img src="https://i.imgur.com/Pvc0dGq.png" width="200">

`foo` is popped off the stack, and `baz` gets invoked. `"Third"` gets logged.

<img src="https://i.imgur.com/WhA2bCP.png" width="200">

The WebAPI can't just add stuff to the stack whenever it's ready. Instead, it pushes the callback function to something called the _queue_.

<img src="https://i.imgur.com/NSnDZmU.png" width="200">

This is where an event loop starts to work. An **event loop** looks at the stack and task queue. If the stack is empty, it takes the first thing on the queue and pushes it onto the stack.

<img src="https://i.imgur.com/uyiScAI.png" width="200">

`bar` gets invoked, `"Second"` gets logged, and it's popped off the stack.

</p>
</details>

---

###### 31. What is the event.target when clicking the button?

```html
<div onclick="console.log('first div')">
  <div onclick="console.log('second div')">
    <button onclick="console.log('button')">
      Click!
    </button>
  </div>
</div>
```

- A: Outer `div`
- B: Inner `div`
- C: `button`
- D: An array of all nested elements.

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

The deepest nested element that caused the event is the target of the event. You can stop bubbling by `event.stopPropagation`

</p>
</details>

---

###### 32. When you click the paragraph, what's the logged output?

```html
<div onclick="console.log('div')">
  <p onclick="console.log('p')">
    Click here!
  </p>
</div>
```

- A: `p` `div`
- B: `div` `p`
- C: `p`
- D: `div`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

If we click `p`, we see two logs: `p` and `div`. During event propagation, there are 3 phases: capturing, target, and bubbling. By default, event handlers are executed in the bubbling phase (unless you set `useCapture` to `true`). It goes from the deepest nested element outwards.

</p>
</details>

---

###### 33. 무엇이 출력 될까요?

```javascript
const person = { name: "Lydia" };

function sayHi(age) {
  console.log(`${this.name} is ${age}`);
}

sayHi.call(person, 21);
sayHi.bind(person, 21);
```

- A: `undefined is 21` `Lydia is 21`
- B: `function` `function`
- C: `Lydia is 21` `Lydia is 21`
- D: `Lydia is 21` `function`

<details><summary><b>정답</b></summary>
<p>

#### 정답: D

With both, we can pass the object to which we want the `this` keyword to refer to. However, `.call` is also _executed immediately_!

`.bind.` returns a _copy_ of the function, but with a bound context! It is not executed immediately.

</p>
</details>

---

###### 34. 무엇이 출력 될까요?

```javascript
function sayHi() {
  return (() => 0)();
}

typeof sayHi();
```

- A: `"object"`
- B: `"number"`
- C: `"function"`
- D: `"undefined"`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

The `sayHi` function returns the returned value of the immediately invoked function (IIFE). This function returned `0`, which is type `"number"`.

FYI: there are only 7 built-in types: `null`, `undefined`, `boolean`, `number`, `string`, `object`, and `symbol`. `"function"` is not a type, since functions are objects, it's of type `"object"`.

</p>
</details>

---

###### 35. Which of these values are falsy?

```javascript
0;
new Number(0);
("");
(" ");
new Boolean(false);
undefined;
```

- A: `0`, `''`, `undefined`
- B: `0`, `new Number(0)`, `''`, `new Boolean(false)`, `undefined`
- C: `0`, `''`, `new Boolean(false)`, `undefined`
- D: All of them are falsy

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

There are only six falsy values:

- `undefined`
- `null`
- `NaN`
- `0`
- `''` (empty string)
- `false`

Function constructors, like `new Number` and `new Boolean` are truthy.

</p>
</details>

---

###### 36. 무엇이 출력 될까요?

```javascript
console.log(typeof typeof 1);
```

- A: `"number"`
- B: `"string"`
- C: `"object"`
- D: `"undefined"`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

`typeof 1` returns `"number"`.
`typeof "number"` returns `"string"`

</p>
</details>

---

###### 37. 무엇이 출력 될까요?

```javascript
const numbers = [1, 2, 3];
numbers[10] = 11;
console.log(numbers);
```

- A: `[1, 2, 3, 7 x null, 11]`
- B: `[1, 2, 3, 11]`
- C: `[1, 2, 3, 7 x empty, 11]`
- D: `SyntaxError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

When you set a value to an element in an array that exceeds the length of the array, JavaScript creates something called "empty slots". These actually have the value of `undefined`, but you will see something like:

`[1, 2, 3, 7 x empty, 11]`

depending on where you run it (it's different for every browser, node, etc.)

</p>
</details>

---

###### 38. 무엇이 출력 될까요?

```javascript
(() => {
  let x, y;
  try {
    throw new Error();
  } catch (x) {
    (x = 1), (y = 2);
    console.log(x);
  }
  console.log(x);
  console.log(y);
})();
```

- A: `1` `undefined` `2`
- B: `undefined` `undefined` `undefined`
- C: `1` `1` `2`
- D: `1` `undefined` `undefined`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

The `catch` block receives the argument `x`. This is not the same `x` as the variable when we pass arguments. This variable `x` is block-scoped.

Later, we set this block-scoped variable equal to `1`, and set the value of the variable `y`. Now, we log the block-scoped variable `x`, which is equal to `1`.

Outside of the `catch` block, `x` is still `undefined`, and `y` is `2`. When we want to `console.log(x)` outside of the `catch` block, it returns `undefined`, and `y` returns `2`.

</p>
</details>

---

###### 39. Everything in JavaScript is either a...

- A: primitive or object
- B: function or object
- C: trick question! only objects
- D: number or object

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

JavaScript only has primitive types and objects.

Primitive types are `boolean`, `null`, `undefined`, `bigint`, `number`, `string`, and `symbol`.

What differentiates a primitive from an object is that primitives do not have any properties or methods; however, you'll note that `'foo'.toUpperCase()` evaluates to `'FOO'` and does not result in a `TypeError`. This is because when you try to access a property or method on a primitive like a string, JavaScript will implicity wrap the object using one of the wrapper classes, i.e. `String`, and then immediately discard the wrapper after the expression evaluates. All primitives except for `null` and `undefined` exhibit this behaviour.

</p>
</details>

---

###### 40. 무엇이 출력 될까요?

```javascript
[[0, 1], [2, 3]].reduce(
  (acc, cur) => {
    return acc.concat(cur);
  },
  [1, 2]
);
```

- A: `[0, 1, 2, 3, 1, 2]`
- B: `[6, 1, 2]`
- C: `[1, 2, 0, 1, 2, 3]`
- D: `[1, 2, 6]`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

`[1, 2]` is our initial value. This is the value we start with, and the value of the very first `acc`. During the first round, `acc` is `[1,2]`, and `cur` is `[0, 1]`. We concatenate them, which results in `[1, 2, 0, 1]`.

Then, `[1, 2, 0, 1]` is `acc` and `[2, 3]` is `cur`. We concatenate them, and get `[1, 2, 0, 1, 2, 3]`

</p>
</details>

---

###### 41. 무엇이 출력 될까요?

```javascript
!!null;
!!"";
!!1;
```

- A: `false` `true` `false`
- B: `false` `false` `true`
- C: `false` `true` `true`
- D: `true` `true` `false`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

`null` is falsy. `!null` returns `true`. `!true` returns `false`.

`""` is falsy. `!""` returns `true`. `!true` returns `false`.

`1` is truthy. `!1` returns `false`. `!false` returns `true`.

</p>
</details>

---

###### 42. What does the `setInterval` method return in the browser?

```javascript
setInterval(() => console.log("Hi"), 1000);
```

- A: a unique id
- B: the amount of milliseconds specified
- C: the passed function
- D: `undefined`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

It returns a unique id. This id can be used to clear that interval with the `clearInterval()` function.

</p>
</details>

---

###### 43. What does this return?

```javascript
[..."Lydia"];
```

- A: `["L", "y", "d", "i", "a"]`
- B: `["Lydia"]`
- C: `[[], "Lydia"]`
- D: `[["L", "y", "d", "i", "a"]]`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

A string is an iterable. The spread operator maps every character of an iterable to one element.

</p>
</details>

---

###### 44. 무엇이 출력 될까요?

```javascript
function* generator(i) {
  yield i;
  yield i * 2;
}

const gen = generator(10);

console.log(gen.next().value);
console.log(gen.next().value);
```

- A: `[0, 10], [10, 20]`
- B: `20, 20`
- C: `10, 20`
- D: `0, 10 and 10, 20`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

Regular functions cannot be stopped mid-way after invocation. However, a generator function can be "stopped" midway, and later continue from where it stopped. Every time a generator function encounters a `yield` keyword, the function yields the value specified after it. Note that the generator function in that case doesn’t _return_ the value, it _yields_ the value.

First, we initialize the generator function with `i` equal to `10`. We invoke the generator function using the `next()` method. The first time we invoke the generator function, `i` is equal to `10`. It encounters the first `yield` keyword: it yields the value of `i`. The generator is now "paused", and `10` gets logged.

Then, we invoke the function again with the `next()` method. It starts to continue where it stopped previously, still with `i` equal to `10`. Now, it encounters the next `yield` keyword, and yields `i * 2`. `i` is equal to `10`, so it returns `10 * 2`, which is `20`. This results in `10, 20`.

</p>
</details>

---

###### 45. What does this return?

```javascript
const firstPromise = new Promise((res, rej) => {
  setTimeout(res, 500, "one");
});

const secondPromise = new Promise((res, rej) => {
  setTimeout(res, 100, "two");
});

Promise.race([firstPromise, secondPromise]).then(res => console.log(res));
```

- A: `"one"`
- B: `"two"`
- C: `"two" "one"`
- D: `"one" "two"`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

When we pass multiple promises to the `Promice.race` method, it resolves/rejects the _first_ promise that resolves/rejects. To the `setTimeout` method, we pass a timer: 500ms for the first promise (`firstPromise`), and 100ms for the second promise (`secondPromise`). This means that the `secondPromise` resolves first with the value of `'two'`. `res` now holds the value of `'two'`, which gets logged.

</p>
</details>

---

###### 46. 무엇이 출력 될까요?

```javascript
let person = { name: "Lydia" };
const members = [person];
person = null;

console.log(members);
```

- A: `null`
- B: `[null]`
- C: `[{}]`
- D: `[{ name: "Lydia" }]`

<details><summary><b>정답</b></summary>
<p>

#### 정답: D

First, we declare a variable `person` with the value of an object that has a `name` property.

<img src="https://i.imgur.com/TML1MbS.png" width="200">

Then, we declare a variable called `members`. We set the first element of that array equal to the value of the `person` variable. Objects interact by _reference_ when setting them equal to each other. When you assign a reference from one variable to another, you make a _copy_ of that reference. (note that they don't have the _same_ reference!)

<img src="https://i.imgur.com/FSG5K3F.png" width="300">

Then, we set the variable `person` equal to `null`.

<img src="https://i.imgur.com/sYjcsMT.png" width="300">

We are only modifying the value of the `person` variable, and not the first element in the array, since that element has a different (copied) reference to the object. The first element in `members` still holds its reference to the original object. When we log the `members` array, the first element still holds the value of the object, which gets logged.

</p>
</details>

---

###### 47. 무엇이 출력 될까요?

```javascript
const person = {
  name: "Lydia",
  age: 21
};

for (const item in person) {
  console.log(item);
}
```

- A: `{ name: "Lydia" }, { age: 21 }`
- B: `"name", "age"`
- C: `"Lydia", 21`
- D: `["name", "Lydia"], ["age", 21]`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

With a `for-in` loop, we can iterate through object keys, in this case `name` and `age`. Under the hood, object keys are strings (if they're not a Symbol). On every loop, we set the value of `item`equal to the current key it’s iterating over. First, `item` is equal to `name`, and gets logged. Then, `item` is equal to `age`, which gets logged.

</p>
</details>

---

###### 48. 무엇이 출력 될까요?

```javascript
console.log(3 + 4 + "5");
```

- A: `"345"`
- B: `"75"`
- C: `12`
- D: `"12"`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

Operator associativity is the order in which the compiler evaluates the expressions, either left-to-right or right-to-left. This only happens if all operators have the _same_ precedence. We only have one type of operator: `+`. For addition, the associativity is left-to-right.

`3 + 4` gets evaluated first. This results in the number `7`.

`7 + '5'` results in `"75"` because of coercion. JavaScript converts the number `7` into a string, see question 15. We can concatenate two strings using the `+`operator. `"7" + "5"` results in `"75"`.

</p>
</details>

---

###### 49. What's the value of `num`?

```javascript
const num = parseInt("7*6", 10);
```

- A: `42`
- B: `"42"`
- C: `7`
- D: `NaN`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

Only the first numbers in the string is returned. Based on the _radix_ (the second argument in order to specify what type of number we want to parse it to: base 10, hexadecimal, octal, binary, etc.), the `parseInt` checks whether the characters in the string are valid. Once it encounters a character that isn't a valid number in the radix, it stops parsing and ignores the following characters.

`*` is not a valid number. It only parses `"7"` into the decimal `7`. `num` now holds the value of `7`.

</p>
</details>

---

###### 50. What's the output`?

```javascript
[1, 2, 3].map(num => {
  if (typeof num === "number") return;
  return num * 2;
});
```

- A: `[]`
- B: `[null, null, null]`
- C: `[undefined, undefined, undefined]`
- D: `[ 3 x empty ]`

<details><summary><b>정답</b></summary>
<p>

#### 정답: C

When mapping over the array, the value of `num` is equal to the element it’s currently looping over. In this case, the elements are numbers, so the condition of the if statement `typeof num === "number"` returns `true`. The map function creates a new array and inserts the values returned from the function.

However, we don’t return a value. When we don’t return a value from the function, the function returns `undefined`. For every element in the array, the function block gets called, so for each element we return `undefined`.

</p>
</details>

---

###### 51. 무엇이 출력 될까요?

```javascript
function getInfo(member, year) {
  member.name = "Lydia";
  year = 1998;
}

const person = { name: "Sarah" };
const birthYear = "1997";

getInfo(person, birthYear);

console.log(person, birthYear);
```

- A: `{ name: "Lydia" }, "1997"`
- B: `{ name: "Sarah" }, "1998"`
- C: `{ name: "Lydia" }, "1998"`
- D: `{ name: "Sarah" }, "1997"`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

Arguments are passed by _value_, unless their value is an object, then they're passed by _reference_. `birthYear` is passed by value, since it's a string, not an object. When we pass arguments by value, a _copy_ of that value is created (see question 46).

The variable `birthYear` has a reference to the value `"1997"`. The argument `year` also has a reference to the value `"1997"`, but it's not the same value as `birthYear` has a reference to. When we update the value of `year` by setting `year` equal to `"1998"`, we are only updating the value of `year`. `birthYear` is still equal to `"1997"`.

The value of `person` is an object. The argument `member` has a (copied) reference to the _same_ object. When we modify a property of the object `member` has a reference to, the value of `person` will also be modified, since they both have a reference to the same object. `person`'s `name` property is now equal to the value `"Lydia"`

</p>
</details>

---

###### 52. 무엇이 출력 될까요?

```javascript
function greeting() {
  throw "Hello world!";
}

function sayHi() {
  try {
    const data = greeting();
    console.log("It worked!", data);
  } catch (e) {
    console.log("Oh no an error!", e);
  }
}

sayHi();
```

- A: `"It worked! Hello world!"`
- B: `"Oh no an error: undefined`
- C: `SyntaxError: can only throw Error objects`
- D: `"Oh no an error: Hello world!`

<details><summary><b>정답</b></summary>
<p>

#### 정답: D

With the `throw` statement, we can create custom errors. With this statement, you can throw exceptions. An exception can be a <b>string</b>, a <b>number</b>, a <b>boolean</b> or an <b>object</b>. In this case, our exception is the string `'Hello world'`.

With the `catch` statement, we can specify what to do if an exception is thrown in the `try` block. An exception is thrown: the string `'Hello world'`. `e` is now equal to that string, which we log. This results in `'Oh an error: Hello world'`.

</p>
</details>

---

###### 53. 무엇이 출력 될까요?

```javascript
function Car() {
  this.make = "Lamborghini";
  return { make: "Maserati" };
}

const myCar = new Car();
console.log(myCar.make);
```

- A: `"Lamborghini"`
- B: `"Maserati"`
- C: `ReferenceError`
- D: `TypeError`

<details><summary><b>정답</b></summary>
<p>

#### 정답: B

When you return a property, the value of the property is equal to the _returned_ value, not the value set in the constructor function. We return the string `"Maserati"`, so `myCar.make` is equal to `"Maserati"`.

</p>
</details>

---

###### 54. 무엇이 출력 될까요?

```javascript
(() => {
  let x = (y = 10);
})();

console.log(typeof x);
console.log(typeof y);
```

- A: `"undefined", "number"`
- B: `"number", "number"`
- C: `"object", "number"`
- D: `"number", "undefined"`

<details><summary><b>정답</b></summary>
<p>

#### 정답: A

`let x = y = 10;` is actually shorthand for:

```javascript
y = 10;
let x = y;
```

When we set `y` equal to `10`, we actually add a property `y` to the global object (`window` in browser, `global` in Node). In a browser, `window.y` is now equal to `10`.

Then, we declare a variable `x` with the value of `y`, which is `10`. Variables declared with the `let` keyword are _block scoped_, they are only defined within the block they're declared in; the immediately-invoked function (IIFE) in this case. When we use the `typeof` operator, the operand `x` is not defined: we are trying to access `x` outside of the block it's declared in. This means that `x` is not defined. Values who haven't been assigned a value or declared are of type `"undefined"`. `console.log(typeof x)` returns `"undefined"`.

However, we created a global variable `y` when setting `y` equal to `10`. This value is accessible anywhere in our code. `y` is defined, and holds a value of type `"number"`. `console.log(typeof y)` returns `"number"`.

</p>
</details>