# GitConfig

## 概要

- 社用と私用にて 2 つの GitHub アカウントを使用しているときには、
- SSH 接続について、 ~/.ssh/config での切替設定を行うときがある
- このとき「github-gsid」と「github-hfid」にて切り替えて利用したい
- .git ディレクトリパスにより自動切替するには~/.gitconfig を設定する

### ~/.ssh/config

```sh
# 会社アカウント（github-gsid）
Host github-gsid
    HostName github.com
    User git
    IdentityFile ~/.ssh/gsid
    IdentitiesOnly yes

# 個人アカウント（github-hfid）
Host github-hfid
    HostName github.com
    User git
    IdentityFile ~/.ssh/hfid
    IdentitiesOnly yes
```

### ~/.gitconfig

- includeIf を加えて指定ディレクトリ配下で使用する config を指定

```sh
[user]
	name = hfujiyoshi
	email = hiroshi.fujiyoshi@g-seed.co.jp
[includeIf "gitdir:/Users/hiroshi.fujiyoshi/development/"]
    path = /Users/hiroshi.fujiyoshi/.gitconfig-hfujiyos
[includeIf "gitdir:/Users/hiroshi.fujiyoshi/github-gsid/"]
    path = /Users/hiroshi.fujiyoshi/.gitconfig-hfujiyoshi
[init]
	defaultBranch = main
[core]
	excludesfile = /Users/hiroshi.fujiyoshi/.gitignore_global
[difftool "sourcetree"]
	cmd = opendiff \"$LOCAL\" \"$REMOTE\"
	path =
[mergetool "sourcetree"]
	cmd = /Applications/Sourcetree.app/Contents/Resources/opendiff-w.sh \"$LOCAL\" \"$REMOTE\" -ancestor \"$BASE\" -merge \"$MERGED\"
	trustExitCode = true
[commit]
	template = /Users/hiroshi.fujiyoshi/.stCommitMsg
[filter "lfs"]
	clean = git-lfs clean -- %f
	smudge = git-lfs smudge -- %f
	process = git-lfs filter-process
	required = true

```

### .gitconfig-hfujiyos

```sh
[user]
    name = hfujiyos
    email = hfujiyos@gmail.com
```

### .gitconfig-hfujiyoshi

```sh
[user]
    name = hfujiyoshi
    email = hiroshi.fujiyoshi@g-seed.co.jp
```
