# FapiaoClaw - Invoice Processing AI Skill

[中文版介绍请见下方 (Scroll down for Chinese version)](#fapiaoclaw---%E5%8F%91%E7%A5%A8%E6%95%B4%E7%90%86-ai-%E6%8A%80%E8%83%BD)

FapiaoClaw is a specialized Python utility and an installable **OpenClaw AI Skill** that automates the process of organizing, filtering, and summarizing Chinese invoice (fapiao) PDFs. 

By integrating this repository into your Workspace, OpenClaw (and Workbuddy) can natively process directories full of invoices through semantic language commands like:
> "Organize the invoices in ./fapiao and check that they contain the keyword 银河科技有限公司"

## Capabilities
> ⚠️ **NOTICE:** This skill will permanently delete duplicate or invalid invoice PDF files (e.g., duplicated hashes). Valid matching invoices will be transported securely to an `invoices/` directory, while non-matching invoices will be moved to `invoices/unknown/` in the target directory.

- Fixed PDF extensions (renaming `?`/`？` ending files to `.pdf`)
- Deduplication using MD5 hashing (creates permanent deletion of duplicates)
- Removal of unwanted files (e.g., those containing "行程单" in their filenames)
- Deep scanning to ensure all PDFs possess one of the required buyer/company `keywords` (supports multiple keywords separated by a semicolon `;`)
- Safely moves accurately matched PDF invoices to a dedicated `invoices` folder.
- Safely moves incorrectly matched or unrecognized PDF invoices to a dedicated `invoices/unknown` folder.
- Extraction and calculation of a Grand Total across all valid invoices

## Installation & Usage

You can seamlessly integrate this AI Skill into your OpenClaw environment in three ways:

### Option A: Automated Installation via OpenClaw Chat
You can simply ask OpenClaw to install this skill for you:
> "Please help me install https://github.com/jie/FapiaoClaw.git as a skill"

### Option B: Use this repository as your workspace
1. Clone this repository:
   ```bash
   git clone https://github.com/jie/FapiaoClaw.git
   cd FapiaoClaw
   ```
2. Install Python dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Open the folder in OpenClaw. OpenClaw will automatically detect and load the skill from `.github/skills/`.

### Option C: Install into your existing project
If you want to add this skill to your own existing project:
1. Copy the `invoice-processing/` directory to your project's `.github/skills/` directory.
2. Copy `main.py` and `requirements.txt` to the root of your project.
3. Install dependencies using `pip install -r requirements.txt`.
4. Open your project in OpenClaw. OpenClaw will automatically detect the newly added skill.

### Trigger The Skill
Once installed via Option A or B, interact with the OpenClaw chat:
- "Please process the invoices in the current directory. The keywords are 'CompanyA;CompanyB'."
- "帮我整理发票，在目录 fapiao 下，要求包含关键字 银河科技 或者 某讯。 (Agent will construct '银河科技;某讯')"

Because the skill file is located in `invoice-processing/`, OpenClaw automatically parses the instructions and safely runs the terminal commands for you.

---

# FapiaoClaw - 发票整理 AI 技能

FapiaoClaw 是一个专用的 Python 工具，也是一个可供安装的 **OpenClaw AI Skill (AI技能)**。它能自动整理、过滤和汇总中文电子发票（PDF 格式）。

通过将此工具集成到您的工作区，OpenClaw（以及 Workbuddy）即可通过自然语言指令原生处理文件夹中的大量发票：
> "帮我整理 ./fapiao 目录下的发票，检查它们是否包含关键字 银河科技有限公司"

## 核心功能
> ⚠️ **通知：** 在使用前**务必备份好您的文件**！本项技能会直接删除与重复的文件，而会将包含关键字的合格发票会保存至 `invoices` 文件夹下，其余未识别或没有匹配关键字的文件会保存至 `invoices/unknown`。

- 修复 PDF 后缀（将以 `?` 或 `？` 结尾的文件重命名为 `.pdf`）
- 基于 MD5 哈希校验剔除重复发票（彻底移除数据）
- 移除无效文件（例如文件名中包含 "行程单" 的文件）
- 深度扫描发票内容，确保所有发票均包含指定的**公司/购买方名称关键字**（支持用分号 `;` 分隔提供多个关键字，满足其一即视为有效发票）
- 安全移动符合关键字的PDF发票至 `<目标目录>/invoices`
- 安全移动不匹配或无法识别的PDF发票至 `<目标目录>/invoices/unknown`
- 自动提取并汇总所有有效发票的总计金额

## 安装与使用

您可以通过以下三种方式在您的 OpenClaw 环境中安装和使用此 AI 技能：

### 方式一：通过 OpenClaw 聊天自动安装
您可以直接让 OpenClaw 自动为您安装此技能：
> "请帮我安装 https://github.com/jie/FapiaoClaw.git 这个SKILL"

### 方式二：直接使用本仓库作为工作区
1. 克隆本仓库到本地：
   ```bash
   git clone https://github.com/jie/FapiaoClaw.git
   cd FapiaoClaw
   ```
2. 安装 Python 依赖库：
   ```bash
   pip install -r requirements.txt
   ```
3. 在 OpenClaw 中打开该仓库文件夹。OpenClaw 会自动从 `.github/skills/` 目录挂载该技能。

### 方式三：安装到您现有的项目中
如果您希望将整理发票的功能添加到自己的项目中：
1. 将本仓库下的 `invoice-processing/` 文件夹复制到您自己项目的 `.github/skills/` 目录下。
2. 将 `main.py` 和 `requirements.txt` 复制到您项目的根目录中。
3. 运行 `pip install -r requirements.txt` 安装所需依赖。
4. 在 OpenClaw 中加载您的项目，OpenClaw 即会自动识别到新放入的技能。

### 触发 AI 技能
完成上述任何一种方式的安装后，您可以直接向 OpenClaw 发送自然语言指令：
- "Please process the invoices in the current directory. The keywords are 'CompanyA;CompanyB'."
- "帮我整理当前目录里的发票，要求包含关键字 银河科技 或者是 某讯。(Agent will construct '银河科技;某讯')"

由于技能规范文件存在于 `invoice-processing/` 之中，OpenClaw 会自动解析您的意图，并在终端为您安全地执行底层 Python 脚本。
