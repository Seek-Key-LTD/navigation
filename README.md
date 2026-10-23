# navigation — git4ta.fun 总览门面站

`git4ta.fun` 的<strong>总览 / 导航</strong>静态站点，部署到 <strong>Cloudflare Pages</strong>。

## 定位

- 现阶段为<strong>非盈利期</strong>，所有主体统一挂在同一个<strong>个体工商户</strong>名下，
  `git4ta.fun` 是其<strong>唯一主体域名</strong>。
- 本站是域名根节点的<strong>总览门面</strong>；六朵小花内容站（NotionNext 承载）按<strong>前缀 / 子路径</strong>
  挂载于本域名之下（如 `/moli/`、`/muxu/` …），SEO 权重回流到这一枚域名。
- 纯静态、零外部依赖、零构建工具（隐私友好、CF Pages 直读根目录）。

## 文件

| 文件 | 作用 |
| --- | --- |
| `index.html` | 总览首页（六朵小花 + 域名定位） |
| `styles.css` | 全站样式（系统字体、响应式、无外链） |
| `404.html` | CF Pages 识别的 404 页 |
| `robots.txt` | 允许全爬 + 指向 sitemap |
| `sitemap.xml` | 目前仅根路径；小花挂出后逐条补充 |
| `_headers` | CF Pages 安全响应头（nosniff / X-Frame-Options 等） |

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
