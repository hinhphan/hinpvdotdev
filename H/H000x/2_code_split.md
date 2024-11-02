# Code Split

+ Là việc tách một file (css, js) lớn thành các file nhỏ hơn
+ Được hiểu như sau:

Ta có 2 màn hình X và Y đang dùng chung file js là app.js (100 KB)

nhưng mà trong file app.js, phần code xử lý của màn X và Y là có sự khác nhau ( không liên quan đến nhau )

=> có thể tách thành các file nhỏ cho từng màn

```text
                  ┌ x.js (45 KB) => khi hiển thị màn X thì chỉ load x.js
app.js (100 KB) ──│
                  └ y.js (55 KB) => khi hiển thị màn Y thì chỉ load y.js
```

+ Đối tượng thường được áp dụng: Router, Component,...

+ Từ khóa: Lazy loading Router, Lazy loading Component,...