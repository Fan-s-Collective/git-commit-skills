# Git Commit

## 概览

根据真实的仓库改动生成提交信息。优先写清楚本次提交的核心意图，不要逐文件复述 diff。`references/commit-convention.md` 是基础风格参考，具体 scope 和措辞必须结合当前仓库推断。

## 工作流程

1. 先检查改动集。
   - 有暂存改动时，优先看 `git diff --staged`。
   - 没有暂存改动，或用户明确要求查看未暂存改动时，看 `git diff`。
   - 用 `git status --short` 判断改动范围。
   - 如果仓库里有自己的提交规范，先读取它。常见文件包括 `COMMIT_CONVENTION.md`、`CONTRIBUTING.md`、`.github/COMMIT_CONVENTION.md`、`.github/CONTRIBUTING.md`。
   - 用 `git log --format=%s -n 20` 查看最近的提交标题，判断仓库惯用的输出语言。若历史提交存在明显主导语种，则沿用该语种；若近期提交标题语种混杂、看不出明确主导语种，或没有历史提交、读取历史失败等异常情况，则默认使用英文。

2. 选择一个提交意图。
   - 如果改动包含多个无关意图，建议拆分提交。
   - 如果用户仍然要求写成一个提交，选择主导意图，并简短说明取舍。

3. 生成 header：

```text
<type>(<scope>): <subject>
```

4. 只有在需要说明意图、影响面、兼容性、迁移背景或混合改动类型时才添加 body。

## Type

- `feat`：新增功能
- `fix`：修复问题或缺陷
- `perf`：性能优化
- `refactor`：重构实现但不改变外部行为
- `style`：格式、代码风格调整，不影响运行结果
- `test`：测试补充或调整
- `docs`：文档或注释更新
- `chore`：依赖、构建、脚手架、杂项维护
- `ci`：持续集成相关调整
- `types`：类型定义变更
- `revert`：撤销已有提交
- `wip`：开发中临时提交

混合改动优先建议拆分提交；如果必须合并，header 使用主导类型，并在 body 的条目里用 `type:` 标注不同类型。

## Scope 选择

从当前仓库推断 `scope`。不要复用参考文件里的 scope，除非它们确实匹配当前改动路径或当前仓库规范。

选择优先级：

1. 优先使用当前仓库提交规范中明确定义的 scope。
2. 其次从改动路径中提取稳定的 workspace、package、app 或模块名，例如 `api`、`web`、`cli`、`core`、`ui`、`docs`，或具体包名。
3. 如果改动集中在更明确的子模块，可以使用更细粒度且可长期复用的 scope。
4. 跨多个模块、仓库级配置、或无法归一到单一模块的改动使用 `repo`。

如果当前仓库规范允许无 scope，并且没有有意义的模块范围，可以省略 scope。

## Subject 和 Body

`subject` 直接写本次修改的核心意图，保持简洁、具体、偏动作。避免 `update`、`fix bug`、`optimize code` 这类空泛标题。

输出语言需要参考仓库最近的提交历史。若存在明确主导语种，则提交信息沿用该语种；若近期历史语种混杂或风格无明显规律，或没有历史提交、读取历史失败等异常情况，则默认使用英文。

需要 body 时：

- 说明修改意图、影响面和必要背景。
- 不要逐文件复述 diff。
- 如果所有条目属于同一种修改类型，不要在每条里重复 type。
- 如果一次提交包含不同类型的改动，在 body 条目前加 `type:`。

示例：

```text
feat(auth): add session refresh flow

- 增加会话刷新入口，减少登录态过期后的重复认证
- 补齐旧 token 兼容逻辑，避免升级后状态丢失
```

```text
refactor: align release workflow

- refactor: 收敛构建与发布脚本的职责边界
- fix: 修正缺少版本号时的默认值异常
- docs: 补充新的发布流程说明
```
