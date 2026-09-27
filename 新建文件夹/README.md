# ☣ 八五生化部 · 机密文件管理系统

一个黑客终端风格的恶搞机要档案网站：启动自检 → 口令闸机 → 绝密文书（三篇纪实风"案件通报/调查报告/审判实录"）→ 部门唯一在编人员「牢电工」的宣传档案。

**技术栈**：React 19 + Vite 7 + Tailwind CSS 4 + framer-motion + lucide-react
**构建产物**：`dist/index.html` —— **全量自包含单文件**（JS / CSS / 图片全部内联，零外部路径依赖），可直接架设于任意静态托管。

---

## 一、部署到 GitHub Pages

### 方式 A：GitHub Actions 自动部署（推荐）

仓库已内置工作流 [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml)：

1. 把整个项目推送到 GitHub 仓库的 `main` 分支；
2. 打开仓库 **Settings → Pages → Source**，选择 **GitHub Actions**；
3. 回到 **Actions** 页签等待 "Deploy to GitHub Pages" 绿灯；
4. 访问 `https://<用户名>.github.io/<仓库名>/`。

> 之后每次 `git push`，站点都会自动重新构建发布，无需任何手动操作。
> 若默认分支是 `master`，把 workflow 里的 `branches: [main]` 改掉即可。

### 方式 B：手动上传（30 秒搞定）

```bash
npm install
npm run build
```

构建完成后，`dist/` 里只有一个 `index.html` —— CSS、JS、图片已全部内联。
你可以：

- 直接把该文件上传到一个启用了 Pages 的仓库（Settings → Pages → **Deploy from a branch**），路径保持 `index.html`；
- 或者丢进 Netlify / Vercel / Cloudflare Pages / 对象存储 / 服务器上任何能被访问到的目录；
- 甚至直接**双击本地打开**也能完整运行（无路由、无路径依赖）。

> `public/.nojekyll` 会随构建进入 `dist/`，可防止 Pages 的 Jekyll 处理吞掉下划线开头的文件。

---

## 二、本地开发

```bash
npm install     # 安装依赖
npm run dev     # 本地调试（默认 http://localhost:5173）
npm run build   # 产出 dist/index.html
```

<details>
<summary>🔑 访问口令（剧透警告）</summary>

口令藏在**开机自检日志**里（那串以 .bit 结尾的密钥）。
实在找不到：`1145141919810`。好时代，来临罢。

</details>

---

## 三、项目结构

```
├── .github/workflows/deploy.yml   # GitHub Pages 自动部署工作流
├── public/.nojekyll               # 关闭 Pages 的 Jekyll 处理
├── src/
│   ├── assets/lao-diangong.jpg    # 人物标准像（构建时 base64 内联）
│   ├── components/
│   │   ├── Effects.tsx            # CRT 覆盖层 / 故障文字 / 涂抹解密条
│   │   ├── MatrixRain.tsx         # Canvas 矩阵雨背景
│   │   ├── BootSequence.tsx       # 开机自检动画
│   │   ├── LockScreen.tsx         # 口令验证闸机
│   │   ├── Archive.tsx            # 档案系统主界面 + 文书阅读器
│   │   └── Personnel.tsx          # 「牢电工」人物宣传档案
│   ├── data/documents.ts          # 三份机密文书全文数据
│   ├── App.tsx                    # 阶段状态机：boot → lock → main
│   └── index.css                  # 扫描线 / 噪点 / 故障抖动等特效
└── vite.config.ts                 # vite-plugin-singlefile 单文件构建
```

## 四、设计特性

- 全流程终端仪式感：BIOS 自检 → 口令验证（含错误冷却与蜂鸣警报）→ 解密过场 → 文书显影
- `████` 机要涂抹条：点击临时还原，符合保密条例（并不）
- 文书为纯数据驱动（`documents.ts`），想加新"案件"只需往数组里追加一份台账
- 全屏 CRT 特效层：扫描线、噪点、暗角、扫描光带、矩阵雨，可随开关调节

---

*本系统纯属虚构恶搞。文中一切人名、机构、"美味饮料"均存在于传说中。请勿在现实中酿造。*
