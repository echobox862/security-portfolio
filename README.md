# security-portfolio

> 网络空间安全方向在校生，做 Web 渗透测试与安全工具开发。这里放我的靶场复现笔记、自研小工具和学习沉淀。

⚠️ **本仓库所有内容仅用于授权测试与安全学习。** 靶场地址、账号、凭据、flag 与可用的完整攻击载荷均已脱敏或不收录。

---

## 目录

| 板块 | 内容 | 入口 |
|---|---|---|
| **Writeups** | 靶场复现笔记：漏洞原理、复现步骤、危害与修复建议 | [writeups/](writeups/) |
| **Tools** | 自研安全小工具（Python），含用法与实现说明 | [tools/](tools/) |
| **Docs** | 学习沉淀：协议/工具/环境类长笔记与踩坑记录 | [docs/](docs/) |

---

## Writeups（5 篇）

> 来自 2025 年 6–7 月生产实习期间的课程实验（授权靶场环境）。

| # | 主题 | 漏洞类型 | 关键手法 |
|---|---|---|---|
| 01 | [Tomcat 弱口令 && 后台 getshell](writeups/01-tomcat-weak-password-getshell.md) | 弱口令 + 任意文件部署 | Manager 后台部署 WAR 包 → JSP 被执行 |
| 02 | [sqli-labs Less 1–10](writeups/02-sqli-labs-less1-10.md) | SQL 注入（五种形态） | 联合查询 / 报错 / 布尔盲注 / 时间盲注 / 写文件 |
| 03 | [海洋 CMS 影视站 RCE](writeups/03-haiyang-cms-param-injection-rce.md) | 参数注入 → 任意代码执行 | 参数交叉引用拼接出危险代码 |
| 04 | [XSS 靶场 1–7 关](writeups/04-xss-labs-1-7.md) | 反射型 / 存储型 XSS | 闭合属性、关键词双写、换函数、换事件 |
| 05 | [CatfishCMS 水平越权](writeups/05-catfishcms-idor.md) | 水平越权（IDOR / BOLA） | 修改请求中的对象 id |

**这五篇的覆盖面**：注入类（SQL 注入五种形态、参数注入 RCE）· 文件与执行类（WAR 部署、`into outfile` 写 webshell）· 客户端类（反射型/存储型 XSS 及多种过滤绕过）· 权限类（水平越权）。

## Tools

| 工具 | 能力 | 状态 |
|---|---|---|
| port-scanner | 端口扫描（python-nmap 封装 + socket 多线程） | 待整理 |
| dict-generator | 按正则规则生成定向密码字典 | 待整理 |
| poc-checker | 常见漏洞存在性验证（无破坏性） | 待整理 |

> 工具列表与用法见 [tools/](tools/)；每整理完一个就把"待整理"改成"可用"。

---

## 关于我

- 方向：**安全服务 / 渗透测试（Web 方向）**
- 渗透测试：SQL 注入（联合查询 / 报错 / 布尔盲注 / 时间盲注 / 写文件）、XSS（反射型 / 存储型及过滤绕过）、参数注入 RCE、弱口令与后台 getshell、水平越权（IDOR）
- 工具：Burp Suite（Proxy / Intruder / Repeater）、sqlmap、Kali Linux、WebShell 管理工具
- 安全开发：参数化查询、PBKDF2 密码存储、RBAC 权限模型、操作审计
- 联系方式：GitHub [@echobox862](https://github.com/echobox862)

---

## 贯穿这些笔记的两条判断框架

写笔记时我尽量把单个漏洞归到可复用的判断上，而不是停在"payload 是什么"：

1. **getshell 三元组**：**能写进去 + 能访问到 + 能被解析**。文件上传、WAR 部署、`into outfile` 写 webshell 三种路径都适用；三者缺一，漏洞就利用不成立。
2. **绕过的统一原理**：**过滤发生在字符串层，而解析发生在语义层，两者不一致处就是缝隙**。关键词双写、变量拼接、路径穿越（`..\`）、`%00` 截断，都是这一条的不同形态。

## 仓库约定

- 笔记按「**现象 → 原理 → 复现 → 危害 → 修复 → 延伸**」六段写，不写"我学会了某某"这类空话
- 每个工具都有独立 README，说明**做什么、怎么用、实现思路、已知限制**
- 敏感信息一律脱敏；不上传任何可用后门或攻击载荷
