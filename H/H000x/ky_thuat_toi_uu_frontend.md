# Các kỹ thuật liên quan đến tối ưu FrontEnd

## CRP (Critical Rendering Path)

+ Là trình tự các bước mà trình duyệt trải qua để chuyển đổi HTML, CSS và JavaScript thành các pixel trên màn hình
+ Là hiểu được bản chất, cách thức mà trình duyệt render lên một trang web
+ Từ đó, dễ dàng tối ưu hiệu năng Frontend một cách hiệu quả hơn
+ Web vitals: là một sáng kiến ​​của Google nhằm cung cấp các hướng dẫn để cải thiện trải nghiệm người dùng trên trang web

## Những vấn đề xoay quanh CRP

### Task

+ Event loop
+ Break long task
+ Web worker
+ Debounce, Throttle

### Size

+ Minify & Compress
+ Code split
+ Tree shaking
+ Bundle analyzer
+ Network

### Cache

+ IndexDB
+ Memorization
+ CDN
+ Service worker

### Priority

+ Lazy loading
+ Intersection Observer
+ Preload, Prefetch, Preconnect
+ Async, Defer
