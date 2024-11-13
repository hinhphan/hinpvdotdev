# Debounce, Throttle

+ Trong lập trình sẽ có các trường hợp xử lý nặng, tốn thời gian nhưng không cần gọi liên tục. Ví dụ, tính năng tìm kiếm, chỉ tìm kiếm khi người dùng nhập xong từ khóa tìm kiếm
=> sẽ sử dụng Debounce: **chỉ thực thi 1 lần SAU một khoảng thời gian nhất định**

+ Còn Throttle sẽ khác với Debounce ở chỗ: **chỉ thực thi 1 lần TRONG một khoảng thời gian nhất định**

## Debounce

+ Cách thức hoạt động:

func search(string keySearch), tiến hành Debounce trong 1000ms

1. Người dùng nhập keySearch => Debounce sẽ tạo timer thực thi func search() sau 1000ms
2. Trong khoảng thời gian 1000ms đó mà người dùng lại tiến hành nhập keySearch thì sẽ clear timer đó đi và tạo timer mới, cũng sẽ thực thi func search() sau 1000ms
3. Nếu người dùng vẫn tiếp tục nhập keySearch thì sẽ lặp lại bước 2
4. Nếu người dùng không nhập nữa, sau 1000ms thì func search() mới được gọi để xử lý

## Throttle

+ Cách thức hoạt động:

func search(string keySearch), tiến hành Throttle trong 1000ms
Set trường hợp isThrottle = false

1. Người dùng nhập keySearch => kiểm tra isThrottle

Nếu isThrottle = False => set isThrottle = True => thực thi func search() => (Step X) Tạo timer xử lý set isThrottle = False sau 1000ms

2. Trong khoảng 500ms của Step X, tiến hành nhập keySearch thì lúc này:

Vì isThrottle = True => không xử lý gì...

3. Sau 1000ms của Step X, nếu nhập keySearch thì sẽ tiến hành xử lý giống bước 1

## Ứng dụng thực thế:

+ Lấy giá trị cuối cùng của phần tử nào đó khi resize window
+ Không gọi API lấy dữ liệu khi người dùng không ngừng nhập input
+ Lấy dữ liệu tiếp theo khi scroll xuống cuối trang
+ Đo vị trí scroll sau một thời gian nhất định
+ ...
