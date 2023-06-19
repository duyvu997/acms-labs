# Câu hỏi phỏng vấn Golang

### Bạn có thể nói gì về ngôn ngữ lập trình Golang
- Go hay Golang là ngôn ngữ lập trình mã nguồn mở được public vào 2009
- Golang giúp tăng năng suất phần mềm đặc biệt là multicore processing (xử lý đa nhân), network (mạng), dự án có source code lớn

### Đặc tính của Golang
- Golang là một ngôn ngữ kiểu tĩnh (static typed) tức là mọi thứ đều phải được khai báo kiểu
- Golang là một ngôn gữ compiler (biên dịch) có trình compiler riêng nên biên dịch rất nhanh so với trình biên dịch kiểu tĩnh khác
- Golang hỗ trợ lập trình đồng thời (concurrent) gọi là Goroutine
- Với những đặc tính trên Go là một ngôn ngữ phù hợp với việc phát triển các dự án về system như Network, Proxy, Distributed Computing, Cloud Native,…

### Những kiểu dữ liệu trong Golang
- Golang có 3 kiểu dữ liệu cơ bản:
 - boolean: true, false
 - number: int, float, byte, complex, ...
 - chuổi: string
- Kiểu dữ liệu dẫn xuất (derived types): pointer, array, struct, function, slice, interface, map, channel, union

### Method khác gì với Function
- Golang không phải ngôn ngữ hướng đối tượng, nhưng ta có thể sử dụng struct để thay cho class. Golang hỗ trợ method -> nó là một hàm được khai báo cho một dữ liệu đặc biệt gọi là receiver. Cú pháp `func (t Type) methodName(parameter list)`
- Điểm khác cơ bản của methods so với function là việc khai báo receiver, từ đó cho phép khai báo trùng tên và chỉ cần khác kiểu dữ liệu nhận (receiver)

### Interface trong Golang là gì?
- Interface trong OOP giúp chúng ta xác định các hành vi sẽ có của một đối tượng (chưa cần khai báo nội dung bên trong). Interface trong Golang cũng là tập hợp những khai báo phương thức mà cho phép chúng ta có thể định nghĩa hoạt động cho nó được. Khi một kiểu dữ liệu định nghĩa tất cả các phương thức trong một interface thì nó được gọi là implement của interface đó. Hay nói cách khác thì trong Golang, Interface được implement một cách ngầm định (implicitly) mà không cần khai báo tường minh bằng từ khóa nào.
- Một tính năng thú vị khác của interface là dùng để khai báo kiểu dữ liệu any (đại diện cho bất kỳ kiểu dữ liệu nào). Cú pháp interface{} gọi là Empty Interface giúp bạn không cần xác định rõ kiểu dữ liệu của biến, rất hay được sử dụng khi làm value cho kiểu dữ liệu map trong Golang.

### Phân biệt Array, Slice và Map trong Golang
- Array hay mảng là một tập hợp các phần tử có cùng kiểu dữ liệu nằm liên tiếp nhau, hay nói cách khác thì Array là một tập hợp có thứ tự, vì thế chúng ta có thể truy cập Array bằng chỉ số (index) của phần tử đó trong mảng.
- Slice về bản chất là các tham chiếu đến mảng hiện có, nó mô tả một phần hoặc toàn bộ Array, vì thế nó có kích thước động (thay đổi được). Thông thường Slice sẽ được tạo từ 1 Array bằng cách lấy từ vị trí phần tử bắt đầu và kết thúc trên Array đó.
- Map cũng là một kiểu dữ liệu tập hợp, tuy nhiên các phần tử trong nó không có thứ tự, tức là chúng ta không thể truy xuất đến phần tử trong Map bằng chỉ số như Slice hay Array. Map sẽ chứa các phần tử dạng key-value, từ đó việc truy xuất sẽ thực hiện qua các key.

### Giải thích về Concurrency trong Golang
- Concurrency là tính năng xử lý song song nhiều tác vụ cùng một lúc, giúp tận dụng năng lực xử lý của CPU. Trong Golang, một luồng được quản lý bởi Go runtime gọi là Goroutine, cú pháp khai báo của Goroutine đơn giản chỉ cần thêm từ khóa “go” vào trước mỗi hàm cần gọi.
- Các Goroutine có khả năng chạy song song cùng lúc, ngoài ra chúng có thể trao đổi dữ liệu với nhau trong qua Channel (kênh). Việc sử dụng Channel cho phép đồng bộ hóa dữ liệu giữa các Goroutine; khi một Goroutine truyền dữ liệu vào Channel thì nó sẽ dừng lại để đợi một Goroutine khác lấy dữ liệu ra thì mới tiếp tục thực hiện tiếp.

### Phương pháp xử lý lỗi trong Golang
- Xử lý lỗi (error handling) trong Golang không giống với xử lý try/catch như các ngôn ngữ khác; lỗi trong Go sẽ được trả về như 1 giá trị của hàm nếu có điều gì không mong đợi (errors hoặc exceptions) xảy ra.
- Go cũng cung cấp cho chúng ta một package error tích hợp sẵn và public với hàm gọi New
- Để đưa ra những Exception thì Go cung cấp cho chúng ta cơ chế Panic. Khi một hàm gặp Panic, nó lập tức dừng xử lý, chấm dứt chương trình và giải phóng stack gọi; thông báo lỗi sẽ được trả về khi chương trình kết thúc.

### Kể tên một số thư viện, framework phổ biến của Golang
- GORM: thư viện ORM giành cho Go
- Viper: thư viện giúp viết và đọc các nội dung liên quan tới thông số cấu hình trong Golang, hỗ trợ các định dạng như TOML, JSON, YAML,…
- Gin-Gonic: Gin là web framework

### Kể tên những dự án nổi tiếng viết bằng Go
- Docker: nền tảng cung cấp cách dựng, kiểm thử và triển khai ứng dụng nhanh chóng thông qua các container
- Kubernetes: một hệ thống mã nguồn mở giúp việc triển khai, nhân rộng dễ dàng và tự động thông qua việc sử dụng các container Docker
- NATS: một Message System, là thành phần quan trọng trong các hệ thống pub/sub, event-driven
- Consul: một service dành cho việc thiết lập mạng (network) trong microservices một cách dễ dàng 
