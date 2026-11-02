# 深深 · 形象美术资源归档

桌宠角色「深深」的形象美术资源归档：动画素材、成品形象包、动作模板与元数据。
面向想直接使用形象包、或想基于这些素材继续创作的人。

- 全部 54 个分卷合计约 **958 MB**
- 每个分卷 20,000,000 字节，同名分卷必须齐全才能解压
- 许可证：[MIT](LICENSE) · 出处与署名：[NOTICE.md](NOTICE.md)

---

## 一、内容介绍

| 模块 | 分卷 | 内含 | 文件数 | 解压后 |
|---|---|---|---|---|
| `01_share-art.zip` | `.001`–`.020` | 女仆装形象包的**完整美术资源**：10 段基础动作动画（待机呼吸、漂浮踏步、东张西望、被拖拽悬空、开心跃动、害羞惊讶、傲娇生气、挠痒咯咯笑、元气挥手、螃蟹走路）、扩展动作动画（事件触发类与随机类）、缩略图、动作元数据 json、随包说明 | 116 | 370.2 MB |
| `02_share-packs.zip` | `.001`–`.022` | 两个**已发布的成品形象包**（zip，可直接导入）：完整版 3.0.2、精简版 2.1.0（无扩展动作） | 2 | 402.5 MB |
| `03_winter-pack.zip` | `.001`–`.007` | **冬装**成品形象包 1.0.0（zip，可直接导入）：鲸鱼兜帽 + 条纹围巾 + 毛边外套，10 段动作 | 1 | 116.9 MB |
| `04_extra-actions.zip` | `.001`–`.004` | **额外动作拓展**：2422 张动作动画 webp + 动作索引 json + 可直接安装的扩展包 zip（0.3.3） | 2438 | 68.1 MB |
| `05_templates.zip` | `.001` | **动作模板与元数据**：14 段动作的关键帧表（纯数据，模型无关）、103 个动作模板 json、部件图 png、导出说明 | 135 | 0.6 MB |

动画为无损 WebP 序列/动图，24 fps，透明底。`01`、`02`、`03` 里的角色动画是同一套动作的不同封装形式：`01` 是素材形态（便于二次创作），`02`/`03` 是可直接装进桌宠的成品包。

## 二、使用方法

### 1. 下载与解压

分卷是 7-Zip 的分卷 zip，**Windows 自带的解压不支持**，请用 [7-Zip](https://www.7-zip.org/)：

```bat
:: 把同一模块的 .001 .002 … 放在同一目录，只对 .001 解压
7z x 01_share-art.zip.001 -o01_share-art
```

macOS / Linux：`brew install sevenzip` 或 `apt install p7zip-full`，命令相同。

### 2. 直接使用形象包

解压 `02_share-packs` 或 `03_winter-pack`，得到成品 zip 后，在 Coopanion 的**装扮页**点「＋ 导入」，把 zip 拖进去即可。
（装扮页导入上限 128 MiB，所以冬装单独成包。）

### 3. 安装额外动作拓展

解压 `04_extra-actions`，用其中的扩展包 zip 安装（包内有安装说明与 `tools/install-extension.mjs`）。

### 4. 二次创作

解压 `05_templates` 得到「动作数据 / 美术部件」分离的模板：

- `clips/<id>.json`：每段动作的关键帧表（`body` 整体轨 + `parts` 部件轨），每段 24 个关键帧，与 24 fps 烘焙对齐
- `index.json`：动作清单、时长、循环、触发器、通道数，以及部件契约 `partContract`
- `parts/*.png`：部件图；`model.json`：层清单样板

换一套美术只需替换部件图与层清单，动作数据不用改；改动作只改 json，代码不动。

### 5. 校验完整性

```bash
sha256sum -c SHA256SUMS-repo-web-parts.txt      # macOS / Linux
certutil -hashfile 01_share-art.zip.001 SHA256  # Windows
```

`manifest-repo-web-parts.csv` 是解压后每个文件的逐条清单（模块、路径、字节数）。

## 三、版权声明

本仓库是**分发归档**，不是原创作品集。细致出处见 [NOTICE.md](NOTICE.md)，法律文本见 [LICENSE](LICENSE)。

- **角色与动画素材**：来自 [MerZlin/dsh-pet-indesktop](https://github.com/MerZlin/dsh-pet-indesktop)，版权归 MerZlin，**MIT** 许可。按 MIT 要求，再分发必须保留版权与许可声明——本文件、`LICENSE`、`NOTICE.md` 以及每个分卷包内的 `NOTICE.txt` / `figure.json` credits 即为此用。本归档对素材**未做任何像素级修改**（无重编码、无裁切、无缩放）。
- **形象包代码与冬装设计稿**：出自 DSH-PET 工作区，**MIT**。
- **额外动作拓展**：由 Daniele贤狼赫萝（丹尼尔）与 奶糖_Net（Net-ang）制作，**MIT**。
- **Coopanion / cortico-world-desktop-pet**：Pal AI Lab 以 **AGPL-3.0-or-later** 发布（[GitHub](https://github.com/Pal-AI-Lab/Coopanion)）。本归档**不含其源代码**，只通过其公开的形象包接口工作。
- **本归档的整理、分卷、清单与文档**：奶糖_Net（Net-ang），**MIT**。

再分发请保留上述声明；修改素材或代码时，请在衍生作品中标注改动。作品按「原样」提供，不附带任何担保。

---

## 附：本仓库不含什么

只收录形象美术资源与成品包。与美术无关的内容——调用外部服务的脚本、运行日志、内部提示词、接口文档、内部源码、编辑器前端产物、临时中间产物——均未纳入；密钥与凭据从未进入本归档（打包后逐字节复核，密钥类命中为 0）。
