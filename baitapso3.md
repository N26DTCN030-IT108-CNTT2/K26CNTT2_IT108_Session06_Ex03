\# Báo cáo Phân tích: Tự động hóa Phân tích File Log



\## 1. Sơ đồ 3 bước (stdout → | → stdin)



Luồng dữ liệu chạy trực tiếp trên RAM thông qua Pipeline, không cần ghi file trung gian:



```text

\[Get-Content access.log] 

&#x20;      │

&#x20;      ▼ (stdout)

&#x20;     \[ | ]  ───► Truyền luồng text qua ống dẫn (Pipeline) trên RAM

&#x20;      │

&#x20;      ▼ (stdin)

\[Select-String "TIMEOUT"] 

&#x20;      │

&#x20;      ▼ (stdout)

&#x20;     \[ | ]  ───► Truyền tiếp các dòng đã lọc

&#x20;      │

&#x20;      ▼ (stdin)

\[Measure-Object]

&#x20;      │

&#x20;      ▼

\[Kết quả: Con số duy nhất]





\## Câu lệnh PWS hoàn chỉnh 1 dòng duy nhất



(Get-Content .\\access.log | Select-String "TIMEOUT" | Measure-Object).Count

