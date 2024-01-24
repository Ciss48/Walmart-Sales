
# Walmart Sales Data Analysis

## Giới thiệu
Dự án này nhằm mục đích khám phá dữ liệu Bán hàng của Walmart để hiểu các chi nhánh và sản phẩm hoạt động tốt nhất, xu hướng bán hàng của các sản phẩm khác nhau, hành vi của khách hàng. Mục đích là nghiên cứu cách cải thiện và tối ưu hóa các chiến lược bán hàng. Tập dữ liệu được lấy từ [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting)

"Trong cuộc thi tuyển dụng này, người tìm việc được cung cấp dữ liệu lịch sử bán hàng của 45 cửa hàng Walmart nằm ở các khu vực khác nhau. Mỗi cửa hàng có nhiều bộ phận và người tham gia phải dự kiến doanh số bán hàng cho từng bộ phận trong mỗi cửa hàng. Để thêm vào thử thách, đã chọn các sự kiện giảm giá ngày lễ được bao gồm trong tập dữ liệu. Những khoản giảm giá này được biết là có ảnh hưởng đến doanh số bán hàng, nhưng rất khó để dự đoán bộ phận nào bị ảnh hưởng và mức độ ảnh hưởng." [source](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting)

## Mục Đích Của Dự Án
Mục đích chính của dự án này là hiểu rõ hơn về dữ liệu bán hàng của Walmart để hiểu các yếu tố khác nhau ảnh hưởng đến doanh số bán hàng của các chi nhánh khác nhau.

## Về Data
Lấy từ [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting)
Tập dữ liệu này chứa các giao dịch bán hàng từ ba chi nhánh khác nhau của Walmart, lần lượt có trụ sở tại Mandalay, Yangon và Naypyitaw. Dữ liệu chứa 17 cột và 1000 hàng:

| Column                  | Description                             | Data Type      |
| :---------------------- | :-------------------------------------- | :------------- |
| invoice_id              | Invoice of the sales made               | VARCHAR(30)    |
| branch                  | Branch at which sales were made         | VARCHAR(5)     |
| city                    | The location of the branch              | VARCHAR(30)    |
| customer_type           | The type of the customer                | VARCHAR(30)    |
| gender                  | Gender of the customer making purchase  | VARCHAR(10)    |
| product_line            | Product line of the product solf        | VARCHAR(100)   |
| unit_price              | The price of each product               | DECIMAL(10, 2) |
| quantity                | The amount of the product sold          | INT            |
| VAT                 | The amount of tax on the purchase       | FLOAT(6, 4)    |
| total                   | The total cost of the purchase          | DECIMAL(10, 2) |
| date                    | The date on which the purchase was made | DATE           |
| time                    | The time at which the purchase was made | TIMESTAMP      |
| payment_method                 | The total amount paid                   | DECIMAL(10, 2) |
| cogs                    | Cost Of Goods sold                      | DECIMAL(10, 2) |
| gross_margin_percentage | Gross margin percentage                 | FLOAT(11, 9)   |
| gross_income            | Gross Income                            | DECIMAL(10, 2) |
| rating                  | Rating                                  | FLOAT(2, 1)    |

### Danh sách phân tích

1. Phân tích sản phẩm

> Tiến hành phân tích dữ liệu để hiểu các dòng sản phẩm khác nhau, dòng sản phẩm hoạt động tốt nhất và dòng sản phẩm cần được cải thiện.

2. Phân tích doanh số bán hàng

> Phân tích này nhằm trả lời câu hỏi về xu hướng bán hàng của sản phẩm. Kết quả của việc này có thể giúp đo lường hiệu quả của từng chiến lược bán hàng mà doanh nghiệp áp dụng và những điều chỉnh cần thiết để đạt được nhiều doanh thu hơn.

3. Phân tích khách hàng

> Phân tích này nhằm mục đích khám phá các phân khúc khách hàng khác nhau, xu hướng mua hàng và lợi nhuận của từng phân khúc khách hàng.

## Tiếp cận 
1. **Data Wrangling:** kiểm tra dữ liệu được thực hiện để đảm bảo phát hiện các giá trị **NULL** và các giá trị bị thiếu cũng như sử dụng các phương pháp thay thế dữ liệu để thay thế, thiếu hoặc **NULL** các giá trị.
> 1. Xây dựng cơ sở dữ liệu
> 2. Tạo bảng và chèn dữ liệu.
> 3. Chọn các cột có giá trị null trong đó. Không có giá trị null trong cơ sở dữ liệu của chúng tôi vì khi tạo bảng, chúng tôi đặt **NOT NULL** cho mỗi trường, do đó các giá trị null sẽ được lọc ra.

2. **Feature Engineering:** tạo một số cột mới từ các cột hiện có.
> 1. Thêm cột mới có tên `time_of_day` để cung cấp thông tin chi tiết về doanh số bán hàng vào Buổi sáng, Buổi chiều và Buổi tối. Điều này sẽ giúp trả lời câu hỏi thời điểm nào trong ngày có nhiều doanh số bán hàng nhất.

> 2. Thêm một cột mới có tên `day_name` chứa các ngày được trích xuất trong tuần mà giao dịch đã cho diễn ra (Thứ Hai, Thứ Ba, Thứ Tư, Thứ Năm, Thứ Sáu). Điều này sẽ giúp trả lời câu hỏi tuần nào trong ngày mỗi chi nhánh bận rộn nhất.

> 3. Thêm một cột mới có tên `month_name` chứa các tháng được trích xuất trong năm mà giao dịch đã cho diễn ra (Tháng 1, Tháng 2, Tháng 3). Giúp xác định tháng nào trong năm có doanh thu và lợi nhuận nhiều nhất.

2. **Exploratory Data Analysis (EDA):** Phân tích dữ liệu thăm dò được thực hiện để trả lời các câu hỏi và mục tiêu được liệt kê của dự án này.

3. **Conclusion:**

## Câu hỏi kinh doanh cần trả lời

### Câu hỏi chung

1. Dữ liệu có bao nhiêu thành phố duy nhất?
2. Chi nhánh ở thành phố nào?

### Danh sách sản phẩm

1. Dữ liệu có bao nhiêu dòng sản phẩm duy nhất?
2. Phương thức thanh toán phổ biến nhất là gì?
3. Dòng sản phẩm bán chạy nhất là gì?
4. Tổng doanh thu theo tháng là bao nhiêu?
5. Tháng nào có giá vốn hàng bán lớn nhất?
6. Dòng sản phẩm nào có doanh thu lớn nhất?
5. Thành phố nào có doanh thu lớn nhất?
6. Dòng sản phẩm nào có VAT lớn nhất?
7. Lấy từng dòng sản phẩm và thêm một cột vào dòng sản phẩm đó hiển thị "Tốt", "Xấu". Tốt nếu nó lớn hơn doanh số trung bình
8. Chi nhánh nào bán được nhiều sản phẩm hơn sản phẩm trung bình bán ra?
9. Dòng sản phẩm phổ biến nhất theo giới tính là gì?
12. Đánh giá trung bình của từng dòng sản phẩm là bao nhiêu?

### Phân tíchdoanh số bán hàng 

1. Số lượng bán hàng được thực hiện vào từng thời điểm trong ngày trong tuần
2. Loại khách hàng nào mang lại nhiều doanh thu nhất?
3. Thành phố nào có tỷ lệ phần trăm thuế/ VAT (**Thuế giá trị gia tăng**) lớn nhất?
4. Đối tượng khách hàng nào phải nộp thuế GTGT nhiều nhất?

### Phân tích khách hàng

1. Dữ liệu có bao nhiêu loại khách hàng duy nhất?
2. Dữ liệu có bao nhiêu phương thức thanh toán duy nhất?
3. Loại khách hàng phổ biến nhất là gì?
4. Loại khách hàng nào mua nhiều nhất?
5. Giới tính của hầu hết khách hàng là gì?
6. Sự phân bổ giới tính ở mỗi ngành như thế nào?
7. Thời điểm nào trong ngày khách hàng đánh giá nhiều nhất?
8. Thời điểm nào trong ngày khách hàng đánh giá nhiều nhất cho mỗi chi nhánh?
9. Ngày nào trong tuần có xếp hạng trung bình tốt nhất?
10. Ngày nào trong tuần có xếp hạng trung bình tốt nhất cho mỗi chi nhánh?
​
## Revenue And Profit Calculations

$ COGS = unitsPrice * quantity $

$ VAT = 5\% * COGS $

$VAT$ được thêm vào $COGS$ và đây là số tiền được lập hóa đơn cho khách hàng.

$ total(gross_sales) = VAT + COGS $

$ grossProfit(grossIncome) = total(gross_sales) - COGS $

**Gross Margin** là lợi nhuận gộp được biểu thị bằng tỷ lệ phần trăm của tổng (lợi nhuận gộp/doanh thu)(gross profit/revenue)



<u>**Example with the first row in our DB:**</u>

**Data given:**

- $ \text{Unite Price} = 45.79 $
- $ \text{Quantity} = 7 $

$ COGS = 45.79 * 7 = 320.53 $

$ \text{VAT} = 5\% * COGS\\= 5\%  320.53 = 16.0265 $

$ total = VAT + COGS\\= 16.0265 + 320.53 = $336.5565$

$ \text{Gross Margin Percentage} = \frac{\text{gross income}}{\text{total revenue}}\\=\frac{16.0265}{336.5565} = 0.047619\\\approx 4.7619\% $
