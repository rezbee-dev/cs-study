# CH1: Getting Started

<details><summary>What is "version control" (aka VCS)?</summary>

- System that records changes to a file or set of files over time so you can revert back or recall specific versions of it later
</details>

<details><summary>What data does Git save?</summary>

- the entire project filesystem is saved as a "snapshot"
- If files have not changed since the last "snapshot", git will just link to the previously stored files instead
- Git will store the project data as a stream of snapshots
- aka commits
</details>

<details><summary>How does Git detect changes in contents of files?</summary>

- Everything in Git is checksummed and referred to by that checksum
  - checksum is like a digital fingerprint (unique and able to identify)
  - aka hashing
- So if there are any changes, then Git will know since the checksum would be different
  - this allows for data integrity
  - even if one character changes in a file, the checksum for it will be different and git will know the data was changed
- Git uses SHA-1 checksum which produces 40 character string
</details>

<details><summary>What are the three main states for files in Git</summary>

1. Untracked: any files that were not in the previous snapshot and not in staging area; all other files would be tracked
2. Modified: file changed, but not committed to git database
3. Staged: modified file marked to go into next commit snapshot
4. committed: data is stored in local database
</details>

<details><summary>Where are git configuration variables stored?</summary>

- `[path]/etc/gitconfig`
  - system-wide config that applies to all users and repos
  - `git config --system`
- `~/.gitconfig` or `/.config/git/config`
  - user-wide config applying to current user and repos located in user dir
  - `git config --global`
  - overrides system configs
- `.git/config`
  - local repository config applying to current repo
  - `git config --local` or `git config` (default)
  - overrides global and system configs
- `git config --list --show-origin`
  - shows all git configs and where they are located/sourced from
</details>

