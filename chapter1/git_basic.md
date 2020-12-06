## 1.     Git 基础  

### Config

#### gitate

In our automation test project native git command is enough for us. But we can also enable a useful tool called gitate. The most used command from gitate is git update. To enable gitate please use following command.

 

gitate init --global

 

#### . gitignore

When we want git to ignore some file in the project, such as generated files during Smartest running. We can create a .gitignore file under each project folder, this file will tell git which file should be ignored. The complete setting information please check the official document. Here is some example we often used.

 

\#To ignore every under this folder except project folder

/*

!/project

 

We can use .gitignore file in sub folders too. The rules in sub folder will overwrite the rules in parent folder, but the rules is only work for the folder it’s in and sub folders under that folder, it can’t set the rule for its’ parent folder. If parent folder has already ignore the .gitignore file in sub folder, for example use * in the rule setting, the rules in the sub folder will also be ignored. 

 

.gitignore file can set rule to ignore itself, and the rules in this file is still work. It is useful when we working on one project and want to ignore the changes made to other projects, we can create a .gitignore file under the st8-gui-automation-test folder, then add rules to ignore other projects and .gitignore itself, the reason we should ignore itself is that other people may create .gitignore file in the same place, and track the file will overwrite each other. But in some place we recommend track the .gitignore file, for example in the workspaces folder, because we only want to keep an empty workspaces folder, and the rule for everyone is the same.

 

#### Add SSH key to bitbucket

Got to bit bucket web site, from your head portrait select manage account -> SSH keys -> add key. Copy the key file content to it. 

​                                     

 

Get key content by this command.

 

$ cat [Linux home]/.ssh/id_rsa.pub

 

### Command    

#### Clone the project

The first thing of making the test case is to clone the project to you local. Before clone, you need to make sure the ssh key had been added to your account in the bitbucket website.

 

$ git clone ssh://git@socgit.advantest.com:7999/soc/st8-gui-automation-test.git



 

#### Git update from master branch

If you want to get the latest code in the master branch, you can use update command. Before the update, please commit all you changes or stash them.

 

$ git update

 

#### Commit your change

After the work is done, you need to save the change to a commit. Do not add irrelevant things together, sometimes you may need to revert the commit because something went wrong. Because git management is base on commits, we can only revert all the changes in the commit. 

 

To commit you change, first you need add the change to the cache, you can choose files to be added to the commit 

 

$ git add [file name] [file name] ...

 

Or you can add all changes at once use option -u 

 

$ git add -u

 

Save and add message for your commit. The message should be easy to seperate from other commit messgae.

 

$ git commit -m "[message]"

 

#### Push you change to the server

After commit, we can push commits to the server side. If we want to make a pull request, you need to push the commits to the sever. It can also be a backup when git update cause conflict. 

 

$ git push

 

#### Create your own branch

Create local branch

 

$ git branch [branch name]

 

switch to a branch

 

$ git checkout [branch name]

 

create local branch and switch to it


 $ git checkout -b [branch name]

 

#### check the changes

check the file has not been add to cache

 

$ git diff [file name]

 

check the file has been add to cache

 

$ git diff –cached [file name]

 

#### Save your changes temporary place

save the changes

 

$ git stash

 

check your save

 

$ git stash list

 

recover your last save

 

$ git stash pop

 

 

delete your last save

 

$ git drop

 

 

#### reset

command:

$ git reset [commit number]

 

this command will delete the commit but remain the file changes.

 

#### hard reset

command:

$ git reset --hard [commit number]

 

this command will not only delete the commit, but also recover the changes to the commit you set.

 

be careful when using reset command, if others got the commits you reset and make further changes, after you reset the commit, all the changes make by other people will be gone too. So there is a more safe way which is by revert command.

 

#### revert commit

command:

$ git revert [commit number]

 

This is command is only work for one commit. It will make the change in the opposite way and create a new commit. It will not discard other's change based on the reverted commit. 

 

 

### Scenario

#### typical work scenario

After work is done, use git status check the file status, use git add to add new files and modified files to the cache, use git commit to save all changes in the cache to a commit. Use git push to the server. Use git update to get update from master, to ensure the changes we made will not cause conflict, if any conflict happed, we must fix it and commit the fix then push to server again. 

 

Got to the bitbucket website, create pull request from the branch we are using to master branch. Add the reviewer. The reviewer will receive a email and check the pull request we made. After check is done, the change will be merged to the master branch. 

 

#### Hot fix scenario

Sometimes during the procedure development, a urgent bug is found, we need fix the bug first. We can use git stash to save all the changes which have not been commit yet. The file go back to the stat of last commit. Then use git update to get latest change of other people, it will ensure you the same code when bug is found. 

 

After the bug is fixed, push the commits to the server, then use git update to check other people’s change, if no conflict is found, use git stash pop to recover the work you didn’t save to a commit, then continue developing the procedure.  

 

 