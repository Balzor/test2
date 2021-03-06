# Git for new Developers

## Creating a new repository :

1. Create a new repository from Github
1. On your local terminal navigate to where your repository would be on your machine
1. Type ```$ git init [project name]```
1. Create a local file. Could be done with ```$ touch README.md``` 
1. After creating your file type ```$ git add [file]``` or ```$ git add .```(to add all your changes if u want)
1. When we have all our changes ready we type ```$ git commit -m "[commit name]"``` to commit our changes/files
1. Because this our first commit to the repository before we push our changes to github we need to type  ```$ git remote add origin [our repository link]```
1. Now we are ready to push our repository to github with ```$ git push -u origin master```

## Branches

When working as team there will be times where many people will work on the same project. To avoid errors and confusion we use branches so each person would work 'separately' while working on the same project. To work on a branch, firstly we need to switch to the branch that we would like to work on.
1. On you your terminal while you are in your repository path we type ```$ git checkout -b [NewBranchName]``` to automatically create and switch to that newly created branch.
1. If you would like to switch to a branch that already exists type ```$ git checkout [BranchName]```
1. If you don't know the branch name type ```$ git branch -av``` to view all the remote and local branches

There are more commands that are helpfull with branches.
* ```$ git branch --merged``` will show all the merged branches
* ```$ git branch --no-merged``` will show all the branches that are not merged

## Merge / Pull Requests

After finishing some work on a branch the next step would be to merge these changes with either master or another branch.
1. First we need to be sure we are in the correct branch so we type ```$ git checkout [branch2]```
1. To merge we type ```$ git merge [branch1]``` so now branch 2 will b merged with branch 1

But if you are working with other people to avoid easily avoided errors, before merging we create pull requests, so other people will check our work and make sure everything is correct before merging.
1. After you push to your branch and your work is on github navigate to your branch on your github page and you will see a button that says **Compare & pull request**
1. After presing that button you will be redirected to a page that asks for a pull request Title and comments
1. When you are satisfied with your title and comments pres the **Create pull request** button
1. After a few seconds a button will appear that says **Merge pull request**
1. When your team reviews your work, if thet are satisfied with it, they will accept the Merge request and your work will be merged with the main branch
>> Remember to always do pull requests when working as a team

## Revert / Fake delete

At one point there migth be a chance that you commit something and then regret it. So how do we remove that mistake from our repo?
>> This will not remove the commit from the history, it will remove the changes that were intoduced in that commit as a new commit. This is done so that commit numbers will not be mixed between team members
1. On our terminal we type ```$ git log```. This will give us a list of our commits
1. All the commits will have a huge commit number like this *20fe6cb967f2a674d74a25f3a615343e096ea0e8*
1. We take the first 6 letetrs of that commit, in this case *20fe6c*
1. And we type ```$ git revert 20fe6c```
1. When we type ```$ git log``` again we will see that the latest commit has a description that says that this commit number changes have been reverted.

## Reset

If you are working on a seperate branch that no one else is working on you can use reset if you want your branch to move back to an earlier stage
1. On our terminal we type ```$ git log```. This will give us a list of our commits
1. All the commits will have a huge commit number like this *20fe6cb967f2a674d74a25f3a615343e096ea0e8*
1. We take the first 6 letetrs of that commit, in this case *20fe6c*
1. We type ```$ git reset --hard [commitNo]```
1. When we check our git log now we will see that alll commits that were introduced after our commit number are now gone
* There is also another version of reset, ```$ git reset --soft [commitNo]```, the difference between hard and soft is that hard will reset your working tree and files, but soft will just move to the commit, keeping the files unchanged and having them ready for commit
* Finally there is ```$ git reset --mixed [commitNo]``` as well. This will keep the files unchanged but it will not have them ready to commit
>> Remember to always commit and push in your branch

## Release

1. On your terminal
1. Type ```$ git tag [tagName]```
1. This is tag the latest commit with the specifed tag name
1. Now we type ```$ git push --tags```
1. This will release this tag (or more) to our repository under the releases tab

We can also release our work with a version and custom description
1. On your terminal instead of ```$ git tag [tagName]```
1. Type ```$ git tag -a v1.0.0 -m "Some message about the release"```
1. Now we type ```$ git push --tags```

## Removing an unused repository from local

Lets say for example instead of navigating to your desired folder to create a repository you type, 
```$ git init [project name]``` by mistake one folder back and now your whole hard drive is a repository.
1. When doing a git init a folder named **.git** is created
1. We find that folder and remove it
1. On your terminal type ```$ ls -a -li```
1. This will give you a detailed list of all the folders in that directory.
1. Make sure **.git** is in
1. Now you type ```$ rm -rf .git```
1. This will delete the the **.git** folder thus removing this directory as a repository
1. To make sure we were successful we type a ```$ git status```, if the response is ```Not a git repository``` then you did it

## Stashing work

On some cases you might want to work on something else but commiting your current changes would just mess up the project.
Our answer to this problem is ```$ git stash```
* firstly we are going to do a ```$ git status```
* something like this should pop out
```
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   fewf.txt
```
* now you don't want to commit this because it is unfinished, but you don't want to lose it either
* so we type ```$ git stash``` and this will show
```
Saved working directory and index state WIP on master: [commit number] [commit name]
```
* On the case above all the files that are untracked will not be stashed. If we want to stash these files as well we can
```
$ git stash --include-untracked
```
* this version of git stash does not include ignored files. To stash ignored files as well we do
```
$ git stash --all
```
* now if we run a git status again we will see that there is nothing to commit
But what if we stash a lot of things
* if we run ```$ git stash list``` we are going to see a list with all our stashes
```
stash@{0}: WIP on master: [commit no 1] [name1]
stash@{1}: WIP on master: [commit no 2] [name2]
stash@{2}: WIP on master: [commit no 3] [name3]
```

After we are all done with stashing our work there will come the time to bring them back
* for that to work we can just type ```$ git stash apply``` and our most recemt stash will appear. But if we want an older one we can type ```$ git stash apply stash@{2}``` and thats specified stash will come instead.

When you have your work again and you are sure you don't need it in your stash anymore type ```$ git stash drop stash@{0}``` to remove it from the list of your stashed workings.
