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
+ Là nơi chứa các callback của Macrotask như: setTimeout, setInterval, element events, setImmediate, requestAnimationFrame, I/O, UI rendering,...
+ Các tên gọi khác: Event Queue, Callback Queue, Macrotask Queue,...
+ ...

## Microtask Queue

+ Giống với Task Queue, nhưng độ ưu tiên cao hơn
+ Là nơi chứa các callback của Microtask như: process.nextTick, Promises, Object.observe, MutationObserver,...
+ ...