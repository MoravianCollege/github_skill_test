# Working with GitHub

This information is relevant to those using a repository through git, but mainly focuses on the attributes of the [Github Workflow](https://guides.github.com/introduction/flow/).

You should first, [Fork a github repository to your account](https://www.oreilly.com/library/view/learning-path-github/9781491972069/video257736.html) and then use this command to create a copy of the repository on your computer:

	git clone https://github.com/account/repository.git

## Remote Repositories

While using Github, and working with collaborators, there are many times that you must work in conjunction with members of the github community with their own forks and clones of the repository. 

In order to view the current remote repositories you have connection to, change into the git directory and use `git remote -v`. 

The output should look similar to this:

	origin	https://github.com/youraccount/repository.git (fetch) 
	origin	https://github.com/youraccount/repository.git (push)

In order to complete the Github workflow, it is important to have connection to *upstream*, or the master repository that you had forked from. This can be done:

	git remote add upstream https://github.com/account/repository.git
	
And now, the command `git remote -v` should display similarly to:

	origin		https://github.com/youraccount/repository.git (fetch) 
	origin		https://github.com/youraccount/repository.git (push)
	upstream	https://github.com/account/repository.git (fetch) 
	upstream	https://github.com/account/repository.git (push)

### Working with Upstream

You **NEVER** want to **PUSH TO UPSTREAM** when using this GitHub workflow. 

In order to elimate the panic that sets in when accidentally entering the command `git push upstream <branch>` we can disable to ability to push to upstream. When we ran `git remote -v`, we see that each remote repository has a `(fetch)` and `(push)` url associated with it. We need to change the `(push)` url in upstream to something that we do not have access to. 

	git remote set-url --push upstream DISABLE

Here, we `set` the url of where to `push` to in the remote repository named `upstream` the actual repository to a "url" named *DISABLE*. Now, run `git remote -v` again to see the state of the remote repositories

	origin		https://github.com/youraccount/repository.git (fetch) 
	origin		https://github.com/youraccount/repository.git (push)
	upstream	https://github.com/account/repository.git (fetch) 
	upstream	DISABLE (push)
	
**WARNING: IF YOU DO NOT SEE THIS UPDATE TO THE REMOTE REPOSITORIES, DO NOT CONTINUE**

From here, we can try the scary command

	git push upstream master
	---
	fatal: 'DISABLE' does not appear to be a git repository
	fatal: Could not read from remote repository.
	
	Please make sure you have the correct access rights
	and the repository exists.

And now, all of you developers that have followed these steps can

* Take a sigh of relief that if you ever accidentally push to upstream that it will not work
* Prank your managers or coworkers when using the command
* Teach others this technique to ensure that they do not accidentally push to a remote repository in which they do not have access