# BA Skills - BMAD Method cho Claude Code

Bộ skills triển khai **BMAD Method** (Phương pháp phát triển phần mềm Agile với AI) cho Claude Code.

> Dựa trên [BMAD Method](https://github.com/bmad-code-org/BMAD-METHOD) của BMAD Code Organization.

---

## Cài đặt

### Cách 1: Tải về và chạy (khuyên dùng)

```bash
curl -sSL https://raw.githubusercontent.com/ThinhTP204/ba-skills-harness/main/install-v6.sh | bash
```

Script sẽ hỏi bạn muốn cài theo kiểu nào:

```
1) Global  - Dùng cho tất cả project  (~/.claude/skills/)
2) Project - Chỉ dùng cho project này (./.claude/skills/)
```

### Cách 2: Truyền tham số (không cần hỏi)

```bash
# Cài cho tất cả project
curl -sSL https://raw.githubusercontent.com/ThinhTP204/ba-skills-harness/main/install-v6.sh | bash -s -- --global

# Chỉ cài cho project hiện tại
curl -sSL https://raw.githubusercontent.com/ThinhTP204/ba-skills-harness/main/install-v6.sh | bash -s -- --project
```

### Cách 3: Clone rồi chạy thủ công

```bash
git clone https://github.com/ThinhTP204/ba-skills-harness.git
cd ba-skills-harness
./install-v6.sh
```

---

## Sau khi cài

1. **Restart Claude Code** (skills tải lúc khởi động)
2. Mở project của bạn
3. Chạy lệnh đầu tiên:

```
/workflow-init
```

---

## Các lệnh chính

| Lệnh | Chức năng |
|------|-----------|
| `/workflow-init` | Khởi tạo BMAD trong project |
| `/workflow-status` | Xem trạng thái + gợi ý bước tiếp |
| `/product-brief` | Phân tích sản phẩm (Phase 1) |
| `/prd` | Tạo tài liệu yêu cầu (Phase 2) |
| `/architecture` | Thiết kế hệ thống (Phase 3) |
| `/sprint-planning` | Lập kế hoạch sprint (Phase 4) |
| `/dev-story` | Triển khai tính năng (Phase 4) |
| `/brainstorm` | Brainstorming có cấu trúc |
| `/research` | Nghiên cứu thị trường / kỹ thuật |
| `/create-ux-design` | Thiết kế UX |

---

## Quy trình cơ bản

**Project nhỏ:**
```
/product-brief → /tech-spec → /dev-story
```

**Project lớn:**
```
/product-brief → /prd → /architecture → /sprint-planning → /dev-story
```

---

## Hỗ trợ

- Báo lỗi: https://github.com/ThinhTP204/ba-skills-harness/issues
