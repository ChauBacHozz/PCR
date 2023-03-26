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













