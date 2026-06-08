# How-To: Cross-File Refactoring

Rename functions, restructure modules, or change interfaces across an entire codebase safely.

## Rename a function everywhere

```
Rename the function `get_user_by_id` to `fetch_user` across the entire codebase.
Update all callers, imports, and tests. Show me a summary of what you changed.
```

gptme will:
```
> shell grep -r "get_user_by_id" src/ tests/ --include="*.py" -l
# finds: src/db.py, src/api.py, tests/test_users.py, tests/test_api.py

> read src/db.py
> patch src/db.py  (rename definition)

> read src/api.py
> patch src/api.py  (update 3 call sites)

> read tests/test_users.py
> patch tests/test_users.py  (update test calls)

> shell grep -r "get_user_by_id" src/ tests/  # verify: no matches
> shell python -m pytest tests/ -q            # verify: all pass
```

---

## Extract a function

```
The function `process_order` in src/orders.py is 120 lines long.
Extract the validation logic (lines 15-45) into a new function `validate_order`.
Update the call site. Run the tests.
```

---

## Move a module

```
Move src/utils/email.py to src/notifications/email.py.
Update all imports across the codebase.
Don't break anything.
```

gptme uses grep to find all importers, patches each one, then verifies with a test run.

---

## Change a function signature

```
Change `create_post(title, body, author_id)` to `create_post(title, body, *, author_id)` 
(make author_id keyword-only).
Update all call sites that pass author_id positionally.
```

---

## Rename a class and its usages

```
Rename class `UserManager` to `UserService` everywhere.
Also rename the file from src/manager.py to src/service.py.
Update __init__.py imports.
```

---

## Large-scale variable rename in one file

```
In src/config.py, rename all variables that start with `GLOBAL_` to `APP_`.
There are about 20 of them. Show me the before/after diff.
```

---

## Convert from one pattern to another

```
We're migrating from requests to httpx.
In src/client.py, replace all requests.get() / requests.post() calls with
the httpx equivalent. Keep the same error handling behavior.
Run the tests when done.
```

---

## Tips

- **Verify with grep after**: "search for the old name to confirm nothing was missed".
- **Run tests each time**: gptme can run the test suite after each file change.
- **Start with definition**: rename the definition first, then the callers.
- **Stage incrementally**: commit each file or logical group separately for a clean history.
