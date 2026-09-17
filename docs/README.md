# Docs · 学习沉淀笔记

> Writeups 记录"打过的靶场"，Docs 记录"搞懂的概念与踩过的坑"。这一块看起来不如工具亮眼，但它最能让面试官判断你的**基础是否扎实**。

## 适合放这里的四类笔记

| 类型 | 例子 | 为什么值钱 |
|---|---|---|
| **原理长文** | 「HTTP 无状态这件事，怎么一路推导出 CSRF 和越权」 | 展示你理解机制而不是背结论 |
| **对照表** | 「命令执行里 `system`/`exec`/`shell_exec`/`passthru` 的回显差异」 | 一看就知道是真用过的人总结的 |
| **踩坑记录** | 「Burp 改了包为什么打不通：`Content-Length` 没同步更新」 | 踩坑记录最真实，也最容易帮到别人 |
| **版本勘误** | 「教材说 MySQL 直接 `into outfile` 写 shell，但在 MySQL 8 上默认走不通」 | 展示你会核实信息，而不是照抄教程 |

## 命名与格式

- 文件名：`主题.md`，例如 `http-csrf-relationship.md`、`mysql-secure-file-priv.md`
- 正文用「问题 → 结论 → 依据 → 延伸」四段，不用"第一章/第一节"这种学术腔
- 涉及引用时附来源链接（官方文档优先）

## 示例结构

```markdown
# MySQL 8 下为什么 into outfile 写不了 webshell

## 问题
教程里说拿到 SQL 注入后可以用 into outfile 写文件到 Web 目录 getshell，
但我在 MySQL 8 环境上试了直接报错。

## 结论
MySQL 5.7 起引入、8.0 起严格执行 `secure_file_priv`，默认值为 NULL，
会完全禁止 `LOAD_FILE()` 与 `SELECT ... INTO OUTFILE`。

## 依据
- 官方文档：MySQL 8.0 Secure Deployment Guide 中对该变量的说明
  （默认 NULL = 禁用导入导出）
- 实测：`SHOW VARIABLES LIKE 'secure_file_priv';`

## 延伸
写文件还额外需要 FILE 权限 + 目录可写 + 路径在允许范围内。
这三条与文件上传的"四个必要条件"是同一套逻辑：
能写进去 + 能访问到 + 能被解析。
```

> 这篇笔记的写法本身就是个样板：**它同时展示了"会查文档"和"能抽象出规律"两件事**——这两点恰恰是面试官最想看到的。
