# CH2: Git Basics

<details><summary>.gitignore rules for patterns</summary>

- Blank lines or lines starting with # are ignored
- patterns starting with `/` avoids recursivity
- patterns ending with `/` specifies a directory
- patterns starting with `!` is negated
</details>

<details><summary>Glob patterns</summary>

- `*` matches zero or more characters
- `a/**/z` matches nested directories (ex: matches `a/z`, `a/b/z`, `a/b/c/z`, etc)
- `[abc]` matches any character inside the brackets (ex: a, b, or c)
- `[0-9]` matches characters between first and last item in brackets (ex: 0 through 9)
- `?` matches a single character
</details>

<details><summary>gitignore example w/ explanation</summary>

```
# ignore all .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in any directory named build
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```
</details>

<details><summary>What does the command "git diff" show exactly?</summary>

- `git diff`
  - compares working directory and staging area, showing changes you made but haven't staged yet
  - "What changes have I made, but not staged?"
- `git diff --staged`
  - compares staging area to last commit, showing what will be included in the next commit
  - "What changes have I staged that will be committed next?"
- `git diff HEAD`
  - compares working directory directly to last commit, showing all uncommitted changes regardless of staging status
  - "What's the total difference between my working files and the last commit?"
</details>

<details><summary></summary>

</details>