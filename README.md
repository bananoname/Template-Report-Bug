# Command Injection on /ping?ip=

## Summary
- **Target**: `http://vulnsite.com/ping`
- **Lỗ hổng**: Command Injection thông qua tham số `ip`
- **Tác động**: Cho phép attacker thực thi lệnh hệ thống từ xa

## Steps to Reproduce
1. Truy cập: `http://vulnsite.com/ping?ip=127.0.0.1;id`
2. Quan sát output trả về bao gồm kết quả của lệnh `id`
3. Thử thêm `whoami`, `uname -a` để xác thực RCE

## Impact
Attacker có thể thực thi lệnh tùy ý, có thể dẫn đến chiếm toàn quyền điều khiển hệ thống.

## Supporting Material / References
- CWE-77: Improper Neutralization of Special Elements used in a Command
- Request:
```http
GET /ping?ip=127.0.0.1;id HTTP/1.1
Host: vulnsite.com
```
- Screenshot:
  ![screenshot](images/command-injection.png)

## Remediation
- Không sử dụng shell command trực tiếp với input của người dùng
- Sử dụng hàm gọi hệ thống an toàn (vd: `subprocess.run` với `shell=False`)
- Validate input chỉ cho phép IP hợp lệ (regex IP)

---

**Author**: user_ctf  
**Date**: 16/04/2025
