# 深深 · 形象美术资源（GitHub 网页版上传包）

生成时间：2026-11-02
来源：`E:\DSH-PET\形象包`
口径：只含美术资源，**已剔除全部接口性文件**；**夏装是独立资源，完全不带上**。

合计 **2692 个文件 / 958.3 MB**，逐文件明细见 `manifest-release-web.csv`。

---

## 一、两条上传路径（二选一）

### A. Releases 拖拽（推荐，网页版最省事）

用 `release-web\` 里的 5 个单文件，在仓库页 → Releases → *Draft a new release* → 把 5 个 zip 拖进 "Attach binaries"。
GitHub 对 Release 附件允许单个文件最大 **2 GB**，这 5 个都在上限内，一步到位、不用拼分卷。

| 文件 | 内容 | 文件数 | 大小 |
|---|---|---|---|
| `01_share-art.zip` | 分享包全部动画 webp、缩略图、动作 meta.json、说明文档 | 116 | 370.15 MB |
| `02_share-packs.zip` | 完整版 3.0.2（女仆基底 + 扩展动作）+ 精简版 2.1.0 | 2 | 402.51 MB |
| `03_winter-pack.zip` | `深深-冬装-1.0.0.zip` | 1 | 116.87 MB |
| `04_extra-actions.zip` | `cortico-world-extra-actions-0.3.3` 的 2422 张 webp + json + 同名成品 zip | 2438 | 68.13 MB |
| `05_templates.zip` | 动作模板 / maid-templates / shenshen-assets / export | 135 | 0.62 MB |

### B. 提交进仓库（"Add file → Upload files"）

用 `repo-web-parts\` 里的 **54 个 20 MB 分卷**。仓库网页上传单文件上限 25 MB（见 GitHub 文档「添加文件到仓库」），因此按 20,000,000 字节（约 19.07 MB 十进制）切卷——注意 24 MiB = 25,165,824 字节会被 GitHub 以「文件太大」拒绝；同一模块的 `.001 .002 …` 必须一次全部传上，缺一卷就解不开。
仓库体积会是 958 MB，接近 GitHub 建议的 1 GB，属于能用但偏大——所以更推荐 A。

分卷按模块分组：`01_share-art` 20 卷、`02_share-packs` 22 卷、`03_winter-pack` 7 卷、`04_extra-actions` 4 卷、`05_templates` 1 卷。

**解压**（需 7-Zip，Windows 自带解压不支持分卷）：

```bat
7z x 01_share-art.zip.001 -o01_share-art
```

## 二、已剔除的内容（原目录零改动）

**接口性文件**

- 密钥：`千问key\key.txt`、`千问key\RunwayKey.txt`、`.qwen-key`
- 脚本：全部 `.mjs / .js / .cjs / .ts / .mts / .cts / .ps1 / .py`（`gen-i2v.mjs`、`key-and-pack.mjs`、`sign-webp.mjs`、`switch-skin.mjs` 等）
- 日志与提示词：`日志\`、`*.log`、`prompt\`（20 个动作 prompt）
- 接口文档/报价：`i2v-doc.txt`、`i2v-legacy.txt`、`legacy-doc.txt`、`pricing.txt`
- 内部源码：`packs\_check\`（含 `world-src` 世界引擎、asr/cua/webui 模块）
- 临时产物与前端构建物：`.tmp-ref`、`.test-thin`、`.out-thin12`、空 `分层输出` / `质检`、`*.html`、`*.css`、`*.gz`

**夏装（独立资源，全部不带）**

- `夏装\` 工作目录（4.8 GB）——整体未读取、未打包
- `分享\夏装-测试版\`（127 MB）
- `分享\夏装-测试版-单文件-0.2.4.zip`（127.3 MB）

> 判断依据：`分享\完整版\深深-3.0.1` 是女仆装基底（anim + ext 扩展动作），`精简版` 是 `shenshen-maid-lite`，两者都不是夏装，故保留。


## 三之二、网页提交的实测上限（2026-11-02 实测）

网页版「Add file → Upload files」的真实约束不是单文件 25 MB，而是**单次提交的总量**：

| 单次提交内容 | 结果 |
|---|---|
| 1 个 20 MB 文件 | ✅ 通过 |
| 2 个 20 MB 文件（40 MB） | ✅ 通过 |
| 3 个 20 MB 文件（60 MB） | ❌ `Commit failed — The file is too large` |
| 4 个 20 MB 文件（80 MB） | ❌ 同上 |
| 20 个 20 MB 文件（370 MB） | ❌ 同上（上传阶段正常，点 Commit 后才失败） |

结论：**边界落在 40–60 MB 之间，40 MB 是实测能过的最大粒度**，与「50 MB 上限」的推断一致。
判据是总量而非单文件——三个 20 MB 单文件各自都远小于 25 MB，合起来才失败。

失败发生在点 `Commit changes` 之后的 “Processing your files…” 阶段（约 1 分钟），上传进度条阶段不报错，所以看起来像网络卡住，实际是提交被服务端拒了。
GitHub 自带的建议 `Consider creating the file in a local clone and pushing it to GitHub` 正是这个原因：git 协议按对象分块传输，没有这个总量门槛。

## 三、校验

- `SHA256SUMS-release-web.txt`（5 条）、`SHA256SUMS-repo-web-parts.txt`（54 条）
- 校验命令：`sha256sum -c SHA256SUMS-release-web.txt`（Windows：`certutil -hashfile 01_share-art.zip SHA256`）
- 5 个归档与 5 组首卷均已用 `7z t` 通过完整性测试；归档内条目已扫描确认 **0 个** 脚本 / 日志 / 密钥 / prompt / 夏装残留

## 四、网页版操作要点

1. 先在 GitHub 网页建一个空仓库（不加 .gitignore、不加 README）。
2. 走 A：Releases → Draft a new release → tag 填 `v1` → 拖 5 个 zip → Publish。
3. 走 B：仓库页 Add file → Upload files → 拖 `repo-web-parts` 里的分卷（**同名分卷要全传**）→ Commit changes。单次拖 54 个文件约 958 MB，浏览器可能超时，建议按模块分 5 次提交。
4. Release 附件不占仓库体积，所以 A 路径不会把仓库撑到 1 GB 以上。

## 五、本仓库的上传记录

- 分卷：`7z a -tzip -mx0 -v20000000`，每卷 20,000,000 字节，共 54 卷（01 批 20 / 02 批 22 / 03 批 7 / 04 批 4 / 05 批 1）。
- 提交粒度：**每 2 卷一个 commit**（40 MB）。实测 60 MB、80 MB 均被 GitHub 以「文件太大」拒绝，40 MB 是网页版能过的最大粒度。
- commit message：`batch-1: 01_share-art.zip .002-.003` 这种写法，批次内卷号范围写在后面，方便回溯。
- 第一次提交的 message 是 `probe-a`，只包含 `01_share-art.zip.001`：那是用来判定「限制是单文件还是单次提交总量」的探针提交。结论是总量限制，所以后续都按 2 卷/提交推进；这条历史保留不删，用于说明来龙去脉。
- 解压仍然需要 7-Zip：`7z x 01_share-art.zip.001 -o01_share-art`，同一组的 `.001`～`.020` 必须齐全。

## 六、版权与许可

- 完整声明：**`NOTICE.md`**（逐项出处、改动说明、再分发要求）
- 许可证：**`LICENSE`**（MIT；分卷内各包保留各自的 MIT 声明）
- 一句话版本：角色与动画素材来自 [MerZlin/dsh-pet-indesktop](https://github.com/MerZlin/dsh-pet-indesktop)（MIT，版权归 MerZlin）；形象包代码与冬装设计稿出自 DSH-PET 工作区（MIT）；额外动作拓展 `cortico-world-extra-actions` 由 Daniele贤狼赫萝 与 奶糖_Net 制作（MIT）；Coopanion / cortico-world-desktop-pet 为 Pal AI Lab 的 AGPL-3.0-or-later 项目，本仓库**不含**其源代码。
- 再分发请保留 `NOTICE.md`、`LICENSE` 以及每个分卷包内的 `NOTICE.txt` / `figure.json` credits。