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
### 5.1. Association Rule Mining
#### 5.1.1. Giới thiệu
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
#### 5.1.2. Tiến Hành Khai Phá Luật Kết Hợp
- **Chọn các thuộc tính đầu vào và đầu ra**
![alt text](/Images/Picture16.png)
- **Kết quả sau khi thực hiện thuật toán được mô tả bởi Dependency Network**
![alt text](/Images/Picture17.png)
- Ở Dependency Network, ta có thể xem được các mô tả mức độ phụ thuộc giữa các hạng mục trong luật kết hợp và mô tả theo độ mạnh (Strongest Links) đến giảm dần (kéo gần đến All Links). 
![alt text](/Images/Picture18.png)
Nhận xét: Dựa vào tất cả những liên kết mà nó phụ thuộc đến giá thuê nhà thấp hơn 15336, cho thấy rằng những nơi cho thuê có quy mô nhỏ với diện tích dưới 1000 có từ 2 3 phòng cho thuê với tình trạng nội thất là không trang bị hay chỉ trang bị một ít, bên cạnh đó những nơi này thuộc khu vực ‘Super’ trong các thành phố như Kolkata, Hyderabad, Chennai, hay Bangalore, thậm chí trong thành phố Delhi mà do chính chủ đứng ra cho thuê thì khả năng giá thuê sẽ khá thấp. 

**Mô hình biểu diễn các yếu tố phụ thuộc ảnh hưởng đến mức giá cho thuê từ 15336 - 31899**
![alt text](/Images/Picture19.png)

Nhận xét: Ta thấy mô hình không thể hiện rõ những yếu tố ảnh hưởng đến giá thuê từ 15336 - 31899. Duy chỉ có những thông tin liên quan đến Diện tích (từ 1038 - 2144). Tuy nhiên dựa vào bấy nhiêu thông tin thì không thể suy ra được rằng những nơi cho thuê có diện tích như thế thì giá thuê sẽ rơi vào 15336 - 31899.  

#### 5.1.3. Áp dụng Association Rule vào mô hình dự đoán giá thuê
- Điền các giá trị cho các thuộc tính trừ cột Rent (vì cột này dùng để dự đoán giá cho thuê). Các giá trị input được mô tả ở hình bên dưới

![alt text](/Images/Picture20.png)

- Kết quả thu được

![alt text](/Images/Picture21.png)

Nhận xét: Với những giá trị đã chọn thì kết quả dự đoán giá thuê là khoảng 9418 với xác suất là 0.964. Ta thấy mô hình dự đoán đúng so với kết quả đã phân tích trước đó.
- Thử một số giá trị khác với thành phố Mumbai và số lượng cho thuê phòng khác

![alt text](/Images/Picture22.png)

- Kết quả thu được

![alt text](/Images/Picture23.png)

Nhận xét: Ta thấy kết quả đưa ra khác với những gì đã phân tích mặc dù quy mô cho thuê lớn với diện tích hơn 2000 feet vuông, tọa lạc ở thành phố Mumbai mà giá thuê dự đoán lại thấp hơn 15000. Lý do là vì những luật kết hợp mà thuật toán đưa ra thì không có luật nào thể hiện tương quan giữa Size = 2144 - 3500 với giá thuê Rent. Nên khi đưa ra kết quả dự đoán sẽ sai so với kết quả đã phân tích được.

#### 5.1.4. Đánh giá mô hình 
##### 5.1.4.1. Nhận xét chung
- Những luật kết hợp mà thuật toán đem lại đã đưa ra những kết quả khá có ý nghĩa khi tìm ra được những yếu tố ảnh hưởng đến giá thuê nhà cụ thể là mức dưới 15336 và mức trên 77028. Điều này sẽ giúp cho 	ta có cái nhìn rõ hơn về những yếu tố ảnh hưởng mạnh đến hai mức giá thuê trên. Và thấy được những yếu tố nào gây ra sự khác biệt rõ rệt giữa hai mức giá thuê này. 	
- Đánh giá về khả năng dự đoán trên tập test (20% của tập dữ liệu)

![alt text](/Images/Picture24.png)

Nhận xét: Như vậy có thể thấy thuật toán Luật kết hợp không thích hợp để dự đoán kết quả vì nó chỉ áp dụng với những trường hợp đúng với các luật kết hợp mà nó sinh ra còn những trường không tồn tại thì nó không đem lại kết quả đúng. 
##### 5.1.4.2. Tính ứng dụng của mô hình
- Nếu đóng vai trò là một người đang tìm thuê nhà đang muốn tìm những căn nhà phù hợp với kinh phí của họ thì cần cân nhắc các yếu tố ảnh hưởng đến giá cho thuê như đã phân tích là thành phố mà nơi cho thuê tọa lạc, hay qui mô căn hộ. 
    + Ví dụ họ muốn tìm thuê nhà có giá tiền dưới 15336 thì nên lựa chọn các nơi có đặc điểm như quy mô căn hộ nhỏ, diện tích bé, số lượng phòng cho thuê không nhiều từ 2 - 3 phòng, không trang bị nội thất hoặc chỉ trang bị những thứ cơ bản và tọa lạc ở những thành phố nhỏ như Kolkata, Hyderbad,.. và nên thuê từ chủ nhà để không phải chịu những chi phí môi giới,... 
- Nếu đóng vai tròn là chủ đầu tư muốn tăng lợi nhuận thì dựa vào những luật kết hợp từ đó tìm hiểu được những điều kiện giúp tăng giá cho thuê cụ thể là nên đầu tư những căn hộ phòng cho thuê ở thành phố Mumbai hoặc Bangalore, có qui mô vừa hoặc lớn với số phòng cho thuê nhiều,.. thì chắc chắn sẽ đem lại lợi nhuận cao. 
### 5.2. Clustering
#### 5.2.1. Giới thiệu
- Microsoft Clustering là một kỹ thuật phân cụm học không giám sát. Áp dụng thuật toán phân cụm để phân nhóm các điểm dữ liệu dựa trên một số đặc trưng. Các cụm được tìm ra chứa các điểm dữ liệu có tính chất tương tự nhau. 
- Với tập dữ liệu House Rent của nhóm, việc áp dụng Clustering giúp cho việc phân nhóm các căn hộ/ nhà/ phòng cho thuê có tính chất tương đồng nhau dựa trên các đặc trưng như diện tích (size), số phòng ngủ (bathroom), khu vực (area type), thành phố (city),... Điều này giúp chúng ta có cái nhìn tổng thể về thị trường nhà cho thuê ở Ấn Độ, đồng thời giúp các chủ đầu tư, chủ hộ đưa ra các quyết định kinh doanh phù hợp. 
- Sau khi đã phân cụm các căn hộ/ nhà/ phòng cho thuê dựa trên các đặc trưng cụ thể thì có thể áp dụng dự đoán thông tin của căn hộ mới thông qua cụm mà nó được gán nhãn. 
#### 5.2.2. Tiến hành khai phá phân cụm
- Chọn các biến input và predict

![alt text](/Images/Picture25.png)
- Kết quả sau khi thực thi. Tiến hành đặt tên cho từng cụm theo đặc điểm 
    + 1 bath 1 bed small size;
    + 2 bath 2-3 bed medium size;
    + 1-2 bath 2 bed lower medium size;
    + Mumbai 2 bath 2 bed;
    + 3 bath 3 bed upper medium size.

![alt text](/Images/Picture26.png)

- Xem sự tương quan của các cụm theo các biến dự đoán và giá trị khác nhau trong Cluster Diagram
- Khi chọn Shading Variable là ‘Rent’ và State là ‘High’, ta thấy được 3 cụm  Mumbai, 3 bath 3 bed upper medium size, 2 bath 2-3 bed medium size có độ đậm cao hơn 2 cụm còn lại, cho thấy các dòng thuộc tính Rent từ 33000-53000 thuộc nhiều vào 3 cụm này. 

![alt text](/Images/Picture27.png)

- Vào tab Mining Model Prediction, điền vào Singleton Query Input các giá trị cho các biến dự đoán và mong đợi rằng tập giá trị này sẽ rơi vào cụm này. Các giá trị theo các biến như sau:

![alt text](/Images/Picture28.png)
- Ta mong đợi rằng tập giá trị này sẽ rơi vào cụm 2 bath 2-3 bed medium size vì đã cố tình đặt giá trị cho Bathroom là 2 và Number of Bedrooms-Halls-Kitchens là 3.
- Kết quả dự đoán được là cụm 2 bath 2-3 bed medium size, đúng với mong đợi ban đầu.

![alt text](/Images/Picture29.png)

#### 5.2.3. Tính ứng dụng 
- Với mô hình phân cụm dùng Microsoft Clustering, tạo ra các cụm với những đặc trưng khác nhau, ở vai trò người dùng, nếu họ chỉ có một vài thông tin không đầy đủ, việc phân cụm sẽ giúp họ có được những dự đoán về các thông tin còn lại dựa vào cụm được phân vào với những thông tin đã có. Chẳng hạn với những thông tin như phòng đang cho thuê có 4 phòng ngủ, 4 phòng tắm, người dùng có thể mong đợi căn phòng ấy sẽ có kích thước upper medium hoặc large và có giá phòng trung bình cao. Mô hình này cũng có thể được dùng theo hướng ngược lại, thay vì dự đoán giá thuê, người dùng có thể xem xét giá thuê mong muốn của họ thuộc vào cụm vào và họ sẽ biết được với giá thuê đó, phòng thuê sẽ có những đặc trưng gì về số phòng, thành phố, kích thước,...

### 5.3. Classification
#### 5.1.1. Giới thiệu
- Thuật toán phân loại (Classification) là một kỹ thuật học máy được sử dụng để dự đoán dựa trên các đặc trưng của điểm dữ liệu và các nhãn hoặc lớp đã biết trước đó.
- Với tập dữ liệu về giá thuê nhà ở Ấn Độ, thì ta có thể phân loại các căn hộ/ nhà/ phòng cho thuê theo các mức giá khác nhau. Từ đó, khi có một căn hộ/ nhà/ phòng cần cho thuê, việc xác định loại giá thuê của căn hộ này sẽ giúp cho chủ hộ hay chủ đầu tư có thể điều chỉnh mức giá thuê thích hợp hoặc người thuê nhà có thể lựa chọn những căn nhà có đặc điểm phù hợp trong mức giá phù hợp với mình.
- Thuật toán nhóm sử dụng chính là:
    + Decision Tree: Xây dựng cây quyết định dựa trên các quy tắc phân loại để dự đoán loại giá thuê của một căn hộ mới. Các quy tắc này được học từ tập dữ liệu bao gồm các căn hộ đã biết giá thuê của chúng.

#### 5.1.2. Khai phá dữ liệu
- Lựa chọn các biến sử dụng trong mô hình

![alt text](/Images/Picture30.png)

- Xem mức độ phụ thuộc ở Dependency Network
![alt text](/Images/Picture31.png)

Nhận xét: Ta thấy biến đầu vào có liên kết mạnh nhất với biến dự đoán là ‘City’.
- Bật tab Mining Model Viewer → Decision Tree để xem cây phân loại.

![alt text](/Images/Picture32.png)

Nhận xét: Decision tree gồm có 6 level.
    + Level 1 - Point Of Contact: Nhà được cho thuê bởi chính chủ nhà sẽ có giá thuê rẻ hơn so với nhà được cho thuê bởi công ty cho thuê.
    + Level 2 - Total Rooms: Khi các căn nhà được cho thuê bởi cùng 1 loại bên cho thuê (hoặc là cùng cho thuê bởi chính chủ nhà, hoặc là cùng được cho thuê bởi công ty cho thuê nhà) thì căn nhà nào có số lượng phòng càng nhiều thì giá thuê càng đắt.
    + Level 3 - City: Thành phố Mumbai là thành phố có giá thuê nhà đắt đỏ nhất trong các thành phố.
    + Level 4 - Size: Những căn nhà có diện tích càng lớn thì giá thuê càng cao
    + Level 5 & 6: Những căn nhà không trang bị nội thất thì sẽ có giá thuê rẻ hơn những ngôi nhà có trang bị nội thất.

#### 5.1.3. Đánh giá mô hình
- Chọn tab Mining Accuracy Chart, quan sát Classification Matrix 

![alt text](/Images/Picture34.png)

Nhận xét:   + Tổng số case mô hình đoán đúng là 898 trên tổng số 1338 case
            + Accuracy: 68%

#### 5.1.4. Tính ứng dụng của mô hình
- Nếu đóng vai trò là một người đang tìm thuê nhà đang muốn tìm những căn nhà phù hợp với kinh phí của họ, chọn background là nhóm giá thuê tương ứng với khoảng giá thuê mà họ có thể chi trả mỗi tháng. Ví dụ họ muốn tìm thuê nhà có giá tiền dưới 15400, như vậy cần chọn background dưới 15400.

![alt text](/Images/Picture35.png)

-> Nếu muốn chọn những căn nhà có giá thuê rẻ (<15400) thì nên lựa chọn những căn nhà dược cho thuê bởi chính chủ nhà, có tổng số phòng <4, không nên lựa chọn thuê nhà ở thành phố Mumbai và nên chọn những căn nhà không bao gồm nội thất.

- Nếu đóng vai tròn là chủ đầu tư muốn chọn một nơi để xây nhà cho thuê, họ sẽ cần lựa chọn những yếu tố giúp tăng giá thuê nhà. Ví dụ mức giá họ mong muốn là trên 77000, chọn background là nhóm >=77000, ta thấy

![alt text](/Images/Picture36.png)

-> Nếu muốn có mức giá cho thuê đó thì chủ đầu tư nên chọn thành phố Mumbai, diện tích căn nhà trên 1807 feet, tuy nhiên cần cân nhắc đến việc giá đất ở Mumbai cũng sẽ khá đắt thì chủ đầu tư nên xây nhiều phòng trong căn nhà cho thuê và nếu có thể thì trực tiếp cho khách hàng thuê chứ không qua công ty môi giới để giảm thiểu chi phí.


## 6. ĐÁNH GIÁ VÀ SO SÁNH BA THUẬT TOÁN
### 6.1 Classification
- Là lựa chọn tối ưu nhất trong 3 thuật toán nếu người dùng muốn phân loại căn nhà với những đặc điểm mà họ mong muốn sẽ thuộc vào khoảng giá thuê từ bao nhiêu đến bao nhiêu, từ đó chuẩn bị ngân sách cho việc thuê nhà hoặc các phương án đầu tư phù hợp.
- Người dùng cũng có thể lựa chọn mức giá thuê nhà mà mình mong muốn và chiếu theo các đặc điểm mà mô hình đưa ra để chọn căn nhà phù hợp với kinh phí của mình trong thực tế.
- Đối với tập dữ liệu ‘Giá nhà cho thuê ở Ấn Độ’ và thuật toán được chọn để dự đoán là Decision Tree thì tập các biến đầu vào nên lựa chọn là ‘Point To Contact’- Bên cho thuê nhà, ‘Total Rooms’- Tổng số phòng, ‘City’- Thành phố, ‘Size’- Diện tích của ngôi nhà, ‘Furnishing Status’- Tình trạng nội thất.
### 6.2 Clustering
- Phù hợp với người dùng muốn có cái nhìn tổng quát cả về giá thuê lẫn các đặc trưng tương ứng với từng mức giá thuê khác nhau. Từ đó sẽ giúp ích cho việc quản lý và phân tích thị trường cho thuê nhà và giúp đưa các quyết định kinh doanh như giá cả, chiến lược quảng cáo,... với từng nhóm nhà. Ví dụ như đối với những nhóm nhà thuê có diện tích nhỏ đến vừa, giá thuê rẻ thì ta có thể tập trung quảng cáo cho đối tượng là sinh viên. Còn với những nhóm căn hộ cao cấp hơn với diện tích lớn thì có thể xây dựng chiến lược quảng bá đến đối tượng là những người có thu nhập cao. 
- Khi dự đoán được căn nhà của người dùng thuộc cụm nào thì có thể suy ra các đặc tính còn lại không được đề cập của nó dựa vào đặc tính chung của cụm.
### 6.3. Association Rule
- Việc áp dụng khai phá luật kết hợp vào bài toán ‘House Rent’ ở Ấn Độ đã tìm ra được các mối quan hệ và kết nối giữa các tiêu chí như diện tích, thành phố, số phòng ngủ, số phòng tắm,... với giá cả. Từ các quan hệ giữa các tiêu chí đó thì có thể đưa ra những lời khuyên cho khách hàng về những lựa chọn phù hợp khi tìm kiếm nhà cho thuê dựa trên các kết quả phân tích. Tuy nhiên vì tập dữ liệu còn giới hạn nên có thể các luật sinh ra chưa phản ánh được đầy đủ cũng như sự khác biệt giữa các mối liên hệ với các mức giá thuê khác nhau. Đồng thời qua quá trình đánh giá và phân tích nhóm nhận thấy rằng thuật toán này không thích hợp để dự đoán giá thuê vì nó chỉ dự đoán đúng khi nó xuất hiện trong các luật kết hợp còn với những trường hợp khác với tập dữ liệu thì nó sẽ không đem lại kết quả chính xác. Vì bản chất thuật toán này thích hợp với những bài toán cho ‘phân tích giỏ hàng’ nên nó sẽ không đem lại kết quả thật sự tối ưu. 