# ntfy-ios — Project Log

## Overview

Fork of [binwiederhier/ntfy-ios](https://github.com/binwiederhier/ntfy-ios) — the official iOS client for ntfy, an open-source push notification service. This fork (`shasb/ntfy-ios`) integrates community PRs and custom features ahead of upstream merges.

## 2026-03-27 — Integrate 5 Community PRs

**PR:** https://github.com/shasb/ntfy-ios/pull/1

Merged 5 upstream community PRs into the fork via squash-merge on a local integration branch, then merged to main via PR on the fork.

### Merge Order and Rationale

1. **PR #28** (laurentftech) — Fix notification delivery, Firebase robustness, persistent logs, tests
   - Bug fix with no dependencies; largest change (718 additions)
   - Fixes: willPresent CoreData save, DispatchGroup completion handler, idempotent notification save, Firebase re-subscription
   - Adds 14 unit tests and persistent logging with share button

2. **PR #29** (AnimaI) — Custom display names for subscriptions
   - Adds `customDisplayName` to Subscription Core Data entity
   - Note: had "Changes requested" review from LucaCappelletti94 on upstream; included as-is

3. **PR #27** (paule76) — Markdown rendering with MarkdownUI library + in-app Safari
   - Adds MarkdownUI SPM dependency
   - Makes URLs clickable, opens links in SFSafariViewController

4. **PR #30** (AnimaI) — Markdown rendering via content-type detection
   - Adds `contentType` field to Message struct and Core Data Notification entity
   - **Conflict resolved:** PR #30 conflicted with PR #27 in `NotificationListView.swift`. Resolution: use MarkdownUI for `text/markdown` content, plain Text for everything else, with in-app Safari link handling

5. **PR #31** (shasb) — ntfy:// URL scheme deep linking
   - Registers `ntfy` URL scheme, adds NtfyURLHandler, wires `.onOpenURL` in AppMain
   - Supports host/topic, custom ports, `secure=false`, display name param

### Blocker Encountered

Could not use `gh pr merge` on upstream PRs — no write access to `binwiederhier/ntfy-ios`. Resolved by fetching PR branches locally, squash-merging into integration branch, and merging via PR on the fork.

### Current State

- All 5 PRs successfully integrated into fork main
- 18 files changed, 977 additions, 47 deletions
- 14 new unit tests from PR #28
- Needs Xcode build verification and test run
