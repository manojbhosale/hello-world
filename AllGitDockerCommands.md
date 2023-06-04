# Version control
Mercurial and git are distributed
Mercurial and git treat all repositories equal
Every operation in git is local , Everyone has complete history, No central authority.
Changes can be shared without server
Git branching is one o fthe most poweful feature of Git
Master isdefault branch created



# Git commands

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
  git branch -d <branch name> <- delete a branch
  git checkout -b <branch name> <sha> <- recover a branch
  
**Git Tag**
   - Branch is liek separate thread but tag is lake a label.
   - Use of tag is to mark the release points
   - $git tag <- lists tags
   - $git tag v1.0 -m "some message" <- create tag with a message
   - $git tag -a v1.0 <- opens default editor for longer message
   
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
` ``` git remote rm <remote branch name>``` <- to remove the remote branch

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
- ```git revert``` <- Undoes a commited snapshot. Its a safe way to undo changes. DOesnot change the project history.
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
