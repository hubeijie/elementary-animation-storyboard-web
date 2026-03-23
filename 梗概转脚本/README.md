# 动画课完整脚本生成器（梗概 + 教研动效 → 五列脚本）

## 你要的效果

- **故事梗概**是叙事主轴，拆成多镜写进脚本，**不会**再单独占一块「参考区」。
- **教研老师的动效说明表**（画面 / 逐字稿 / 动效 / 备注）被 **AI 融合进对应教学镜**（台词里保留知识点与【n】，画面描述里保留可执行动效）。
- 导出 **Excel**：`脚本表·完整剧情` + `教研·（各原表）` 备份。

> 剧情与知识点的「理解、编排、改写」必须依赖 **大模型**。本仓库支持：**Gemini / OpenAI / Claude**（网页或 Python）、以及 **复制提示词到任意聊天模型**。

---

## 方式一：网页 `index.html`

1. 填 **故事梗概**，上传 **教研 .xlsx**。
2. **方式 A**：选择 **服务商**（Gemini / OpenAI / Claude）→ 填 **API Key** 与 **模型** →「调用 API 生成完整脚本」。  
   - **OpenAI / Claude** 官方域名**常被浏览器 CORS 拦截**，若失败请用方式 B 或方式二（Python 无此限制）。
3. **方式 B**：点 **复制提示词** → 粘贴到 **Cursor / ChatGPT / Claude** 等 → 将模型返回的 **Markdown 表**粘回「模型输出」→ **解析表格并下载**。

依赖：需能加载 SheetJS CDN；API Key 仅在你本机浏览器发往对应厂商，**不经过我们的服务器**。

---

## 方式二：本地 Python（推荐 OpenAI / Claude）

```bash
cd elementary-animation-storyboard-web/梗概转脚本
python3 -m venv .venv && source .venv/bin/activate   # Windows 用 .venv\Scripts\activate
pip install -r requirements.txt
```

**Gemini（默认）**

```bash
export GEMINI_API_KEY="你的密钥"
python generate_full_script.py --synopsis synopsis.txt --teaching /path/to/动效说明.xlsx --title "课题名"
```

**OpenAI**

```bash
export OPENAI_API_KEY="sk-…"
python generate_full_script.py --provider openai --model gpt-4o-mini --synopsis synopsis.txt --teaching /path/to/动效说明.xlsx --title "课题名"
```

**Anthropic Claude**

```bash
export ANTHROPIC_API_KEY="sk-ant-…"
python generate_full_script.py --provider claude --model claude-sonnet-4-20250514 --synopsis synopsis.txt --teaching /path/to/动效说明.xlsx --title "课题名"
```

- `--model` 可省略，将使用各服务商内置默认模型。
- 生成文件默认在教研表同目录：`课题名_完整脚本.xlsx`（可用 `--out` 指定）。

---

## 规范口径

与 Cursor Skill **elementary-animation-storyboard-script** 一致：镜号 · 画面 · 台词 · 画面描述 · 备注；【n】对齐；`*复用*`。

---

## 分享同事

可打包整个文件夹；或只发 `index.html`（需能访问 SheetJS CDN）。**不要**在公开场合泄露任何 API Key。
