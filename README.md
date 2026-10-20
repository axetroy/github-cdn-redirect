# GitHub CDN Redirect

[简体中文](README.zh-CN.md) | English

An Agent Skill that uses jsDelivr to retrieve file contents from public GitHub repositories when reading, inspecting, or analyzing repository files.

## What it does

For eligible public GitHub file URLs, the skill converts the source URL to the jsDelivr CDN format while preserving the owner, repository, ref, and file path. For example:

```text
https://github.com/example/project/blob/main/src/index.ts
https://cdn.jsdelivr.net/gh/example/project@main/src/index.ts
```

It applies to public file contents such as source code, documentation, configuration, and static assets. It does not redirect GitHub APIs, issues, pull requests, commit pages, repository listings, private repository access, or Git operations. If the ref or path is ambiguous, the skill requires resolving it before conversion; if CDN retrieval fails or returns unexpected content, it falls back to an appropriate GitHub source and verifies the result. See [`SKILL.md`](.agents/skills/github-cdn-redirect/SKILL.md) for the full rules and workflow.

## Install

Install with the Skills CLI (Node.js and npm/npx required):

```sh
npx skills add axetroy/github-cdn-redirect --skill github-cdn-redirect
```

Follow the prompts to select your agent and installation scope. The selected agent will use the skill when it encounters an eligible public GitHub file-content request.

To install manually, copy `.agents/skills/github-cdn-redirect` into a skills directory recognized by your client. Keep the `github-cdn-redirect` folder and its `SKILL.md` file together.

## Uninstall

To remove a CLI installation, run:

```sh
npx skills remove github-cdn-redirect
```

Follow the prompts to select the agent and installation scope where the skill was installed.

To remove a manual installation, delete the `github-cdn-redirect` folder from the skills directory where you copied it.

## Use

For example, when asked to read this public GitHub file:

```text
https://github.com/example/project/blob/main/README.md
```

the agent retrieves its contents from:

```text
https://cdn.jsdelivr.net/gh/example/project@main/README.md
```

The skill preserves the original ref, including a tag or commit when specified. It does not guess unknown refs or paths, and uses GitHub's normal pages or APIs for GitHub-specific operations.

## Key files

```text
.
├── .agents/skills/github-cdn-redirect/SKILL.md
├── LICENSE
├── README.md
└── README.zh-CN.md
```

No runtime dependencies or build step are required.

## License

This project is licensed under the [MIT License](LICENSE).
