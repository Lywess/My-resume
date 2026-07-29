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
