---
marp: true
theme: gaia
class: lead
---

## Enpoint Security Monitoring Checkpoint

---
<!-- class: default -->

<style scoped>
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

<style scoped>
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

<style scoped>
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

---
<!-- class: default -->

<style scoped>
  h1 {
    text-align: center;
    margin-top: 0px;
    padding-bottom: 5px;
    border-bottom: none;
  }
  
  /* These rules will NOW ONLY apply to this specific slide! */
  p, li {
    font-size: 22px; 
    line-height: 1.4;
  }

  code {
    background-color: #2d3748;
    color: #e2e8f0;
    padding: 2px 6px;
    border-radius: 4px;
    font-size: 20px;
  }
  
  .cmd-line {
      margin-top: 15px;
      font-weight: bold;
  }
</style>

# Core Windows Processes

**Task Manager**

* Một tiện ích tích hợp sẵn của Windows được sử dụng để giám sát các tiến trình đang chạy, theo dõi mức sử dụng tài nguyên (CPU/Memory) và terminate các ứng dụng.
* Thẻ **Process** phân loại tất cả các hoạt động đang chạy thành Apps, Background processes, và Windows processes.
* Thẻ **Details** hiển thị các cột dữ liệu quan trọng phục vụ cho điều tra số – như PID, Image path name, và Command line – những thông tin cần thiết để phát hiện malicious outliers.
* Hạn chế chính của Task Manager là không hiển thị mối quan hệ tiến trình cha-con, đòi hỏi các nhà phân tích phải sử dụng các công cụ nâng cao như Process Hacker hoặc Process Explorer để có khả năng giám sát sâu hơn.

<p class="cmd-line">Mở Task Manager từ powershell: <code>taskmgr</code></p>

---
<!-- class: default -->

<style scoped>
  h1 {
    text-align: center;
    margin-top: 0px;
    padding-bottom: 10px;
    border-bottom: none;
  }
  
  .image-gallery {
    display: flex;
    justify-content: space-around; /* Distributes the images evenly across the slide */
    align-items: center; /* Centers them vertically relative to each other */
    margin-top: 10px;
  }

  .image-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 48%; /* Keeps them side by side without overlapping */
  }

  .image-gallery img {
    max-height: 400px; /* This is the magic fix! It stops the tall image from pushing the text off the slide */
    width: auto;
    max-width: 100%;
    border-radius: 6px;
    box-shadow: 0 4px 8px rgba(0,0,0,0.15);
    border: 1px solid #e2e8f0;
    object-fit: contain;
  }

  .caption {
    text-align: center;
    font-size: 24px;
    font-weight: bold;
    margin-top: 15px;
    color: #2d3748;
  }
</style>

# Core Windows Processes

**Task Manager**

<div class="image-gallery">

<div class="image-container">
  <img src="process.png" alt="Processes Tab">
  <div class="caption">Thẻ Processes</div>
</div>

<div class="image-container">
  <img src="details.png" alt="Details Tab">
  <div class="caption">Thẻ Details</div>
</div>

</div>

---
<!-- class: default -->

<style scoped>
  h1 {
    text-align: center;
    margin-top: 0px;
    padding-bottom: 10px;
    border-bottom: none;
  }
  
  p, li {
    font-size: 22px; 
    line-height: 1.4;
  }

  .two-column {
    display: grid;
    grid-template-columns: 55% 45%;
    gap: 20px;
    align-items: center; 
    margin-top: 15px;
  }

  .two-column img {
    max-width: 100%;
    height: auto;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2); 
    border: 1px solid #cbd5e0;
  }

  .pid-badge {
    color: #323538;
    padding: 2px 6px;
    border-radius: 4px;
    font-weight: bold;
    font-family: monospace;
  }
  
  .baseline-text {
      color: #2f855a;
      font-weight: bold;
  }
  
  .abnormal-text {
      color: #c53030;
      font-weight: bold;
  }
</style>

# Core Windows Processes

#### **<span class="pid-badge">System (PID 4)</span>**

<div class="two-column">
<div class="column">

* Là một kernel-mode thread chỉ thực thi mã trong system space và cấp phát bộ nhớ động từ các vùng nhớ heap của hệ điều hành.
* <span class="baseline-text">Normal Baseline:</span> Luôn được gán PID 4, chạy dưới quyền tài khoản Local System, và tiến trình cha duy nhất của nó là System Idle Process (PID 0).
* <span class="abnormal-text">Các dấu hiệu bất thường:</span>
  * Sở hữu PID khác 4.
  * Có nhiều instances đang chạy đồng thời.
  * Hoạt động bên ngoài Session 0.
  * Có một tiến trình cha khác với PID 0.

</div>
<div class="column">

![Remote Process Explorer](system.png)

</div>
</div>

---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 10px;
  border-bottom: none;
}

/* Standard body styling */
p, li {
  font-size: 24px;
  line-height: 1.5;
}

/* Highlight styling for process hierarchy */
.process-badge {
  color: #323538;
    padding: 2px 6px;
    border-radius: 4px;
    font-weight: bold;
    font-family: monospace;
}

/* Inline code path styling */
code {
  background-color: #e2e8f0;
  color: #c53030; /* Dark red to make paths stand out */
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
  font-family: monospace;
}

/* Make the "Normal Baseline" and "Abnormal" text pop consistently */
.baseline-text {
  color: #2f855a;
  font-weight: bold;
}

.abnormal-text {
  color: #c53030;
  font-weight: bold;
}
</style>

# Core Windows Processes

#### <span class="process-badge">System &gt; smss.exe</span>

- Là user-mode process đầu tiên được khởi chạy bởi kernel, chịu trách nhiệm chính trong việc tạo các phiên hệ thống và phiên cho người dùng mới.
- Nó sinh ra các bản sao tạm thời của chính nó để khởi chạy các hệ thống con cần thiết (như <code>csrss.exe</code>, <code>wininit.exe</code>, và <code>winlogon.exe</code>), và các bản sao này sẽ tự terminate ngay lập tức sau khi quá trình thiết lập hoàn tất.
- <span class="baseline-text">Normal Baseline:</span> Chạy dưới quyền tài khoản Local System, có tiến trình cha là System, và được thực thi từ <code>%SystemRoot%\System32\smss.exe</code>.
- <span class="abnormal-text">Các dấu hiệu bất thường:</span>
  - Có tiến trình cha khác với System (PID 4).
  - Chạy từ bất kỳ image path nào khác ngoài <code>C:\Windows\System32</code>.
  - Quan sát thấy có nhiều hơn một master instance đang chạy cùng lúc.



---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 10px;
  border-bottom: none;
}

p, li {
  font-size: 24px;
  line-height: 1.5;
}



/* The text sitting next to the badge */
.desc {
  font-size: 26px;
  font-weight: bold;
  color: #4a5568;
  margin-left: 10px;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
}

.baseline-text {
  color: #2f855a;
  font-weight: bold;
}

.abnormal-text {
  color: #c53030;
  font-weight: bold;
}
</style>

# Core Windows Processes

<div style="margin-bottom: 15px;">
  <span class="badge">csrss.exe</span><span class="desc">(Client Server Runtime Process)</span>
</div>

- Là process chạy ở user mode của Windows subsystem, chịu trách nhiệm quản lý Win32 console window, tạo process/thread và xử lý quá trình tắt hệ thống.
- <span class="baseline-text">Normal Baseline:</span> Chạy dưới quyền tài khoản Local System từ `C:\Windows\System32\csrss.exe`, với hai hoặc nhiều phiên bản (instances) thường chạy cùng lúc.
- Được khởi chạy bởi `smss.exe` (tiến trình này tự chấm dứt ngay lập tức), điều này có nghĩa là một tiến trình `csrss.exe` hợp lệ sẽ luôn hiển thị **tiến trình cha không tồn tại**.
- <span class="abnormal-text">Các dấu hiệu bất thường (Red Flags):</span>
  - Hiển thị một tiến trình cha đang hoạt động.
  - Thực thi từ bất kỳ đường dẫn nào khác ngoài `C:\Windows\System32`.
  - Chạy dưới bất kỳ tài khoản người dùng nào khác ngoài SYSTEM.


---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 5px;
  border-bottom: none;
}

p, li {
  font-size: 21px;
  line-height: 1.35;
}

/* Clean, badge-less styling for the process title */
.process-title {
  font-size: 26px;
  font-weight: bold;
  color: #2d3748; /* Dark slate */
  margin-bottom: 10px;
  display: block;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 1px 5px;
  border-radius: 4px;
  font-size: 19px;
}

.baseline-text {
  color: #2f855a;
  font-weight: bold;
}

.abnormal-text {
  color: #c53030;
  font-weight: bold;
}
</style>

# Core Windows Processes

<span class="process-title">wininit.exe (Windows Initialization Process)</span>

- Chịu trách nhiệm khởi chạy các tiến trình nền quan trọng bên trong Session 0, cụ thể là `services.exe` (Service Control Manager), `lsass.exe` (Local Security Authority), và `lsaiso.exe` (nếu tính năng Credential Guard được bật).
- <span class="baseline-text">Normal Baseline:</span> Hoạt động dưới quyền tài khoản Local System từ `C:\Windows\System32\wininit.exe`. Sẽ chỉ có duy nhất một instance hoạt động tại mọi thời điểm.
- Tương tự như `csrss.exe`, nó được tạo ra bởi instance `smss.exe` tạm thời, điều này có nghĩa là một tiến trình `wininit.exe` hợp lệ sẽ luôn hiển thị một tiến trình cha không tồn tại (non-existent parent process).
- <span class="abnormal-text">Các dấu hiệu bất thường:</span>
  - Hiển thị một tiến trình cha đang hoạt động.
  - Có nhiều hơn một instance chạy cùng lúc.
  - Thực thi từ bất kỳ đường dẫn nào khác ngoài `C:\Windows\System32` hoặc tên tệp sai chính tả.
  - Không chạy dưới quyền tài khoản SYSTEM.


---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 5px;
  border-bottom: none;
}

p, li {
  font-size: 20px;
  line-height: 1.35;
}

/* Stripped h2 styling: no background, no borders, just clean text */
h2 {
  color: #2d3748;
  font-weight: bold;
  font-family: monospace;
  font-size: 26px;
  margin-bottom: 10px;
  display: block;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
}

.baseline-text {
  color: #2f855a;
  font-weight: bold;
}

.abnormal-text {
  color: #c53030;
  font-weight: bold;
}
</style>

# Core Windows Processes

<h2>wininit.exe > services.exe (Service Control Manager)</h2>

- Chịu trách nhiệm load, tương tác, khởi động và kết thúc các dịch vụ hệ thống và auto-start device drivers. Nó duy trì một cơ sở dữ liệu có thể được truy vấn bằng lệnh `sc.exe`.
- Sau khi người dùng đăng nhập thành công, nó sẽ cập nhật cấu hình **Last known good control set** trong registry, cho phép hệ điều hành khôi phục nếu các driver hoặc dịch vụ mới gây ra lỗi khởi động nghiêm trọng.
- <span class="baseline-text">Normal Baseline:</span> Chạy dưới quyền tài khoản Local System từ `C:\Windows\System32\services.exe`. Sẽ chỉ có chính xác một instance đang chạy trên hệ thống.
- Tiến trình cha hợp lệ của nó luôn là `wininit.exe`. Nó đóng vai trò là tiến trình cha cho các tiến trình quan trọng khác như `svchost.exe`, `spoolsv.exe`, `msmpeng.exe`, và `dllhost.exe`.
- <span class="abnormal-text">Các dấu hiệu bất thường:</span>
  - Có tiến trình cha khác với `wininit.exe`.
  - Có nhiều hơn một instance đang chạy.
  - Thực thi từ một đường dẫn khác ngoài `C:\Windows\System32` hoặc không chạy dưới quyền tài khoản SYSTEM.

---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 5px;
  border-bottom: none;
}

/* Center the image and constrain its height */
.center-image {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.center-image img {
  max-height: 450px; /* Keeps it large but fits the slide */
  width: auto;
  border-radius: 6px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  border: 1px solid #4a5568;
}

/* Caption styling at the bottom */
.caption {
  text-align: center;
  font-size: 22px;
  color: #4a5568;
  margin-top: 20px;
  font-style: italic;
}
</style>

# Core Windows Processes

<div class="center-image">
  <img src="service.png" alt="sc.exe command interface">
</div>

<div class="caption">
  Giao diện dòng lệnh sc.exe (Service Controller) dùng để tương tác và truy vấn cơ sở dữ liệu của services.exe
</div>


---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 5px;
  border-bottom: none;
}

p, li {
  font-size: 18px;
  line-height: 1.35;
}

.two-column {
  display: grid;
  grid-template-columns: 55% 45%;
  gap: 15px;
  align-items: center;
  margin-top: 10px;
}

.two-column img {
  max-width: 100%;
  max-height: 400px;
  height: auto;
  border-radius: 6px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
  border: 1px solid #4a5568;
}

h2 {
  color: #2d3748;
  font-weight: bold;
  font-family: monospace;
  font-size: 30px;
  margin-bottom: 5px;
  display: block;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 1px 4px;
  border-radius: 4px;
  font-size: 18px;
  font-family: monospace;
}

.baseline-text {
  color: #2f855a;
  font-weight: bold;
}

.abnormal-text {
  color: #c53030;
  font-weight: bold;
}
</style>

# Core Windows Processes

<h2>wininit.exe &gt; services.exe &gt; svchost.exe (Service Host)</h2>

<div class="two-column">
<div class="column">

- Chịu trách nhiệm host và quản lý các dịch vụ Windows được triển khai dưới dạng DLL.
- Vì có quá nhiều dịch vụ, Windows gộp các dịch vụ tương tự lại với nhau để dùng chung một tiến trình `svchost.exe` duy nhất nhằm giảm thiểu việc tiêu thụ tài nguyên bằng cách sử dụng tham số `-k`.
- <span class="baseline-text">Normal Baseline:</span> Thực thi từ `C:\Windows\System32\svchost.exe` với tiến trình cha luôn là `services.exe`. Việc thấy nhiều instance đang chạy đồng thời dưới các tài khoản người dùng khác nhau là điều bình thường.
- <span class="abnormal-text">Các dấu hiệu bất thường:</span>
  - Hoàn toàn không có tham số `-k` trong command.
  - Có bất kỳ tiến trình cha nào khác `services.exe`.
  - Thực thi từ một đường dẫn khác ngoài `C:\Windows\System32` hoặc sử dụng các lỗi sai chính tả để ẩn mình một cách tinh vi.

</div>
<div class="column">

![svchost command line -k parameter](k_flag.png)

</div>
</div>

---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 10px;
  border-bottom: none;
}

p, li {
  font-size: 21px;
  line-height: 1.5;
}

h2 {
  color: #2d3748;
  font-weight: bold;
  font-family: monospace;
  font-size: 30px;
  margin-bottom: 10px;
  display: block;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
  font-family: monospace;
}

/* Specifically highlight high-value targets like Mimikatz */
.threat-tool {
  background-color: #fbd38d; /* Soft orange/warning background */
  color: #9c4221;
  padding: 2px 6px;
  border-radius: 4px;
  font-weight: bold;
}

.baseline-text {
  color: #2f855a;
  font-weight: bold;
}

.abnormal-text {
  color: #c53030;
  font-weight: bold;
}
</style>

# Core Windows Processes

<h2>wininit.exe &gt; lsass.exe (Local Security Authority)</h2>

- Thực thi các system security policies, xử lý quá trình xác thực người dùng, tạo access tokens (SAM, AD, NETLOGON), và ghi dữ liệu vào Windows security log.
- Là mục tiêu hàng đầu của attackers tìm cách trích xuất credentials trực tiếp từ bộ nhớ (ví dụ: sử dụng <span class="threat-tool">Mimikatz</span>) hoặc sử dụng các tên gần giống để che giấu các tiến trình độc hại một cách tinh vi.
- <span class="baseline-text">Normal Baseline:</span> Hoạt động dưới quyền tài khoản Local System từ `C:\Windows\System32\lsass.exe`. Sẽ chỉ có chính xác một instance đang chạy trên hệ thống và tiến trình cha của nó luôn là `wininit.exe`.
- <span class="abnormal-text">Các dấu hiệu bất thường:</span>
  - Hiển thị bất kỳ tiến trình cha nào khác ngoài `wininit.exe` hoặc có nhiều instance chạy đồng thời.
  - Thực thi từ một đường dẫn khác ngoài `C:\Windows\System32`, sử dụng các lỗi sai chính tả nhỏ hoặc chạy dưới một tài khoản khác ngoài SYSTEM.


---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 10px;
  border-bottom: none;
}

p, li {
  font-size: 20px;
  line-height: 1.5;
}

h2 {
  color: #2d3748;
  font-weight: bold;
  font-family: monospace;
  font-size: 30px;
  margin-bottom: 10px;
  display: block;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
  font-family: monospace;
}

/* Special highlight for Registry Keys */
.registry-key {
  background-color: #e6fffa; /* Soft mint/cyan background */
  color: #234e52; /* Deep teal text */
  padding: 2px 6px;
  border-radius: 4px;
  font-weight: bold;
  font-family: monospace;
}

.baseline-text {
  color: #2f855a;
  font-weight: bold;
}

.abnormal-text {
  color: #c53030;
  font-weight: bold;
}
</style>

# Core Windows Processes

<h2>winlogon.exe (Windows Logon)</h2>

- Quản lý quá trình đăng nhập của người dùng, xử lý Secure Attention Sequence (SAS) (Ctrl+Alt+Delete) để thu thập credentials một cách an toàn.
- Load profile `NTUSER.DAT` của người dùng vào registry (<span class="registry-key">HKCU</span>), sau đó `userinit.exe` sẽ khởi chạy shell của người dùng (`explorer.exe`). Nó cũng quản lý việc khóa màn hình và chạy trình bảo vệ màn hình.
- <span class="baseline-text">Normal Baseline:</span> Chạy dưới quyền tài khoản Local System từ `C:\Windows\System32\winlogon.exe`.
- Được tạo ra bởi một instance `smss.exe` tạm thời, vì vậy một phiên bản hợp lệ sẽ luôn hiển thị một tiến trình cha không tồn tại (non-existent parent process). Bạn sẽ thấy một phiên bản tương ứng cho mỗi phiên người dùng.
- <span class="abnormal-text">Các dấu hiệu bất thường:</span>
  - Hiển thị một tiến trình cha đang hoạt động.
  - Thực thi từ bên ngoài `C:\Windows\System32` hoặc không chạy dưới quyền tài khoản SYSTEM.
  - Giá trị <span class="registry-key">"Shell"</span> trong registry trỏ đến bất kỳ tệp nào khác ngoài `explorer.exe`.


---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 10px;
  border-bottom: none;
}

p, li {
  font-size: 22px;
  line-height: 1.5;
}

h2 {
  color: #2d3748;
  font-weight: bold;
  font-family: monospace;
  font-size: 30px;
  margin-bottom: 10px;
  display: block;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
  font-family: monospace;
}

/* Highlight for Network/Outbound anomalies */
.network-alert {
  background-color: #feebc8; /* Soft yellow/orange */
  color: #c05621; /* Dark orange */
  padding: 2px 6px;
  border-radius: 4px;
  font-weight: bold;
}

.baseline-text {
  color: #2f855a;
  font-weight: bold;
}

.abnormal-text {
  color: #c53030;
  font-weight: bold;
}
</style>

# Core Windows Processes

<h2>explorer.exe (Windows Explorer)</h2>

- Là shell chính của người dùng, cung cấp giao diện đồ họa để truy cập các tệp, thư mục, Start menu và Taskbar.
- <span class="baseline-text">Normal Baseline:</span> Thực thi từ `C:\Windows\explorer.exe`. Bạn thường sẽ thấy một hoặc nhiều instances cho mỗi người dùng đăng nhập tương tác, chạy với quyền tài khoản của người dùng đó.
- Là tiến trình cha cho nhiều ứng dụng được người dùng khởi chạy, nhưng tiến trình cha của chính nó (`userinit.exe`) sẽ thoát ngay lập tức sau khi sinh ra nó. Do đó, một tiến trình `explorer.exe` hợp lệ sẽ luôn hiển thị một tiến trình cha không tồn tại.
- <span class="abnormal-text">Các dấu hiệu bất thường:</span>
  - Hiển thị một tiến trình cha đang hoạt động.
  - Thực thi từ bất kỳ đường dẫn nào khác ngoài `C:\Windows` (lưu ý rằng nó **không** nằm trong thư mục `System32`).
  - Khởi tạo các kết nối mạng <span class="network-alert">TCP/IP outbound</span> bất thường.


---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 5px;
  border-bottom: none;
}

p, li {
  font-size: 17px;
  line-height: 1.3;
  margin-bottom: 2px;
}

/* Subheader styling for the category */
h2 {
  color: #2d3748;
  font-weight: bold;
  font-size: 30px;
  margin-bottom: 5px;
  display: block;
}

/* Styling for the tool names to make them pop */
.tool-name {
  background-color: #2b6cb0; /* Professional blue */
  color: #ffffff;
  padding: 2px 6px;
  border-radius: 4px;
  font-weight: bold;
  font-family: monospace;
  font-size: 19px;
  display: inline-block;

}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 1px 3px;
  border-radius: 4px;
  font-size: 17px;
  font-family: monospace;
}

/* Highlight specifically for VirusTotal */
.vt-badge {
  background-color: #e2e8f0;
  color: #1a202c;
  border: 1px solid #718096;
  padding: 1px 4px;
  border-radius: 3px;
  font-weight: bold;
  font-size: 17px;
}
</style>

# Sysinternals

<h2>File and Disk Utilities</h2>

<span class="tool-name">Sigcheck</span>
- Một tiện ích dòng lệnh được sử dụng để xác minh metadata của tệp, trạng thái bảo mật và chuỗi chứng chỉ số.
- Tích hợp trực tiếp với <span class="vt-badge">VirusTotal</span> và mang lại hiệu quả cao trong việc săn tìm các unsigned executables trong các thư mục cốt lõi (sử dụng cờ `-u` và `-e`).

<span class="tool-name">Streams</span>
- Một công cụ được thiết kế để xem các Alternate Data Streams (ADS) ẩn được đính kèm vào các tệp.
- Phát hiện phần mềm độc hại đang che giấu payload bên ngoài luồng `$DATA` mặc định, hoặc để kiểm tra xem tệp có nguồn gốc từ Internet hay không (`Web - Zone.Identifier`).

<span class="tool-name">SDelete</span>
- Một tiện ích dọn dẹp vĩnh viễn các tệp, thư mục, hoặc vùng không gian đĩa chưa được cấp phát bằng cách sử dụng giao thức xóa sạch 3 bước.
- Thường xuyên được attackers sử dụng để xóa dữ liệu và xóa dấu vết.


---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 5px;
  border-bottom: none;
  margin-bottom: 5px;
}

p, li {
  font-size: 20px;
  line-height: 1.4;
}

h2 {
  color: #2d3748;
  font-weight: bold;
  font-size: 30px;
  margin-bottom: 5px;
  display: block;

}

.tool-name {
  background-color: #2b6cb0;
  color: #ffffff;
  padding: 2px 8px;
  border-radius: 4px;
  font-weight: bold;
  font-family: monospace;
  font-size: 22px;
  display: inline-block;
  margin-top: 5px;
  margin-bottom: 10px;
}

/* Layout for the text and image */
.two-column {
  display: grid;
  grid-template-columns: 50% 50%; /* Equal split for the text and the wide image */
  gap: 15px;
  align-items: center;
  margin-top: 5px;
}

.two-column img {
  max-width: 100%;
  max-height: 400px; /* Constrains the image so it fits neatly */
  height: auto;
  border-radius: 6px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
  border: 1px solid #4a5568;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 1px 4px;
  border-radius: 4px;
  font-size: 19px;
  font-family: monospace;
}
</style>

# Sysinternals

<h2>Networking Utilities: TCPView</h2>

<div class="two-column">
<div class="column">


- Phiên bản nâng cấp có GUI của `netstat`, có chức năng liệt kê tất cả các TCP và UDP network endpoints đang hoạt động.
- Map network traffic với quá trình thực thi cục bộ bằng cách map trực tiếp các local/remote addresses, cổng và trạng thái kết nối (connection states) với PID sở hữu chúng.
- Cung cấp tính năng Lọc trạng thái (ví dụ: chỉ cô lập các kết nối đã thiết lập - "Established") đối với lưu lượng TCP.
- Thêm `Tcpvcon` là phiên bản CLI của TCPView.

</div>
<div class="column">

![TCPView Interface](tcpview.png)

</div>
</div>



---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 0px;
  border-bottom: none;
  margin-bottom: 5px;
}

p, li {
  font-size: 21px; /* Scaled slightly to fit 5 dense bullet points */
  line-height: 1.4;
  margin-bottom: 3px;
}

h2 {
  color: #2d3748;
  font-weight: bold;
  font-size: 30px;
  margin-bottom: 5px;
  display: block;
}

.tool-name {
  font-weight: bold;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 1px 3px;
  border-radius: 4px;
  font-size: 19px;
  font-family: monospace;
}

/* Subtle highlight for critical security terms */
.alert-text {
  color: #c53030;
  font-weight: bold;
}
</style>

# Sysinternals

<h2>Process Utilities</h2>

- <span class="tool-name">Process Explorer:</span> Theo dõi process, có thể xem các handle đang mở (tệp, khóa registry) và các DLL được tải cho mỗi process, đi kèm với tính năng xác minh chữ ký và phân loại trạng thái bằng màu sắc.
- <span class="tool-name">Process Monitor (ProcMon):</span> Ghi lại hoạt động file system, registry và process/thread trong thời gian thực; có thể dùng bộ lọc để xử lý khối lượng sự kiện khổng lồ.
- <span class="tool-name">Autoruns:</span> Kiểm tra các app khởi động cùng hệ thống, các khóa `Run/RunOnce`, các scheduled tasks và `IFEO` để phát hiện <span class="alert-text">persistence</span>.
- <span class="tool-name">ProcDump:</span> Dump bộ nhớ của các process dựa trên mức sử dụng CPU tăng vọt, các ngoại lệ hoặc manual flags, ghi lại toàn bộ user-mode memory space của các tiến trình như `lsass.exe`.
- <span class="tool-name">PsExec:</span> Thực thi các lệnh console tương tác giữa các máy tính thông qua SMB/named pipes, thường xuyên bị lạm dụng cho <span class="alert-text">lateral movement</span>.


---
<!-- class: default -->

<style scoped>
  h1 {
    text-align: center;
    margin-top: 0px;
    padding-bottom: 5px; 
    border-bottom: none;
    margin-bottom: 5px;
  }
  
  p, li {
    font-size: 24px; 
    line-height: 1.5;
  }

  h2 {
    color: #2d3748;
    font-weight: bold;
    font-size: 30px;
    margin-bottom: 15px;
    display: block;
  }
  
  .tool-name {
    background-color: #2b6cb0;
    color: #ffffff;
    padding: 3px 10px;
    border-radius: 4px;
    font-weight: bold;
    font-family: monospace;
    font-size: 24px;
    display: inline-block;
  }

  .highlight-term {
    color: #2b6cb0;
    font-weight: bold;
  }
</style>

# Sysinternals

<h2>Security Utilities - Sysmon (System Monitor)</h2>


* Hoạt động như một system service và device driver, chạy liên tục ngay cả khi khởi động lại để liên tục ghi lại hoạt động vào Windows event log.
* Cung cấp khả năng giám sát, xác định <span class="highlight-term">malicious anomalies</span> bằng cách theo dõi high-fidelity indicators như việc tạo tiến trình, kết nối mạng, và sửa mốc thời gian tạo tệp (file creation time).
* Được thiết kế để defenders có thể tổng hợp dữ liệu từ xa thông qua tính năng Windows Event Collection hoặc các SIEM agents.

---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 5px;
  border-bottom: none;
  margin-bottom: 5px;
}

p, li {
  font-size: 20px;
  line-height: 1.4;
}

h2 {
  color: #2d3748;
  font-weight: bold;
  font-size: 30px;
  margin-bottom: 5px;
  display: block;
}


/* Two-column layout */
.two-column {
  display: grid;
  grid-template-columns: 50% 50%;
  gap: 15px;
  align-items: center;
  margin-top: 5px;
}

.two-column img {
  max-width: 100%;
  max-height: 380px; /* Constrains the screenshot height */
  height: auto;
  border-radius: 6px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
  border: 1px solid #4a5568;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 1px 4px;
  border-radius: 4px;
  font-size: 19px;
  font-family: monospace;
}
</style>

# Sysinternals

<h2>System Information - WinObj</h2>

<div class="two-column">
<div class="column">

- Sử dụng API Windows NT gốc (thông qua `NTDLL.DLL`) để trực quan hóa và tương tác với namespace nội bộ của NT Object Manager.
- Rất hiệu quả trong việc kiểm tra các ranh giới hệ thống, chẳng hạn như session 0 và session 1 (Hệ thống vs người dùng).
- Dùng để xác minh core process isolation.

</div>
<div class="column">

![WinObj Interface](winobj.png)

</div>
</div>

---
<!-- class: default -->

<style scoped>
  h1 {
    text-align: center;
    margin-top: 0px;
    padding-bottom: 5px; 
    border-bottom: none;
    margin-bottom: 5px;
  }
  
  p, li {
    font-size: 24px; 
    line-height: 1.5;
  }

  h2 {
    color: #2d3748;
    font-weight: bold;
    font-size: 30px;
    margin-bottom: 15px;
    display: block;
  }
  
  .tool-name {
    font-weight: bold;
  }
</style>

# Sysinternals

<h2>Miscellaneous Utilities</h2>

<span class="tool-name">Strings</span>
* Một command-line tool quét các binary executables hoặc memory dumps để trích xuất văn bản ANSI và UNICODE.

<span class="tool-name">BgInfo</span>
* Tự động tạo và hiển thị các thông số hệ thống quan trọng trực tiếp trên nền desktop.

<span class="tool-name">RegJump</span>
* Dùng để mở chính xác một registry key ngay lập tức bằng cách cung cấp đường dẫn chi tiết cho registry đó.


---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 10px;
  border-bottom: none;
}

p, li {
  font-size: 24px;
  line-height: 1.5;
  margin-bottom: 10px;
}

/* Styling for the main conceptual question */
.concept-title {
  font-size: 30px;
  font-weight: bold;
  color: #1a202c; /* Deep black/slate */
  margin-bottom: 15px;
  display: block;

}

/* Highlight important technical terms */
.highlight-blue {
  color: #3182ce;
  font-weight: bold;
}

.highlight-red {
  color: #e53e3e;
  font-weight: bold;
}

code {
  background-color: #edf2f7;
  color: #2d3748;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
  font-family: monospace;
  font-weight: bold;
}
</style>

# Windows Event Logs

<span class="concept-title">What are Windows Event Logs?</span>

- Một bản ghi tập trung, theo trình tự thời gian về các hoạt động của hệ thống, bảo mật và ứng dụng do hệ điều hành Windows tạo ra, được lưu trữ dưới định dạng `*.evtx`, dựa trên XML.
- Nền tảng của hoạt động audit trên Windows xoay quanh ba tệp logs chính: <span class="highlight-blue">System</span>, <span class="highlight-blue">Application</span>, và <span class="highlight-blue">Security</span>.
- Mỗi log entry chứa metadata quan trọng. Các trường quan trọng nhất là <span class="highlight-red">Event ID</span>, Source, Timestamp, và Event Data/XML payload.
- Chúng là các bằng chứng được sử dụng để dựng execution timelines, theo dõi các dấu vết/chuyển động đáng ngờ, và thiết lập baseline để kích hoạt các cảnh báo SIEM tự động.


---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 5px;
  border-bottom: none;
  margin-bottom: 10px;
}

p, li {
  font-size: 24px;
  line-height: 1.5;
}

.tool-title {
  font-size: 30px;
  font-weight: bold;
  color: #2d3748;
  margin-bottom: 5px;
  display: inline-block;
}

/* Highlight styling for the Run command */
.run-cmd {
  background-color: #2b6cb0;
  color: #ffffff;
  padding: 3px 10px;
  border-radius: 6px;
  font-weight: bold;
  font-family: monospace;
  font-size: 24px;
  margin-left: 10px;
  vertical-align: text-bottom;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
  font-family: monospace;
}

/* Warning text styling for the limitations */
.warning-text {
  color: #c53030;
  font-style: italic;
  font-weight: bold;
}
</style>

# Windows Event Logs

<div style="margin-bottom: 15px; text-align: center;">
  <span class="tool-title">Event Viewer - eventvwr.msc</span>
</div>

- Một tool Microsoft Management Console (MMC) được tích hợp sẵn, sử dụng để đọc, tìm kiếm và quản lý các tệp nhật ký `.evtx` trên các endpoints cục bộ và từ xa.
- Loại bỏ các thông tin nhiễu bằng cách xây dựng các bộ lọc dựa trên XML (`XPath`) để lọc theo các Event ID, người dùng hoặc khung thời gian cụ thể.
- <span class="warning-text">Lưu ý:</span> Hiệu quả khi phân tích log file nhỏ trong 1 máy trạm, nhưng chậm và dễ bị treo khi phân tích log lớn ➔ Nên sử dụng các giải pháp thay thế bằng command-line hoặc tích hợp SIEM.

---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 10px;
  border-bottom: none;
  margin-bottom: 5px;
}

p, li {
  font-size: 24px;
  line-height: 1.5;
}

.tool-title {
  font-size: 30px;
  font-weight: bold;
  color: #2d3748;
  margin-bottom: 5px;
  display: inline-block;
}

.cmd-badge {
  background-color: #2b6cb0;
  color: #ffffff;
  padding: 3px 10px;
  border-radius: 6px;
  font-weight: bold;
  font-family: monospace;
  font-size: 24px;
  margin-left: 10px;
  vertical-align: text-bottom;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
  font-family: monospace;
}

/* Deep red styling for malicious commands / alerts */
.malicious-cmd {
  background-color: #fed7d7; /* Light red background */
  color: #9b2c2c; /* Dark red text */
  padding: 2px 6px;
  border-radius: 4px;
  font-family: monospace;
  font-weight: bold;
}

/* Specific styling for Event IDs so they stand out */
.event-id {
  color: #c53030;
  font-weight: bold;
  border-bottom: 2px solid #c53030;
}
</style>

# Windows Event Logs

<div style="margin-bottom: 15px; text-align: center;">
  <span class="tool-title">Windows Event Utility - wevtutil.exe</span>
</div>

- Native command-line administrative tool được sử dụng để truy xuất log metadata, truy vấn các sự kiện, xuất log, và cài đặt hoặc gỡ cài đặt các event manifests.
- Thường xuyên bị lợi dụng bởi attackers để clear log: <span class="malicious-cmd">wevtutil cl Security</span>
- Cần giám sát <span class="event-id">Event ID 4688</span> hoặc <span class="event-id">Sysmon ID 1</span> cho text `"cl"`. Event có từ này thường sẽ đi kèm với <span class="event-id">Event ID 1102</span> (The audit log was cleared).

---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 10px;
  border-bottom: none;
  margin-bottom: 5px;
}

p, li {
  font-size: 24px;
  line-height: 1.5;
}

.tool-title {
  font-size: 30px;
  font-weight: bold;
  color: #2d3748;
  margin-bottom: 5px;
  display: inline-block;
}

/* Deep blue for the PowerShell cmdlet badge */
.ps-badge {
  background-color: #1A365D; /* Darker, "PowerShell" blue */
  color: #ffffff;
  padding: 3px 10px;
  border-radius: 6px;
  font-weight: bold;
  font-family: monospace;
  font-size: 24px;
  margin-left: 10px;
  vertical-align: text-bottom;
}

code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
  font-family: monospace;
}

/* Specific styling for PowerShell Parameters */
.ps-param {
  background-color: #EBF8FF; /* Very light cyan */
  color: #2C7A7B; /* Deep teal */
  padding: 2px 6px;
  border-radius: 4px;
  font-weight: bold;
  font-family: monospace;
  font-size: 22px;
}
</style>

# Windows Event Logs

<div style="margin-bottom: 15px; text-align: center;">
  <span class="tool-title">PowerShell's Get-WinEvent</span>
</div>

- Một cmdlet PowerShell được sử dụng để truy vấn cả classic event logs và ETW, vượt trội hoàn toàn so với lệnh `Get-EventLog` cũ.
- Sức mạnh thực sự của nó nằm ở việc parse các tập dữ liệu khổng lồ trước khi chuyển objects vào pipeline, sử dụng các tham số như <span class="ps-param">-FilterHashtable</span> và <span class="ps-param">-FilterXPath</span> để thực hiện các query cực nhanh.
- Có thể sử dụng để viết scripts cho incident response, tìm kiếm nhanh chóng event mong muốn không cần qua GUI.

---
<!-- class: default -->

<style scoped>
  h1 {
    text-align: center;
    margin-top: 0px;
    padding-bottom: 10px;
    border-bottom: none;
  }
  
  p, li {
    font-size: 24px; 
    line-height: 1.5;
    margin-bottom: 12px;
  }

  .concept-title {
    font-size: 30px;
    font-weight: bold;
    color: #1a202c; 
    margin-bottom: 20px;
    display: block;
  }

  /* Inline code for files and commands */
  code {
    background-color: #edf2f7;
    color: #c53030;
    padding: 2px 6px;
    border-radius: 4px;
    font-size: 22px;
    font-family: monospace;
  }

  /* Specific styling for XML Nodes/Fields */
  .xml-node {
    background-color: #FAF5FF; /* Very light purple */
    color: #553C9A; /* Deep purple */
    padding: 2px 6px;
    border-radius: 4px;
    font-weight: bold;
    font-family: monospace;
    font-size: 22px;
  }
</style>

# Windows Event Logs

<span class="concept-title">XPath Queries</span>

* Được sử dụng để điều hướng, truy vấn và trích xuất các node dữ liệu cụ thể trực tiếp từ cấu trúc XML của các tệp nhật ký Windows `.evtx`.
* Lọc dữ liệu <span class="xml-node">EventData</span>, ví dụ như là một <span class="xml-node">TargetUserName</span> hoặc <span class="xml-node">IpAddress</span> cụ thể.
* Là underlying engine cho Event Viewer GUI filter, và có thể sử dụng qua cả lệnh `wevtutil` và `Get-WinEvent`.

---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 10px;
  border-bottom: none;
  margin-bottom: 15px;
}

.concept-title {
  font-size: 30px;
  font-weight: bold;
  color: #1a202c;
  margin-bottom: 30px;
  display: block;
}

/* Table Container to center it on the slide */
.table-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

/* Custom styling for the Markdown table */
table {
  border-collapse: collapse;
  width: 85%; /* Keeps the table from stretching too wide */
  font-size: 22px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

th {
  background-color: #2b6cb0;
  color: white;
  text-align: left;
  padding: 12px 20px;
  border: none;
}

td {
  padding: 12px 20px;
  border-bottom: 1px solid #e2e8f0;
  color: #2d3748;
}

/* Alternating row colors for readability */
tr:nth-child(even) {
  background-color: #f7fafc;
}

/* Specific styling to make the IDs pop */
.event-id {
  color: #c53030;
  font-weight: bold;
  font-family: monospace;
  font-size: 24px;
}
</style>

# Windows Event Logs

<span class="concept-title">Critical Security Event IDs</span>

<div class="table-container">

| Event ID | Mô tả sự kiện (Description) |
|:---|:---|
| <span class="event-id">4624</span> & <span class="event-id">4625</span> | Successful and failed authentication |
| <span class="event-id">4688</span> | Process creation |
| <span class="event-id">7045</span> | A new service was installed |
| <span class="event-id">1102</span> | Audit Log Cleared |
| <span class="event-id">4104</span> | PowerShell Script Block Logging |

</div>

---
<!-- class: default -->

<style scoped>
h1 {
  text-align: center;
  margin-top: 0px;
  padding-bottom: 5px;
  border-bottom: none;
  margin-bottom: 15px;
}

/* Main category sub-header styling */
.concept-title {
  font-size: 30px;
  font-weight: bold;
  color: #1a202c;
  margin-bottom: 20px;
  display: block;
}

p, li {
  font-size: 24px;
  line-height: 1.5;
  margin-bottom: 12px;
}

/* Inline code highlighting for specific technical terms/paths */
code {
  background-color: #edf2f7;
  color: #c53030;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 22px;
  font-family: monospace;
}

/* Specific highlight for renowned security configs */
.config-badge {
  background-color: #EBF8FF; /* Light cyan */
  color: #2C7A7B; /* Dark teal */
  padding: 2px 6px;
  border-radius: 4px;
  font-weight: bold;
  font-family: monospace;
  font-size: 22px;
}

/* Highlight the log path to make it stand out */

</style>

# Sysmon

<span class="concept-title">Sysmon (System Monitor) Overview</span>

- A background system service and device driver thuộc bộ công cụ Sysinternals giúp nâng cấp đáng kể logging capabilities của Windows.
- Bổ sung context cho event logs mà bình thường Windows event logs bỏ sót, vd: `file hashes`, `command-lines`, `unique GUID` của các tiến trình cha-con.
- Dựa vào các tệp cấu hình XML có thể tùy chỉnh (như các cấu hình chuẩn trong ngành của <span class="config-badge">SwiftOnSecurity</span> hoặc <span class="config-badge">SysmonModular</span> của Olaf Hartong) để lọc bỏ các thông tin nhiễu.
- Ghi dữ liệu trực tiếp vào một kênh của riêng nó (<span class="log-path">Applications and Services Logs > Microsoft > Windows > Sysmon > Operational</span>), cho phép nó tích hợp liền mạch với SIEM như Winlogbeat hoặc Wazuh.