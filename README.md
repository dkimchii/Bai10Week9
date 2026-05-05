1.
- lỗi file: pom.xml
- Trong thẻ <dependency> của logback-classic (khoảng dòng 19-23)
- trên git: [ERROR] Failed to execute goal on project shipping-app: Could not resolve dependencies for project com.lab:shipping-app:jar:1.0-SNAPSHOT: Could not find artifact ch.qos.logback:logback-classic:jar:9.9.9 in central (https://repo.maven.apache.org/maven2)
- vấn đề: Maven không thể tìm thấy thư viện logback-classic phiên bản 9.9.9 trên kho lưu trữ tập trung (Maven Central)
- nguyên nhân:Phiên bản 9.9.9 là một phiên bản không có thực (dummy version). Logback hiện tại chỉ có các phiên bản như 1.2.x, 1.4.x hoặc 1.5.x. Do khai báo sai phiên bản, quá trình đóng gói dự án bị dừng lại vì thiếu thư viện bổ trợ
2. 
- lỗi ở file pom.xml dòng 27-35 trong thẻ <build> -> <plugins>)
- trên git: [INFO] --- surefire:2.12.4:test (default-test) @ shipping-app ---
- nguyên nhân: Đoạn log này cho thấy Maven đang sử dụng maven-surefire-plugin (phiên bản 2.12.4) để chạy kiểm thử, nhưng sau đó nó không thực thi một file test nào (do bản quá cũ và không tự động nhận diện JUnit 5)
3. 
- lỗi ở file ShippingCalculator.java dòng 9
- trên git: Caused by: java.lang.NullPointerException: Cannot invoke "String.equals(Object)" because "type" is null
  at com.lab.ShippingCalculator.calculate(ShippingCalculator.java:9)
- nguyên nhân: Nếu tham số type truyền vào là null (hoặc trong trường hợp kiểm thử giá trị đầu vào không hợp lệ nhưng tham số type bị để trống/null), lệnh type.equals() sẽ không thể thực thi và văng ra ngoại lệ NullPointerException