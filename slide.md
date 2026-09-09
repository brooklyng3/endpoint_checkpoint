---
marp: true
theme: gaia
class: lead
---

## Enpoint Security Monitoring Checkpoint

---
<!-- class: default -->

<style>
  h1 {
    text-align: center;
    margin-top: 0px;
    padding-bottom: 10px;
    border-bottom: none;
  }
  
  /* Shrink the text slightly so all 4 bullets fit on the slide */
  p, li {
    font-size: 26px; 
    line-height: 1.4;
  }
</style>

# Intro to Endpoint Security

**Endpoint Security Fundamentals**

* Việc hiểu rõ các tiến trình của Hệ điều hành Windows là yếu tố cốt lõi để phân tích log endpoint một cách hiệu quả và phát hiện các hoạt động bất thường.
* Task Manager là một công cụ tốt để tìm hiểu về các tiến trình lõi của Windows, vì nó hiển thị các tiến trình đang hoạt động cùng với mức tiêu thụ CPU và bộ nhớ của chúng.
* Analysts phải sử dụng các bộ phần mềm chuyên dụng để kiểm tra các artifact chạy ngầm của hệ thống và đánh giá chính xác môi trường endpoint, chẳng hạn như bộ công cụ Sysinternals.
* Các ứng dụng đáng chú ý trong bộ công cụ này là TCPView dùng để giám sát mạng và Process Explorer để xem thông tin chi tiết hơn về các tiến trình đang chạy.

---
<!-- class: default -->

<style>
  /* Keep the header centered and consistent */
  h1 {
    text-align: center;
    margin-top: 0px;
    padding-bottom: 10px;
    border-bottom: none;
  }
  
  /* Ensure paragraph text fits nicely */
  p, li {
    font-size: 26px; 
    line-height: 1.5;
  }

  /* Style the nested tool list for better visual hierarchy */
  ul > li > ul > li {
    font-size: 24px;
    color: #4a5568; /* Slightly muted color for sub-bullets */
    font-weight: bold;
    margin-top: 5px;
    list-style-type: square; /* Change bullet shape for sub-items */
  }
</style>

# Intro to Endpoint Security

**Endpoint Logging and Monitoring**

* Mặc dù việc giám sát các tiến trình đang chạy rất hữu ích cho việc quan sát thời gian thực, nhưng không thể bỏ qua việc ghi log endpoint liên tục để truy vết và liên tục theo dõi các hoạt động của người dùng.
* Các công cụ ghi và tổng hợp log phổ biến bao gồm:
  * Windows Event Logs
  * Sysmon
  * OSQuery
  * Wazuh

---
<!-- class: default -->

<style>
  h1 {
    text-align: center;
    margin-top: 0px;
    padding-bottom: 10px;
    border-bottom: none;
  }
  
  /* Reset font size for standard readability */
  p, li {
    font-size: 24px; 
    line-height: 1.5;
  }

  /* Two-column layout grid */
  .two-column {
    display: grid;
    grid-template-columns: 60% 40%;
    gap: 20px;
    align-items: center; /* Centers items vertically relative to each other */
    margin-top: 20px;
  }

  /* Style the image to fit nicely within its column */
  .two-column img {
    max-width: 100%;
    height: auto;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Adds a subtle drop shadow to the white image */
  }
</style>

# Intro to Endpoint Security

**Endpoint Log Analysis**

<div class="two-column">
<div>

* Thiết lập baseline là việc xác định các điều kiện hoạt động bình thường, theo dự kiến của một môi trường IT. Điều này rất cần thiết để tạo ra một điểm tham chiếu nhằm nhanh chóng phát hiện outlier có khả năng gây nguy hiểm.
* Analysts phải correlate events để tìm ra các mối liên kết có ý nghĩa giữa những artifact nằm rải rác trong log mạng, ứng dụng và endpoint, từ đó xâu chuỗi lại thành một bức tranh toàn cảnh về một sự cố bảo mật.

</div>
<div>

![Baseline Chart](baseline.png)

</div>
</div>
