# git workflow


## Step1:  Create/clone a git repo.
	
```BASH
	    
	git clone <repo url>
	git remote add upstream <original repo link>
```
### Description:-

    First clone the repository.
    Then set the upstream repository(the original repository)



## Step2: Create a branch to make local changes.

```BASH
	  
	git checkout -b <branch name>
```
### 2.1: Add default text editor to the git
```BASH
	git config --global core.editor "subl -n -w"
```

### Description:-
 	Making a branch in the local forked repostory.


## Step3: Make changes, add file and commit file to the branch.
```BASH
	git add --all/git add <file name>
	git commit 
```


#### Description:- 
	 Make changes to the file, then add the file to staging area, from where you can commit.
	 [how to write a good commit message](http://api.coala.io/en/latest/Developers/Writing_Good_Commits.html)


## Step4: Push the changes to the forked repository.
```BASH
	git push origin <branch name>
```
### Description:-
	Pushing the changes to the forked repository, so that you can make a pull request to the upstream.


## Step5: Create a pull request from the GUI of any client.

## Step6 : If changes requested, create change and undo/amend commit
```BASH
	git commit -a --amend
	git push -f origin <branch-name>
```

### Description:- 
	Make the changes as requested by the reviewer.
	Ammend the original commit.(Don't push multiple commits because all of the commits gets stacked into a single one, multiple commits don't override the original commit).
	Force push the changes.

		
