# Version control
Mercurial and git are distributed
Mercurial and git treat all repositories equal
Every operation in git is local , Everyone has complete history, No central authority.
Changes can be shared without server
Git branching is one o fthe most poweful feature of Git
Master isdefault branch created




# Git commands
"HEAD" is a symbolic name for the currently checked out commit. HEAD always points to the most recent commit which is reflected in the working tree. Most git commands which make changes to the working tree will start by chaning HEAD
Normally HEAD points to a branch name.
Detaching HEAD just means attaching it to a commit instead of a branch.
``` git checkout <sha>``` It will move the HEAD to the required commit.

# Common commands

``` git pull --rebase ; git push``` <- rebased our work onto new commits from remote. publish our work on remote.

3 stages in git
  1. Working directory
  2. Staging area (aka index)
  3. Repository (.git directory)

**Git Branching**
  1. git branch <branch name> <- create a branch
  2. git checkout -b <branch name> <- go to already created branch
  3. To **merge** a branch with master branch, first check out the master branch and then "git merge <branch name>"
  4. git branch -d <branch name> <- delete a branch
  5. If master branch has progressed before merging then it may cause conflicts. Also in this case merging create non linear structure. Solution is "REBASE"
  6. Rebase works in 2 steps. First undo changes on feature branch and then reapply changes on master branch HEAD
  7. git rebase master; git checkout master ; git merge <branch name>
  8. git branch -m <old branch> <new branch> <- rename a branch
  ```git branch -d <branch name>``` <- delete a branch
  ```git checkout -b <branch name> <sha>``` <- recover a branch
  ```git branch -f main HEAD~3``` <- move main to 3 parents before HEAD by force 
  ```git reset <commit>``` Reset will move branch BACKWARDS in time to an older commit as if the commits after it were nerver made in first place.
  ``` git revert <commit>``` Git rever works great locally in rewriting the history but does not work for remote branches. In order to reverse changes and share those changes with otehrs use REVERT
``` git cherry-pick <commit1> <commit2> <commit3>``` <- A way of saying I would like to copy a series of commits below my current location (HEAD). 
``` git rebase -i <commit> ``` <-  Interactive rebase with flexibility to select/deselect/edit/combine commits. Its alternative for cherry-pick.
                                  
``` git rebase <base> <target>```                                  
``` git commit --amend``` to edit the commit     
``` git checkout main^``` <- first parent
``` git checkout main^2``` <- second parent
``` git checkout HEAD~^2~2``` <- combining traversal
``` git branch -b bugWork main^^2^ ``` <- combining 2 commands
``` git push ``` git push is opposite of git pull. push with no argument depends on push.defaults setting      
``` git pull --rebase ; git push``` <- used to take changes from remote to local. Merge with local and rebase. Then push to the remote.
- For locked remote main need to raise PULL REQUEST
- origin/main can not be moved with ``` git branch -f <> <> ```. It will only move with pull or push
- Git push will only push the branches ending in the "main" commit branch
- Some developers love to preserve history and thus prefer merging. Others (like myself) prefer having a clean commit tree and prefer rebasing. It all comes down to preferences :D  
- During a pull operation, commits are downloaded onto o/main and then merged into the main branch. The implied target of the merge is determined from this connection.
- During a push operation, work from the main branch was pushed onto the remote's main branch (which was then represented by o/main locally). The destination of the push is determined from the connection between main and o/main.
- The main branch is set to track o/main -- this means there is an implied merge target and implied push destination for the main branch.
- You may be wondering how this property got set on the main branch when you didn't run any commands to specify it. Well, when you clone a repository with git, this property is actually set for you automatically.
- You can make any arbitrary branch track o/main, and if you do so, that branch will have the same implied push destination and merge target as main. This means you can run git push on a branch named totallyNotMain and have your work pushed to the main branch on the remote! There are two ways to set this property. The first is to checkout a new branch by using a remote branch as the specified ref. Running ```git checkout -b totallyNotMain o/main ``` .Creates a new branch named totallyNotMain and sets it to track o/main.
- Another way to set remote tracking on a branch is to simply use the git branch -u option. Running
```git branch -u o/main foo```
will set the foo branch to track o/main. If foo is currently checked out you can even leave it off:
```git branch -u o/main```
- During a clone, git creates a remote branch for every branch on the remote (aka branches like o/main). It then creates a local branch that tracks the currently active branch on the remote, which is main in most cases.
- Once git clone is complete, you only have one local branch (so you aren't overwhelmed) but you can see all the different branches on the remote (if you happen to be very curious). It's the best of both worlds!
 
 
## Git Push
 ``` git push <remote> <place> ```
 ``` git push origin main ``` <- Go to the branch named "main" in my repository, grab all the commits, and go to branch "main" on the remote named "origin". Place whatever commits are missing on that branch and tell me when you are done. Keep in mind that since we told git everything it needs to know (by specifying both arguments), it totally ignores where we are checked out! e.g. ``` git push origin foo``` <- Go to the branch named "foo" grab all commits and got to "foo" branch on the remote named "origin". Place whatever commits are missing on the branch and tell me when you are done.
``` git push origin foo^:main``` <- push specific commit 
```git push origin main:<newbranch>``` <- create new branch while pushing
``` git push origin main:foo ``` ``` git push origin main^:foo ```
 
## Git fetch                                          
``` git fetch <remote> <place> ``` e.g. ``` git fetch origin foo ```
Git fetch only downloads the changes but does not merge. It does not update local non remote branches 
``` git fetch <remote> <source from local>:<destination on remote>``` <- source is place in remote and destination is place on local. If destination does not exist then the fetch will create it just like push command.
If no args are provided to fetch command then it just downloads all the commits from the remote onto all the remote branches.                                               

## git source parameter
Pushing nothing to remote branch deletes it. Fetchin nothing makes a new branch
``` git push origin :side```
``` git fetch origin :bugFix```                

## Git pull
``` git pull origin foo ``` is equivalent to ``` git fetch origin foo; git merge o/foo ```                                                   
``` git pull <remote> <source from remote>:<destination on local>``` 
``` git pull origin bar:foo ```
``` git pull origin main:side ```
  
## Git tag(aka anchor)**
   - Branch is liek separate thread but tag is lake a label.
   - Use of tag is to mark the release points
   - Tags can not be checked out                               
   - $git tag <- lists tags
   - $git tag v1.0 -m "some message" <commit> <- create tag with a message at specified commit. If commit is not selected then at HEAD
   - $git tag -a v1.0 <- opens default editor for longer message
   - ``` git describe <ref>``` <- describes where you are relative to the closest anchor or tag. Output of describe is as <tag>_<num commits>_g<ref>.
 **Git stash**
  - Stash is temporary store
  - ```$git stash``` <- stores working dir temporarily to stash
  - ```$git stash list``` <- show all stash
  - ```$fit stash apply``` <- reapply recent shash
                                    
## GitHub   
- One repository where we all sync up our changes
- Remote server is just simply a Git repository
- Github is one example of remote repository
- ``` git remote add origin <github url>``` <- origin can be replaced with any other word like remote-branch
- ``` git remote ``` Get names of all remotes
- ``` git remote -v ``` get names and details of all remotes
- ``` git clone <github url> ``` <- pulls up the remote repository locally and sets up the connection information
- After cloning origin/master is new branch is created called as tracking branch
- ``` git pull origin ``` "Pull" is Fetch + merge in one step. Fetches changes from remote master branch and merges with local master branch.
- Fetch is between remote repository to local repository. Merge is between local repository to working directory.                                   
- If remote branch has some more commits compared to last pull then need to perform rebase after pull to get the commits lienar and then push. ``` git rebase master ```
- We always checkout the branch with which we want to merge.
- Mergning after rebase will keep the origin/master pointer in old place. Local main pointer will come to the latest commit
- ``` git push origin``` To publish the changes to remote branch. This moves remote the pointer to latest commit. We are in complete in sync with remote.
- Git will reject the push if remote has newer changes                                    
- Always **"PULL THEN PUSH"** 
- ```git branch -a ``` to view all branches
- ``` git remote rename <old name origin> <new name>``` <- to rename the remote branch
- ``` git remote rm <remote branch name>``` <- to remove the remote branch
- Remote branches reflect state of remote repository in local repository. Remote branches are on your local repository and not on remote repository. One can not work directly on remote branch instead detached HEAD mode is triggered on checkout
- Remote repositories have different naming convension <remote name>/<branch name>. origin/main will only update when remote updates. Till then work on detached HEAD mode   
-```git fetch``` Downloads commits present in remote but missing in local repository  and updates the remote branches point. It does not however change your main branch or change anything about how your file system looks right now
  
.gitignore is added to the base project directory(parallel to .git directory). Need to commit it to repository.

- ```git add .```
- ```git commit```
- ```git commit``` -am "<message>" #for already commited files only
- ```git rm``` <- To remove the file tracking  for changes
- ```git status``` <- displays state of working directory and staging area
- ```git log``` <- options like "--oneline", "--grep=<pattern>", "git log <file>"
- ```git push```
- ```git config --global user.name="mannoj"``` #set username at global level to track checkin
- ```git config --global user.email="mannoj@gmail.com"``` #set username at global level to track checkin
- ```git checkout <branchname>```
- ```git pull origin ```
- ```git branch -f master C6``` # move master branch to the C6 commit as parent
- ```git reset``` <- Its a permanent Undo. Dangerous than "revert". Resets staging area to most recent commit but leaves working directory unchanged.
- ```git revert``` <- Undoes a commited snapshot. Its a safe way to undo changes. Doesnot change the project history.
- ```git cherry-pick <commits>```
- ```git rebase -i HEAD~4```
- ```git stash```
- ```git stash pop```
- ```git mege --abort```

#IF need to discard all local changes and get to the master branch
git fetch --all
git reset --hard origin/master

git fetch downloads the latest from remote without trying to merge or rebase anything.

Then the git reset resets the master branch to what you just fetched. The --hard option changes all the files in your working tree to match the files in origin/master

#Dependency resolve
mvn eclipse:eclipse

#Adding existing repo to Github
git add .
git commit -m "message"
git remote add origin <repository URL>
gir remote -v
git push origin master


# DOCKER Commands
docker pull selenium/hub
docker images
docker run -d -p 4444:4444 –name selenium-hub selenium/hub
http://localhost:4444/grid/console
docker run -d --link selenium-hub:hub selenium/node-chrome
docker contanier ls
docker info
docker run -it ubuntu bash
docker stop 96f3e6e1aed3

# Selenium grid
>java -jar selenium-server-standalone-2.41.0.jar -role hub

>java -jar selenium-server-standalone-2.41.0.jar -role node -hub
http://localhost:4444/grid/register -port 5556 -browser browserName=chrome
#Enalbe Hyper-V on win10
PowerS>Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
#create VM with Docker For windows
#Enable hypervisor 
# set up the external network switch
#restart
docker-machine create --driver hyperv testGrid
OR
docker-machine create -d hyperv --hyperv-virtual-switch "Primary Virtual Switch" manager1
OR #for local ISO
docker-machine create -d hyperv --hyperv-virtual-switch "Primary Virtual Switch" --hyperv-boot2docker-url file://localhost/Softs/Docker/boot2docker.iso testGrid1
#remember to select default external switch controller like Reltek for ethernet and wireless for wifi https://github.com/docker/machine/issues/4328

#switch to moby linux on docker with windows
docker run --privileged -it -v /var/run/docker.sock:/var/run/docker.sock jongallant/ubuntu-docker-client 
#go in to the new MV
>docker-machine ssh testGrid

#Docker deamon should already be present to use the VM as docker Host

#shutdown Docker Grid infrastructure
sudo docker stop $(sudo docker ps -a -q)
sudo docker rm $(sudo docker ps -a -q)

#to install ifconfig and other net commands on centos
#to start a docker machine
docker-machine start dev
yum install net-tools
