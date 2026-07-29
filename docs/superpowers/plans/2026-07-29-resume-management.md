# 多岗位简历落盘 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 将原始 txt 整理进 Git 仓库：`main` 保留完整素材，三个岗位分支各有一份精简可投递 `resume.md`。

**Architecture:** 岗位分支彼此独立，不强制模块拼装。`main` 放 `source/original.md` 作备份；`role/vision`、`role/motion-control`、`role/project-mgmt` 各维护完整 `resume.md`。同一段工作经历按岗位改写职责侧重点。

**Tech Stack:** Markdown、Git 分支；无运行时代码。

**Spec:** `docs/superpowers/specs/2026-07-29-resume-management-design.md`

## Global Constraints

- 源格式：Markdown（`.md`）
- 岗位分支根目录仅需可投递 `resume.md`（可另有 README 指向用法）
- 工作经历按分支岗位改写（视觉写视觉、控制写控制、项目写交付）
- RTK：视觉可留；运动控制默认不放；项目管理可弱写一条
- 每岗项目 3～5 个；经历 3～5 条；亮点 4 条；删除背景长文
- Git 提交：仅在用户明确要求时执行（本仓库用户规则优先于「每任务必 commit」）
- 响应与简历正文使用简体中文

## File Map

| 文件 | 责任 |
|------|------|
| `README.md` | 仓库用法：分支说明、如何改某一岗、如何新开岗位 |
| `source/original.md` | 从 txt 结构化的完整素材总库（可偏长） |
| `role/vision` → `resume.md` | 视觉算法可投递稿 |
| `role/motion-control` → `resume.md` | 运动控制可投递稿 |
| `role/project-mgmt` → `resume.md` | 项目管理可投递稿 |

---

### Task 1: main 总库与 README

**Files:**
- Create: `README.md`
- Create: `source/original.md`
- Reference: `D:\Downloads\王渊的简历.txt`
- Reference: `docs/superpowers/specs/2026-07-29-resume-management-design.md`

**Interfaces:**
- Consumes: 原始 txt 全文；设计文档中的分支约定
- Produces: `main` 上可读的总库与用法说明，供后续开分支复制

- [ ] **Step 1: 创建 `README.md`**

写入以下内容（可微调措辞，勿改分支名）：

```markdown
# My-resume

用 Git 分支管理不同岗位的简历。岗位稿彼此独立，按猎头要求改对应分支即可。

## 分支

| 分支 | 用途 |
|------|------|
| `main` | 完整素材总库（`source/original.md`），不直接投递 |
| `role/vision` | 视觉算法 / 机器视觉 |
| `role/motion-control` | 运动控制 / 设备上位机 |
| `role/project-mgmt` | 项目管理 / 软硬件协同交付 |

## 怎么改某一岗

1. `git checkout role/vision`（或其它岗位分支）
2. 编辑根目录 `resume.md`
3. 保存；需要时自行提交

## 怎么新开岗位

1. 从 `main` 或最接近的 `role/*` 开分支，例如 `role/quality`
2. 放入或改写根目录 `resume.md`
3. 在本 README 表格中补一行

## 设计文档

见 `docs/superpowers/specs/2026-07-29-resume-management-design.md`
```

- [ ] **Step 2: 创建 `source/original.md`**

从 `D:\Downloads\王渊的简历.txt` 整理为 Markdown，要求：

1. 保留全部事实：联系方式、两段工作经历、全部项目、教育、证书
2. 用标题分级：`# 王渊` → `## 基本信息` / `## 优势亮点` / `## 求职期望` / `## 工作经历` / `## 项目经验` / `## 教育经历` / `## 资格证书`
3. 每个项目用 `### 项目名`，其下用列表写描述、职责、业绩（可保留原文要点，但去掉无意义换行）
4. 不在此文件做岗位裁剪；允许偏长
5. 文首加一行说明：`> 完整素材总库，供参考；投递请用各 role/* 分支的 resume.md`

- [ ] **Step 3: 自检总库**

在仓库根目录确认存在：

- `README.md`
- `source/original.md`
- `docs/superpowers/specs/2026-07-29-resume-management-design.md`

打开 `source/original.md`，确认含：超达、新诺、飞拍、极高精度、多模型、杨泰、Vmask、质量信息化、市场信息化、RTK、JetsonHub、AEB、点喷、自动标定、AgriCore-X、WFC。

- [ ] **Step 4: 提交（仅当用户要求）**

若用户要求提交，在 `main` 上：

```bash
git add README.md source/original.md docs/superpowers/specs/2026-07-29-resume-management-design.md
git commit -m "$(cat <<'EOF'
Add resume source library and management design.

EOF
)"
```

若用户未要求，跳过本步。

---

### Task 2: `role/vision` 视觉算法简历

**Files:**
- Create on branch `role/vision`: `resume.md`
- Reference: `source/original.md`；设计文档「岗位选材 · vision」

**Interfaces:**
- Consumes: 总库事实；视觉侧选材规则；RTK 可保留
- Produces: 可直接投递的视觉岗 `resume.md`

- [ ] **Step 1: 创建分支**

```bash
git checkout main
git checkout -b role/vision
```

- [ ] **Step 2: 写入 `resume.md`**

创建根目录 `resume.md`，内容须符合下列结构与要点（措辞可润色，项目集合与经历侧重不可偏离）：

```markdown
# 王渊 · 机器视觉 / 视觉算法工程师

男 · 25岁 · 本科 · 杭州 | 18871182489 | 1622304283@qq.com

## 优势亮点

- （4 条：C++/OpenCV 视觉工程、飞拍与高精度对位、深度学习粗定位+传统精定位、软硬件联调）

## 求职意向

机器视觉 / 视觉算法 | 期望面议 | 杭州/广州等

## 工作经历

### 江苏超达智能科技有限公司 · 软件工程师（人工智能部）| 2025.12 – 至今

- 3～5 条：侧重视觉感知、定位相关工程、图像/嵌入式落地（按真实工作写具体模块，避免空泛「参与训练」）

### 杭州新诺微电子有限公司 · 软件工程师（C++）| 2023.08 – 2025.11

- 只写视觉相关主责，例如：飞拍硬触发与靶点识别；高精度/多模型对位工程化；主控视觉接口；PCB 图形渲染优化；避免罗列 MES/低代码等

## 项目经验（3～5 个）

### 飞拍功能实现（C++）· 项目负责人 | 2023.08 – 2024.04
- 1 句：运动中硬触发取像与靶点识别
- 职责/业绩：硬触发同步、算法优化、产能+20%、对位时间-30% 等（精炼 3～4 条）

### 极高精度算法（C++/Python/Halcon）| 2023.11 – 2024.03
- 自动标注、模型部署、视觉接口重构；精度至 3μm 内等

### 多模型识别（C++/Python）| 2023.08 – 2024.01
- 深度学习粗定位 + 模板精定位；出错率/跳动改善等量化结果

### Vmask PCB 图形渲染优化（C++）| 2025.07 – 2025.08
- 图元缩放/裁剪一致性、像素补偿；稳定运行与软著（各 1 条即可）

### RTK 多引擎定位框架（可选第 5 个）| 2023.06 – 至今
- 插件式多接收机适配、统一配置、协议解析（定位中间件，非运动控制）

## 教育 / 证书

吉林大学珠海学院（现珠海科技学院）· 计算机科学与技术 · 2019.09 – 2023.06
CET-4 · 计算机三级 · 程序员
```

禁止：市场/质量信息化长文、WFC 毕设、杨泰运动细节堆砌、背景目标散文。

- [ ] **Step 3: 自检视觉稿**

检查清单（全部为是）：

- [ ] 求职意向仅为视觉相关
- [ ] 新诺经历无 MES/低代码堆砌
- [ ] 项目数 3～5，含飞拍 + 高精度或多模型
- [ ] 若含 RTK，表述为定位/协议适配而非轴控
- [ ] 无大段「项目背景/项目目标」

- [ ] **Step 4: 提交（仅当用户要求）**

```bash
git add resume.md
git commit -m "Add vision-role resume draft."
```

---

### Task 3: `role/motion-control` 运动控制简历

**Files:**
- Create on branch `role/motion-control`: `resume.md`

**Interfaces:**
- Consumes: 总库；设计文档 motion-control 选材；**不含 RTK**
- Produces: 运动控制岗可投递稿

- [ ] **Step 1: 创建分支**

```bash
git checkout main
git checkout -b role/motion-control
```

- [ ] **Step 2: 写入 `resume.md`**

结构同 Task 2，但内容替换为：

- 标题：运动控制 / 设备上位机 / 自动化软件
- 亮点 4 条：主控架构、运动与 IO/激光联调、硬触发同步、C++/WPF 或 Qt 上位机
- 超达经历：若有控制/联调/嵌入式通信则写；否则写与设备联动相关的实际工作，勿硬编轴控
- 新诺经历：杨泰主控重构（IO/激光/运动平台/压板/同步板）、飞拍与运动同步、设备联调与性能；**不写**纯视觉模型训练长述、不写信息化平台
- 项目必选：杨泰系统重构、飞拍（强调触发与运动同步）、AEB 控制链路；点喷控制层可作第 4 个
- **不要**放 RTK、质量/市场信息化、AgriCore-X、WFC

业绩保留原文可信数字：主控响应提升 15%～20%、耦合问题减少 30%、飞拍产能/对位时间等。

- [ ] **Step 3: 自检运动控制稿**

- [ ] 无 RTK 项目块
- [ ] 含杨泰重构与飞拍（同步视角）
- [ ] 经历条目读起来像控制/主控/联调，而非算法论文
- [ ] 项目 3～5 个，无背景长文

- [ ] **Step 4: 提交（仅当用户要求）**

```bash
git add resume.md
git commit -m "Add motion-control-role resume draft."
```

---

### Task 4: `role/project-mgmt` 项目管理简历

**Files:**
- Create on branch `role/project-mgmt`: `resume.md`

**Interfaces:**
- Consumes: 总库；设计文档 project-mgmt 选材；RTK 可弱写一条
- Produces: 项目管理岗可投递稿

- [ ] **Step 1: 创建分支**

```bash
git checkout main
git checkout -b role/project-mgmt
```

- [ ] **Step 2: 写入 `resume.md`**

- 标题：项目管理 / 软硬件项目交付（或数字化项目负责人，按经历真实角色）
- 亮点 4 条：跨部门推进、质量/市场信息化落地、视觉功能项目负责、联调验收与版本交付
- 超达：写带人/推进/交付类真实职责（下属或协作若适用）
- 新诺：多子系统协同（视觉/主控/成像/FPGA）、飞拍项目负责、质量与市场信息化负责人视角、现场验收；少写算子级细节
- 项目优先：质量管理信息化、市场管理信息化、飞拍（负责人）、杨泰（联调交付视角）；可选：多模型/高精度的「工程落地与客户部署」；RTK 最多一条「多引擎框架架构到落地」
- 量化保留：8D 线上化 100%、处理时效、审批周期、飞拍产能、客户部署等
- 禁止：WFC 毕设、大段算法原理、纯代码清单

- [ ] **Step 3: 自检项目管埋稿**

- [ ] 经历读起来是推进/交付/协同，不是纯开发流水账
- [ ] 含质量或市场信息化至少其一，以及飞拍或杨泰交付
- [ ] 项目 3～5 个
- [ ] 无大段背景目标文

- [ ] **Step 4: 回到 main（收尾）**

```bash
git checkout main
```

确认 `main` 仍有 `README.md` 与 `source/original.md`；三角色分支可用 `git branch` 列出。

- [ ] **Step 5: 提交（仅当用户要求）**

分别在各分支或按用户指示提交；未要求则跳过。

---

## Plan Self-Review

1. **Spec coverage:** 独立岗位分支、Markdown、三岗选材、经历按岗改写、RTK 归类、首次不做 PDF/拼装脚本、提交需用户同意 → 均有对应 Task。
2. **Placeholders:** 无 TBD；简历正文用结构要点约束，允许润色但锁定选材。
3. **Consistency:** 分支名与设计文档一致；RTK 规则在 Task 2/3/4 一致。

---

## Execution Handoff

Plan complete and saved to `docs/superpowers/plans/2026-07-29-resume-management.md`.

两种执行方式：

1. **Subagent-Driven（推荐）** — 每任务开一个子代理，任务间复查  
2. **Inline Execution** — 本会话按任务直接做完  

你选哪一种？（也可以直接说「你在本会话做完」——等同方式 2。）
