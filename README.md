# macSetup
Useful things that are easy to forget when setting up my ideal mac os dev environment

## iTerm

How to setup my preferred keybindings

| Keys         | Usage                             |
|--------------|:---------------------------------:|
| ctrl+f       | Move one word forward             |
| ctrl+b       | Move one word backwards           |
| ctrl+opt+del | delete word                       |
| ctrl+cmd+del | delete line                       |
| opt+b        | Send ctrl+b (page back in vim)    |
| opt+f        | Send ctrl+f (page forward in vim) |

![image](https://user-images.githubusercontent.com/3334671/45964556-25afbe00-bff4-11e8-9f3d-81efa2dce6c0.png)

## Git setup in .bash_profile (and some misc java aliases)
Setup the prompt and also a shortcut for throwing a commit back into the prior commit (although it's better to just not commit the next bit and do the amend)

```
[ -f /usr/local/etc/bash_completion ] && . /usr/local/etc/bash_completion

GIT_PS1_SHOWDIRTYSTATE=true

alias git-push="git push -u origin HEAD"
alias mvn-stacks="mvn -DtrimStackTrace=false "
alias jshell="/Library/Java/JavaVirtualMachines/openjdk-11.0.2.jdk/Contents/Home/bin/jshell"

git-squash-into-last() {
	git reset --soft HEAD~1
	git commit --amend --no-edit
}

git-quick-squash() {
	git commit --amend --no-edit
}

git-rebase-master() {
	curbran=$(git rev-parse --abbrev-ref HEAD)
	git stash
	git checkout master
	git pull
	git checkout $curbran
	git stash pop
	git rebase master
}

gb() {
	echo -n ' [' && git branch 2>/dev/null | grep "^*" | colrm 1 2 | tr -d '\n' && echo -n ']'
}

git-branch() {
	gb | sed 's/ \[\]//'
}

PS1='\[\033[0;32m\]\[\033[0m\033[0;32m\]\u\[\033[0;36m\]@\w\[\033[0;32m\]$(git-branch)\[\033[0;32m\]\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\]\[\033[0m\] '
```
