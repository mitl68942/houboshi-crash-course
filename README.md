## 猴博士速通 skill 上线

- **结构**：SKILL.md（猴博士体 SOP）+ references/（5 科套路库）+ scripts/（讲义生成器 + 小抄生成器）
- **覆盖科目**：高数、线性代数、概率论、C 语言、数据结构（已建库）；其它科目临场 AI 套路，自动追加
- **产出**：docx 讲义，猴博士原版风格（红/蓝配色、表格、emoji 标注、页眉页脚）
- **Smoke test**：`test/sample-高数第3章.docx`（13.5 KB）已生成验证通过
- **依赖**：全局 docx（Node）库已就位（`require('docx')` OK）
- **踩坑**：本机 `soffice.py` 在 Windows 上 socket.AF_UNIX 不兼容，转 PDF 验证会失败；docx 库本身输出无问题，可直接交付 docx
- **后续**：用户给具体科目+章节时，按 SKILL.md SOP 走；AI 临场套路生成后**主动增量**到 references/ 对应科目

## 猴博士 skill · 增强：双模式

按用户要求，在 SKILL.md 末尾追加两个核心 SOP（增量修改，未覆盖原内容）：

### 默认答题模式（核心）
- 角色：猴博士距离考试 20 分钟状态
- 开头 `🐒🔥`，结尾问 `下一题扔不扔？`
- 四种题型分流：
  1. 名词解释：定义 ≤ 15 字 + 3 个关键词
  2. 计算题：核心公式 + 步骤 + 结果（猜也给）
  3. 论述题：强行压成 3 个方面
  4. 太偏：直接说别看了
- 用户不显式要求"打小抄" / "讲义" 时默认走此模式

### 小抄模式
- 触发词：打小抄 / 生成PDF / 做小抄
- 工具：`scripts/generate_cheatsheet.js`
- 排版铁律：3pt 字号 / 3pt 行距 / 无边框 / 纯文本 || 分隔 / Helvetica / 纯黑
- 演示：`test/高数第3章_小抄.pdf`（2.0 KB，A4 横向，10 行知识点）
- 依赖：skill 本地 `node_modules/pdfkit`（`npm install pdfkit` 已装）
