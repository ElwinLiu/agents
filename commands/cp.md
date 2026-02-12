---
description: Commit and push - draft a commit message, stage all changes, commit, and push
---

Draft a commit message following the [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) specification, then run `git add .`, commit the changes with the drafted message, and push to the repository.

## Format

The commit message structure is:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Commit Types

The following types are specified:

- **fix:** a commit of the type `fix` patches a bug in your codebase (this correlates with `PATCH` in Semantic Versioning).
- **feat:** a commit of the type `feat` introduces a new feature to the codebase (this correlates with `MINOR` in Semantic Versioning).
- **BREAKING CHANGE:** a commit that has a footer `BREAKING CHANGE:`, or appends a `!` after the type/scope, introduces a breaking API change (correlating with `MAJOR` in Semantic Versioning). A BREAKING CHANGE can be part of commits of any type.
- **Other types:** Types other than `fix:` and `feat:` are allowed, for example `build:`, `chore:`, `ci:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, and others.

## Scope

A scope MAY be provided to a commit's type, to provide additional contextual information and is contained within parenthesis, e.g., `feat(parser): add ability to parse arrays`.

## Breaking Changes

Breaking changes MUST be indicated in the type/scope prefix of a commit, or as an entry in the footer.

If included as a footer, a breaking change MUST consist of the uppercase text BREAKING CHANGE, followed by a colon, space, and description, e.g., `BREAKING CHANGE: environment variables now take precedence over config files`.

If included in the type/scope prefix, breaking changes MUST be indicated by a `!` immediately before the `:`. If `!` is used, `BREAKING CHANGE:` MAY be omitted from the footer section, and the commit description SHALL be used to describe the breaking change.

## Footer Format

One or more footers MAY be provided one blank line after the body. Each footer MUST consist of a word token, followed by either a `:<space>` or `<space>#` separator, followed by a string value (this is inspired by the git trailer convention).

A footer's token MUST use `-` in place of whitespace characters, e.g., `Acked-by` (this helps differentiate the footer section from a multi-paragraph body). An exception is made for `BREAKING CHANGE`, which MAY also be used as a token.

A footer's value MAY contain spaces and newlines.

## Steps to Execute

1. First, check the current git status to understand what changes are present
2. Review the git diff to understand what changes are being made
3. Draft a commit message following the Conventional Commits specification based on the changes
4. Run `git add .` to stage all changes
5. Commit the changes using the drafted message with `git commit -m "<message>"`
6. Push the commit to the repository with `git push`

## Important Notes

- Before committing, run `git diff --cached` to review ALL changes being committed
- Examine the diff for secrets, credentials, API keys, or sensitive data (especially in config files, logs, environment files, and build outputs)
- If sensitive data is detected, STOP and warn the user before proceeding
- If the commit fails due to pre-commit hooks, retry ONCE to include automated changes. If it fails again, a pre-commit hook is likely preventing the commit
- If files were modified by the pre-commit hook, amend the commit to include them

## Examples

### Commit message with description and breaking change footer

```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

### Commit message with `!` to draw attention to breaking change

```
feat!: send an email to the customer when a product is shipped
```

### Commit message with scope and `!` to draw attention to breaking change

```
feat(api)!: send an email to the customer when a product is shipped
```

### Commit message with both `!` and BREAKING CHANGE footer

```
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

### Commit message with no body

```
docs: correct spelling of CHANGELOG
```

### Commit message with scope

```
feat(lang): add Polish language
```

### Commit message with multi-paragraph body and multiple footers

```
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

Refs: #123
```
