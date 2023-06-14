# Khai Phá Dữ Liệu Giá Thuê Nhà Ở Ấn Độ 
![image](https://dynamic.realestateindia.com/blog_images/20180221144841_image1.jpg)
## 1. Lý do chọn đề tài
- Nhà ở tại Ấn Độ phát triển lâu đời từ những lâu đài cổ xưa cho đến những tòa nhà cao tầng hiện đại trong các thành phố lớn đến những túp lều nhỏ ở các thị trấn xa xôi. Với mức thu nhập tăng lên theo từng giai đoạn, lĩnh vực nhà ở  ở Ấn Độ cũng có sự tăng trưởng vượt bậc. Thuê nhà, hay mướn nhà là hình thức để sử dụng nhà ở một các tạm thời mà ngôi nhà hay căn hộ đó được sở hữu bởi một người chủ khác. Thuê nhà là một cách để chia sẻ về mặt kinh tế khi người thuê thì trả tiền thuê để ở và người chủ thì chi trả cho phí tài sản phát sinh bởi quyền sở hữu. Chi phí phải trả để thuê một căn nhà có thể được định giá dựa trên nhiều yếu tố, từ vị trí thành phố nơi nhà hay căn hộ đó tọa lạc, kích thước nhà hay căn hộ, đến số lượng các phòng trong căn nhà như số phòng tắm, phòng ngủ,... mà chi phí đó có thể biến thiên từ rất thấp đến rất cao. Với mục tiêu tìm hiểu và dự đoán xem giá thuê của một căn nhà có phải là phù hợp hay không, hay giá thuê đó đã bị phóng đại thành một con số khổng lồ, nhóm chúng em đã chọn tập dữ liệu ‘House Rent Dataset’ để thực hiện trực quan và dự đoán giá thuê này của hơn 4700 nhà cho thuê tại Ấn Độ được đăng năm 2022.

## 2.Tổng quan về tập dữ liệu
- Nhóm sử dụng tập dữ liệu House Rent Dataset trên Kaggle. Dữ liệu này cung cấp thông tin về các căn hộ/phòng cho thuê ở Ấn Độ được mô tả dựa trên nhiều đặc điểm khác nhau như kích thước phòng, vị trí căn hộ, số lượng phòng cho thuê, đối tượng ưu tiên,.. giá cho thuê.  
- Nguồn dữ liệu: https://www.kaggle.com/datasets/iamsouravbanerjee/house-rent-prediction-dataset
- Tập dữ liệu gồm có hơn 4.700 dòng (rows) là các nhà cho thuê và 12 cột (columns) là thông tin về căn hộ cho thuê đó. Cụ thể là 
    + BHK: Số lượng phòng ngủ(Bedrooms), sảnh(Hall), phòng bếp (Kitchen).
    + Rent: Giá cho thuê của nhà/ căn hộ.
    + Size: Diện tích nhà/ căn hộ (feet vuông).
    + Floor: Tầng đang cho thuê trong tổng số các tầng (Example: Ground out of 2, 3 out of 5, etc.)
    + Area Type: Loại khu vực.
    + Area Locality: Vị trí của nhà/ căn hộ.
    + City: Thành phố nơi nhà/ căn hộ tọa lạc.
    + Furnishing Status: Tình trạng nội thất trong nhà/ căn hộ (Nội thất đầy đủ > Nội thất chưa đầy đủ > Không có nội thất).
    + Tenant Preferred: Đối tượng ưu tiên cho thuê.
    + Bathroom: Số lượng phòng tắm.
    + Point of Contact: Người cần liên lạc nếu cần biết thêm thông tin cho thuê nhà/ căn hộ.

## 3. Tiền xử lý dữ liệu
- Tải dữ liệu
![alt text](/Images/Picture1.png)
- Xem mô tả về tập dữ liệu
![alt text](/Images/Picture2.png)
-> Ta thấy rằng tập dữ liệu không có missing value 
- Đổi tên cột ‘BHK’ thành ‘Number of Bedrooms-Halls-Kitchens’
![alt text](/Images/Picture3.png)
- Thêm hai cột ‘Recent Floor’ và ‘Total Floors’ được tách từ cột ‘Floor’. Sau đó loại bỏ cột ‘Floor’ khỏi tập dữ liệu bằng lệnh drop()
![alt text](/Images/Picture4.png)
- Tiếp theo ta tiến hành đổi dữ liệu cho cột ‘Recent Floor’. 
    * Nếu Recent Floor = ‘Ground’ thì đổi thành 0 
    * Nếu Recent Floor = ‘Upper Basement’ thì đổi thành -1
    * Nếu Recent Floor = ‘Lower Basement’ thì đổi thành -2
![alt text](/Images/Picture5.png)
- ̵Khoảng giá trị của ‘Rent’ khá lớn nên sẽ gây ra sự chênh lệch giữa các dữ liệu như hình bên dưới.
![alt text](/Images/Picture6.png)
- Ta sẽ xóa các dữ liệu có ‘Rent’ lớn hơn 100.000
![alt text](/Images/Picture7.png)
- Tạo index cho các dòng
![alt text](/Images/Picture8.png)

## 4. Trực quan dữ liệu
##### 4.1. Quy mô của các Houses/Apartments/Flats cho thuê có ảnh hưởng đến giá thuê không?
- Biểu đồ nhiệt thể hiện sự tương quan giữa các biến Number of Bedrooms - Halls - Kitchens, Size, Bathroom và Rent.

![alt text](/Images/Picture9.png)

    Nhận xét: Ta có thể thấy có sự tương quan mạnh giữa ba biến Number of Bedrooms - Halls - Kitchens, Bathroom và Size với nhau. Cho thấy chúng có tỉ lệ thuận đồng nghĩa là quy mô Houses/Apartments/Flats lớn thì số lượng phòng Bedrooms - Halls - Kitchens nói chung hay số lượng phòng Bathroom và diện tích chung cũng sẽ lớn theo. 
- Biểu đồ tương quan giữa Diện tích, Số lượng Bedrooms - Halls - Kitchens cho thuê với giá thuê.

![alt text](/Images/Picture10.png)

    Nhận xét: Khi kết hợp các yếu tố lại với nhau ta thấy nếu diện tích cho thuê lớn với nhiều phòng cho thuê thì chắc chắn giá cho thuê sẽ mắc. Tuy nhiên với những nơi cho thuê có diện tích nhỏ ít số phòng thì không thể khẳng định chúng có giá cho thuê rẻ. 
##### 4.2. Loại khu vực của các Houses/Apartments/Flats cho thuê có liên quan đến giá cho thuê hay không?
- Phân loại các loại khu vực tại các Houses/Apartments/Flats cho thuê

![alt text](/Images/Picture11.png)

    Nhận xét: Ta thấy các nơi cho thuê được chia ra 2 khu vực chính là Super Area và Carpet Area. 
- Sự phân bố giá thuê giữa khu Super và Carpet

![alt text](/Images/Picture12.png)

    Nhận xét: Hầu hết các hầu các chỗ thuê thuộc khu vực Super có mức giá từ trung bình đến thấp. Còn khu vực Carpet sở hữu nhiều nơi cho thuê có giá khá cao so với khu vực Super. Carpet sở hữu nhiều những căn hộ/ phòng/ nhà cho thuê  khá đắt đỏ.
##### 4.3. Những loại người thuê nhà được ưa thích?
- Các loại đối tượng ưu tiên cho thuê nhà

![alt text](/Images/Picture13.png)

    Nhận xét: 72,6% chủ sở hữu nhà sẵn sàng cho cả gia đình và người độc thân thuê nhà của họ.
- Phân bố giá thuê nhà giữa đối tượng ‘Family’ và ‘Bachelors

![alt text](/Images/Picture14.png)

    Nhận xét: Ta thấy không có nhiều sự khác biệt về giá thuê giữa hai đối tượng ‘Bachelors’ và ‘Family’
##### 4.4. Dashboard giá thuê nhà ở Ấn Độ
![alt text](/Images/Picture15.png)

## 5. Khai phá dữ liệu bằng công cụ SSAS
**SSAS (SQL Server Analysis Services) là một công cụ phân tích dữ liệu của Microsoft SQL Server. Nó cho phép người dùng tạo các mô hình dữ liệu đa chiều (multidimensional) và mô hình dữ liệu phẳng (tabular) để phân tích dữ liệu từ các nguồn khác nhau**
##### 5.1 Sử dụng thuật toán Association Rule
- Association Rule: là quá trình tìm ra các mối quan hệ (tương quan) giữa các đối tượng trong tập dữ liệu. Có dạng X => Y với:
    ●X: antecedent (tiền đề)
    ●Y: consequent (hệ quả)
- Hai tham số quan trọng được dùng để đo lường luật kết hợp là:
    ●Support (độ hỗ trợ): Xác suất mà X và Y đồng thời cùng xuất hiện.
    ●Confidence (độ tin cậy): Xác suất xảy ra Y khi có X  
- Ngoài hai tham số chính là Minimum probability và Minimum support thì thuật toán Microsoft Association Rule còn cung cấp thêm một tham số là Importance (độ quan trọng) - xác định sự tương quan giữa sự kiện X và sự kiện Y. Nếu
    ●Importance > 0 (dương) cho thấy khi X xảy ra thì khả năng xuất hiện Y cũng sẽ tăng lên. Importance có giá trị dương lớn cho thấy X có ảnh hưởng tích cực đến sự xuất hiện của Y.  
    ●Importance < 0 (âm) cho thấy khi X xảy ra thì khả năng xuất Y sẽ giảm đi. Importance có giá trị âm lớn cho thấy X có ảnh hưởng tiêu cực đến sự xảy ra của Y. 
    ●Importance = 0 thì điều này cho thấy không có mối liên hệ giữa X và Y
- Đối với tập dữ liệu House Rent - Giá thuê nhà ở Ấn Độ, thì sử dụng khai phá luật Kết hợp để tìm ra các mối quan hệ giữa các thuộc tính, các quy luật kết hợp ảnh hưởng đến giá cho thuê (Rent), ví dụ như nếu nơi cho thuê thuộc thành phố lớn và diện tích rộng thì giá thuê sẽ mắc. 
̵Khi tìm ra các quy luật kết hợp, ta có thể sử dụng chúng để phân tích và đưa ra dự đoán giá thuê nhà dựa trên các mối quan hệ phụ thuộc đó. 
- **Chọn các thuộc tính đầu vào và đầu ra**
![alt text](/Images/Picture16.png)
- **Kết quả sau khi thực hiện thuật toán được mô tả bởi Dependency Network**
![alt text](/Images/Picture17.png)
- Ở Dependency Network, ta có thể xem được các mô tả mức độ phụ thuộc giữa các hạng mục trong luật kết hợp và mô tả theo độ mạnh (Strongest Links) đến giảm dần (kéo gần đến All Links). 
![alt text](/Images/Picture18.png)
Nhận xét: Dựa vào tất cả những liên kết mà nó phụ thuộc đến giá thuê nhà thấp hơn 15336, cho thấy rằng những nơi cho thuê có quy mô nhỏ với diện tích dưới 1000 có từ 2 3 phòng cho thuê với tình trạng nội thất là không trang bị hay chỉ trang bị một ít, bên cạnh đó những nơi này thuộc khu vực ‘Super’ trong các thành phố như Kolkata, Hyderabad, Chennai, hay Bangalore, thậm chí trong thành phố Delhi mà do chính chủ đứng ra cho thuê thì khả năng giá thuê sẽ khá thấp. 