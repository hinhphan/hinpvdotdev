# Event Loop

+ Là một cơ chế cho phép xử lý các tác vụ bất đồng bộ trong JavaScript (mặc dù JavaScript là single-thread)
+ Sử dụng một vòng lặp vô tận để kiểm tra, quản lý các tác vụ
+ Javascript là **single-thread** (đơn luồng)
+ Các thành phần liên quan: Event Loop, Call Stack, Web APIs, Task Queue, Microtask Queue.
+ Tham khảo: [https://www.youtube.com/watch?v=eiC58R16hb8](https://www.youtube.com/watch?v=eiC58R16hb8)

## Event loop

+ Liên tục kiểm tra Call Stack xem có trống hay không
+ Nếu trống thì chuyển tác vụ tiếp theo vào Call Stack để thực thi
+ ...

## Call Stack

+ Dùng để quản lý việc thực thi tác vụ của chương trình
+ Hoạt động theo cơ chế FILO (First In Last Out)
+ Tác vụ nào thực hiện sẽ bị đẩy ra khỏi Call Stack
+ ...

=> JavaScript chỉ có thể xử lý 1 tác vụ tại một thời điểm 

=> Tác vụ chạy lâu có thể chặn các tác vụ thực thi phía sau => Treo chương trình

=> Ở phần sau chúng ta sẽ tìm phương pháp xử lý khi bị treo do có tác vụ chạy lâu

## Web APIs

+ Là môi trường chạy do trình duyệt cung cấp
+ Xử lý các tác vụ ngoài trình thông dịch của JavaScript
+ Các Web APIs có thể kể đến như: fetch, setTimeout, URL, localStorage, sessionStorage, document,...
+ JavaScript sẽ chuyển giao các công việc tương ứng cho các API trên và cung cấp một hàm callback để thực thi khi API hoàn tất công việc được chỉ định
+ Khi đó callback sẽ được đẩy vào Task Queue
+ ...

## Task Queue

+ Là một hàng đợi tác vụ chờ được đẩy vào Call Stack để thực thi
+ Hoạt động theo cơ chế FIFO (First In First Out)
+ Là nơi chứa các callback của **Macrotask** như: setTimeout, setInterval, element events, setImmediate, requestAnimationFrame, I/O, UI rendering,...
+ Sẽ chỉ được thực hiện sau khi Call Stack trống và Microtask Queue trống
+ Các tên gọi khác: Event Queue, Callback Queue, Macrotask Queue,...
+ ...

## Microtask Queue

+ Giống với Task Queue, nhưng độ ưu tiên cao hơn
+ Là nơi chứa các callback của **Microtask** như: process.nextTick, Promises, Object.observe, MutationObserver,...
+ Nếu có await thì tất cả những gì sau await sẽ được đưa vào Microtask Queue
+ Đẩy job liên tục vào Microtask Queue có thể làm trình duyệt bị treo
+ ...

## Vậy thì trình tự chạy các tác vụ sẽ như nào ?

+ Code đồng bộ > Microtask > (Rendering) > Macrotask
+ ...

## Lưu ý thêm

+ Main Thread (UI Thread): hầu hết code mà chúng ta viết thực thi ở thread này, nếu mà thread này bị block thì web sẽ bị treo và trình duyệt báo lỗi **Page unresponsive**
+ Worker: sẽ có thread riêng so với Main Thread kể trên
+ Mỗi thread chỉ có 1 Event Loop
+ Mỗi tab trên trình duyệt sẽ có một môi trường riêng, với Event Loop riêng
+ setTimeout() với time = 5s thì là chờ sau 5s mới cho callback vào Macrotask Queue (Nhiệm vụ check 5s nói trước đó do trình duyệt hoặc Nodejs runtime chứ k phải do Event Loop xử lý)
+ Khi await Promise, Event Loop sẽ chờ cho cái Promise đó resolve thì mới chạy tiếp
+ ...

## Ví dụ: Thử phân tích thứ tự chạy của đoạn code sau và đưa ra kết quả

```js
console.log("script start");

setTimeout(function() {
  console.log("setTimeout 1 start");

  setTimeout(function() {
    console.log("nested setTimeout 1");

    new Promise(function(resolve) {
      console.log("promise in nested setTimeout 1");
      resolve();
    }).then(function() {
      console.log("then in nested setTimeout 1");
    });

  }, 0);

  new Promise(function(resolve) {
    console.log("promise in setTimeout 1");
    resolve();
  }).then(function() {
    console.log("then in setTimeout 1");

    setTimeout(function() {
      console.log("nested setTimeout 2");

      new Promise(function(resolve) {
        console.log("promise in nested setTimeout 2");
        resolve();
      }).then(function() {
        console.log("then in nested setTimeout 2");
      });

    }, 0);
  });

  console.log("setTimeout 1 end");
}, 0);

new Promise(function(resolve) {
  console.log("outer promise");
  resolve();
}).then(function() {
  console.log("outer promise then");

  return new Promise(function(resolve) {
    console.log("nested promise");
    resolve();
  }).then(function() {
    console.log("nested promise then");
  });
});

setTimeout(function() {
  console.log("setTimeout 2 start");

  new Promise(function(resolve) {
    console.log("promise in setTimeout 2");
    resolve();
  }).then(function() {
    console.log("then in setTimeout 2");
  });

  console.log("setTimeout 2 end");
}, 0);

console.log("script end");
```

Kết quả:

```js

```