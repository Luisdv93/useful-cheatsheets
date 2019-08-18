# Git Cheatsheet

<div style="background-color: #515964; color: #FFF; font-weight: 700; text-align: center; margin-top: 30px; margin-top: 30px">MOST USED</div>

```
git status: To see changed files in your working directory

git add . : Add all current changes to the staged area

git commit -m "commit msg":  Commit previously staged changes

git checkout <branch>: Switch HEAD branch

git branch -b <new-branch>: Create a new branch based on your current HEAD and change to that branch

git branch -d <branch>: Delete local branch

git pull <remote> <branch>: Download changes and directly merge/integrate into HEAD

git push <remote> <branch>: Publish local changes on a remote

git merge <branch>: Merge <branch> into your current HEAD
```

<div style="background-color: #515964; color: #FFF; font-weight: 700; text-align: center; margin-top: 30px; margin-top: 30px">CREATE</div>

#### Clone an existing repository

```
git clone <link>
```

#### Create a new local repository

```
git init
```

<div style="background-color: #515964; color: #FFF; font-weight: 700; text-align: center; margin-top: 30px">LOCAL CHANGES</div>

#### Changed files in your working directory

```
git status
```

#### Changes to tracked files

```
git diff
```

#### Add all current changes to the staged area

```
git add .
```

#### Add some changes in <file> to the staged area

```
git add -p <file>
```

#### Commit all local changes in tracked files

```
git commit -a
```

#### Commit previously staged changes

```
git commit -m "commit msg"
```

#### Change the last commit

```
git commit -amend
```

<div style="background-color: #515964; color: #FFF; font-weight: 700; text-align: center; margin-top: 30px">COMMIT HISTORY</div>

#### Show all commits, starting with newest

```
git log
```

#### Show changes over time for a specific file

```
git log -p <file>
```

#### Who changed what and when in the <file>

```
git blame <file>
```

<div style="background-color: #515964; color: #FFF; font-weight: 700; text-align: center; margin-top: 30px">BRANCHES & TAGS</div>

#### List all existing branches

```
git branch -av
```

#### Switch HEAD branch

```
git checkout <branch>
```

#### Create a new branch based on your current HEAD and change to that branch

```
git branch -b <new-branch>
```

#### Create a new tracking branch based on a remote branch

```
git checkout --track <remote/branch>
```

#### Delete local branch

```
git branch -d <branch>
```

#### Mark the current commit with a tag

```
git tag <tag-name>
```

<div style="background-color: #515964; color: #FFF; font-weight: 700; text-align: center; margin-top: 30px">UPDATE & PUBLISH</div>

#### List all currently configured remotes

```
git remote -v
```

#### Show information about a remote

```
git remote show <remote>
```

#### Add new remote repository, named <remote>

```
git remote add <shortname> <url>
```

#### Download all changes from <remote>, but don't integrate into HEAD

```
git fetch <remote>
```

#### Download changes and directly merge/integrate into HEAD

```
git pull <remote> <branch>
```

#### Publish local changes on a remote

```
git push <remote> <branch>
```

#### Delete a branch on the remote

```
git branch -dr <remote/branch>
```

#### Publish your tags

```
git push --tags
```

<div style="background-color: #515964; color: #FFF; font-weight: 700; text-align: center; margin-top: 30px">MERGE & REBASE</div>

#### Merge <branch> into your current HEAD

```
git merge <branch>
```

#### Rebase your current HEAD onto <branch>. Don't rebase published commits!

```
git rebase <branch>
```

#### Abort a rebase

```
git rebase --abort
```

#### Continue a rebase after resolving conflicts

```
git rebase --continue
```

#### Use your configured merge tool to solve conflicts

```
git mergetool
```

#### Use your editor to manually solve conflicts and after resolving mark file as resolved

```
git add <resolved-file>
git rm <resolved-file>
```

<div style="background-color: #515964; color: #FFF; font-weight: 700; text-align: center; margin-top: 30px">UNDO</div>

#### Discard all local changes in your working directory

```
git reset --hard HEAD
```

#### Discard local changes in a specific file

```
git checkout HEAD <file>
```

#### Revert a commit by producing a new commit with contrary changes

```
git revert <commit>
```

#### Reset your HEAD pointer to a previous commit and discard all changes since then

```
git reset --hard <commit>
```

#### Reset your HEAD pointer to a previous commit and preserve all changes as unstaged changes

```
git reset <commit>
```

#### eset your HEAD pointer to a previous commit and preserve uncommited local changes

```
git reset --keep <commit>
```

<div style="background-color: #515964; color: #FFF; font-weight: 700; text-align: center; margin-top: 30px; margin-top: 30px">GIT TRICKS</div>

## 1. Checkout a single file from another branch

Have you ever destroyed a file and just wished you could have a fresh start? Or needed the changes you made in one file in another branch? This command lets you grab just one file from another branch.

This is an effective trick if cherry-pick would pick up other files that you don't need.

```
git checkout some-other-branch -- yarn.lock

You can use the same trick to checkout one file from a specific commit.

git checkout 9146367 -- yarn.lock
```

## 2. View the log without merge commits

Merge commits annoy some people. In fact, some people would rather never use the merge command because they are so annoyed by merge commits.

Personally, I think they are an important part of the history of a project, and you shouldn't try to circumvent them in your workflow.

That being said, if you want to look at a project's history in at a glance, you can use this flag to filter out merge commits.

```
git log --oneline --no-merges
```

## 3. Get rid of all untracked changes

Pretty self-explanatory, but in case you're not familiar with the idea:

If you create a new file that didn't previously exist in the git history, you've made an untracked change. To start tracking that file, you'd need to commit it to the repo.

Sometimes, you change your mind halfway through a commit and really just want to start over without all the changes you've got. Well, git checkout . will get rid of all the tracked changes you've made, but your untracked changes will still be floating around. To remedy that, we've got git clean.

```
git clean -f -d
```

## 4. Print out a cool visualization of your log

This one mostly just makes you look cool. It can be useful, though, to visualize all of your long standing branches.

```
git log --pretty=oneline --graph --decorate --all
```

## 5. Ask git for a changelog

If you're looking for a condensed explanation of what changed, and who changed it, you can ask git to give you something that looks a lot like a changelog.

```
git shortlog <commit>..HEAD
```

In this example <commit> should be replaced with the commit you want to target for the beginning of your log. Basically with git shortlog eafbc3c..HEAD you're saying, "Show me what changed between commit eafbc3c and right now."

The shortlog is grouped by commit author and shows the first line of each commit message. If your commit messages are well-written this should give you a solid idea of what each commit actually did.

You can do cool tricks like git shortlog HEAD~20.. to get the shortlog for the last 20 commits.

## 6. View the log for a specific date range

In a similar vein of thinking, you might need to see what changed in a repo between two days.

Thankfully, git has your back. The git log command accepts --since and --until as flags.

So if I wanted to see what happened in Solidus between February 10th, 2016 and February 19th, 2016 I could run:

```
git log --since='FEB 10 2016' --until='FEB 19 2016'
```

## 7. List all git aliases

Sometimes you might alias a few commands and forget them later, or maybe there are some aliases defined by a shared config you use.

This is a trick I found somewhere, and even though it's not exclusively a feature of git, we are taking advantage of the git config command.

```
git config -l | grep alias | sed 's/^alias\.//g'
```

Try it out, see if you have any forgotten aliases!

## 8. Search for commits that include a keyword

If you know exactly what piece of code you are looking for, or exactly what keyword you need to find changes on, you can search the log by code.

This will give you a list of commits that somehow affected a line of code or text containing your search string.

```
git log -S"config.menu_items"
```

In this example, I'll find a list of commits that somehow manipulated the string config.menu_items.

## 9. Get the date of the earliest commit in a repository

Occasionally, when I want to see exactly how old an Open Source project is, or I'm trying to figure out when a repo was made, I ask git to tell me when the first commit was made.

```
git log --date-order --format=%cI | tail -1
```

## 10. See the number of commits each person has made in the last month

This is something that I generally don't need, but occasionally I am stuck on a project and need to figure out who I should ask for help.

The easiest way for me to do that is to figure out who worked on the repository most recently. With this command, you can swap out --since='1 month ago' to whatever timeframe you think makes the most sense.

```
git shortlog --summary --since='1 month ago'
```

## 11. Show all ignored files

```
git ls-files --others -i --exclude-standard
```

## 12. List all unmerged branches branches

This snippet lists every branch that hasn't been merged. You can remove the -a flag if you don't want to include branches on your remotes.

```
git checkout master && git branch -a --no-merged
```

## 13. List all changes to a specific file, even if it's been renamed

This is a super handy trick. With this command, you can see all of the commits that have touched a file.

Because git is awesome, it will show you the changes to that file even if the name has been changed at some point in its history.

```
git log --follow -p -- <file_path>
```

## 14. Delete local branches that have been merged into master

If you find that you have a lot of random branches on your machine that are no longer needed, you can practice good git hygiene by deleting them.

This snippet will check for any branches that have been merged into master and delete them for you automatically.

Be careful with this one, if you are afraid of deleting old branches.

```
git checkout master
&& git branch --merged master
| grep -v "master"
| xargs -n 1 git branch -d
```

## 15. Show the last time each local branch changed

During the lifespan of a project, it's possible that some branches get abandoned.

The following snippet is a quick way to figure out if you have a branch locally that hasn't been updated in a long time.

```
git for-each-ref --sort=committerdate refs/heads/
--format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset) - (%(color:green)%(committerdate:relative)%(color:reset))'
```
