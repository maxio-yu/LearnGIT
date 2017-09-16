# This is a study memo

- Last time I use GIT was about 4 years ago when I was in Marvell
- I am using Perforce in my company
- I almost forget all things about GIT

```
if (knowledge.GIT == null) {
    print "Not a good coder\n";
}
```

== Let's start ==

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

>Install Vundle per instructions
>Try to commit something as per usual with git commit
>Type a commit message using $EDITOR, which is set to vi
>Watch commit fail with "error: There was a problem with the editor 'vi'."
>Search for a solution, find this blog post
>Try the workaround it suggests (git config --global core.editor $(which vim)), notice that it works
>Notice that it also works to reset $EDITOR from vi to /usr/bin/vim
>Feel frustrated, because no one seems to understand why this is happening
>Search for related issues in the Vundle GitHub repo, find this issue
>Remain frustrated because while everyone agrees on the workaround, there is still no actual explanation or solution
>Realize that this is a cycle that many more users will struggle through unless a proper fix shows up
>Write this comment in hopes the issue might be reopened

