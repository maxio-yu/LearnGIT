#This is a study memo

- Last time I use GIT was about 4 years ago when I was in Marvell
- I am using Perforce in my company
- I almost forget all things about GIT

```
if (knowledge.GIT == null) {
    print "Not a good coder\n";
}
```

==Let's start==

## Editor issue

When I tried to commit my first version, I encoutered a issue, the git report:
```
error: There was a problem with the editor 'vi'.
Please supply the message using either -m or -F option.
```
I searched on Google, and it's resolved by setting:
```
git config --global core.editor $(which vim)
```
The issue only happened when user use Vundle in vi
but nobody know the root cause. Below is someone's comments:

>just went through this process as well:
>1. Install Vundle per instructions
>2. Try to commit something as per usual with git commit
>3. Type a commit message using $EDITOR, which is set to vi
>4. Watch commit fail with "error: There was a problem with the editor 'vi'."
>5. Search for a solution, find this blog post
>6. Try the workaround it suggests (git config --global core.editor $(which vim)), notice that it works
>7. Notice that it also works to reset $EDITOR from vi to /usr/bin/vim
>8. Feel frustrated, because no one seems to understand why this is happening
>9. Search for related issues in the Vundle GitHub repo, find this issue
>10. Remain frustrated because while everyone agrees on the workaround, there is still no actual explanation or solution
>11. Realize that this is a cycle that many more users will struggle through unless a proper fix shows up
>12. Write this comment in hopes the issue might be reopened

## Git log/reset/reflog

- Git log show commit history which before the HEAD
- Git reset change the HEAD (a pointer)
- Git reflog checks all command you entered.

## Git add

- Git add is for change, not file
- if you change the file after you add it, the later change will not be submitted if you commit
- test line after add README.md

## Git checkout for file

- Git checkout revert the changes which is not been added
- That means if you already use git add, the file will not be reverted

## Git diff

- I just found when you added the change, git diff will show nothing
- searched on Google, should use git diff --staged
- staged is a area which git add those files in

## Stage area

- Git has 3 area: working, stage, master
- we work in working area, add add change in stage area, commit add change to master

## Rebase

- Add rebase area in master branch

## Git branch

- create test branch
- use git push origin test to create the new test branch on GitHub.
- Although git push origin test can push code, but local git don't record it as default setting
- use below ways to set the defalt behavior so next time 'git push' without other parameter will work:
    1. git push --set-upstream origin test 
    2. git branch --set-upstream-to origin/test

 ## Rebase and push

 - when did rebase and try push, server will decline
