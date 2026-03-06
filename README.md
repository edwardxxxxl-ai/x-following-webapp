# Xfinder

[中文说明](#中文说明) | [English](#english)

![App Screenshot](./assets/app-screenshot.png)

> Find who smart accounts follow, overlap them, and surface hidden nodes.
>
> 通过别人的 X 关注图谱，发现你原本不认识的小众关键账号。

## English

Local web app for mapping X follow graphs on macOS by reusing your logged-in Arc session.

### What It Does

- Input one or more X handles
- Reuse your active Arc login session for X
- Fetch following lists as structured account profiles
- Compute overlap across multiple seed accounts
- Rank accounts with an overlap-first, small-but-important discovery score
- Export Markdown, JSON, and a research brief

### How It Works

This project does not use official X API credentials.

Instead, it:

1. Runs a local Node server
2. Temporarily switches the active Arc tab to `x.com/home`
3. Executes a small in-page script through Arc AppleScript support
4. Reads following lists through X's current web endpoints
5. Enriches each account with profile metadata and topic labels
6. Computes overlap and discovery ranking
7. Returns the result to the local web app as Markdown, JSON, and a research brief

This makes the tool easy to run locally, but also tightly couples it to:

- Arc being installed
- Arc AppleScript behavior
- Your existing X login session in Arc
- X's current web endpoint behavior

### Requirements

- macOS
- Arc browser installed
- Arc open on the machine
- Logged into X inside Arc
- Node.js installed

### Run Locally

```bash
git clone https://github.com/edwardxxxxl-ai/xfinder.git
cd xfinder
npm start
```

Then open:

```bash
http://127.0.0.1:4321
```

### Input

Accepted input examples:

- `odysseyml`
- `@odysseyml`
- `odysseyml reflexrobot`
- one handle per line

### Output

The app currently generates:

- `Markdown`
- `JSON`
- `Research brief`

Profile fields include:

- `screen_name`
- `name`
- `bio`
- `location`
- `url`
- `followers_count`
- `friends_count`
- `statuses_count`
- `verified`
- `protected`
- `created_at`
- `topic_labels`
- `followed_by`
- `followed_by_count`
- `discovery_score`

Example brief excerpt:

```md
# Research Brief: @odysseyml, @reflexrobot

- Seed accounts: 2
- Accounts analyzed: 6
- Overlap accounts: 0
- Ranking logic: prioritize multi-seed overlap first, then rank for small-but-important accounts.

## Potential hidden nodes

- @JonathanSadeghi — followed by 1/2 | score: 1285 | topics: AI, Research
- @rragavender — followed by 1/2 | score: 1250 | topics: Robotics
```

### Project Structure

```text
server.js           Local HTTP server and Arc/X export logic
public/index.html   Single-page UI
public/styles.css   Frontend styling
```

### Limitations

- This is a local automation workflow, not a hosted SaaS app
- It currently depends on Arc, not Chrome or Safari
- X may change internal endpoints at any time
- If Arc blocks AppleScript or X changes page behavior, the exporter may break
- The app temporarily reuses the active Arc tab and then restores its URL
- Discovery ranking is heuristic, not ground truth

### Safety Notes

- The app runs locally on your machine
- It does not require storing X credentials in this repo
- It relies on your already authenticated Arc browser session

Review the code before using it with any sensitive account.

## 中文说明

这是一个本地网页工具：在 macOS 上复用你已经登录在 Arc 里的 X 会话，分析一个或多个账号的关注图谱。

### 它能做什么

- 输入一个或多个 X 用户名
- 复用你当前 Arc 中的 X 登录态
- 抓取 following 列表并转成结构化账号画像
- 计算多个种子账号之间的共同关注
- 按“先看共同关注，再看小而关键”排序
- 导出 Markdown、JSON 和研究简报

### 工作原理

这个项目不依赖官方 X API Key。

它的流程是：

1. 在本机启动一个 Node 服务
2. 临时把 Arc 当前标签切到 `x.com/home`
3. 通过 Arc 的 AppleScript 能力注入一小段页内脚本
4. 读取 X 当前网页可用的 following 接口
5. 补齐 bio、粉丝数、链接等资料
6. 计算交集、主题标签和 discovery score
7. 把结果回传给本地网页，并生成多种输出

这也意味着它依赖以下前提：

- 你的机器上安装了 Arc
- Arc 仍然支持当前这套 AppleScript 控制方式
- 你已经在 Arc 中登录了 X
- X 当前网页接口没有发生破坏性变化

### 运行要求

- macOS
- 已安装 Arc 浏览器
- Arc 处于打开状态
- Arc 中已登录 X
- 本机已安装 Node.js

### 本地运行

```bash
git clone https://github.com/edwardxxxxl-ai/xfinder.git
cd xfinder
npm start
```

然后打开：

```bash
http://127.0.0.1:4321
```

### 输入格式

支持下面几种形式：

- `odysseyml`
- `@odysseyml`
- `odysseyml reflexrobot`
- 每行一个账号

### 输出内容

目前支持三种输出：

- Markdown
- JSON
- 研究简报

账号画像字段包括：

- `screen_name`
- `name`
- `bio`
- `location`
- `url`
- `followers_count`
- `friends_count`
- `statuses_count`
- `verified`
- `protected`
- `created_at`
- `topic_labels`
- `followed_by`
- `followed_by_count`
- `discovery_score`

研究简报会额外给出：

- 主题信号
- 共同关注列表
- 优先研究账号排序

### 项目结构

```text
server.js           本地 HTTP 服务与 Arc/X 导出逻辑
public/index.html   单页前端
public/styles.css   前端样式
```

### 当前限制

- 这是本地自动化工具，不是托管 SaaS
- 目前只适配 Arc，没有适配 Chrome 或 Safari
- X 内部网页接口未来可能随时变动
- 如果 Arc 限制 AppleScript，或 X 改了页面逻辑，这个工具就可能失效
- 工具会临时复用当前 Arc 活动标签页，完成后再把 URL 切回去
- discovery score 是启发式排序，不是绝对结论

### 安全说明

- 工具完全运行在本地
- 仓库本身不保存你的 X 账号密码
- 它依赖的是你 Arc 浏览器中已经存在的登录态

如果你要把它用于敏感账号，建议先自行审查代码。

## License

MIT
