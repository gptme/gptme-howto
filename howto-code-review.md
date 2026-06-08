# How-To: Code Review with Context

Review a PR or local diff with full codebase context — not just the changed lines.

## Review the current git diff

```
Review my staged changes. Focus on:
- Logic bugs
- Missing error handling
- Anything that would break existing tests
```

gptme runs `git diff --cached`, reads related files for context, and gives specific findings.

---

## Review a specific PR

```
Review PR #142 in this repo. Look for security issues and API contract violations.
```

gptme will:
```
> shell gh pr diff 142
> shell gh pr view 142
> read <files changed in the PR>
# analysis with line references
```

---

## Deep review with test context

```
Review the changes in src/auth.py against its test file tests/test_auth.py.
Does the implementation match what the tests expect?
```

gptme reads both files and cross-references — catching cases where tests pass
only because they don't cover the new code path.

---

## Review before merging

```
I'm about to merge branch feature/billing into main.
Show me the diff, check for breaking changes to the public API,
and flag anything that needs a migration.
```

gptme runs `git diff main...feature/billing`, checks API surface, flags schema changes.

---

## Review your own work before a commit

```
I've been working on the payment module. Before I commit:
1. Check for debug print statements or TODOs I left in
2. Verify all new functions have docstrings
3. Make sure error cases return appropriate HTTP status codes
```

---

## Generate a structured review checklist

```
Create a code review checklist for this PR as a markdown comment I can paste into GitHub.
Cover correctness, security, performance, and test coverage.
```

---

## Tips

- **Give context**: "this is a public API" or "this hits the database" focuses the review.
- **Ask for severity**: "flag critical issues separately from style nits".
- **Iterate**: if a finding is wrong, say so — gptme will re-examine.
