# pmh-only/style
@pmh-only 의 코딩스타일

> JavaScript(TS) 기준으로 작성되었습니다\
> 기본적으로 린터의 설정을 따르는 편입니다

## 1. 변수/상수/함수 선언
* 사용하지 않는 변수/상수/함수는 선언하지 않는다

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

// 자제 (화살표 함수에 너무 많은 작업이 몰려있음)
const doManyThings = (key) => { if (key.length < 3) { return null } else { return decrypt(key) } }

function doManyThings (key) { // 좋음
  if (key.length < 3) return null
  else return decrypt(key)
}
```

## 키워드 사용
### 조건문
* `undefined`와 `null`의 감지는 `!`를 사용한다
* 빈 문자열의 감지는 `string.length < 0`를 사용한다
* 빈 배열과 빈 객체의 감지는 `array.length < 0`, `Object.keys(obj).length < 0`를 사용한다
* 삼행연산은 선언문/대입문에서만 사용하는것을 권장한다

```js
const emptyString = ''
const emptyArray = []
const emptyObject = {}

const [firstItem] = emptyArray // = undefined

if (!firstItem) console.log('firstItem doesn\'t exist') // 좋음 (undefined의 감지는 !를 이용)
if (emptyString.length < 0) console.log('string is empty') // 좋음 (빈 문자열의 감지는 length이용)
if (emptyArray.length < 0) console.log('string is empty') // 좋음 (문자열과 마찬가지)
if (Object.keys(emptyObject).length < 0) console.log('string is empty') // 좋음 (빈 객체의 감지는 Object.keys 사용)

const longerPerson = alice.age > bob.age ? 'alice' : 'bob' // 좋음 (선언문에서 삼행연산을 사용)
```

### 반복문
* 라벨링을 사용한 반복을 **금지**한다
* `for`의 사용을 1순위로 하며 `while` 사용은 자제한다
* 배열 내용을 반복할경우 가독성을 위해 `.forEach()` 보다 `for (...of...)`를 권장한다 (단, 함수를 미리 선언 한 경우 `forEach`를 권장한다)
* `continue`의 사용은 가능하되 `continue` 뒤에 아무런 구문을 적지 않는다

```js
const fileExtensions = ['.c', '.cs', '.js', '.ts', 'namu']
const validExtensions = []

function logEach (item, index) {
  console.log((index + 1) + '. ' + item)
}

for (const fileExtension of fileExtensions) { // 좋음 (of 키워드 사용)
  if (!fileExtension.startsWith('.')) continue // 좋음 (continue뒤에 아무 구문 없음)
  validExtensions.push(fileExtension)
}

validExtensions.forEach(logEach) // 좋음 (미리 선언된 함수는 forEach 사용)
```

## 비동기 작업
* 기본적으로 비동기 작업의 사용을 자제한다
* 모든 비동기 작업은 `async`, `await` 사용을 1순위로 한다
* 가독성을 위해 `Promise`와 `Callback`의 사용을 자제한다

```js
// 좋음 (가독성을 위해 적절하게 await, Promise, Callback을 섞어 씀, 한줄로 json파싱까지 완료)
const response = await fetch('https://h_api.pmh.codes').then((res) => res.json())

async function doAsyncJob (id) { // 좋음 (await 사용)
  const [data] = await db.select('*').from('userdata').where({ id })
  return data
}

function doAsyncJob () { // 자제 (Callback 지옥임, 참고로 이 함수는 위 함수와 같은일을 함)
  return new Promise((resolve, reject) => {
    db.select('*').from('userdata').where({ id }).then(([data]) => {
      resolve(data)
    }).catch(reject)
  })
}
```
