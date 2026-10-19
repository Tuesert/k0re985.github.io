# 小小星球 · Decap CMS + GitHub Pages

这是一个童趣风格的静态博客，文章和主页设置由 Decap CMS 管理，内容存入 GitHub 仓库。网站部署在 GitHub Pages。

## 本项目包含

- `index.html`：博客前台，读取 `content/site.yml` 并显示文章。
- `admin/index.html`：Decap CMS 后台入口。
- `admin/config.yml`：后台配置，使用 Decap Turbo 托管认证，不含访问令牌或客户端密钥。
- `content/site.yml`：主页文字与示例文章。
- `images/uploads/`：文章封面图片上传目录。

## 重要说明

Decap Turbo 为 CMS 提供托管认证和 GitHub API 代理。你仍然需要在 Turbo 控制台连接 GitHub、创建站点，并把生成的 Site ID 填入 `admin/config.yml`。不要把 GitHub Personal Access Token、OAuth client secret 或其他密钥放进公开文件。

## 部署步骤

### 1. 上传项目文件

1. 登录 GitHub，打开仓库：`https://github.com/k0re985/k0re985.github.io`
2. 下载并解压本项目压缩包。
3. 将解压后所有文件和文件夹上传到仓库根目录（不是把整个外层文件夹再套一层上传）。
4. 如果仓库已经有自己的 `index.html` 或其他文件，先下载备份；上传时确认需要替换哪些文件，避免覆盖你已有的内容。
5. 提交更改到 `main` 分支。

### 2. 打开 GitHub Pages

仓库 Settings → Pages → Build and deployment，选择 `Deploy from a branch`，分支 `main`，目录 `/(root)`。保存后等待部署。对于 `k0re985.github.io` 这种用户名站点仓库，预期网址是 `https://k0re985.github.io/`。

### 3. 设置 Decap Turbo 托管认证

1. 打开 https://turbo.decapcms.org/ 并注册/登录 Decap Turbo。
2. 在组织的 Git connection 中安装/连接 Turbo GitHub App，并授权访问 `k0re985/k0re985.github.io` 这个仓库。建议只授权这个仓库，而不是所有仓库。
3. 在 Turbo 的 Sites 页面创建一个站点：
   - Git provider：GitHub
   - Repository：`k0re985/k0re985.github.io`
   - Branch：`main`
   - Config path：`admin/config.yml`
   - Admin interface URL：`https://k0re985.github.io/admin/`
4. 创建后，在站点 Overview 页面复制 Site ID（UUID）。
5. 在 GitHub 仓库中打开 `admin/config.yml`，把
   `REPLACE_WITH_DECAP_TURBO_SITE_ID`
   替换成实际 Site ID，然后提交更改。
6. 等待 GitHub Pages 重新部署，再访问 `https://k0re985.github.io/admin/`。
7. 使用 Decap Turbo 登录流程登录，并确认自己有该站点的访问权限。

官方说明：
- Turbo 开始使用：https://decapcms.org/docs/turbo-getting-started/
- 连接站点和配置： https://decapcms.org/docs/turbo-connecting-a-site/
- Decap CMS 配置：https://decapcms.org/docs/configure-decap-cms/

## 日常写博客

1. 打开 `https://k0re985.github.io/admin/`。
2. 登录后选择「主页与文章」→「主页设置与博客文章」。
3. 修改主页文字，或在「博客文章」里新增、编辑、删除文章。
4. 上传封面图片（可选），点击保存/发布。
5. Decap CMS 会把内容提交到 GitHub 仓库的 `content/site.yml`；GitHub Pages 更新后，公开首页会显示新内容。

## 故障排查

- 后台提示需要 `turbo_site_id`：确认 `admin/config.yml` 里已经填入真实 Site ID，不是占位文字。
- 登录被拒绝：确认 Turbo Site 的 Admin interface URL 精确包含 `https://k0re985.github.io/admin/`，GitHub App 已授权目标仓库，且当前 Turbo 用户有此站点访问权限。
- 首页显示“加载失败”：确认 `content/site.yml` 在仓库根目录下的 `content/` 文件夹中，并且 YAML 文件有效。
- 修改后网页暂时没更新：等待 Pages 部署完成并刷新浏览器。
- 首页是静态页面，因此内容会通过 YAML 数据渲染；本项目没有把任何 API 密钥写入前端。

## 隐私提醒

GitHub Pages 上的网页是公开的。请勿将个人隐私、密码、令牌或私密日记上传到公开仓库。
