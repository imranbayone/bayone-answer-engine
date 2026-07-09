# GitHub Workflow

How changes move from an idea to running on the server. Everything in this project is versioned — every prompt tweak, every rubric change, every skill update is a commit, so we always have a record of what changed and can trace it against results.

## The Golden Rule

**Laptop is where you write. Server is where it runs. GitHub is the bridge between them.**

You never edit files directly on the server. You edit on your laptop, push to GitHub, then pull the update onto the server.

## Day-to-Day Commands

Open Command Prompt, navigate into the repo folder:

```
cd %USERPROFILE%\Documents\bayone-answer-engine
```

**Before starting any new work**, always pull the latest first:
```
git pull
```

**After making changes**, in this order:
```
git status
```
(Confirm only the files you intended to change are listed — check nothing key-like or secret-like appears here.)

```
git add .
git commit -m "short description of what changed and why"
git push
```

## Getting Changes Onto the Server

Once pushed to GitHub, connect to the server via Lightsail's browser SSH and run:

```
cd ~/bayone-answer-engine
git pull
```

The server can only pull, never push — it connects with a read-only deploy key (see `docs/SERVER_SETUP.md`, section 4). If the server ever needs to send something back (it shouldn't), that's a manual, deliberate action, not a routine one.

## Commit Message Habits

Write commit messages that would make sense to someone (including future you) reading the log months later:

- Good: `"tighten scoring rubric - reduce false positives on career-advice threads"`
- Good: `"add r/AI_Agents to Portfolio A after Rachel's feedback"`
- Avoid: `"update"`, `"fix"`, `"changes"`

## Tags and Releases

At key milestones, tag the repo so we can always return to a known-good state:

```
git tag v1.0-pilot
git push origin v1.0-pilot
```

Planned tags:
- `v1.0-pilot` — end of Sprint 2, first time scoring + drafting is live
- `v1.1`, `v1.2`, etc. — one per subsequent sprint close

## If Something Breaks

Check the log to see recent history:
```
git log --oneline -10
```

To see exactly what changed in a specific commit:
```
git show <commit-hash>
```

To temporarily revert to a previous tagged version on the server:
```
git checkout v1.0-pilot
```

Never force-push (`git push --force`) without discussing it first — it can silently overwrite history other people are relying on.
