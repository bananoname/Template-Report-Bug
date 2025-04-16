# 🧠 Tập viết Bug Bounty Report theo format chuyên nghiệp

---

## 🔍 Mục tiêu của giai đoạn này

- Biết cách viết một report bảo mật ngắn gọn, rõ ràng, chuyên nghiệp.
- Áp dụng được cho các nền tảng bug bounty như HackerOne, Bugcrowd.
- Làm quen với markdown + xuất PDF đẹp.
- Sẵn sàng để trình bày report cho công ty, cộng đồng.

---

## 📂 Bước 1 – Chuẩn bị template viết báo cáo

Bạn sẽ dùng **Markdown** vì:
- Dễ viết.
- Dễ quản lý bằng Git.
- Xuất HTML/PDF bằng công cụ như `pandoc`.

### ✅ Template chuẩn Bug Bounty Report

```markdown
# [Tên lỗ hổng] on [Target]

## Summary
- Mục tiêu: [target URL / ứng dụng]
- Lỗ hổng: [type of bug, eg. SQL Injection, XSS, Command Injection]
- Tác động: [chiếm quyền truy cập, leak dữ liệu,...]

## Steps to Reproduce
1. Truy cập [đường dẫn cụ thể]
2. Gửi payload: `[payload cụ thể]`
3. Quan sát phản hồi: [mô tả hoặc screenshot]

## Impact
[Mô tả rõ ràng hậu quả nếu khai thác được – nguy cơ thực tế]

## Supporting Material / References
- Screenshot minh họa
- CVE/CWE (nếu có)
- Request/Response dạng code block

## Remediation
[Đề xuất cách khắc phục cụ thể]

---

**Author**: [Tên bạn]  
**Date**: [Ngày báo cáo]
```

---

## 🧪 Bước 2 – Thực hành viết báo cáo thực tế

Bạn chọn một lỗi bạn từng khai thác được (ví dụ như Command Injection, SQLi, LFI, IDOR...), và điền nội dung vào template theo các mục như trên.

### Ví dụ: Command Injection trên trang ping

```markdown
# Command Injection on /ping?ip=

## Summary
- Target: `http://vulnsite.com/ping`
- Lỗ hổng: Command Injection thông qua tham số `ip`
- Tác động: Cho phép attacker thực thi lệnh hệ thống từ xa

## Steps to Reproduce
1. Truy cập: `http://vulnsite.com/ping?ip=127.0.0.1;id`
2. Quan sát output trả về bao gồm kết quả của lệnh `id`
3. Thử thêm `whoami`, `uname -a` để xác thực RCE

## Impact
Attacker có thể thực thi lệnh tùy ý, có thể dẫn đến chiếm toàn quyền điều khiển hệ thống.

## Supporting Material / References
- CWE-77: Improper Neutralization of Special Elements used in a Command
- Request:

http
GET /ping?ip=127.0.0.1;id HTTP/1.1
Host: vulnsite.com

- Screenshot:
  ![screenshot](images/command-injection.png)

## Remediation
- Không sử dụng shell command trực tiếp với input của người dùng
- Sử dụng hàm gọi hệ thống an toàn (vd: `subprocess.run` với `shell=False`)
- Validate input chỉ cho phép IP hợp lệ (regex IP)
---
**Author**: user_ctf  
**Date**: 16/04/2025
---
```
### 💡 Bước 3 – Tips luyện tập

- Viết lại những lỗi bạn đã từng khai thác theo đúng format.
- Mỗi lần đọc writeup trên mạng, hãy thử tự viết lại báo cáo riêng.
- So sánh báo cáo của bạn với writeup gốc để học cách diễn đạt hay hơn.
- Đặt mục tiêu mỗi tuần viết ít nhất 1 báo cáo markdown → PDF.
