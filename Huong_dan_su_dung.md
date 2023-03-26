# PCR

# Hướng dẫn sử dụng python để chạy thuật toán hồi quy cấu tử chính (PCR)

## Cài đặt python và các ứng dụng cần thiết
- Bước 1: Tải python từ trang: https://www.python.org/downloads/
Chú ý: Tích vào 2 ô Install launcher for all users và Add Python to PATH, sau khi cài đặt mở ứng dụng cmd và gõ "python --version" và ấn Enter, nếu hiển thị phiên bản python đã cài về thì đã cài đặt thành công, nếu không thì ấn lại vào file installer vừa tải về để gỡ cài đặt python. Sau đó bấm lại vào installer để cài lại python, lưu ý hãy chọn vào 2 dòng trên.
- Bước 2: Cài đặt visual studio code  (VS Code) từ trang: https://code.visualstudio.com/download
- Bước 3: sau khi cài đặt VS Code, mở ứng dụng và vào file -> chọn open folder -> Tại một folder mới tại nơi muốn lưu code rời ấn Open
- Bước 4: ở màn hình VS Code, vào phần extenson (Ctrl + Shift + X) gõ "python" (nếu không hiển thị chữ install ở dưới tức là đã được cài đặt, nếu không hãy bấm vào install), sau đó gõ "jupyter" và cài đặt lựa chọn xuất hiện đầu tiên
![image](https://user-images.githubusercontent.com/90232557/226867539-d31397b4-444e-4148-82f1-089b563cc1c6.png)
- Bước 5: trong phần tìm kiếm của extension gõ "Code runner" và cài đặt lựa chọn xuất hiện đầu tiên

## Tạo file thực thi và cài đặt các thư viện cần thiết
- Bước 1: Ấn Ctrl + Shift + E để mở phần Explorer của VS Code, tạo file ipynb để chạy code bằng cách gõ {Tên file}.ipynb, ví dụ: main.ipynb sau đó ấn Enter (Tất cả code python sẽ nằm trong file này)
- Bước 2: Ấn Ctrl + Shift + ` để mở cửa sổ terminal, hoặc vào phần Terminal ở thành toolbar của VS Code -> chọn New Terminal
- Bước 3: Gõ lệnh "pip install numpy, pandas, matplotlib, scikit-learn, openpyxl" vào cửa sổ terminal rồi ấn Enter, chờ quá trình cài đặt cho đến khi có thông báo "Successfully installed" hiện lên là coi như đã cài đặt thành công.

*Lưu ý: ipynb là đuôi của file dạng jupyter notebook, sủ dụng nhân python để chạy lệnh, nên khi code sẽ giống như code python, tuy nhiên jupyter notebook có khả năng chạy từng khối lệnh (cell) riêng biệt, cho nên được dùng rất phổ biến khi code học máy và phân tích dữ liệu*

## Code PCR bằng python
### Giới thiệu các thư viện: numpy, matplotlib, pandas
- numpy: thư việc đại số tuyến tính của python (xử lý nhân ma trận, nghịch đảo ma trận, vv...) dể xử lý số liệu
- matplotlib: thư viện hiển thị dữ liệu (giống như Chart của excel)
- pandas: thư viện dùng để đọc dataset từ các file dạng csv, xlsx, text,...
- scikit-learn: thư viện học máy dùng cho đa mục đích
### Cách thao tác với file jupyter notebook trên VS Code
- Khi mới tạo ra file .ipynb, chúng ta thấy giao diện sẽ trông như sau
![image](https://user-images.githubusercontent.com/90232557/227752292-b543d502-d3b3-4c61-b241-c8ffa16779ec.png)
File sẽ có 2 thành phần chính, phần thanh công cụ (phía trên_xanh lá) và phần code cell (ô hình chữ nhật_đỏ)
![image](https://user-images.githubusercontent.com/90232557/227752330-e7fa16d2-9cea-4e89-8cb9-a4612e26ee95.png)
Trong phần thanh công cụ ta chỉ cần chú ý tới 2 nút: Code và Run All
  + Code: tạo thêm một khối lệnh mới
  + Run All: chạy tất cả các khối lệnh từ trên xuống
 Phần khối lệnh là nơi ta sẽ để code python vào bên trong đó, ở bên trái khối lệnh ta sẽ thấy hiện thị biểu tượng tam giác, khi nhấn vào sẽ chạy khối lệnh hiện tại. Nếu muốn chạy tất cả các khối lệnh, hãy ấn Run All ở trên thanh công cụ
#### Có thể tham khảo code ở link: https://github.com/ChauBacHozz/PCR/blob/main/PCR.ipynb
### Bước 1: Import thư viện vào file code
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from sklearn.preprocessing import scale 
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import KFold, cross_val_score, train_test_split
from sklearn.metrics import mean_squared_error
from sklearn.decomposition import PCA
```
- Từ **as** có nghĩa là ta định nghĩa tên gọi tắt cho thư viện, nhằm giúp cho việc code không bị dài dòng và thuận tiện cho việc gọi các hàm từ thư viện
### Bước 2: Sử dụng python để đọc file dữ liệu và tiến hành tiền xử lý dữ liệu
##### Đọc file dữ liệu
- Bấm vào nút "+ Code" để tạo code cell mới
- Copy file dữ liệu (dạng csv, xlsx, txt, ...) vào cùng thư mục với file python
![image](https://user-images.githubusercontent.com/90232557/227753581-cfc248f2-6b1e-46f8-9371-7e3a588ad81f.png)
- Sau đó trong file .ipynb, tạo một biến đặt tên là data (data sẽ lưu trữ thông tin của file dữ liệu) và đọc bảng dữ liệu bằng lệnh pd.read_excel({Tên file})
- Xuống dòng gõ lệnh print(data) rồi chuột phải, chọn "Run All" để kiểm tra python đã đọc được dữ liệu hay chưa
![image](https://user-images.githubusercontent.com/90232557/227753704-6ac487c2-bdf6-471f-8dd5-abc5ebade51b.png)
 *Nếu dữ liệu được đọc thành công, sau khi run code bảng dữ liệu sẽ hiển thị ở phía dưới như hình*

##### Tiền xử lý dữ liệu
- Kiểm tra dữ liệu trống: Kiểm tra file dữ liệu có ô nào bị bỏ trống không bằng lệnh print(data.isnull().values.any()) sau đó run all, nếu ở dưới hiện lên là False tức là không có ô nào trong bảng dữ liệu bị trống, còn nếu hiện lên là True thì cần rà soát kiểm tra lại file dữ liệu, nếu không khi luyện mạng sẽ gây lỗi
- Chia dữ liệu thành các cột x và Y: Ở đây bài toán chính là sử dụng mô hình máy học để sự đoán nồng độ các chất trong hỗn hợp sản phẩm (thuốc) vậy nên mình sẽ coi dữ liệu đầu vào (X) là tín hiệu Abs, còn dữ liệu đích (Y) chính là nồng độ các chất. Để tách thành các cột X và Y trong trường hợp dữ liệu trên ta sử dụng lệnh:
```
X = data.iloc[:, 4:]
y = data.iloc[:, 1:4]
```
*Do các cột nồng độ từ cột thứ 1 đến cột thứ 3, các cột Abs là từ cột thứ 3 trở đi, python đánh số bắt đầu từ 0, cho nên cột đầu tiên(STT) chính là cột thứ 0*
Chia tập dữ liệu thành tập dữ liệu luyện (train) và tập dữ liệu kiểm tra (test), sử dụng câu lệnh sau:
```
# Nếu trước đó không chuẩn hóa hoặc chính quy hóa dữ liệu
X_train, X_test, y_train, y_test = train_test_split(data.iloc[:,3:], data.iloc[:,0:3],test_size=0.2, random_state=42)
# Nếu trước đó đã chuẩn hóa hoặc chính quy hóa dữ liệu
X_train, X_test, y_train, y_test = train_test_split(data[:,3:], data[:,0:3],test_size=0.2, random_state=42)
```
+ X_train: các cột Abs của tập dữ liệu train
+ y_train: các cột nồng độ của tập dữ liệu train
+ X_test: các cột Abs của tập dữ liệu test
+ y_test: các cột nồng độ của tập dữ liệu test
- Co giãn dữ liệu: với bảng dữ liệu nồng độ - tín hiệu của phổ UV-VIS thì dữ liệu khá đơn giản nên không cần tới quá nhiều kĩ thuật tiền xủ lý dữ liệu, tuy nhiên nếu giá trị giữa các cột nồng độ - Abs cách nhau quá lớn (>10 lần), có thể co dữ liệu về các giá trị nằm trong khoảng 0 - 1 để khiến cho tốc độ luyện mạng nhanh hơn
- Chính quy hóa dữ liệu: với dữ liệu dạng nhiều chiều (nhiều cột) thì việc chính quy hóa giúp cho giá trị của mỗi đặc trưng có trung bình bằng 0 và phương sai bằng 1. Từ đó giúp model dễ dàng tiến được tới giá trị min của hàm loss, đồng thời khiến cho tốc độ học máy tăng lên. thư viện scikit-learn cung cấp một hàm giúp chúng ta có thể vừa chuẩn hóa và vừa chính quy hóa dữ liệu cùng một lúc bằng lệnh sau:
```
X_train_scaled, X_test_scaled = scale(X_train), scale(X_test)
```
*Nên ưu tiên chuẩn hóa với tín hiệu đầu vào (X)*
![image](https://user-images.githubusercontent.com/90232557/227754831-5f978627-303c-4a92-8893-4f0712ac0068.png)
 #### Lưu ý: Các kỹ thuật tiền xử lý dữ liệu như chuẩn hóa, co giãn, chính quy hóa dữ liệu được sử dụng tùy trong từng trường hợp cụ thể. Với những dữ liệu đặc trưng sẽ phải thử để chọn ra những kỹ thuật sao cho việc học máy được diễn ra một cách tối ưu nhất. #### Lưu ý: Các kỹ thuật tiền xử lý dữ liệu như chuẩn hóa, co giãn, chính quy hóa dữ liệu được sử dụng tùy trong từng trường hợp cụ thể. Với những dữ liệu đặc trưng sẽ phải thử để chọn ra những kỹ thuật sao cho việc học máy được diễn ra một cách tối ưu nhất.

### Bước 3: Sử dụng phương pháp PCR để phân tích các cấu tử chính
##### Khảo sát, đánh giá và chọn số cấu tử chính tối ưu để thực hiện hồi quy
- Sử dụng phương thức fit_transform trong class PCA() của thư viện scikit-learn để chuyển tập dữ liệu train bằng câu lệnh sau:
```
lin_reg = LinearRegression()
rmse_list = []
pca = PCA()
X_train_pc = pca.fit_transform(X_train_scaled)
print(X_train_pc.shape)
```
Dòng lệnh cuối sẽ in ra dạng của ma trận X_train sau khi đã phân tích có dạng(a,b), trong đó a là số dòng và b là số cột, ở đây chúng ta sẽ chú ý b vì b chính là số chiều cần phân tích
- Dùng Kfold để chia tập dữ liệu thành các tập dữ liệu con để đnhs giá chéo bằng câu lệnh:
```
cv = KFold(n_splits=7, shuffle=True, random_state=42)
```
- Tính giá trị RMSE (Root mean square error) trên từng trường hợp pc (từ 1 đến 7, tương ứng với sô cột Abs):
```
for i in range(1, X_train_pc.shape[1]+1):
    rmse_score = -1 * cross_val_score(lin_reg, 
                                      X_train_pc[:,:i], # Use first k principal components
                                      y_train, 
                                      cv=cv, 
                                      scoring='neg_mean_squared_error').mean()
    rmse_list.append(rmse_score)
```
- Biểu diễn tổng quan giá trị RMSE theo từng pc
```
plt.plot(rmse_list, '-o')
plt.xlabel('Number of principal components in regression')
plt.ylabel('Cross-Validation RMSE')
plt.title('PCR')
plt.xlim(xmin=-1);
plt.xticks(np.arange(X_train_pc.shape[1]), np.arange(1, X_train_pc.shape[1]+1))
```
- Sau khi chạy lệnh, sẽ hiện lên một biểu đồ hiển thị giá trị của RMSE theo từng pc, từ đó ta có thể chọn sô pc tối ưu nhất
![image](https://user-images.githubusercontent.com/90232557/227783449-37d5c835-3b4c-444b-a698-02f34d7c9be2.png)
  *Như trong trường hợp trên, số pc tối ưu là 4*
- Sau khi chọn được số pc tối ưu, lưu số pc ta chọn vào một biến gọi là best_pc_num:
```
best_pc_num = 4
```
- Rồi sử dụng model Linear Regression của thư viện scikit-learn để xử lý hồi quy đa biến (trên tập dữ liệu train) với số pc đã chọn ():
```
lin_reg_pc = LinearRegression().fit(X_train_pc[:,:best_pc_num], y_train)
```
- Ta có thể in ra hệ số R2 sau khi xử lý hồi quy đa biến với lệnh:
```
print(lin_reg_pc.score(X_train_pc[:,:best_pc_num], y_train))
```
![image](https://user-images.githubusercontent.com/90232557/227787590-c822c9ca-e6c8-4ed1-9ee1-a89f1bce59ed.png)

##### Tính các giá trị theo tập test và so sánh với dữ liệu thực
- Sử dụng PCA để chuyển hóa tập dữ liệu test theo số pc đã chọn:
```
X_test_pc = pca.transform(X_test_scaled)[:,:best_pc_num]
```
- Sử dụng hàm predict để tính toán theo X_test_pc, sau đó in ra MSE (Mean Square Error) của giá trị tính và giá trị thực:
```
preds = lin_reg_pc.predict(X_test_pc)
pcr_score_test = mean_squared_error(y_test, preds, squared=False)
print(pcr_score_test)
```




















