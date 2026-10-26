# 手机端智能体接入说明

## 可直接转发给手机端的说明

请接入已经存在的学习仓库，不需要重新创建仓库。

- GitHub 账号：`xxyzyl`
- 仓库：<https://github.com/xxyzyl/study-log>
- 仓库名：`study-log`，可见性：公开，分支：`main`。
- 我授权手机端智能体在这个仓库新增、编辑、修改学习记录，与电脑端共同维护。请先读取 `AGENTS.md`、`INDEX.md` 和 `templates/daily.md`。
- 学习日志保存到 `daily/YYYY/MM/YYYY-MM-DD.md`，按北京时间确定日期；我指定日期时以指定日期为准。同一天的补充合并到同一文件。
- 同步更新 `INDEX.md`。保留我提供的学习内容，区分已完成、疑问和计划；不要虚构时长、题量或掌握程度。
- 仓库已公开，仅上传我明确交付的学习材料，不上传聊天中的账号凭据、其他个人资料或无关附件。
- 每次修改前先读取远程最新内容，保留电脑端及手机端已有记录；发生冲突时合并，禁止强制推送或直接覆盖。
- 写入成功后读取 GitHub 上的提交或文件进行核验，并回复日志链接和提交编号。没有写入凭据或接口返回失败时明确报告，不能声称已经同步。
- 不创建截图中曾提到的 `daily-study` 私有仓库，不更改本仓库可见性，不操作其他仓库。

## GitHub 权限配置

用户要求的授权配置为：

| 项目 | 配置 |
| --- | --- |
| 类型 | Fine-grained personal access token |
| 名称 | `study-log-mobile-trae` |
| Resource owner | `xxyzyl` |
| Expiration | No expiration（无自动到期日，仍可撤销） |
| Repository access | Only select repositories → `study-log` |
| Contents | Read and write |
| Metadata | Read-only（GitHub 必需权限） |
| 其他权限 | 不开通 |

公开仓库可以匿名读取，公开并不意味着任何人都可以写入。新增、编辑和修改文件需要有效写入凭据。Contents 的写入权限也允许删除文件，不能通过该权限单独排除删除；本工作约定不授权删除学习历史。

本文件只说明授权范围和接入方法，不含 Token，也不证明 Token 已生成或手机端已连接。不得将 Token 提交到仓库、打印到日志或在回复中复述。截图中的经典 Token 全量 `repo` 权限不适用于本次仅操作一个现有仓库的需求。

## API 写入与并发规则

- 文件接口为 `/repos/xxyzyl/study-log/contents/{path}`；请求使用受保护的运行时凭据，并避免将认证信息打印到输出。
- 更新文件前先读取远程文件及其当前 `sha`。更新时带上该 `sha`；新文件不传旧文件 `sha`。文件内容使用 UTF-8 后进行 Base64 编码，分支指定 `main`。
- 遇到冲突或远程变化，重新读取文件并合并，不能用旧内容反复提交。若使用 Git，先获取远程变化后正常推送，禁止 `--force`。
- 日志与索引最好一次 Git 提交写入；若逐文件使用 Contents API，逐一核验，两者都成功后才报告全部同步。
- 验收以第一条真实学习内容的写入、回读和提交链接为准，不创建虚假学习打卡作为测试。

官方参考：[管理个人访问令牌](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)、[精细权限令牌的接口权限](https://docs.github.com/en/rest/authentication/permissions-required-for-fine-grained-personal-access-tokens)。
