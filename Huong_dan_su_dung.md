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
![image](https://user-images.githubusercontent.com/90232557/226869390-0af1db5d-06d1-46ae-a5a1-d8d0f3ddbecc.png)
- Bước 3: Gõ lệnh "pip install numpy, pandas, matplotlib, scikit-learn, openpyxl" vào cửa sổ terminal rồi ấn Enter, chờ quá trình cài đặt cho đến khi có thông báo "Successfully installed" hiện lên là coi như đã cài đặt thành công.
*Lưu ý: ipynb là đuổi của file dạng jupyter notebook, sủ dụng nhân python để chạy lệnh, nên khi code sẽ giống như code python, tuy nhiên jupyter notebook có khả năng chạy từng khối lệnh (cell) riêng biệt, cho nên được dùng rất phổ biến khi code học máy và phân tích dữ liệu*

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
X = data[:, 4:]
y = data[:, 1:4]
```
*Do các cột nồng độ từ cột thứ 1 đến cột thứ 3, các cột Abs là từ cột thứ 3 trở đi, python đánh số bắt đầu từ 0, cho nên cột đầu tiên(STT) chính là cột thứ 0*
- Co giãn dữ liệu: với bảng dữ liệu nồng độ - tín hiệu của phổ UV-VIS thì dữ liệu khá đơn giản nên không cần tới quá nhiều kĩ thuật tiền xủ lý dữ liệu, tuy nhiên nếu giá trị giữa các cột nồng độ - Abs cách nhau quá lớn (>10 lần), có thể co dữ liệu về các giá trị nằm trong khoảng 0 - 1 để khiến cho tốc độ luyện mạng nhanh hơn














