# Claudy

A native macOS desktop app for the [Claude Code](https://claude.com/claude-code) CLI.

Claudy runs the `claude` binary already installed on your Mac, so it uses your existing login or subscription. It adds a full
desktop workspace around it: streaming chats, per-turn diffs you can revert, a built-in browser, a terminal, git, a database
browser, SSH servers and more.

This repository hosts the **signed and notarized builds** of Claudy. The source lives in a separate, private repository.

## Download

**[⬇ Download the latest release](https://github.com/Abdelraman/claudy-releases/releases/latest)**

| File | Use it for |
| --- | --- |
| `Claudy-<version>-arm64.dmg` | First install: open it and drag Claudy into Applications |
| `Claudy-<version>-arm64.zip` | The same app as a zip (used by the in-app updater) |

Older versions are on the [Releases](https://github.com/Abdelraman/claudy-releases/releases) page.

### Requirements

- A Mac with **Apple Silicon** (M1 or later). Intel builds aren't published.
- The **Claude Code CLI**. Claudy finds it on your login shell `PATH`, in `~/.local/bin` or in Homebrew, or you can set the
  path in Settings. If it's missing, Claudy offers to install it for you.
- **git**, used for change snapshots and the git tools.

### Updates

Claudy checks this page for new releases every hour. When one is available, it downloads the release zip, verifies its
SHA-512 checksum and swaps the app in place on restart. You can also check by hand from **Settings › About**, which shows
your version and build.

Claudy keeps the Claude Code CLI up to date too. It runs `claude update` on launch and every 6 hours (you can turn this off
in Settings), and the ↻ button in a chat header restarts that chat on the new CLI version without losing its context.

## Features

### Chat with Claude Code
- **Streaming chat** with Markdown, syntax highlighting and collapsible tool cards for Bash, Read, Edit, Write, Grep,
  todos, agents and more.
- **Modes**: Plan, Ask, Edits and Auto. Switch with the composer switch or `⇧Tab`, and the change applies to a running
  session right away. In Plan mode, proposed plans show an approval card: approve into Auto, Accept edits or Ask, or keep
  planning with feedback.
- **Permission prompts**: allow, always allow for this chat, or deny with a message. `AskUserQuestion` shows up as
  clickable options.
- **Tasks panel** showing running agents, background shells and the current todo list.
- **Model picker** (Opus, Sonnet, Haiku or a custom model id), a context-usage ring and a usage tab.
- **Session history** for each project folder, read from `~/.claude/projects`. You can resume any conversation and search a
  project's chats.
- **Notifications**: a sound, a system notification and a Dock badge when a chat needs your attention.

### Tabs and project groups
- **Chat tabs**: a Chrome-style tab strip across the top of the window, one tab per open chat. Each tab sits in its
  project's group, and each project keeps its own colour across launches. Chat (Cowork) tabs share a group of their own.
- **Group menu**: click a project's label to switch between its open tabs, search and reopen its past chats, start a new
  chat in that project or close the whole group.
- **Pinned tabs**: pin a tab from its right-click menu. Pinned tabs shrink to an icon, sit at the front of the strip and
  reopen pinned. Closing one asks first, and closing a group or other tabs leaves pinned tabs alone.
- **Shortcuts**: `⌘T`, `⌘W` and `⌘N` work on tabs, and you can drag tabs to reorder them. Chat tabs and group colours can
  each be turned off in Settings.

### Review and undo changes
- **Last-turn changes**: Claudy snapshots every turn in a shadow git repo kept outside your project. This works in folders
  that aren't git repos and also catches edits made through Bash. Click "N files changed" to see unified or split diffs,
  then revert one file or the whole turn.
- **File history**: for any file, see every turn snapshot and git commit that touched it.

### Built-in browser
- A **Browser panel** (🌐 or `⌘⇧B`) for previewing your dev server. Localhost links in the chat open there, and the page
  stays loaded while the panel is hidden.
- **Pick an element** to comment on it, with a cropped screenshot attached, or attach the whole viewport.
- **Claude can drive it too** through a built-in MCP server (`claudy-browser`) that can navigate, take snapshots, click,
  type, take screenshots and read console logs. Running JavaScript (`evaluate`) asks you first.

### Project tools
- **Files and editor**: an IDE-style file tree with tabs, fuzzy search and rendered Markdown, plus a code editor with
  syntax highlighting (including `.env` files) that saves as you type or on `⌘S`. The gutter marks lines changed since the
  last commit.
- **Git**: switch and create branches, commit with an AI-written message, view a history graph, and work through merges,
  cherry-picks, reverts and rebases, including a conflict editor.
- **Database**: browse a project's MySQL or MariaDB database (read from a Laravel-style `.env`), edit rows, and use a SQL
  console, import, export and table tools. Saved passwords are sealed with the macOS keychain.
- **Run**: start and stop a project's `package.json` scripts, or `flutter run` on simulators, emulators and devices, with
  a live log.
- **Memory**: edit `CLAUDE.md` files, auto-memory and `settings.json` permission rules.
- **Plugins**: browse and install Claude Code plugins.

### Terminal and Servers
- **Terminal**: tabbed login shells, available both as their own activity and as a panel inside each chat.
- **SSH**: a terminal tab per host, with commands suggested from that host's history as you type. Hosts and keys are kept
  in a password-encrypted vault, and setup recipes cover PHP, Nginx and MariaDB, Node.js with PM2, and Docker.
- **SFTP**: your Mac and the server side by side. Drag files between them or drop them in from Finder, and upload,
  download, rename, create folders and delete.

### Cowork
Switch the sidebar between **Code** and **Cowork** with `⌘⇧K`. Cowork gives Claude tasks on documents and files, like
Claude Desktop does. Each task can have folders attached or get its own scratch folder. A side panel shows progress, the
files the task produced, connectors and document skills, and you can install `document-skills@anthropic-agent-skills` in
one click.

### Comfort
- Light, dark or system theme, plus a choice of code themes.
- Workspace font size with `⌘+`, `⌘−` and `⌘0`, or the slider in Settings.
- Customizable keyboard shortcuts.

## Troubleshooting

- **"Claudy can't find claude"**: set the CLI path in **Settings**, or install Claude Code with
  `curl -fsSL https://claude.ai/install.sh | bash`.
- **macOS blocks the app**: releases are signed with a Developer ID and notarized by Apple, so this shouldn't happen with a
  download from this page. If it does, open the app from **System Settings › Privacy & Security › Open Anyway**.
- **Notifications don't appear**: allow them for Claudy in **System Settings › Notifications**.

## Feedback

Found a bug or want a feature? [Open an issue](https://github.com/Abdelraman/claudy-releases/issues) and include your
Claudy version (from **Settings › About**) and your macOS version.
