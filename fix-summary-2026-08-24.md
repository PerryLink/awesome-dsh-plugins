# 本次处理总结 · 2026-08-24

> 仓库：`kejixiaoliang/awesome-dsh-plugins`
> 任务：处理当前开放的 issues（12 个开放 PR + 1 个自动死链 issue #43）
> 原则：单插件 PR 按规范收录；**一次 PR 塞大量插件（批量收录、同作者打包）一律不通过**（#24/#30/#20）。

---

## 一、PR 处理结果（12 个）

| PR | 插件 / 内容 | 作者 | 结果 |
|---|---|---|---|
| #42 | dsh-nuke-plugin（tools）| @beijingwahw | ✅ 收录（安装命令修为 `github:beijingwahw/dsh-nuke-plugin`，未发 npm）|
| #41 | dsh-novel-writer（fun-other）| @siweina | ✅ 收录（npm 3.7.0，⭐7）|
| #40 | task-chime（notifications）| @Abel-86 | ✅ 收录（npm 1.0.1）|
| #35 | DSH-EasyRewrite（ui-themes）| @Renzic-Stone | ✅ 收录（npm 2.1.0，⭐59）+ 补英文描述 |
| #34 | dsh-meow-smooth（ui-themes）| @Phant0Meow | ✅ 收录（npm 0.4.0，⭐12）|
| #39 | dsh-labnana（multimodal）| @exoticknight | ✅ 收录（未发 npm → `github:`）|
| #38 | dsh-plugin-hub（infrastructure-dev）| @Noob-stupid | ✅ 收录（npm 0.1.8，⭐69；仅取新条目，忽略其过期 star 改动）|
| #32 | dph-fleet → dsh-devices 更名 | @polaris-smart | ✅ 修正收录（仓库已更名，npm 0.1.2，⭐5）|
| #31 | dsh-tray-launcher + dsh-plugin-usage-meter | @fancr-code | ✅ 收录 2 条（npm 1.4.0 / 1.7.2）|
| #24 | 36 个插件（JohnXu22786）| @JohnXu22786 | ⛔ 拒收（一次 PR 批量收录 36 个，滥竽充数）|
| #30 | 28 个插件（PerryLink）| @PerryLink | ⛔ 拒收（一次 PR 批量收录 28 个，滥竽充数）|
| #20 | suhui（context-memory）| @stargazer-2026 | ⛔ 拒收（纯 SKILL.md、无 DSH manifest；且其 diff 会回退上次 CI 重构、重新引入已删除的 `data/plugins.json`）|

**收录 9 个新插件 + 1 个更名；拒收 3 个批量/不合规 PR。**

### 核验口径
- 仓库公开、未归档、含 README + `cordis.patch.yml`/`dsh.plugin.json`（DSH 清单）→ 视为有效 DSH 插件。
- 安装命令按是否已发 npm 校正（未发 npm → `github:owner/repo`；已发 → `dsh plugin add <pkg>`）。
- #24/#30 的 64 个仓库经全量核验确实存在且大多有效，但按「单条审核、不批量塞入」的主仓标准不予收录。

---

## 二、issue #43（自动死链报告）处理

- 报告为旧结构快照：大量报错是引用了已删除文件（`data/plugins.json` / `data/README.md` / `docs/reconcile.md`），随上次重构上推即消失。
- 真实死链 2 条（均 404 已验证）：
  - `Nexus-Aethra/DSH-plugin-switch`（infrastructure-dev.md）→ 从目录删除
  - `stushansusu/dsh-miku-skin`（ui-themes.md）→ 从目录删除
  - 同步清理其英文描述（`descriptions-en.json`）与 `docs/wishlist.md` 中的残留引用、`reconcile.md` 引用。
- 修复后重新生成 README/INDEX/web 数据，`linkcheck` 不再报这两条。

---

## 三、数据一致性

| 维度 | 处理前 | 处理后 |
|---|---|---|
| 目录条目 | 299 | **306**（+9 新，-2 死链）|
| 唯一数 | 299 | 306（无重复）|
| 分类 | 14 | 14 |
| 校验 | - | `validate.mjs` 通过（306 唯一，无格式/重复错误）|
| 英文描述 | 531 | 537（+9 新，-2 死链，-1 更名替换，净 +6）|

---

## 四、变更文件

- `plugins/*.md`：tools / fun-other / notifications-channels / multimodal / ui-themes / desktop-tui-mobile / infrastructure-dev / agent-orchestration（9 条新增 + 1 更名 + 2 死链删除）
- `data/descriptions-en.json`、`docs/wishlist.md`、`CHANGELOG.md`
- 重新生成：`INDEX.md` / `README.md` / `README.zh.md` / `web/data.js`

---

## 五、后续可选项（未做）

1. #24/#30：建议作者**拆分**成单插件 PR 逐个提交；若坚持批量，可开 Issue 提出「个人插件集收录标准」再议。
2. 若想彻底避免死链 issue，可考虑让 `linkcheck.yml` 正确排除 `**/*.md`（当前顶层 .md 未被排除，导致 README/INDEX 也进报告）。
