# Giải bài tập 3 Terminal nâng cao
## Làm cái gì?
- Lọc từ TIMEOUT có trong tất cả file .log đếm số lượng của nó
## Phân tích
- Tìm tất cả file `.log` có trong dự án bằng `Get-ChildItem`
- Sau đó sử dụng `Get-Content` để đọc nội dung trong 
- Lọc các dòng có chứa **TIMEOUT** trong nội dung
- Lọc ngược loại bỏ các dòng có từ **NOT TIMEOUT**
- Đếm số lượng các dòng có từ __TIMEOUT__
:rocket: **Powershell**
```
(Get-ChildItem -Filter *.log -Recurse |Get-Content | Select-String "Timeout" | Where-Object {$_ "Not Timeout" -Notmatch}).Count
```  
:rocket: __Bash__
```
find -type f -name "*.log" -exec cat {} + | grep -i "Timeout" | grep -i -v "Not Timeout" | wc -l
```
## So sánh Powershell và Bash
| Câu lệnh | Powershell | Bash | 
|:---| :---| :---|
|Tìm tất cả các File .log có trong dự án|`Get-ChildItem -Filter *.log -Recurse`|`find -type f -name "*.log"`
|Đọc nội dung trong các file| `Get-Content` | `-exec cat {} +`
|Lọc từ **TIMEOUT** có trong file log| `Select-String "Timeout"`| `grep -i "Timeout"`
|Loại bỏ từ **NOT TIMEOUT** có trong nộ dung đã lọc|`Where-Object {$_ "Not Timeout" -Notmatch}`|`grep -i -v "Not Timeout"`
|Đếm sô lượng dòng có từ **TIMEOUT**|`().Count`| `wc -l`