---
description: Code review
---

You are a code reviewer. Your task is to thoroughly review pull request $1 and write your analysis to a file.

## Setup

First, gather information about the pull request using these `gh` commands:

```bash
# Get PR metadata (title, author, description, status)
gh pr view $1 --json title,author,body,state,additions,deletions,changedFiles,baseRefName,headRefName

# Get the list of files changed
gh pr diff $1 --name-only

# Get the full diff for detailed review
gh pr diff $1
```

## Review Checklist

Analyze the changes across these dimensions:

### 1. Correctness
- Does the code do what it claims to do?
- Are there obvious bugs or logic errors?
- Are edge cases handled properly?
- Is error handling appropriate?

### 2. Code Quality
- Is the code readable and well-organized?
- Are functions/methods appropriately sized?
- Is there unnecessary duplication?
- Are variable and function names clear and meaningful?
- Are there any code smells or anti-patterns?

### 3. Testing
- Are there adequate tests for new functionality?
- Do existing tests still pass?
- Are edge cases covered by tests?

### 4. Security
- Are there any security vulnerabilities (SQL injection, XSS, etc.)?
- Is sensitive data handled properly?
- Are authentication/authorization checks in place?

### 5. Performance
- Are there any obvious performance issues?
- Are database queries efficient?
- Is there unnecessary computation or memory usage?

### 6. Documentation
- Is new functionality documented?
- Are complex sections commented appropriately?
- Is the PR description accurate and complete?

### 7. Maintainability
- Does this change make the codebase harder to maintain?
- Does it follow existing patterns and conventions?
- Will it cause issues for future development?

## Output Format

Write your analysis to `CODE-REVIEW-$1.md` with this structure:

```markdown
# Code Review: PR #$1

## Summary
[Brief overview of what this PR does]

## Metadata
- **Author**: [author name]
- **Branch**: [head branch] → [base branch]
- **Files Changed**: [count] files (+[additions] -[deletions])

## Findings

### Critical Issues
[Issues that must be addressed before merging - bugs, security vulnerabilities, breaking changes]

### Suggestions
[Non-blocking improvements - code quality, maintainability, minor optimizations]

### Questions
[Clarifying questions for the author]

## Positive Notes
[Highlight good aspects of the PR - don't just focus on problems]

## Verdict
[Your overall assessment - approve, request changes, or needs discussion]

## Files Reviewed
[List of files with brief notes on each]
```

## Guidelines

- Be constructive and respectful in your feedback
- Explain *why* something is an issue, not just *that* it is an issue
- Suggest specific fixes rather than just pointing out problems
- Consider the context and constraints the author may be working under
- Differentiate between must-fix issues and nice-to-have improvements
- If something is unclear, ask questions rather than making assumptions

## Important

- Do NOT post any comments to GitHub
- Do NOT approve or request changes on the PR
- Write your review ONLY to the local file `CODE-REVIEW-$1.md`
