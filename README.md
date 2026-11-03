# 学习问题反馈墙

同学们填写现阶段的学习难点与课程困惑，提交后汇总到公示栏，老师与同学可直接查看。页面是纯静态文件，数据存放在腾讯云开发 CloudBase（PostgreSQL）。

- 线上地址：<https://pioneer-stomic-d9gvr5ztg66f4d931-1524448489.tcloudbaseapp.com/>
- 备用入口：<https://pioneer-stomic.github.io/opensurvey/>（自动跳转到线上地址）
- 数据表：`public.feedback`

## 功能

- **提交**：学习难点（必填，5–1000 字）、姓名（选填，留空显示「匿名」）、课程（选填）
- **公示栏**：按提交时间倒序，30 秒自动刷新
- **管理员**：右上角登录后可删除单条反馈；密码只保存在数据库函数里，不在本仓库
- **视觉**：Neumorphism（新拟物派）单色系 + 双光源阴影，响应式适配手机

## 文件

| 文件 | 说明 |
|---|---|
| `index.html` | 页面结构（表单、公示栏、管理员弹窗） |
| `styles.css` | 新拟物样式与响应式布局 |
| `app.js` | 交互、渲染、轮询、管理员逻辑 |
| `api.js` | 数据层（CloudBase PostgreSQL 查询与 RPC） |
| `validation.js` | 前后端共用的表单校验 |
| `config.js` | CloudBase 环境 ID 与 Publishable Key |
| `.nojekyll` | 静态托管占位文件 |

## 更新与发布

1. 修改文件后 push 到 `main`
2. CloudBase 控制台 → 静态网站托管 → 应用部署列表 → 点「部署」
3. 页脚会显示构建版本号；若仍是旧页面，按 Ctrl+F5 强制刷新

## 技术说明

- 前端为原生 HTML/CSS/ES Modules，无构建步骤
- 数据访问：`cloudbase.init({ env, accessKey })` + `app.rdb()`（PostgREST 风格）
- 权限：`anon` 角色只有 `SELECT` / `INSERT`；删除通过带密码校验的数据库函数 `admin_verify` / `admin_delete` 完成
