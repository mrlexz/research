# research
# Redux toolkit
Redux toolkit là thư viện dùng để viết Redux tốt, dễ và đơn giản hơn.
Redux toolkit giải quyết các vấn đề của Redux: 
+ Cấu hình Redux store khá phức tạp
+ Cài đặt thêm nhiều package mới có thể hoàn chỉnh logic quản lý state
+ Quá nhiều boilerpalte code
Redux toolkit bao gồm 
+ configureStore(): có sẵn Redux DevTools và middleware redux-thunk
+ createReducer(): có thể mutate data trực tiếp vì dùng ImmerJs ở phía dưới
+ createSlice(): gom create action và create reducer viết chung trong 1 hàm.
Redux-thunk
  - Ưu: 
    + ít boilerplate code
    + dễ hiểu, dễ học, dễ tiếp cận hơn saga
  - Nhược:
    + có thể khó scale up
    + actions có thể có nhiều async logic
    + khó để test
Redux-saga
  - Ưu:
    + dễ scale up hơn redux-thunk
    + actions là pure 
    + dễ test vì tất cả async logic nằm cùng nhau
  - Nhược:
    + Nhiều boilerplate code
    + khó hiểu, nhiều khái niệm phải học hơn như generator functions, các redux-saga effects,...

Middleware là phần lớp nằm giữa reducers và dispatch action, là trước khi reducers nhận được action 
và sau khi 1 actions được dispatch.
Bởi vì redux có 1 số rằng buộc như các xử lí trong reducers phải là các hàm đồng bộ và pure, 
trả về 1 state mớivà reducers không được sử dụng các hàm async vì ko được thay đổi global state nên 
những việc xử lí side effect như call api, đọc cookie từ trình duyệt,.. này được xử lí ở middleware

- Đồng bộ dữ liệu được lưu dưới local (local của máy hoặc browser) và store
=> sử dụng thư viện "redux-persist" nó sẽ lấy redux state object và lưu nó vào storage, sau đó khi chạy
ứng dụng nó sẽ truy xuất trạng thái persisted này và lưu ngược trở về redux. Thư viện cung cấp 1 số option
có thể tùy chỉnh những gì được lưu
- Sự khác nhau giữa compose và applyMiddleWare là gì? Khi nào sử dụng cái nào.
=> applyMiddleWare: là 1 store enhancers, để wrapping các store s dispatch function(theo em hiểu là những gì
có liên quan tới dispatch).
    compose: cho phép kết hợp các enhancers có thể ko liên quan tới dispatch ex: kết hợp applyMiddleWare và devTools

  ----------------------------------------------------------------------------------------------------  
# Redux vs ContextAPI
  Việc quản lí vấn đề chia sẻ state trong react thuần khá phức tạp và rắc rối, xảy ra tình trạng props 
  truyền đi qua nhiều component con (props drilling), dẫn đến việc follow theo luồng đi của props khó
  nên redux giải quyết được vấn đề này dựa trên việc tập trung dữ liệu ở 1 nơi và những commponent nào
  cần dùng thì lấy ra cũng như cập nhật state trực tiếp
  React cũng đã cho ra mắt Context API để quản lý state tập trung thay vì sử dụng redux

  Context API có thể thay thế redux đối với những project nhỏ đơn giản và data không có sự thay đổi nhiều
  Tuy nhiên, nếu project lớn, data update nhiều, cần có các middleware để xử lí nhiều với side effect, 
  cần có tool theo dõi trạng thái thay đổi như redux devtools, thì nên sử dụng redux
  Sự khác nhau giữa context api và redux: 
  - Context API không phải là state management, nó chỉ là 1 dạng của Dependency Injection - là 1 cơ chế
    transport. Nó không "manage" gì cả, mọi "state management" đều được thực hiện bởi code của mình thông
    qua useState và useReducer, nó chỉ dùng để chia sẻ data || Còn redux là 1 state management, giúp tách logic 
    cập nhật state với phần còn lại của ứng dụng và giúp dễ dàng theo dõi khi nào / ở đâu / tại sao /
    state đã thay đổi như thế nào, cũng cho phép bất cứ thành phần nào trong ứng dụng có thể truy cập vào
    state.
  - Context API re-renders tất cả các component nằm trong provider khi props value của provider thay đổi ||
    Redux chỉ re-render các component được cập nhật.

  Sự khác nhau giữa useReducer và redux 
  - Nơi mà state được quản lí. Redux tạo ra 1 global state cho toàn bộ 
  ứng dụng, còn useReducer tạo 1 local state trong component
  - Middleware/side effect. Redux có hệ sinh thái middleware phong phú trong khi useReducer không có

  useReducer tạo ra giúp cho việc state component phức tạp và có nhiều action với logic phức tạp làm thay đổi state đó.
  useReducer có thế kết hợp với contextAPI để thay thế redux cho những dự án đơn giản. 

---------------------------------------------------------------------------------------------------------
# RESTful API vs GraphQL
  - RESTful API là một giao diện lập trình ứng dụng (API) mà tuân thủ các ràng buộc và quy ước
   kiến trúc REST được sử dụng trong việc giao tiếp giữa client và server. REST là viết tắt của
   REpresentational State Transfer.
  - GraphQL, viết tắt của Graph Query Language, là một ngôn ngữ truy vấn dữ liệu cho API hiệu quả, 
  mạnh mẽ và mang tính linh hoạt cao.

  Mục đích sử dụng
  -Nếu xây dựng ứng dụng mà việc caching quan trọng thì REST tốt hơn bởi vì nó có tích hợp sẵn khả 
    năng lưu bộ nhớ đệm
  -Nếu không muốn lòng vòng để fetching dữ liệu, và dữ liệu sử dụng không dư thừa, API 
  có thể sử dụng cho nhiều nền tảng (web, mobile, …) thì GraphQL tốt hơn

  Giống nhau và khác nhau: 
    -Giống: truy cập dữ liệu từ các dịch vụ web, thực hiện cùng một chức năng là truyền dữ liệu qua 
    các giao thức internet như HTTP
    -Khác: 
      +GraphQL là ngôn ngữ truy vấn trong khi REST là 1 mẫu kiến trúc
      +GraphQL Được triển khai qua HTTP bằng cách sử dụng một endpoint duy nhất. REST Được triển 
      khai trên một tập hợp các URL trong đó mỗi URL cung cấp một tài nguyên duy nhất
      +GraphQL Sử dụng kiến trúc hướng đến client, REST Sử dụng kiến trúc hướng đến server
      +GraphQL có thể được tổ chức theo lược đồ, REST được sắp xếp theo các endpoints.
      +GraphQL API chỉ 1 endpoints, REST API có thể có nhiều endpoints
      +GraphQL định dạng message của GraphQL mutations là 1 chuỗi, REST định dạng message của REST 
        mutations là bất cứ gì
      +GraphQL có tốc độ phát triển nhanh, REST có tốc độ phát triển chậm
      +GraphQL cung cấp tính nhất quán cao trên tất cả các nền tảng, REST khó để có được sự nhất quán 
        trên tất cả các nền tảng.
      +GraphQL thiếu cơ chế lưu vào bộ nhớ đệm tự động, REST tự động sử dụng bộ nhớ đệm
      +GraphQL xử lí phức tạp các status code HTTP để xác định lỗi, REST sử dụng status code HTTP để
        xác định lỗi
  Hiệu suất:
    -Các truy vấn tùy chỉnh của GraphQL có hiệu suất cao hơn REST, từ việc giảm 
    số lượng lệnh gọi API cần thiết đến đảm bảo bạn nhận được lượng dữ liệu phù hợp.
    -Tuy nhiên REST có lợi thế hơn đối với các các ứng dụng yêu cầu caching
  
  Ưu điểm GraphQL: 
    +Được thể hiện dưới dạng một schema, hệ thống quy định cấu trúc dữ liệu mà máy chủ có thể trả về
    +Fetching data bằng 1 lệnh gọi API
    +Tránh under-fetching hoặc over-fetching dữ liệu bởi vì chỉ lấy đúng dữ liệu mình cần
    +Thích hợp phát triển song song FE và BE
    +Việc mở rộng API và thêm chức năng sẽ không ảnh hưởng đến các truy vấn GraphQL của ứng dụng client hiện tại.
  Nhược điểm GraphQL
    +Các vấn đề về hiệu suất với các truy vấn phức tạp.
    +Chỉ support JSON cho các respone
    +Thiếu khả năng tích hợp lưu vào bộ nhớ đệm
    +Vì nó luôn trả về mã trạng thái HTTP là 200, cho dù yêu cầu có thành công hay không, điều này có 
      thể làm phức tạp việc xử lí lỗi và giám sát API
    +Cộng đồng support vẫn còn nhỏ và đang phát triển
  
  Ưu điểm REST:
    +Việc tách biệt các kiến ​​trúc client và server cung cấp khả năng mở rộng các ứng dụng một cách dễ dàng
    +Kiến trúc được sử dụng rộng rãi + lâu đời, cộng đồng support mạnh mẽ
    +Hỗ trợ các định dạng khác nhau như plain text, HTML, JSON,...
  
  Nhược điểm REST:
    +Dễ under-fetching hoặc over-fetching, dữ liệu truy vấn được đôi khi bị dư thừa
    +Yêu cầu nhiều request để fetch được dữ liệu cần tìm
    +Không thể tạo các fields tùy chỉnh mới
