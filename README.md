# pmh-only/style
@pmh-only 의 코딩스타일

> JavaScript(TS) 기준으로 작성되었습니다\
> 기본적으로 린터의 설정을 따르는 편입니다

## 1. 변수/상수/함수 선언
### 선언자
* `const`의 사용을 1순위로 한다
* `var`를 사용한 선언을 **금지**한다
* `let`를 사용한 선언은 되도록 하지 않는다
* 값이 변하지 않는 변수/상수는 `const`만을 사용한다
* 모든 넓은 의미의 객체(객체, 배열 등...)는 `const`로 선언한다
* 화살표 함수를 변수에 대입하여 선언할때에는 `const`로 선언한다

```js
var variable = 30 // 금지
let unmodifed = 10 // 금지 (값이 변한적이 없을경우)

const car = new Car() // 좋음
const arr = ['alice', 'bob'] // 좋음
const obj = { name: 'alice' } // 좋음
const func = (a, b) => a + b // 좋음

let mutable = 30 // 가능하나, 자제 (값이 변할경우)
mutable += 30
```

### 변수/상수/함수 이름
* 최대한 Ascii에서 표현 가능한 문자를 사용한다
* 모든 변수/상수/함수 이름은 약자를 쓰지 않으며 정확한 의미를 가져야 한다 (단, forEach나 filter에서 사용되는 등 매우 일시적일 경우 약자를 사용할 수 있다)
* 전역에서 쓰이고 값이 변하지 않는 상수는 `CAPITAL_SNAKE_CASE`를 사용한다
* 일시적으로 쓰이는 변수/상수는 `camelCase`를 사용한다
* 클래스나 기타 Type(Interface, Enum 등...)은 `PascalCase`를 사용한다
* 함수 이름은 가독성을 위해 동사로 시작하는것을 권장한다
* 한 타입만을 포함하는 배열일 경우 가독성을 위해 이름뒤에 복수를 뜻하는 `s`를 삽입하는것을 권장한다
* boolean을 타입으로 하는 변수/상수는 가독성을 위해 `is`를 앞에 붙히는것을 권장한다

```js
const SERVER_PORT = 8080 // 좋음
class BookInfo {} // 좋음

const languages = ['c', 'cs', 'js', 'ts'] // 좋음 (s를 붙혀 배열임을 표현)
for (const language of languages) { // 좋음
  // ...
}

const 웹포트 = 3030 // 자제 (Ascii에서 표현 불가능한 이름)
const srv = new Server() // 자제 (의미가 불분명한 약자 (service? server?))

languages.filter((e) => e !== 'cs') // 가능 (매우 일시적인 e의 사용)

const isEnabled = true // 좋음 (is를 앞에 붙혀 가독성을 높힘)
```

### 함수 선언
* 선언하고자 하는 함수가 작업이 간단하고 리턴이 단순한 경우 화살표 함수 사용을 권장한다
* 화살표 함수가 너무 긴경우 가독성을 위해 `=>` 이후에 엔터를 입력 하는것을 권장한다
* 많은 작업이 필요한 경우 `function` 키워드 사용을 권장한다

```js
const sumAges = (x, y) => x.age + y.age // 좋음
const formatGreeter = (name) => 'Hello, ' + name + '!' // 좋음

const formatLongURL = (baseURL, path, query) =>
  'https://' + baseURL + '/' + path + '?q=' + query // 좋음 (긴경우 화살표후 엔터)

const doManyThings = (key) => { if (key.length < 3) { return null } else { return decrypt(key) } }
// 자제 (화살표 함수에 너무 많은 작업이 몰려있음)

function doManyThings (key) { // 좋음
  if (key.length < 3) return null
  else return decrypt(key)
}
```

2021/01/10 작성중..
<!-- ## 키워드 사용
### 반복문
* 라벨링을 사용한 반복을 **금지**한다
* `for`의 사용을 1순위로 하며 `while` 사용은 자제한다
* 배열 내용을 반복할경우 가독성을 위해 `.forEach()` 보다 `for (...in...)`를 권장한다
* `continue`의 사용은 가능하되 라벨링은 **금지**한다

```js

``` -->
