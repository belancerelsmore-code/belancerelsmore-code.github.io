# 个人主页 · 静态站点（GitHub Pages）

这是个人网页的**静态导出版本**，由 Next.js `output: 'export'` 生成，可直接部署到 GitHub Pages。
包含首页以及所有跳转页面：产品 PRD、产品原型、策略视频、简历 PDF 等。

## 一、上传到 GitHub

因为你使用的是 **用户主页域名** `https://belancerelsmore-code.github.io/`，
仓库名必须**正好等于** `belancerelsmore-code.github.io`（在账号 `belancerelsmore-code` 下创建）。

1. 在 GitHub 新建仓库，名称填：`belancerelsmore-code.github.io`（Public）。
2. 把**本文件夹里的所有内容**（不是这个文件夹本身）上传到仓库根目录。
   - 网页上传：进入仓库 → Add file → Upload files → 把文件夹内所有文件拖进去。
   - 或用命令行（在本文件夹内执行）：
     ```bash
     git init
     git add -A
     git commit -m "deploy personal site"
     git branch -M main
     git remote add origin https://github.com/belancerelsmore-code/belancerelsmore-code.github.io.git
     git push -u origin main
     ```
   > 注意：`.nojekyll` 是隐藏文件，务必一并上传（它让 GitHub 正确加载 `_next/` 目录，缺失会导致样式/脚本全部 404）。

## 二、开启 GitHub Pages

仓库 → Settings → Pages →
- Source 选 **Deploy from a branch**
- Branch 选 **main**，目录选 **/ (root)** → Save

约 1 分钟后访问：**https://belancerelsmore-code.github.io/**

## 三、以后想绑定自己的域名（可选）

1. 在本目录新增一个名为 `CNAME` 的文本文件，内容只写你的域名，例如：
   ```
   www.yourdomain.com
   ```
2. 在域名服务商处配置 DNS：
   - **www 子域名**：加一条 `CNAME` 记录，指向 `belancerelsmore-code.github.io`
   - **根域名 (apex)**：加 `A` 记录指向 GitHub Pages 官方 IP（185.199.108.153 / .109.153 / .110.153 / .111.153）
3. 提交 `CNAME` 文件后，在 Settings → Pages → Custom domain 填入并勾选 Enforce HTTPS。

## 四、以后修改网页后如何重新生成本文件夹

回到源码项目 `个人网页` 目录：
```bash
pnpm build          # 生成最新的 out/ 目录
```
然后把 `out/` 里的全部内容覆盖到本文件夹（保留 `.nojekyll`），重新提交即可。

---
静态导出说明：`next.config.mjs` 已设置 `output: 'export'` 与 `images.unoptimized: true`；
所有资源使用根路径 `/`，与用户主页域名的根目录一致，无需 `basePath`。
