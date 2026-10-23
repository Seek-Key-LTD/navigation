# navigation — git4ta.fun 总览门面站

`git4ta.fun` 的<strong>总览 / 导航</strong>静态站点，部署到 <strong>Cloudflare Pages</strong>。

## 定位

- 现阶段为<strong>非盈利期</strong>，所有主体统一挂在同一个<strong>个体工商户</strong>名下，
  `git4ta.fun` 是其<strong>唯一主体域名</strong>。
- 本站是域名根节点的<strong>总览门面</strong>；七朵小花内容站（六朵以 NotionNext 承载，紫罗兰以 3DGS 承载）按<strong>前缀 / 子路径</strong>
  挂载于本域名之下（如 `/moli/`、`/muxu/` …、`/ziluolan/`），SEO 权重回流到这一枚域名。
- 纯静态、零外部依赖、零构建工具（隐私友好、CF Pages 直读根目录）。

## 署名（不入站）

- 导航页只展<strong>七朵小花</strong>；<strong>格竹阁</strong>（夏竹 · 司马光笔，阁主本名）<strong>不入导航页</strong>，仅在此 README 与文档侧栏署名。
- 取意「你们负责演，我负责写」：阁主是写人的人，凌驾群芳而不并列成花。
- 紫罗兰为第七位，即 <strong>Hermes 智能体</strong>（不受控黑盒），主理【无人值守 · 自运维 · 华夏祭坛】（3DGS / 太虚幻境入口），并含 <strong>forecast</strong>（虚拟现实 · 未来交互处理）；与组织<strong>若即若离</strong>。
- <strong>华夏祭坛 · 双向 reference</strong>：「紫罗兰 · 紫府台」=《鲲鹏志 · 无人值守自运维华夏祭坛》（主组织 <code>seekkey</code>，即你说的「CK」）。
  - 规范正典（源）：<code>seekkey/kunpengzhi-altar</code>｜上层 <code>seekkey/kunpengzhi</code>｜AI 分叉 <code>seekkey/kunpengzhi-ai</code>（记忆银行 / 辩论引擎）。
  - 在线装置：https://altar.git4ta.fun/ ｜ 主线正典文字稿：https://podcast.git4ta.fun/ 。
  - <strong>正向</strong>：本页「紫罗兰 · 紫府台」卡片已直链 <code>altar.git4ta.fun</code>。<strong>反向</strong>：祭坛 README 需补一行「← 返回总览 https://git4ta.fun/」回指本站（该仓有 <code>.cnb.yml</code>/<code>.gitea</code> 触发，不擅推 main，交主理人 / PR / 信号灯落地）。

## 文件

| 文件 | 作用 |
| --- | --- |
| `index.html` | 总览首页（七朵小花 + 域名定位） |
| `styles.css` | 全站样式（系统字体、响应式、无外链） |
| `404.html` | CF Pages 识别的 404 页 |
| `robots.txt` | 允许全爬 + 指向 sitemap |
| `sitemap.xml` | 目前仅根路径；小花挂出后逐条补充 |
| `_headers` | CF Pages 安全响应头（nosniff / X-Frame-Options 等） |

## 上线现状（2026-10-23 校准）

| 项 | 值 |
| --- | --- |
| Gitea 真相源 | `media/navigation`（本仓） |
| GitHub 镜像 | `Seek-Key-LTD/navigation`（default branch `main`，内容逐文件一致） |
| CF Pages 项目 | `navigation`（源 = GitHub，`production_branch=main`） |
| Pages 子域 | `https://navigation-ep9.pages.dev/` |
| apex 自定义域 | `git4ta.fun` → CNAME `navigation-ep9.pages.dev`（自定义域 status=active，证书已签） |
| 构建 | 免构建（`build_command` 空），输出目录 = 仓库根 |
| pages.dev 封锁 | `_headers` 内 `X-Robots-Tag: noindex, nofollow`（**CF 的 pages.dev 无法真正禁用**，官方只提供 noindex 或 zone 级 Bulk Redirect；本账号 token 无 rulesets 权限） |

**回滚**：把 apex CNAME 改回 `68e19eebeab09d56.vercel-dns-017.com` 即可（Vercel 部署已由主理人删除）。

> ⚠️ **CF Pages 的两条硬约束（2026-10-23 实测）**：
> ① `_headers` 里**不能写 `Location`** —— 它不在 CF Pages 的 header 白名单内，会让
>    响应处理挂住，表现为 TLS 握手正常、证书正常、但响应永远不回来（连部署 URL 都空）。
> ② `_redirects` **只按 path 匹配、不区分 host** —— 写 `/* → 主体域` 会把主体域自己也跳走，
>    形成 301 死循环。
>    要做「仅 pages.dev 跳转、主体域不动」，只能用 zone 级 Bulk Redirect（需更高权限）或 Worker。
>
> ⚠️ **内网注意**：内网 DNS（AdGuard CT122）有 300s TTL 缓存，割接后短时间内仍可能解析到
> 旧 Vercel IP 并看到 404。**这是缓存，不是配置错误**——等 TTL 过期即恢复。
> 验证方法：`dig +short @alfred.ns.cloudflare.com git4ta.fun A` 看权威答案。

## Cloudflare Pages 部署设置

纯静态、无需构建：

- **Build command**：留空（no build）
- **Output directory**：`.` 或 `/`（即仓库根目录）
- **Production branch**：`main`

自定义域名 `git4ta.fun` 的绑定与 DNS 由基础设施侧统一管理（CF 单账号）。
仓库本身不含任何机密，站点内容即为公开展示内容。

## 治理

- 六席站点配置与上线流程归口内网 `media/notion-ops`（`seats.yaml` / `runbook.md`）。
- 上线后按 notion-ops 规矩跑 `seo-audit.sh <域名>`。
