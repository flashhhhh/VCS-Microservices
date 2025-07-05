# # VCS-Microservices

## Khải niệm về kiến trúc Microservices
Microservices là một cách tiếp cận trong việc phát triển phần mềm, phần mềm sẽ bị chia nhỏ ra thành các **services** không phụ thuộc lẫn nhau và giao tiếp với nhau qua các APIs được định nghĩa rõ ràng.

## Ưu, nhược điểm của kiến trúc Microservices
### Ưu điểm
* **Khả năng mở rộng (Scalability)**: Mỗi microservice có thể được mở rộng độc lập, cho phép ứng dụng xử lý lượng tải trọng lớn mà không ảnh hưởng đến hiệu năng của các services khác.
* **Tính linh hoạt (Flexibility)**: Mỗi service được phát triển, triển khai và cập nhật độc lập với các services khác. Ngoài ra còn có thể thêm các tính năng và sửa đổi tính năng đã có sẵn mà không ảnh hưởng đến hệ thống.
* **Tính bền bỉ (Resilience)**: Khi 1 service bị lỗi, hệ thống vẫn sẽ không bị sập.
* **Đa dạng công nghệ (Technology Heterogeneity)**: Microservices cho phép mỗi service có thể sử dụng công nghệ các công nghệ khác nhau để tối ưu hóa khả năng thực thi của service đó.

### Nhược điểm
* **Ranh giới dịch vụ (Service Boundries)**; Khó khăn trong việc chia nhỏ ứng dụng thành các services, việc chia giới hạn cho từng service đúng ảnh hưởng đến thành công của ứng dụng.
* **Khám phá dịch vụ (Service Discovery)**: Khó khăn trong việc tìm kiếm và kết nối tới các services khác. Khi số lượng services tăng lên, việc theo dõi các services và địa chỉ của các services trở nên phức tạp.
* **Tính đồng nhất dữ liệu (Data Consistency)**: Do mỗi services lưu trữ dữ liệu riêng, việc duy trì tính đồng nhất qua nhiều services trở nên khó khăn.
* **Tính bảo mật (Security)**: Phải bảo mật cho từng service riêng biệt, bao gồm xác thực, phân quyền, và kết nối giữa chúng.
* **Quản lý Transaction (Transaction Management)**: Transaction bị phân mảnh qua nhiều services dễ bị không đồng nhất và không thể khôi phục.
* **Kiểm thử (Testing)**: Phải đảm bảo có thể test mỗi service độc lập và test toàn bộ hệ thống.

## Decomposition Patterns
Decomposition Patterns cho phép tách ứng dụng thành các services nhỏ ít phụ thuộc vào nhau. Có 3 cách tiếp cận chính để chia nhỏ một ứng dụng.

### Decomposition by Business Capability
Mục tiêu của cách tiếp cận này là tạo ra microservices căn chỉnh theo yêu cầu business và có thể được phát triển và bảo trì độc lập. **Business capability** là các chức năng cụ thể mà một tổ chức cung cấp cho khách hàng, tập trung vào việc business **làm gì**, thay vì tập trung vào **làm như thế nào**.

#### Use cases tốt nhất
* Khi team có đủ hiểu biết sâu sắc về các đơn vị business của tổ chức và sở hữu một SME cho từng đơn vị business.
* Một ứng dụng có nhiều chức năng có liên quan đến nhau, hoặc các chức năng đó có thể thay đổi liên tục.
* Tổ chức có nhiều đơn vị business với các lĩnh vực khác nhau về chức năng hay luồng thực thi (workflows).

#### Ưu điểm
* **Liên kết Business:** Việc liên kết phát triển phần mềm với các mục tiêu và mục đích kinh Đdoanh trở nên dễ dàng hơn.
* **Tăng trải nghiệm người dùng:** Microservices có thể được tối ưu cho nhu cầu cụ thể của người dùng, giúp trải nghiệm người dùng tốt hơn.

#### Nhược điểm
* **Khó khăn trong việc xác định business capacities**: Việc xác định và định nghĩa **business capacities** phù hợp để sử dụng làm cơ sở cho các microservices với ranh giới phù hợp có thể là một quá trình phức tạp và tốn thời gian.
* **Độ phức tạp trong việc phối hợp các microservices**: Việc phối hợp các microservices khác nhau liên quan đến một năng lực kinh doanh có thể phức tạp, đặc biệt nếu năng lực kinh doanh đó bao gồm nhiều bước hoặc tương tác với các hệ thống bên ngoài.

### Decomposition by Transaction

### Decomposition by Subdomain

## API Gateway
### Định nghĩa
API Gateway là cổng duy nhất mà người dùng bên ngoài phải đi qua để truy cập vào hệ thống microservices. API Gateway sẽ nhận các requests từ phía client, chỉnh sửa, xác thực và điều hướng chúng đến các API cụ thể trên các services phía sau.

Ngoài nhiệm vụ chính là proxy request thì một hệ thống API Gateway thường sẽ đảm nhận luôn vài vai trò khác như bảo mật API, monitoring, analytics số lượng requests cũng như tình trạng hệ thống phía sau.
### Lợi ích
#### Che dấu được cấu trúc của hệ thống microservices với bên ngoài
Clients sẽ tương tác với hệ thống của chúng ta thông qua api gateway chứ không gọi trực tiếp tới một services cụ thể, các endpoints của các services sẽ chỉ được gọi nội bộ, tức là gọi giữa các services với nhau hoặc được gọi từ API gateway, người dùng sẽ gọi các api này thông qua các public endpoints từ API Gateway. Chính vì vậy cho nên phía client không cần và cũng không thể biết được các services phía backend được phân chia như thế nào, việc refactor code frontend cũng dễ dàng hơn đối với lập trình viên.

#### Phần code phía frontend sẽ gọn gàng hơn
Vì không phải tracking nhiều endpoints, tất cả chỉ việc gọi đến api gateway nên phần code frontend sẽ gọn gàng hơn so với việc phải tracking hàng tá endpoints trên từng services một, nhất là khi mà hệ thống ngày một phình to ra.

#### Dễ dàng theo dõi và quản lý traffic.
Hầu hết các hệ thống API gateway phổ biến hiện nay đều sẽ đi kèm tính năng theo dõi và quản lý lượng traffic bằng GUI hoặc thông qua các APIs của hệ thống Gateway, VD như với Kong (bản EE).

#### Requests caching và cân bằng tải.
API Gateway sẽ kiêm luôn vai trò load balancer của hệ thống, requests sẽ không được gửi trực tiếp đến backend nên sẽ giảm thiểu được rủi ro hệ thống bị quá tải.

#### Thêm một lớp bảo mật nữa cho hệ thống.
API gateway giúp ngăn chặn các cuộc tấn công bằng cách thêm một lớp bảo vệ các loại tấn công như ddos, slq injections,...

#### Thay thế authentication services
API gateway thường cung cấp nhiều cơ chế xác thực, chúng ta có thể sử dụng nó để xác thực người dùng luôn, giúp tiết kiệm thời gian và làm hệ thống chúng ta đơn giản hơn. VD một vài cơ chế xác thực hỗ trợ bởi Kong API gateway

### Nhược điểm
#### Tăng thời gian response
Vì phải đi qua server trung gian cho nên việc response sẽ bị trễ hơn so với việc gọi trực tiếp tới hệ thống.

#### Thêm tác nhân gây lỗi
Để sử dụng API Gateway thì chúng ta sẽ phải config, rồi chỉnh sửa code, quản lý server gateway, ... khiến cho chúng ta có thêm việc phải lo, chẳng may gateway có lỗi thì requests sẽ không thể tới được phía server.

#### Có thể gây nghẽn cổ chai
Nếu như không được scale hay config hợp lý thì gateway sẽ có thể bị quá tải và làm chậm hệ thống của chúng ta.

## Inter-Process Communication
### Định nghĩa
Inter-Process Communicataion là một kỹ thuật được cung cấp bởi hệ điều hành để các services có thể giao tiếp với nhau.
### Giao tiếp đồng bộ
Ở kiểu giao tiếp này, client sẽ gửi request chứa dữ liệu đến một service. Service xử lý request đó theo logic được định nghĩa, và gửi phản hồi về client. Một số client sẽ tạm dừng tất cả thao tác khác chỉ để chờ đợi phản hồi.

#### REST
REST là 1 chuẩn giao tiếp sử dụng HTTP. Mỗi resource biểu diễn 1 thực thể business chiếm vai trò quan trọng trong kỹ thuật này. Có thể thao tác các thao tác khác nhau sử dụng HTTP verbs:
* **POST**: Tạo resource mới.
* **GET**: Yêu cầu trả về resource mong muốn.
* **PUT/PATCH**: Yêu cầu cập nhật 1 resource.
* **DELETE**: Yêu cầu xóa bỏ 1 resource.

Nhược điểm của REST là sự thiếu hụt HTTP verbs. Dẫn đến việc khó trong các thao tác cập nhật hoặc tạo mới trên cùng một resource.

#### gRPC
gRPC là 1 chuẩn giao tiếp mới giúp định nghĩa các thao tác với các tham số và kiểu dữ liệu trả về trong 1 tin nhắn cụ thể thông qua protocol buffer.

### Giao tiếp bất đồng bộ
Ở kiểu giao tiếp này, client gửi request chứa dữ liệu đến 1 service. Service đó sẽ xử lý request dựa trên logic được định nghĩa trước, nhưng sẽ có delay trước khi client nhận được phản hồi. Các hệ thống sử dụng tin nhắn không đồng bộ làm phong cách giao tiếp thường sử dụng một **message broker**. Trong tin nhắn không đồng bộ có hai khái niệm quan trọng:

* **Message**: Message bao gồm tiêu đề và nội dung chứa dữ liệu.
* **Channel**: Message trao đổi qua các channels.

Các kiểu giao tiếp qua tin nhắn:
* **Asynchronous request/response**: Trong mô hình này, trước tiên, **client (producer)** gửi yêu cầu qua **request queue**. Sau đó, **server (consumer)** sẽ xử lý tin nhắn đến một cách không đồng bộ, rồi gửi phản hồi trở lại qua **response queue**. Cuối cùng, client sẽ sử dụng phản hồi từ **response queue**.
* **Publish/ Subcribe**: Trong mô hình này, một **producer** sẽ xuất bản một tin nhắn thông qua một **message broker**. Mặt khác, có thể có nhiều **consumer** có thể sử dụng tin nhắn đã xuất bản từ **message broker** đó.
* **Notification**: Trong mô hình này, client gửi tin nhắn qua **queue**. Ở phía bên kia, server sẽ tiếp nhận và xử lý tin nhắn đến, nhưng sẽ không có phản hồi nào để gửi lại cho client.

## Service Discovery
### Định nghĩa
Service discovery là quá trình tự động mà các service trong hệ phân tán định vị và giao tiếp tới nhau. Trong kiến trúc microservices, mỗi service được chạy trong môi trường container hay trên máy ảo với IP và port thay đổi động, service discovery hoạt động để các service biết được địa chỉ của các services khác.
* **Service Registry**: CSDL để duy trì vị trí của tất cả các services có thể truy cập được.
* **Service Provider**: Services tự đăng ký chính nó với registry khi register khởi động.
* **Service Consumer**: Services truy vấn registry để xác định vị trí của các services khác mà nó muốn giao tiếp.

### Lợi ích
* **Dynamic Scaling**: Services thường được scale lên xuống theo tải trọng, việc tạo và hủy các instances một cách linh hoạt.
* **Các instances tạm thời**: Các container và VM được chỉ định địa chỉ IP động thay đổi thường xuyên
* **Yêu cầu về khả năng phục hồi**: Hệ thống phải tự động xử lý các trường hợp lỗi và chuyển hướng lưu lượng đến các trường hợp bình thường
* **Kiến trúc phi tập trung**: Các dịch vụ cần giao tiếp mà không cần sự kết hợp chặt chẽ hoặc phụ thuộc được hardcode.

### Client-side Discovery
Trong mô hình này, client chịu trách nhiệm:
* Truy vấn **service registry** để biết các phiên bản khả dụng.
* Chọn một instance (thường sử dụng cân bằng tải phía client).
* Gửi yêu cầu trực tiếp đến instance đã chọn.

#### Lợi ích
* Kiến trúc đơn giản không có thao tác bổ sung nào ngoài registry.
* Cho phép quyết định cân bằng tải cụ thể cho ứng dụng.
* Tránh các bước nhảy mạng bổ sung.

#### Bất lợi
* Client phải cài đặt thêm logic discovery.
* Yêu cầu triển khai cho từng ngôn ngữ lập trình hoặc framework.
* Làm cho các ứng dụng client phức tạp hơn.

### Server-side Discovery
Trong mẫu này:
* Client gửi yêu cầu đến bộ cân bằng tải/bộ định tuyến được biết đến.
* Bộ cân bằng tải truy vấn registry.
* Bộ cân bằng tải định tuyến yêu cầu đến các instance khả dụng.

#### Lợi ích
* Clients không cần quan tâm về logic discovery.
* Không cần triển khai logic khám phá bằng nhiều ngôn ngữ.
* Thường được cung cấp bởi các nền tảng đám mây (ví dụ: AWS ELB)

#### Bất lợi
* Yêu cầu cơ sở hạ tầng bổ sung (bộ cân bằng tải)
* Cần một bước nhảy mạng bổ sung.
* Phải hỗ trợ tất cả các giao thức truyền thông bắt buộc.

## Data Management
Microservices chia ứng dụng thành các services nhỏ, không phụ thuộc vào nhau, mỗi service sẽ có dữ liệu riêng. Điều này gây ra 1 số vấn đề sau:
* **Data consistency**: Tính đồng nhất dữ liệu giữa các services.
* **Transaction Management**: Transaction sẽ bị phân mảnh ra nhiều services.
* **Data duplication**: Dữ liệu sẽ bị lặp lại do nhiều services phải lưu lại dữ liệu đó.
* **Query Complexity**: Truy vấn sẽ bị dàn trải ra nhiều services.
* **Eventual Consistency**: Dữ liệu phải đảm báo tính nhất quán cuối cùng.

### Key patterns cho Data Management
#### 1. Database per Service
* Mỗi microservices có CSDL riêng của mình.
* Các dịch vụ không thể truy cập trực tiếp vào CSDL của dịch vụ khác.
* Thách thức: Việc kết hợp dữ liệu giữa các services trở nên phức tạp.

#### 2. Saga
* Quản lý **distributed transaction** qua nhiều services.
* Có 2 cách cài đặt:
	* **Choreography**: Services tạo ra events để kích hoạt cho bước tiếp theo.
	* **Orchestration**: Có 1 điều phối trung tâm để quản lý luồng transaction.
* Cung cấp tính chất **eventual consistency** thay vì tính **ACID**.

#### 3. CQRS
* Tách biệt các hoạt động read và write..
* Mô hình write (lệnh) được tối ưu hóa cho các transactions.
* Mô hình read (truy vấn) được tối ưu hóa cho các truy vấn, thường là **denormalized**.
* Sử dụng **event sourcing** để giữ cho các mô hình read được cập nhật với mô hình write.

#### 4. Event Sourcing
* Lưu trữ các thay đổi trạng thái dưới dạng chuỗi events.
* Trạng thái hiện tại được suy ra bằng cách phát lại các events trước đó.
* Cho phép truy vấn theo thời gian ("trạng thái tại thời điểm X là gì?")
* Tạo điều kiện cho kiến trúc **event-driven**.

#### 5. API Composition
* Đối với các truy vấn cần dữ liệu từ nhiều services.
* Dịch vụ **API composer** lấy dữ liệu từ nhiều services.
* Kết hợp và chuyển đổi kết quả.
* Đơn giản hơn CQRS nhưng có thể có vấn đề về hiệu suất.

## Configuration Management
Microservices thường phải thay đổi trên nhiều môi trường khác nhau (development, testing, production) và external dependencies (databases, third-party APIs, message queues).

### Lợi ích của External Configuration
* **Quản lý tập trung**: Xử lý configuration cho nhiều services từ 1 nguồn duy nhất.
* **Hỗ trợ nhiều môi trường khác nhau**: Các config khác nhau cho các môi trường khác nhau.
* **Cho phép scale**: Thay đổi settings như LBs hoặc caching theo scale của ứng dụng.

### Các loại config trong config server hoặc config files
#### 1. Database configurations
Microservices thường cần kết nối với CSDL và việc lưu trữ thông tin kết nối trong cấu hình cho phép linh hoạt trên nhiều môi trường khác nhau.
* **Database URLs**: Endpoint của CSDL.
* **Username, Password**: Thông tin xác thực để truy cập vào CSDL.
* **Connection Pool**: Các tham số như số lương kết nối tối đa, timeouts, hay số lượng kết nối rảnh rỗi.

#### 2. Service-Specific Configurations
Mỗi microservice có thể có các config riêng biệt xác định cách thức hoạt động của nó trong hệ thống.
* **Port**: Xác định port mà service muốn nghe.
* **Endpoint**: URLs của các microservices khác service này muốn giao tiếp.
* **Feature Toggle**: Để bật hoặc tắt một số tính năng nhất định khi chạy mà không cần triển khai lại.

#### 3. API Keys, Credentials
Để giao tiếp an toàn với các external services, các microservices yêu cầu API Keys và thông tin xác thực OAuth.
* **API Keys**: Cho việc tích hợp các APIs của bên thứ 3.
* **OAuth Credentials**: Client ID và secret cho việc xác thực và phân quyền OAuth2.
* **Encryption Keys**: Được sử dụng để mã hóa dữ liệu nhạy cảm trong quá trình truyền tải.

#### 4. Logging and Monitoring Configurations
Đảm bảo ghi log và giám sát đúng cách là rất quan trọng để theo dõi tình trạng dịch vụ, hiệu suất và các vấn đề gỡ lỗi.
* **Log Levels**: Kiểm soát mức độ chi tiết của nhật ký, thường được đặt ở mức DEBUG, INFO, WARN, ERROR.
* **Monitoring URLs**: Tích hợp với các công cụ giám sát như Prometheus hoặc Grafana để theo dõi số liệu và hiệu suất dịch vụ.

#### 5. Environment-Specific Settings
Microservices thường hoạt động trong nhiều môi trường (development, staging, production) và cần có cấu hình khác nhau cho từng môi trường.
* **Environment Variable**: Settings cụ thể cho môi trường dev, staging, prod.
** Load Balancer Config**: URL hoặc settings cho LB.