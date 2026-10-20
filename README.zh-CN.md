# GitHub CDN Redirect

简体中文 | [English](README.md)

一个 Agent Skill：读取、检查或分析公开 GitHub 仓库文件时，使用 jsDelivr 获取文件内容。

## 功能

对于符合条件的公开 GitHub 文件 URL，此 Skill 会将源 URL 转换为 jsDelivr CDN 格式，并保留仓库所有者、仓库名、ref 和文件路径。例如：

```text
https://github.com/example/project/blob/main/src/index.ts
https://cdn.jsdelivr.net/gh/example/project@main/src/index.ts
```

适用内容包括公开的源代码、文档、配置文件和静态资源。GitHub API、Issue、Pull Request、提交页面、仓库目录列表、私有仓库访问和 Git 操作不适用此转换。如果 ref 或路径有歧义，必须先确认后再转换；如果 CDN 请求失败或返回内容异常，则回退到合适的 GitHub 来源并核验结果。完整规则和工作流程请参阅 [`SKILL.md`](.agents/skills/github-cdn-redirect/SKILL.md)。

## 安装

使用 Skills CLI 安装（需要 Node.js 和 npm/npx）：

```sh
npx skills add axetroy/github-cdn-redirect --skill github-cdn-redirect
```

根据提示选择要使用的 Agent 和安装范围。安装后，当所选 Agent 遇到符合条件的公开 GitHub 文件内容请求时，就会使用此 Skill。

如需手动安装，请将 `.agents/skills/github-cdn-redirect` 目录复制到客户端识别的 skills 目录中，并保留 `github-cdn-redirect` 文件夹及其中的 `SKILL.md` 文件。

## 卸载

如需卸载通过 CLI 安装的版本，请运行：

```sh
npx skills remove github-cdn-redirect
```

根据提示选择安装此 Skill 时使用的 Agent 和安装范围。

如需卸载手动安装的版本，请从复制该 Skill 的 skills 目录中删除 `github-cdn-redirect` 文件夹。

## 使用方法

例如，用户要求读取以下公开 GitHub 文件：

```text
https://github.com/example/project/blob/main/README.md
```

Agent 会从以下地址获取文件内容：

```text
https://cdn.jsdelivr.net/gh/example/project@main/README.md
```

此 Skill 会保留原 URL 中指定的 ref，包括 tag 或 commit；不会猜测未知 ref 或路径。对于 GitHub 特有的操作，仍使用 GitHub 页面或 API。

## 核心文件

```text
.
├── .agents/skills/github-cdn-redirect/SKILL.md
├── LICENSE
├── README.md
└── README.zh-CN.md
```

本项目无需运行时依赖或构建步骤。

## 许可证

本项目采用 [MIT 许可证](LICENSE)。
