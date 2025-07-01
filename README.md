# VCS-Microservices

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

