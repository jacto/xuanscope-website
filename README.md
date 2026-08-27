# XuanScope 官网（GitHub Pages 静态站）

落地页 + 隐私政策 + 服务条款，纯静态零依赖，直接部署到 GitHub Pages。

## 目录结构

```
website/
├── index.html      # 落地页（含 Hero/功能/钓鱼专区/订阅对比/FAQ）
├── privacy.html    # 隐私政策（与 App 内 assets/agreement/privacy_policy.md 同步）
├── terms.html      # 服务条款（与 assets/agreement/service_agreement.md 同步）
├── assets/style.css
└── CNAME           # 自定义域名（当前 xuanscope.com，买好域名后按需修改）
```

## 部署步骤（约 10 分钟）

### 1. 建仓库
在 GitHub 建一个**公开**仓库，名字随意（如 `xuanscope-website`；如果建 `你的用户名.github.io` 则直接成为主站）。

### 2. 推送本目录内容
把 `website/` 里的**所有文件**（含 CNAME）推到仓库 main 分支根目录：

```bash
cd website
git init && git add -A && git commit -m "init site"
git remote add origin https://github.com/<你的用户名>/xuanscope-website.git
git push -u origin main
```

### 3. 开启 Pages
仓库 **Settings → Pages → Build and deployment → Source: Deploy from a branch**，选 `main` / `(root)`，保存。1 分钟后访问 `https://<你的用户名>.github.io/xuanscope-website/` 应能看到落地页。

### 4. 绑定自定义域名（买好域名后）
1. 修改仓库里的 `CNAME` 文件为你的域名（当前写的是 xuanscope.com）
2. 到域名注册商 DNS 管理，添加两条记录：

   | 类型 | 主机 | 值 |
   |------|------|-----|
   | A | `@` | `185.199.108.153` |
   | A | `@` | `185.199.109.153` |
   | A | `@` | `185.199.110.153` |
   | A | `@` | `185.199.111.153` |
   | CNAME | `www` | `<你的用户名>.github.io` |

3. 回到 Settings → Pages → Custom domain 填入域名，等 DNS 生效后勾选 **Enforce HTTPS**
4. （建议）按 Pages 页面提示添加域名验证 TXT 记录，防域名被他人抢绑

### 5. 回填到 App
域名生效后，把两个 URL 填入 `app/.../data/config/AppConfig.kt`：
```kotlin
val serviceAgreementUrl: String = "https://xuanscope.com/terms.html",
val privacyPolicyUrl: String = "https://xuanscope.com/privacy.html",
```
App 内"关于/协议"页会自动切换为网页版展示。**Google Play 上架表单的隐私政策 URL 也填这个地址。**

## 后续维护

- **协议同步**：法律文本改动时，同时改 App 内 `assets/agreement/*.md` 和本站 `privacy.html` / `terms.html`，保持一致
- **定价**：`index.html` 订阅区价格目前是 TBA，Play 后台配好订阅价格后回来替换
- **Play 链接**：全部指向 `https://play.google.com/store/apps/details?id=com.xuanscope`，App 上架后自动生效
- **图片素材**：当前 Hero 区是纯 CSS 示意图；有真机截图/宣传视频后替换为 `<img>` / YouTube 嵌入
- 本地预览：直接双击 `index.html` 用浏览器打开即可
