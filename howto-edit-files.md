# How-To: Surgical File Editing

Edit files precisely — apply a targeted change without rewriting everything around it.

## The prompt

```
Read src/config.py, find the DEFAULT_TIMEOUT constant, and change it from 30 to 60.
Then verify the change is correct.
```

## What gptme does

```
> read src/config.py
# shows file contents

> patch src/config.py
<<<<<<< ORIGINAL
DEFAULT_TIMEOUT = 30
=======
DEFAULT_TIMEOUT = 60
>>>>>>> UPDATED

> read src/config.py
# confirms change applied
```

## Why it works

gptme's `patch` tool applies minimal diffs — it doesn't rewrite the whole file.
This keeps unrelated formatting intact and avoids merge conflicts.

---

## Editing multiple locations at once

```
In src/app.py:
- Rename `get_user` to `fetch_user` everywhere
- Change the default `page_size` parameter from 20 to 50
```

gptme will read the file, make both changes with separate patch blocks, then verify.

---

## Creating a new file from scratch

```
Create a new file scripts/cleanup.sh that:
- Deletes all .pyc files recursively
- Removes __pycache__ directories
- Prints a summary of what was deleted
Make it executable.
```

gptme uses `save` for new files, then `shell` to `chmod +x`.

---

## Applying changes across multiple files

```
Update the API base URL from "https://api.example.com/v1" to
"https://api.example.com/v2" in all Python files under src/.
Show me each file you're changing.
```

gptme will `shell grep -r` to find occurrences, then patch each file.

---

## Tips

- **Be specific about location**: "line 42" or "the function named `process`" helps avoid ambiguity.
- **Ask for verification**: gptme will re-read after patching to confirm.
- **Staged edits**: gptme won't `git add` unless you ask — you keep control.
