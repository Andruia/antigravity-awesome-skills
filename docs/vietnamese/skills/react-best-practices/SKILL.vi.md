---
name: vercel-react-best-practices
description: Hướng dẫn tối ưu hóa hiệu năng React và Next.js từ Vercel Engineering. Kỹ năng này nên được sử dụng khi viết, review, hoặc refactor code React/Next.js để đảm bảo các mẫu hiệu năng tối ưu. Kích hoạt cho các nhiệm vụ liên quan đến React components, Next.js pages, data fetching, bundle optimization, hoặc cải thiện hiệu năng.
---

# Vercel React Best Practices

Hướng dẫn tối ưu hóa hiệu năng toàn diện cho ứng dụng React và Next.js, được bảo trì bởi Vercel. Chứa 45 quy tắc qua 8 danh mục, được ưu tiên theo mức độ tác động để hướng dẫn refactoring tự động và tạo code.

## Khi nào Áp dụng

Tham khảo các hướng dẫn này khi:
- Viết các React components hoặc Next.js pages mới
- Thực hiện data fetching (client hoặc server-side)
- Review code để tìm vấn đề hiệu năng
- Refactor code React/Next.js hiện có
- Tối ưu hóa kích thước bundle hoặc thời gian tải

## Danh mục Quy tắc theo Mức độ Ưu tiên

| Ưu tiên | Danh mục | Tác động | Tiền tố |
|----------|----------|--------|--------|
| 1 | Loại bỏ Waterfalls | CRITICAL | `async-` |
| 2 | Tối ưu hóa Bundle Size | CRITICAL | `bundle-` |
| 3 | Hiệu năng Server-Side | HIGH | `server-` |
| 4 | Data Fetching Client-Side | MEDIUM-HIGH | `client-` |
| 5 | Tối ưu hóa Re-render | MEDIUM | `rerender-` |
| 6 | Hiệu năng Rendering | MEDIUM | `rendering-` |
| 7 | Hiệu năng JavaScript | LOW-MEDIUM | `js-` |
| 8 | Mô hình Nâng cao (Advanced Patterns) | LOW | `advanced-` |

## Tham khảo Nhanh

### 1. Loại bỏ Waterfalls (CRITICAL)

- `async-defer-await` - Di chuyển await vào trong các nhánh nơi thực sự được sử dụng
- `async-parallel` - Sử dụng Promise.all() cho các thao tác độc lập
- `async-dependencies` - Sử dụng better-all cho các phụ thuộc từng phần
- `async-api-routes` - Bắt đầu promise sớm, await muộn trong API routes
- `async-suspense-boundaries` - Sử dụng Suspense để stream nội dung

### 2. Tối ưu hóa Bundle Size (CRITICAL)

- `bundle-barrel-imports` - Import trực tiếp, tránh barrel files
- `bundle-dynamic-imports` - Sử dụng next/dynamic cho các component nặng
- `bundle-defer-third-party` - Tải analytics/logging sau khi hydration
- `bundle-conditional` - Load modules chỉ khi tính năng được kích hoạt
- `bundle-preload` - Preload khi hover/focus để tăng tốc độ cảm nhận

### 3. Hiệu năng Server-Side (HIGH)

- `server-cache-react` - Sử dụng React.cache() để deduplication theo request (per-request)
- `server-cache-lru` - Sử dụng LRU cache cho caching chéo request (cross-request)
- `server-serialization` - Tối thiểu hóa dữ liệu truyền xuống client components
- `server-parallel-fetching` - Cấu trúc lại components để song song hóa việc fetch
- `server-after-nonblocking` - Sử dụng after() cho các thao tác không chặn (non-blocking)

### 4. Data Fetching Client-Side (MEDIUM-HIGH)

- `client-swr-dedup` - Sử dụng SWR để tự động deduplication request
- `client-event-listeners` - Deduplicate các global event listeners

### 5. Tối ưu hóa Re-render (MEDIUM)

- `rerender-defer-reads` - Đừng subscribe vào state chỉ được dùng trong callbacks
- `rerender-memo` - Tách các tác vụ tốn kém vào memoized components
- `rerender-dependencies` - Sử dụng primitive dependencies trong effects
- `rerender-derived-state` - Subscribe vào các boolean dẫn xuất, không phải giá trị thô
- `rerender-functional-setstate` - Sử dụng functional setState để stable callbacks
- `rerender-lazy-state-init` - Truyền function vào useState cho các giá trị khởi tạo tốn kém
- `rerender-transitions` - Sử dụng startTransition cho các update không khẩn cấp

### 6. Hiệu năng Rendering (MEDIUM)

- `rendering-animate-svg-wrapper` - Animate div wrapper, không phải SVG element
- `rendering-content-visibility` - Sử dụng content-visibility cho danh sách dài
- `rendering-hoist-jsx` - Tách static JSX ra ngoài components
- `rendering-svg-precision` - Giảm độ chính xác tọa độ SVG
- `rendering-hydration-no-flicker` - Sử dụng inline script cho dữ liệu client-only
- `rendering-activity` - Sử dụng Activity component để show/hide
- `rendering-conditional-render` - Sử dụng ternary, không phải && cho điều kiện

### 7. Hiệu năng JavaScript (LOW-MEDIUM)

- `js-batch-dom-css` - Nhóm các thay đổi CSS qua classes hoặc cssText
- `js-index-maps` - Xây dựng Map cho các lookups lặp lại
- `js-cache-property-access` - Cache truy cập thuộc tính object trong vòng lặp
- `js-cache-function-results` - Cache kết quả function trong module-level Map
- `js-cache-storage` - Cache đọc localStorage/sessionStorage
- `js-combine-iterations` - Kết hợp nhiều filter/map thành một vòng lặp
- `js-length-check-first` - Kiểm tra độ dài mảng trước khi so sánh tốn kém
- `js-early-exit` - Return sớm từ functions
- `js-hoist-regexp` - Đưa RegExp creation ra ngoài vòng lặp
- `js-min-max-loop` - Sử dụng vòng lặp để tìm min/max thay vì sort
- `js-set-map-lookups` - Sử dụng Set/Map cho O(1) lookups
- `js-tosorted-immutable` - Sử dụng toSorted() cho tính bất biến (immutability)

### 8. Mô hình Nâng cao (LOW)

- `advanced-event-handler-refs` - Lưu trữ event handlers trong refs
- `advanced-use-latest` - useLatest cho stable callback refs

## Cách Sử dụng

Đọc từng file quy tắc để có giải thích chi tiết và ví dụ code (Trong tài liệu gốc tiếng Anh, phần này tham chiếu đến các file chưa được dịch, nhưng các nguyên tắc trên là đủ để áp dụng).

```
rules/async-parallel.md
rules/bundle-barrel-imports.md
rules/_sections.md
```

Mỗi file quy tắc chứa:
- Giải thích ngắn gọn tại sao nó quan trọng
- Ví dụ code SAI kèm giải thích
- Ví dụ code ĐÚNG kèm giải thích
- Ngữ cảnh bổ sung và tham khảo

## Tài liệu Tổng hợp Đầy đủ

Để xem hướng dẫn hoàn chỉnh với tất cả các quy tắc được mở rộng: `AGENTS.md`
