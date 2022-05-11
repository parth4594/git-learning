# git-learning


## git init
git add README.md

git commit -m "first commit"

git branch -M master

git remote add origin 

git push -u origin master

## Git Workflow
There are several publicized Git workflows that may be a good fit for your team. Here, we will discuss some of these Git workflow options.

The Centralized Workflow is a great Git workflow for teams transitioning from SVN. Like Subversion, the Centralized Workflow uses a central repository to serve as the single point-of-entry for all changes to the project. Instead of trunk, the default development branch is called main and all changes are committed into this branch. This workflow doesn’t require any other branches besides main.

Developers start by cloning the central repository. In their own local copies of the project, they edit files and commit changes as they would with SVN; however, these new commits are stored locally - they’re completely isolated from the central repository. This lets developers defer synchronizing upstream until they’re at a convenient break point.

**git push** will push the new committed changes to the central repository. When pushing changes to the central repository, it is possible that updates from another developer have been previously pushed that contain code which conflict with the intended push updates. Git will output a message indicating this conflict. In this situation, git pull will first need to be executed.

**git push origin main:** Remember that origin is the remote connection to the central repository that Git created when John cloned it. The main argument tells Git to try to make the origin’s main branch look like his local main branch. Since the central repository hasn’t been updated since John cloned it, this won’t result in any conflicts and the push will work as expected.

**In case of a conflict**  since the local history has diverged from the central repository, Git will refuse the request with a rather verbose error. This prevents us from overwriting official commits. We need to pull existing updates to our repository, integrate them with our local changes, and then try again.

use git pull --rebase origin main

We can use git pull to incorporate upstream changes into our repository. This command is sort of like svn update—it pulls the entire upstream commit history into our local repository and tries to integrate it with our local commits. The --rebase option tells Git to move all of our commits to the tip of the main branch after synchronising it with the changes from the central repository.The pull would still work if you forgot this option, but you would wind up with a superfluous “merge commit” every time someone needed to synchronize with the central repository. For this workflow, it’s always better to rebase instead of generating a merge commit.

The great thing about Git is that anyone can resolve their own merge conflicts. We would simply run a git status to see where the problem is. Conflicted files will appear in the Unmerged paths section.

**Git checkout** works hand-in-hand with git branch. The git branch command can be used to create a new branch. When you want to start a new feature, you create a new branch off main using git branch new_branch. Once created you can then use git checkout new_branch to switch to that branch. Additionally, The git checkout command accepts a -b argument that acts as a convenience method which will create the new branch and immediately switch to it. You can work on multiple features in a single repository by switching between them with git checkout. 

**Head:** A Git repository is a collection of objects and references. Objects have relationships with each other, and references point to objects and to other references. The main objects in a Git repository are commits, but other objects include blobs and trees. The most important references in Git are branches, which you can think of as labels you put on a commit.

HEAD is another important type of reference. The purpose of HEAD is to keep track of the current point in a Git repo. In other words, HEAD answers the question, “Where am I right now?”

**Detached Head** This is a warning telling you that everything you’re doing is “detached” from the rest of your project’s development. If you were to start developing a feature while in a detached HEAD state, there would be no branch allowing you to get back to it. When you inevitably check out another branch (e.g., to merge your feature in), there would be no way to reference your feature. The point is, your development should always take place on a branch—never on a detached HEAD. This makes sure you always have a reference to your new commits. However, if you’re just looking at an old commit, it doesn’t really matter if you’re in a detached HEAD state or not.

## How Do I Fix a Detached HEAD in Git?
You can’t fix what isn’t broken. As I’ve said before, a detached HEAD is a valid state in Git. It’s not a problem. But you may still want to know how to get back to normal, and that depends on why you’re in this situation in the first place.

### Scenario #1: I’m Here by Accident
If you’ve reached the detached HEAD state by accident—that is to say, you didn’t mean to check out a commit—going back is easy. Just check out the branch you were in before:

git checkout <branch-name>

If you’re using Git 2.23.0 or newer, you can also use switch instead of checkout:

git switch <branch-name>

### Scenario #2: I’ve Made Experimental Changes and I Want to Discard Them
You’ve entered the detached HEAD state and made a few commits. The experiment went nowhere, and you’ll no longer work on it. What do you do? You just do the same as in the previous scenario: go back to your original branch. The changes you made while in the alternate timeline won’t have any impact on your current branch.

### Scenario #3: I’ve Made Experimental Changes and I Want to Keep Them
If you want to keep changes made with a detached HEAD, just create a new branch and switch to it. You can create it right after arriving at a detached HEAD or after creating one or more commits. The result is the same. The only restriction is that you should do it before returning to your normal branch.

Let’s do it in our demo repo:

git branch alt-history
git checkout alt-history

Notice how the result of git log –oneline is exactly the same as before (the only difference being the name of the branch indicated in the last commit)
