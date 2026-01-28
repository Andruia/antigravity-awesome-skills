---
name: clean-code
description: Tiêu chuẩn code thực dụng - súc tích, trực tiếp, không kỹ thuật quá mức, không có comments thừa thãi.
allowed-tools: Read, Write, Edit
version: 2.0
priority: CRITICAL
---

# Clean Code - Tiêu chuẩn Coding AI Thực dụng

> **KỸ NĂNG QUAN TRỌNG** - Hãy **súc tích, trực tiếp và tập trung vào giải pháp**.

---

## Các Nguyên tắc Cốt lõi

| Nguyên tắc | Quy tắc |
|-----------|------|
| **SRP** | Trách nhiệm Duy nhất (Single Responsibility) - mỗi hàm/lớp làm MỘT việc |
| **DRY** | Đừng Lặp lại Chính mình (Don't Repeat Yourself) - trích xuất phần trùng lặp, tái sử dụng |
| **KISS** | Giữ nó Đơn giản (Keep It Simple) - giải pháp đơn giản nhất có thể hoạt động |
| **YAGNI** | Bạn Sẽ Không Cần Nó Đâu (You Aren't Gonna Need It) - đừng xây dựng tính năng chưa dùng đến |
| **Hướng đạo sinh** | Để lại code sạch hơn lúc bạn tìm thấy nó |

---

## Quy tắc Đặt tên

| Thành phần | Quy ước |
|---------|------------|
| **Biến** | Bộc lộ ý định: `userCount` không phải `n` |
| **Hàm** | Động từ + danh từ: `getUserById()` không phải `user()` |
| **Booleans** | Dạng câu hỏi: `isActive`, `hasPermission`, `canEdit` |
| **Hằng số** | SCREAMING_SNAKE: `MAX_RETRY_COUNT` |

> **Quy tắc:** Nếu bạn cần comment để giải thích tên, hãy đổi tên nó.

---

## Quy tắc Hàm (Function)

| Quy tắc | Mô tả |
|------|-------------|
| **Nhỏ** | Tối đa 20 dòng, lý tưởng là 5-10 dòng |
| **Một việc** | Làm một việc, làm tốt việc đó |
| **Một cấp độ** | Một cấp độ trừu tượng trên mỗi hàm |
| **Ít tham số** | Tối đa 3 tham số, ưu tiên 0-2 |
| **Không tác dụng phụ** | Không thay đổi đầu vào một cách bất ngờ |

---

## Cấu trúc Code

| Mẫu | Áp dụng |
|---------|-------|
| **Guard Clauses** | Return sớm cho các trường hợp biên |
| **Phẳng > Lồng nhau** | Tránh lồng nhau sâu (tối đa 2 cấp) |
| **Kết hợp (Composition)** | Các hàm nhỏ kết hợp lại với nhau |
| **Đặt cùng nhau (Colocation)** | Giữ code liên quan ở gần nhau |

---

## Phong cách Coding của AI

| Tình huống | Hành động |
|-----------|--------|
| Người dùng yêu cầu tính năng | Viết nó trực tiếp |
| Người dùng báo lỗi | Sửa nó, đừng giải thích lòng vòng |
| Không rõ yêu cầu | Hỏi, đừng giả định |

---

## Anti-Patterns (KHÔNG NÊN)

| ❌ Mẫu | ✅ Cách sửa |
|-----------|-------|
| Comment mỗi dòng | Xóa comment hiển nhiên |
| Helper cho code 1 dòng | Viết thẳng code (Inline) |
| Factory cho 2 objects | Khởi tạo trực tiếp |
| utils.ts với 1 hàm | Đặt code ở nơi sử dụng |
| "Đầu tiên chúng ta import..." | Chỉ viết code thôi |
| Lồng nhau sâu | Dùng Guard clauses |
| Số ma thuật (Magic numbers) | Dùng hằng số có tên |
| Hàm thần thánh (God functions) | Tách nhỏ theo trách nhiệm |

---

## 🔴 Trước khi Sửa BẤT KỲ File nào (HÃY NGHĨ TRƯỚC!)

**Trước khi thay đổi một file, hãy tự hỏi:**

| Câu hỏi | Tại sao |
|----------|-----|
| **Cái gì import file này?** | Chúng có thể bị hỏng |
| **File này import cái gì?** | Thay đổi Interface |
| **Test nào bao phủ file này?** | Test có thể fail |
| **Đây có phải component chia sẻ?** | Nhiều nơi bị ảnh hưởng |

**Kiểm tra Nhanh:**
```
File cần sửa: UserService.ts
└── Ai import nó? → UserController.ts, AuthController.ts
└── Họ có cần thay đổi không? → Kiểm tra chữ ký hàm (function signatures)
```

> 🔴 **Quy tắc:** Sửa file + tất cả các file phụ thuộc trong CÙNG một task.
> 🔴 **Không bao giờ để lại import hỏng hoặc thiếu cập nhật.**

---

## Tóm tắt

| Nên | Không Nên |
|----|-------|
| Viết code trực tiếp | Viết hướng dẫn (tutorials) |
| Để code tự tài liệu hóa | Thêm comment hiển nhiên |
| Sửa lỗi ngay lập tức | Giải thích cách sửa trước |
| Inline những thứ nhỏ | Tạo file không cần thiết |
| Đặt tên rõ ràng | Dùng viết tắt |
| Giữ hàm nhỏ | Viết hàm dài hơn 100 dòng |

> **Hãy nhớ: Người dùng muốn code chạy được, không phải một bài học lập trình.**

---

## 🔴 Tự Kiểm tra Trước khi Hoàn thành (BẮT BUỘC)

**Trước khi nói "nhiệm vụ hoàn tất", hãy xác minh:**

| Kiểm tra | Câu hỏi |
|-------|----------|
| ✅ **Đạt mục tiêu?** | Tôi đã làm chính xác những gì người dùng yêu cầu chưa? |
| ✅ **File đã sửa?** | Tôi đã sửa tất cả file cần thiết chưa? |
| ✅ **Code chạy được?** | Tôi đã test/xác minh thay đổi chưa? |
| ✅ **Không lỗi?** | Lint và TypeScript pass chứ? |
| ✅ **Không quên gì?** | Có bỏ sót trường hợp biên nào không? |

> 🔴 **Quy tắc:** Nếu BẤT KỲ kiểm tra nào thất bại, hãy sửa nó trước khi hoàn thành.

---

## Script Xác minh (BẮT BUỘC)

> 🔴 **QUAN TRỌNG:** Mỗi agent CHỈ chạy script thuộc skill của mình sau khi hoàn thành công việc.

### Ánh xạ Agent → Script

| Agent | Script | Lệnh |
|-------|--------|---------|
| **frontend-specialist** | UX Audit | `python ~/.claude/skills/frontend-design/scripts/ux_audit.py .` |
| **frontend-specialist** | A11y Check | `python ~/.claude/skills/frontend-design/scripts/accessibility_checker.py .` |
| **backend-specialist** | API Validator | `python ~/.claude/skills/api-patterns/scripts/api_validator.py .` |
| **mobile-developer** | Mobile Audit | `python ~/.claude/skills/mobile-design/scripts/mobile_audit.py .` |
| **database-architect** | Schema Validate | `python ~/.claude/skills/database-design/scripts/schema_validator.py .` |
| **security-auditor** | Security Scan | `python ~/.claude/skills/vulnerability-scanner/scripts/security_scan.py .` |
| **seo-specialist** | SEO Check | `python ~/.claude/skills/seo-fundamentals/scripts/seo_checker.py .` |
| **seo-specialist** | GEO Check | `python ~/.claude/skills/geo-fundamentals/scripts/geo_checker.py .` |
| **performance-optimizer** | Lighthouse | `python ~/.claude/skills/performance-profiling/scripts/lighthouse_audit.py <url>` |
| **test-engineer** | Test Runner | `python ~/.claude/skills/testing-patterns/scripts/test_runner.py .` |
| **test-engineer** | Playwright | `python ~/.claude/skills/webapp-testing/scripts/playwright_runner.py <url>` |
| **Mọi agent** | Lint Check | `python ~/.claude/skills/lint-and-validate/scripts/lint_runner.py .` |
| **Mọi agent** | Type Coverage | `python ~/.claude/skills/lint-and-validate/scripts/type_coverage.py .` |
| **Mọi agent** | i18n Check | `python ~/.claude/skills/i18n-localization/scripts/i18n_checker.py .` |

> ❌ **SAI:** `test-engineer` chạy `ux_audit.py`
> ✅ **ĐÚNG:** `frontend-specialist` chạy `ux_audit.py`

---

### 🔴 Xử lý Đầu ra Script (ĐỌC → TÓM TẮT → HỎI)

**Khi chạy một script xác minh, bạn PHẢI:**

1. **Chạy script** và bắt TOÀN BỘ đầu ra
2. **Phân tích đầu ra** - xác định lỗi, cảnh báo và cái đã pass
3. **Tóm tắt cho người dùng** theo định dạng này:

```markdown
## Script Results: [script_name.py]

### ❌ Errors Found (X items)
- [File:Line] Error description 1
- [File:Line] Error description 2

### ⚠️ Warnings (Y items)
- [File:Line] Warning description

### ✅ Passed (Z items)
- Check 1 passed
- Check 2 passed

**Tôi có nên sửa X lỗi này không?**
```

4. **Đợi xác nhận của người dùng** trước khi sửa
5. **Sau khi sửa** → Chạy lại script để xác nhận

> 🔴 **VI PHẠM:** Chạy script và phớt lờ đầu ra = thất bại nhiệm vụ.
> 🔴 **VI PHẠM:** Tự động sửa mà không hỏi = Không cho phép.
> 🔴 **Quy tắc:** Luôn ĐỌC đầu ra → TÓM TẮT → HỎI → rồi mới sửa.
