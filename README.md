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

## Git branch

- create test branch
- use git push origin test to create the new test branch on GitHub.
- A&lt;hough git push origin test can push code, but local git don't record it as defau&lt; setting
- use below ways to set the defa&lt; behavior so next time 'git push' without other parameter will work:
    1. git push --set-upstream origin test 
    2. git branch --set-upstream-to origin/test
- After more test, I found if server don't have the test branch, you need to push first:
    - git push origin test
- when you clone a git, you're on master branch, if you want to checkout to dev branch (already have on server),
  you should try git branch dev origin/dev

## Rebase

- Add rebase area in master branch

### Rebase and push
 - when did rebase and try push, server will decline
 - it suggest you to do git pull, commit and push
### rebase, pull generate abundant commits 
- I tried pull,commit,push, then when you use 'git log', there are 2 commit id for same change.
- it's because rebase does not simply change the link sequence, it generate new commit id:

```
      A---B---C test
     /
D---E---F---G master
```
after rebase: git rebase master or git rebase master topic
```
              A'---B'---C'---D test
             /              /
D---E---F---G master      /
             \          /
              A---B---C 
```
- it's not the old A, B, C anymore
- git log may confusing, but git log --graph is more clear.
- check https://git-scm.com/docs/git-rebase for more details.
- I did lots of test to simply rebase server's test branch, but no way except for 'push --hard'
- 'push --hard' will abundant old A B C commit and replace it with the new A' B' C'
- then I found it's not suggest to do it: https://git-scm.com/book/en/v2/Git-Branching-Rebasing

## Git log --graph

- make log clear for the history chain


## Git fetch
- Add some thing from server
- Git record the server's status locally
- fetch means to update status from server
- fetch won't change your local branch's status

## Remote
- git branch -a can see branches in server
- I noticed some branch which already been deleted on server still listed
- git remote show origin can check more details
- those branch are 'stale' status
- use git remote prune to clean them

## Understand Origin/Remote
- Remote is the remote side (server side)
- Origin is the defau&lt; name when you clone a git from server
- git remote -v can see remote info
- you can add more remote by git remote add name location 
- more ref check git help remote

## How to manage your branches
- master should be stable
- work usually on dev
- merge -no-ff (no fast forward) can keep merge history

## Git Stash
- Use git stash to save your work temporarily
- use git stash list to see the stashed list
- use git stash pop to recover the changes
- git apply + git drop == git pop

## Work flow
- modify, git pull, [git merge,] git add, git commit, git push

## understand HEAD
- HEAD is the point point to the current commit id
- HEAD is the defau&lt; value for git commands:
    - git branch dev == git branch dev HEAD
    - git diff == git diff HEAD
    - git show == git show HEAD
    - etc.

## Tag
- tag is more readable
- git tag show all tags
- git tag &lt;tagname&gt; to create a tag
- git tag v0.5 == git tag v0.5 HEAD
- can create tag for old commit: git tag v0.1 [commit_id]

## Detached HEAD
- I tried a wrong command: git checkout v0.5, which I mean git reset --hard v0.5
- it has some warning message but i ignored
- when I made some change, commit, and want to push, it declined
- then I use git status, git branch to check, i found i'm not on master branch
- below is the user guide for checkout commit:
    >git checkout --detach [&lt;branch&gt;], git checkout [--detach] &lt;commit&gt;
    >Prepare to work on top of &lt;commit&gt;, by detaching HEAD at it (see "DETACHED HEAD" section), and updating the index and the files in the working tree. Local modifications to
    >the files in the working tree are kept, so that the resu&lt;ing working tree will be the state recorded in the commit plus the local modifications.
    >
    >When the &lt;commit&gt; argument is a branch name, the --detach option can be used to detach HEAD at the tip of the branch (git checkout &lt;branch&gt; would check out that branch
    >        without detaching HEAD).
    >
    >Omitting &lt;branch&gt; detaches HEAD at the tip of the current branch.

## Side episode
- Markdown cannot show &gt; &lt; &ge; &le; directly
- need to use \&gt; \&lt; \&ge; \&le; to replace
