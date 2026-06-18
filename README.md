# BA Skills - BMAD Method cho Claude Code

Bộ skills triển khai **BMAD Method** (Phương pháp phát triển phần mềm Agile với AI) cho Claude Code — biến Claude Code thành một môi trường phát triển agile hoàn chỉnh với các agent chuyên biệt.

> Dựa trên [BMAD Method](https://github.com/bmad-code-org/BMAD-METHOD) của [BMAD Code Organization](https://github.com/bmad-code-org).

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

**Sau khi cài:** Restart Claude Code, mở project và chạy `/workflow-init`.

---

## Tổng quan

BMAD chia quá trình phát triển thành các phase rõ ràng, mỗi phase có agent chuyên trách:

| Phase | Agent | Lệnh chính |
|-------|-------|-----------|
| 1 - Phân tích sản phẩm | Business Analyst | `/product-brief` |
| 2 - Lập yêu cầu | Product Manager | `/prd`, `/tech-spec` |
| 3 - Thiết kế hệ thống | System Architect | `/architecture` |
| 4 - Triển khai | Scrum Master + Developer | `/sprint-planning`, `/dev-story` |
| Sáng tạo | Creative Intelligence | `/brainstorm`, `/research` |
| UX | UX Designer | `/create-ux-design` |
| Mở rộng | Builder | `/create-agent`, `/create-workflow` |

---

## Quy trình cơ bản

**Project nhỏ (1–10 tính năng):**
```
/product-brief → /tech-spec → /dev-story
```

**Project vừa và lớn:**
```
/product-brief → /prd → /architecture → /sprint-planning → /dev-story
```

---

## Chi tiết từng Phase

### Phase 1 — Phân tích sản phẩm

**Agent:** Business Analyst  
**Khi nào dùng:** Bắt đầu project mới hoặc tính năng lớn

**Lệnh:**
- `/workflow-init` — Khởi tạo cấu trúc BMAD trong project
- `/workflow-status` — Xem trạng thái hiện tại và gợi ý bước tiếp theo
- `/product-brief` — Tạo tài liệu phân tích sản phẩm

**Output:** Tài liệu product brief gồm phân tích thị trường, user persona, tính năng cốt lõi.

**Ví dụ:**
```
User: /product-brief

Business Analyst:
> Chúng ta đang xây dựng gì?
"Ứng dụng quản lý công việc cho team nhỏ"

> ✓ Product brief đã tạo!
>
> Tính năng cốt lõi: Quản lý task, cộng tác nhóm, theo dõi thời gian
> Người dùng mục tiêu: Team 5–20 người
> Độ phức tạp: Level 2 (nên dùng /prd)
>
> Bước tiếp theo: /prd
```

---

### Phase 2 — Lập yêu cầu

**Agent:** Product Manager  
**Khi nào dùng:** Sau product brief, trước khi thiết kế hệ thống

**Lệnh:**
- `/prd` — Tạo tài liệu yêu cầu đầy đủ (project level 2+)
- `/tech-spec` — Tạo tech spec gọn nhẹ (project level 0–1)

**Output:** Tài liệu gồm functional requirements (FR-XXX), non-functional requirements (NFR-XXX), user stories, acceptance criteria, phân loại MoSCoW.

**Ví dụ:**
```
User: /prd

Product Manager:
> ✓ PRD đã tạo: bmad-outputs/prd.md
>
> - 24 Functional Requirements
> - 8 Non-Functional Requirements
> - 4 Epics
>
> Bước tiếp theo: /architecture
```

---

### Phase 3 — Thiết kế hệ thống

**Agent:** System Architect  
**Khi nào dùng:** Sau khi có yêu cầu, trước khi code

**Lệnh:**
- `/architecture` — Tạo tài liệu kiến trúc hệ thống
- `/solutioning-gate-check` — Kiểm tra chất lượng kiến trúc (cần đạt ≥90%)

**Output:** Kiến trúc hệ thống gồm tech stack, data model, API spec, lý do chọn công nghệ, đảm bảo NFR.

**Ví dụ:**
```
User: /architecture

System Architect:
> ✓ Kiến trúc đã tạo: bmad-outputs/architecture.md
>
> Tech Stack:
> - Backend: Python + FastAPI
> - Frontend: React + TypeScript
> - Database: PostgreSQL
> - Cache: Redis
>
> Độ phủ: FR 100% (24/24) | NFR 100% (8/8)
>
> Bước tiếp theo: /solutioning-gate-check

User: /solutioning-gate-check

> ✓ Gate Check đạt! Điểm: 96/100
> Sẵn sàng triển khai → /sprint-planning
```

---

### Phase 4 — Triển khai

**Agent:** Scrum Master + Developer  
**Khi nào dùng:** Sau khi kiến trúc được duyệt

**Lệnh:**
- `/sprint-planning` — Lập kế hoạch sprint
- `/create-story` — Tạo user story chi tiết
- `/dev-story` — Triển khai story (code + test)

**Ví dụ:**
```
User: /sprint-planning

Scrum Master:
> ✓ Sprint 1 đã lên kế hoạch!
>
> Sprint Goal: MVP quản lý task cơ bản
> Stories: 8 stories (21 points) | Thời gian: 2 tuần
>
> Ưu tiên cao:
> 1. Đăng nhập / xác thực (5 points)
> 2. Tạo & chỉnh sửa task (3 points)
> 3. Danh sách task (3 points)

User: /dev-story

Developer:
> ✓ Story-001 hoàn thành!
>
> Files đã tạo:
> - src/api/auth.py
> - src/models/user.py
> - tests/test_auth.py (15 test cases)
>
> Tests: 15/15 passed ✓ | Coverage: 94%
```

---

### Creative Intelligence — Brainstorming & Nghiên cứu

**Khi nào dùng:** Khám phá ý tưởng, nghiên cứu thị trường, phân tích đối thủ

**Lệnh:**
- `/brainstorm` — Brainstorming có cấu trúc (5 Whys, SCAMPER, SWOT, Six Hats...)
- `/research` — Nghiên cứu thị trường, kỹ thuật, người dùng

**Ví dụ:**
```
User: /brainstorm

> Chủ đề: Ý tưởng tính năng cho app quản lý task v2.0
> Kỹ thuật: SCAMPER + Mind Mapping + SWOT
>
> ✓ Kết quả:
> - 32 ý tưởng trong 6 nhóm
> - Top 3: AI gợi ý task, Dashboard analytics, Redesign mobile-first
>
> Document: bmad-outputs/brainstorming-2025-06-18.md

User: /research

> Chủ đề: Phân tích đối thủ cạnh tranh
>
> ✓ Đã phân tích: Asana, Trello, Monday, ClickUp, Notion
>
> Phát hiện chính:
> - Tất cả đối thủ có app mobile (mình chưa có)
> - AI features đang trở thành tiêu chuẩn
> - Cơ hội: UI đơn giản hơn, tập trung privacy
```

---

### UX Designer — Thiết kế trải nghiệm người dùng

**Khi nào dùng:** Sau khi có yêu cầu, song song với thiết kế hệ thống

**Lệnh:**
- `/create-ux-design` — Tạo tài liệu UX đầy đủ

**Output:** User flows, wireframes (ASCII), WCAG 2.1 accessibility, design tokens, tài liệu bàn giao cho developer.

---

### Builder — Tạo agent và workflow tùy chỉnh

**Khi nào dùng:** Cần agent hoặc workflow riêng cho domain cụ thể

**Lệnh:**
- `/create-agent` — Tạo agent mới (QA, DevOps, Security...)
- `/create-workflow` — Tạo workflow command mới

**Ví dụ:**
```
User: /create-agent

> Tên agent: QA Engineer
> Nhiệm vụ: Tạo test plan, chạy test, báo cáo bug
>
> ✓ QA Engineer skill đã tạo!
> File: ./custom-agents/qa-engineer/SKILL.md
> Lệnh mới: /create-test-plan, /execute-tests, /bug-report
```

---

## So sánh

| | Cách truyền thống | BMAD v6 |
|---|---|---|
| Mất context | Phải giải thích lại mỗi lần | Lưu trạng thái tự động qua YAML |
| Chuyển vai | Tự switch thủ công | Tự động theo lệnh |
| Tài liệu | Rải rác, lỗi thời | Có cấu trúc, template, lưu trong repo |
| Token | Tốn nhiều | Tiết kiệm 70–85% nhờ helper pattern |
| Quy trình | Ad-hoc | 4 phase rõ ràng |
| Mở rộng | Khó | Builder tạo agent/workflow mới |

---

## Theo dõi trạng thái project

BMAD lưu trạng thái vào file YAML trong project:

```yaml
# bmad-outputs/bmm-workflow-status.yaml
project_level: 2
phase_1_analysis:
  product_brief_completed: true
phase_2_planning:
  prd_completed: true
  functional_requirements_count: 24
phase_3_solutioning:
  architecture_completed: true
  gate_check_score: 96
phase_4_implementation:
  stories_created: 12
  stories_completed: 5
```

Chạy `/workflow-status` bất kỳ lúc nào để xem tiến độ và gợi ý bước tiếp theo.

---

## Hỗ trợ

- Báo lỗi: https://github.com/ThinhTP204/ba-skills-harness/issues
- Tài liệu gốc BMAD: https://github.com/bmad-code-org/BMAD-METHOD
