# Tree Shaking

+ Kỹ thuật loại bỏ "code dead" (code chét) (dead code elimination technique)
+ Khi code mà import thì chỉ import các hàm biến mà mình sử dụng, không import cả một thư viện
+ Ví dụ:

```js
// common.js
export function a() {

}

export function b() {

}

export function c() {

}

// Giả định x.js chỉ sử dụng func a() và c()

// K nên
import * as common from './common.js'

// Nên
import { a, c } from './common.js'
```

+ Cách kiểm tra thư viện hỗ trợ Tree shaking: [https://bundlephobia.com/](https://bundlephobia.com/)