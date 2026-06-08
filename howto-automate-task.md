# How-To: Automate a Recurring Shell/Git Workflow

Turn a multi-step manual process into a reusable script — described once, built immediately.

## The prompt

```
I have a release workflow I do manually every week:
1. Run the test suite
2. Bump the version in pyproject.toml (patch version)
3. Update CHANGELOG.md with the date and version number
4. Commit with message "chore: release vX.Y.Z"
5. Create a git tag

Write a script scripts/release.sh that does all of this.
```

gptme reads your `pyproject.toml` and `CHANGELOG.md`, writes the script, makes it executable.

---

## Automate a git cleanup workflow

```
Write scripts/cleanup-branches.sh that:
- Lists all local branches merged into main
- Deletes them (with confirmation prompt)
- Prunes remote tracking branches

Test it with --dry-run first.
```

---

## Automate log analysis

```
I have nginx logs at /var/log/nginx/access.log.
Write a script that:
- Shows the top 10 most requested URLs
- Shows the top 5 IPs by request count
- Flags any 5xx errors from the last hour

Run it now and show me the output.
```

gptme writes the script, runs it, shows live results.

---

## Automate database backups

```
Write scripts/backup-db.sh that:
- Dumps the postgres database named "myapp"
- Saves to ~/backups/myapp-YYYY-MM-DD.sql.gz
- Deletes backups older than 30 days
- Logs success/failure to /var/log/db-backup.log

Then add it to crontab to run at 2am daily.
```

---

## Turn a manual deploy into a script

```
Our deploy process is:
1. ssh to server: ssh deploy@prod.example.com
2. cd /opt/myapp
3. git pull
4. pip install -r requirements.txt
5. systemctl restart myapp
6. check: systemctl status myapp

Write scripts/deploy.sh that does this. Add --rollback flag that runs git reset --hard HEAD~1 and restarts.
```

---

## Build a project scaffolder

```
Write scripts/new-module.sh <name> that creates:
- src/<name>/__init__.py (empty)
- src/<name>/core.py (with a stub class named after the module)
- tests/test_<name>.py (with a basic test class)

Run it with "new-module payments" to test it.
```

---

## Tips

- **Show examples**: "here's a run that works manually" helps gptme match your exact format.
- **Ask for error handling**: "exit with code 1 and print the error if any step fails".
- **Test immediately**: gptme can run the script right after writing it.
- **Iterate**: "add a `--verbose` flag" or "make the confirmation skippable with -y".
