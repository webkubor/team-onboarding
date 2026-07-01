# 🧭 小白看板 — 让 Agent 带你写代码

> 👤 **你是新手？来对地方了。** 你只说话，Agent 帮你搞定所有操作。
>
> 🎯 不需要懂代码、不需要懂 API、不需要懂命令行。
> 你只需要两件事：**说清楚你要什么，看结果满不满意。**

---

## ⚡ 先别往下翻，花 10 秒做一件事

**对 Agent 说下面这句话：**

> 「你是什么 Agent？用大白话告诉我。」

Agent 会告诉你它是什么。记住它的名字，后面会用到。

> 💡 如果 Agent 回复的内容你看不懂，复制它的回复，继续对它说：「用大白话解释，像跟小学生说话一样。」

---

## 🧭 导航：从这里开始

如果你是**第一次听说 Agent**，按顺序看：

| 序号 | 看这篇 | 花多久 | 看完你会 |
|:--:|--------|:------:|---------|
| ① | [Agent 是什么？](./docs/what-is-agent.md) | 3 分钟 | 知道这玩意跟豆包有什么区别 |
| ② | [我为什么要用？](./docs/why-agent.md) | 3 分钟 | 知道 Agent 能帮你做什么事 |
| ③ | [3 分钟第一次实战](./docs/first-project.md) | 3 分钟 | 亲自指挥 Agent 做出一个网页！ |
| ④ | 回到本页继续 ↓ | — | 开始装工具、学流程 |

如果你想**先试试再看理论**，直接从 ③ 开始。

---

## 🗺️ 完整学习路径

### 🌱 预备知识（零代码必读）

| 文档 | 说明 |
|------|------|
| [Agent 是什么？](./docs/what-is-agent.md) | Agent vs 豆包，用类比讲清楚 |
| [我为什么要用 Agent？](./docs/why-agent.md) | 能帮你做什么？值不值得学？ |
| [术语大白话词典](./docs/glossary.md) | Git、Token、CLI……遇到不懂的词来查 |
| [怎么跟 Agent 说话](./docs/how-to-speak-to-agent.md) | 万能公式，让 Agent 更懂你 |

### 🚀 动手实践

| 章节 | 你能学到什么 |
|------|-------------|
| [3 分钟第一次实战](./docs/first-project.md) | 亲自指挥 Agent 做一个网页 |
| [环境自检](#第零步自检先跑这个30-秒搞定) | 30 秒检查你的电脑准备好了没 |
| [安装工具](#第一步安装-cli-工具) | 装 Git、GitLab CLI、GitHub CLI |
| [登录配置](#第二步登录gitlab--github) | Token 申请 + 安全存储 |
| [项目管理](#第三步项目管理gitlab--github-通用) | 创建/克隆/推送项目 |
| [Git 工作流](#第四步gitflow-工作流每天用的) | 每天怎么用 Git 干活 |
| [用 AI 写代码](#第五步用-ai-写代码) | 怎么跟 Agent 说话让它帮你写 |

### 🛠️ 进阶技能

| 章节 | 你能学到什么 |
|------|-------------|
| [提 Bug / 反馈](#提-bug--反馈) | 怎么规范地报告问题 |
| [常见踩坑](#️-常见踩坑agent-推不上去看这里) | 推不上去？权限不够？看这里 |
| [配套工具](#配套工具) | Keyring / Agent Eyes 等生态 |
| [Agent 配合手册](./AGENTS.md) | Agent 怎么读 AGENTS.md 执行任务 |

---

## 支持的 Agent

你想用哪个都行，文档里都写了怎么配合。

| Agent | 一句话描述 | 适合谁 |
|-------|-----------|--------|
| 🧠 **Hermes Agent** | 最聪明，能同时让多个小助手并行干活 | 有服务器的人 |
| 🦞 **OpenCLAW** | 轻量灵活，跟 Hermes 差不多 | 喜欢简单的人 |
| 📝 **Claude Code** | 稳扎稳打，一步一步来 | 用 Claude 的人 |
| 🔧 **Codex** | OpenAI 家的，后台异步不卡顿 | 用 ChatGPT/Codex 的人 |

---

## 第零步：自检（先跑这个，30 秒搞定）

> 🤖 **Agent 请读 [AGENTS.md](./AGENTS.md)**。下面这个脚本 Agent 会帮你跑，你不需要自己敲。

对你 Agent 说：「帮我跑一下环境自检脚本。」

<details>
<summary>📋 自检脚本（Agent 专用，你不用看）</summary>

```bash
echo "===== 检查环境 ====="

# 1. Git
if git --version > /dev/null 2>&1; then
  echo "✅ Git 已安装: $(git --version)"
else
  echo "❌ Git 未安装 → 去 https://git-scm.com 下载"
fi

# 2. GitLab CLI
if glab version > /dev/null 2>&1; then
  echo "✅ glab（GitLab）已安装: $(glab version 2>&1 | head -1)"
else
  echo "⚠️  glab 未安装 → 看下面「第一步」"
fi

# 3. GitHub CLI
if gh --version > /dev/null 2>&1; then
  echo "✅ gh（GitHub）已安装: $(gh --version 2>&1 | head -1)"
  if gh auth status > /dev/null 2>&1; then
    echo "✅ gh 已登录: $(gh api user 2>/dev/null | python3 -c 'import sys,json;print(json.load(sys.stdin).get(\"login\",\"?\"))' 2>/dev/null || echo 'ok')"
  else
    echo "⚠️  gh 未登录 → 对 Agent 说「帮我登录 GitHub」"
  fi
else
  echo "⚠️  gh 未安装 → 看下面「第一步」"
fi

# 4. GitLab 登录状态 & 账户信息
if glab auth status > /dev/null 2>&1; then
  echo "✅ glab 已登录"
  echo ""
  echo "===== 账户信息 ====="
  glab api user 2>/dev/null | python3 -c "
import sys,json
u=json.load(sys.stdin)
print(f'  用户名: {u.get(\"username\",\"?\")}')
print(f'  邮箱:   {u.get(\"email\",\"?\")}')
print(f'  姓名:   {u.get(\"name\",\"?\")}')
"
  echo ""
  echo "===== 群组权限 ====="
  glab api groups/hym-company 2>/dev/null | python3 -c "
import sys,json
g=json.load(sys.stdin)
if g.get('message')=='401 Unauthorized' or g.get('message')=='404 Group Not Found':
  print('  ❌ 没有 hym-company 群组权限 → 联系管理员加你进组')
else:
  print(f'  ✅ 群组: {g.get(\"full_name\",\"?\")}')
  print(f'  权限:  {g.get(\"access_level\",\"?\")} (10=Guest 20=Reporter 30=Developer 40=Maintainer 50=Owner)')
" 2>&1 || echo "  ⚠️  网络异常，跳过权限检查"
else
  echo "❌ glab 未登录 → 看下面「第二步」"
fi

# 5. Node.js（前端项目需要）
if node --version > /dev/null 2>&1; then
  echo "✅ Node.js: $(node --version)"
else
  echo "⚠️  Node.js 未安装 → https://nodejs.org (LTS 版)"
fi

# 6. Keyring（密钥安全工具）
if ky --version > /dev/null 2>&1; then
  echo "✅ Keyring 已安装"
else
  echo "❌ Keyring 未安装 → pip install keyring-cli && kyi"
  echo "   Windows 如果找不到 pip: py -m pip install keyring-cli && kyi"
fi
```

</details>

根据结果，缺哪个补哪个：

| 检查项 | ✅ | ❌ 怎么办 |
|--------|----|----------|
| Git | 跳过 | [安装 Git](https://git-scm.com) |
| glab（GitLab） | 跳过 | 看第一步 ↓ |
| gh（GitHub） | 跳过 | 看第一步 ↓ |
| GitLab 登录+权限 | 显示用户名和群组权限 | 看第二步 ↓ |
| Node.js | 跳过 | [安装 Node.js LTS](https://nodejs.org) |
| Keyring | 跳过 | `pip install keyring-cli && kyi` |

---

## 第一步：安装 CLI 工具

> **你只需要对 Agent 说**：「帮我安装 GitLab CLI 和 GitHub CLI」

Agent 会自动执行：

<details>
<summary>📋 手动安装命令（Agent 不在身边时备用）</summary>

```bash
# GitLab CLI
# macOS
brew install glab
# Windows
winget install GitLab.GitLabCLI

# GitHub CLI
# macOS
brew install gh
# Windows
winget install GitHub.cli

# 验证
glab version
gh --version
```
</details>

---

## 第二步：登录（GitLab + GitHub）

> **你只需要对 Agent 说**：「帮我登录 GitLab」或「帮我登录 GitHub」

<details>
<summary>📋 手动步骤（Agent 不在身边时备用）</summary>

### GitLab

#### 2.1 申请 Token

1. 打开 https://gitlab.com/-/user_settings/personal_access_tokens
2. Token name: `HYM-Dev`
3. 勾选权限: `api`, `read_repository`, `write_repository`
4. 点 Create personal access token
5. ⚠️ **立刻复制 token**（关掉页面就看不到了）

#### 2.2 Agent 帮你存好

对 Agent 说：「用这个 token 登录 GitLab：`glpat-xxxx`」

### GitHub

#### 2.1 申请 Token

1. 打开 https://github.com/settings/tokens → Generate new token (classic)
2. Note: `HYM-Dev`，勾选: `repo`（全部）、`read:org`
3. 点 Generate token → ⚠️ **立刻复制**

#### 2.2 验证

```bash
glab auth status   # 应该显示 ✓ Logged in
gh auth status     # 应该显示 ✓ Logged in
```
</details>

---

## 第三步：项目管理（GitLab / GitHub 通用）

**你只需要说话，Agent 帮你干活。**

### 3.1 创建新项目

「帮我在 GitLab 创建一个叫 xxx 的项目」

### 3.2 把本地代码推上去

「帮我把这个项目推送到 GitLab」

### 3.3 克隆已有项目

「帮我把 xxx 项目拉下来」

### 3.4 装依赖跑起来

「帮我装依赖并跑起来」

---

## 第四步：GitFlow 工作流（每天用的）

> 你不需要记命令。对 Agent 说「帮我创建新分支」「帮我推送」「帮我提交」，Agent 全搞定。

### Commit 信息规范

| 前缀 | 含义 | 例子 |
|------|------|------|
| `feat:` | 新功能 | `feat: 添加出图页面` |
| `fix:` | 修bug | `fix: 登录按钮不响应` |
| `docs:` | 文档 | `docs: 更新 README` |
| `style:` | UI调整 | `style: 改按钮颜色` |

---

## 第五步：用 AI 写代码

```
你说需求 → AI 写代码 → 你 Review → 跑起来看 → 有问题让 AI 改
```

### 怎么跟 AI 说

```
"帮我在客户端加一个订单列表页面，显示用户名、图片缩略图和下单时间"
"这个页面的按钮点不动，帮我排查一下"
"帮我把这个组件拆成两个，一个负责列表一个负责弹窗"
```

### 原则
1. 说清楚要什么，不用写代码
2. AI 交出来你先看一遍
3. 跑起来验证
4. 不行就让 AI 接着改

---

## 🕳️ 常见踩坑（Agent 推不上去？看这里）

### 坑 1：推 main 分支报权限错误

**Agent 会说**：「main 分支被保护了，需要你去网页上解一下」

**你做**（30 秒）：打开 GitLab 项目设置 → Protected branches → Unprotect main

### 坑 2：根本没进群组

**Agent 会说**：「你的账号没有群组权限」

**你做**：在飞书群「栖洲的 AI 团队」里 @ webkubor

### 坑 3：Token 过期

**Agent 会说**：「Token 有问题，需要重新创建一个」

**你做**：去 GitLab 个人设置重新生成 Token，发给 Agent

---

## 提 Bug / 反馈

不要私聊说"出问题了"，直接在需求池里提。

---

## 配套工具

| 工具 | 用途 | 地址 |
|------|------|------|
| **Keyring** | 安全管理密码/Token | [agent-secret-skills](https://github.com/webkubor/agent-secret-skills) |
| **Smart Router** | Agent 自动省钱 | [smart-router-skills](https://github.com/webkubor/smart-router-skills) |
| **Agent Eyes** | Agent 自动监控前端报错 | [vite-plugin-agent-eyes](https://github.com/webkubor/vite-plugin-agent-eyes) |

---

> 不会就问 Agent，别憋着。Agent 说不明白就来找我们。
