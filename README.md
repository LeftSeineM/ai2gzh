# ai2gzh

让 AI 把素材写成公众号文章、排版，并真正发表后返回微信链接。

> 使用 $ai2gzh，把我提供的德国旅行照片和笔记整理成游记，配好封面，发表到公众号，不群发给粉丝。

**这是给 AI 助手使用的 Skill，不是独立发文软件或微信公众号官方 SDK。** 它需要助手具备浏览器/桌面自动化能力，并能操作你自己的公众号登录会话。

## 能做什么

- 根据真实素材写作、拟标题、整理 HTML 排版和封面。
- 操作个人订阅号网页后台，完成编辑、封面裁剪、AI 内容声明和正式发表。
- 区分草稿、待扫码、审核中、失败和已发表，返回正式文章链接。
- 默认不群发；防止超时或重启导致重复发表。

实际验证过个人订阅号的网页发表路径：填写文章 → 上传并裁剪封面 → 声明 AI 生成 → 关闭群发通知 → 发表 → 取得正式微信链接。页面和账号验证要求可能变化，需要按当前页面适配。未承诺免扫码或全程无人值守。

## 安装到 Codex

把本仓库放到 Codex 的 skills 目录，目录名为 `ai2gzh`：

```powershell
# Windows PowerShell；已存在该目录时不要覆盖，先检查已有内容。
$skillRoot = if ($env:CODEX_HOME) { Join-Path $env:CODEX_HOME 'skills' } else { Join-Path $env:USERPROFILE '.codex\skills' }
New-Item -ItemType Directory -Force -Path $skillRoot | Out-Null
git clone https://github.com/LeftSeineM/ai2gzh.git (Join-Path $skillRoot 'ai2gzh')
```

```bash
# macOS / Linux
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone https://github.com/LeftSeineM/ai2gzh.git "${CODEX_HOME:-$HOME/.codex}/skills/ai2gzh"
```

在支持加载该 Skill 的新会话中使用 `$ai2gzh`。其他支持 `SKILL.md` 的助手可按自身技能目录约定安装；未逐一验证所有客户端。

## 示例

**先预览**

> 用 $ai2gzh，根据这些笔记写一篇公众号文章，先给我预览，不要发表。

**授权发表**

> 这篇成稿可以发表了。用 $ai2gzh 发布到我已登录的公众号，不群发，完成后给我正式链接。

**从旅行素材开始**

> 用 $ai2gzh，把附件里的柏林和慕尼黑旅行笔记写成游记。不要编造经历，照片按内容插入。

若只有“帮我写德国游记”而没有个人经历，助手会询问素材，或按你的要求写明确标注的虚构示例/通用攻略。

## 账号和费用

公众号登录、二维码验证和接口权限由微信决定。Skill 不包含账号、Cookie、API 密钥、私有服务地址或收费模型额度。使用的模型和浏览器工具由你的 AI 助手环境提供；外部模型调用按你授权的账号计费。

## 仓库结构

- `SKILL.md`：技能入口。
- `agents/openai.yaml`：Codex 展示元数据。
- `references/browser-publish.md`：实际网页流程及易错点。
- `references/result-check.md`：成功判据与防重复发表。

本项目与微信、腾讯、秀米无隶属关系。
