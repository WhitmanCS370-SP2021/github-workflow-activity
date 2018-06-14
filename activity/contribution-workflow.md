# Contribution Workflow

## Prepare to work on an issue

### Find or create, and claim an issue

__Assumptions__

* You are the contributor.
* You are signed into GitHub.

__Instructions__

1. Navigate to your team's repository on GitHub (_not_ your fork).
2. Click the __Issues__ tab.
3. Search to see if there is an existing issue for what you want to do.
4. If no reasonable issue exists for what you want to do, create one.
5. If someone is assigned to the ticket or has claimed it by leaving a comment that they are working on it, move on, or maybe leave a comment asking about the progress and express interest in working on the issue.
6. If no-one is working on the issue assign yourself to the ticket (or leave a comment that you are working on it).
7. Help your recorder note the issue number of the issue you will be working on.

Congratulations, you now have a claimed issue for the work you plan to do.

Issues provide a way for developers to collaborate. They are used for many purposes including proposing and discuss ideas; prioritizing, sizing, and valuing requests; clarify requirements; verify bugs; and generally to coordinate development efforts. When looking for something to work on, use the issue tracker to find issues that the community (and the maintainers in particular) are interested in. Otherwise you may be working on something that will never be accepted.


### Create a feature branch and a pull request (PR) for your work

__Assumptions__

* You are the contributor.
* You have claimed an issue for the work you plan to do.
* You have a terminal opened and positioned to the root of your local clone.
* You are signed into GitHub.

__Instructions__

1. You are going to create a new branch to hold your work. New branches should always be branched from master. So first ensure that the master branch is checked out.
    ```
    git checkout master
    ```
2. Also you should always make sure that you start your branch based on the most recent copy of master. So let's pull changes from upstream (your team's repository on GitHub). In this activity, there shouldn't be any new changes in upstream, but this is a good habit to get into. So let's practice. At the same time, let's make sure your fork has those changes too.
    ```
    git pull upstream master
    git push origin master
    ```
2. Create the feature branch for the issue. Name it something short but meaningful and relevant to the issue. Replace BRANCH_NAME in the command below with your chosen name.
    ```
    git branch BRANCH_NAME
    ```
3. Checkout the branch you just created. Checking out a branch makes it the active branch so that any new commits you make will be added to this branch.
    ```
    git checkout BRANCH_NAME
    ```
4. Create an empty commit so that you can immediately issue a pull-request in the steps below. (Alternatively you could make a small change, stage it, and commit it. For now, just create an empty commit.)
    ```
    git commit --allow-empty -m "Start BRANCH_NAME"
    ```
5. Push your new branch containing the empty commit to your fork. Recall that your clone has a remote named `origin` that points to your fork. At the same time, use `-u` to tell git to track this remote branch with the local branch with the same name. Basically you are telling git that the new remote and local branches mean the same thing. You only use `-u` when you first create and push a branch.
    ```
    git push -u origin BRANCH_NAME
    ```
6. On GitHub, navigate to your fork.
7. Open a PR by clicking __New pull request__ (subtle grey button in the middle) or __Compare & pull request__ (big green button on the right).
8. Make sure that
    * The base repository is set to your team's repository under the organization
    * The base branch is set to master
    * The compare repository is set to your fork of the team's repository
    * The compare branch is set to your feature branch (e.g., BRANCH_NAME)
9. Briefly describe what you plan to do, and mention the issue that this PR is addressing. Mention the issue by putting its issue number in the body using this format: `#i` where `i` is the issue number. When GitHub sees this, it cross-references the issue and the PR allowing folks to easily to get from one to the other.
10. Click the __Create pull request__ button.

Congratulations! You have created a feature branch to hold the changes you will make while working on the issue. You have also opened a PR for this feature branch back to the upstream repository. This will allow others to follow your progress as you work. Also, the PR is a place where developers can discuss designs and implementations for solutions to issues.


## Work on the issue

__Assumptions__

* You are a contributor.
* You have a terminal opened and positioned to the root of your local clone.
* You have the feature branch for the issue checked out.
* You have an open PR associated with the feature branch.

__Instructions__

1. Make a small change using your standard development environment (e.g., Atom.io, Notepad++, Eclipse, etc.).
2. Test the change to make sure it works. Again, use whatever development tools you like.
3. Stage your changes.
    ```
    git add .
    ```
4. Confirm that only files that should be committed are staged.
    ```
    git status
    ```
5. If there are files staged that shouldn't be (e.g., anything that can be generated from source, personal/private configurations or data, etc.) complete [Unstage changes](unstage-changes.md). When you are done, return here and continue.
6. Commit changes and provide a good commit message.
    ```
    git commit
    ```
7. Push your changes that are in FEATURE_BRANCH to your fork.
    ```
    git push origin FEATURE_BRANCH
    ```

Congratulations, you have made a change, committed it to your feature branch, and pushed it up to your fork, which automatically updates the PR associated with your feature branch!

* If you are not done working on the issue, return to [Work on the issue](#work-on-the-issue).
* If you give up, close the PR on GitHub and then go to [Clean up](#clean-up).
* If you think your work is ready to be upstreamed, continue to the next section.


## Collaborate to upstream your work

### Update your PR with changes in upstream

__Assumptions__

* You are the contributor.
* You have a terminal opened and positioned to the root of your local clone.
* You have a feature branch and a corresponding PR opened back to the upstream repository.

__Instructions__

1. Synchronize master
    ```
    git checkout master
    git pull upstream master
    git push origin master
    ```
2. Merge changes from master into your feature branch.
    ```
    git checkout FEATURE_BRANCH
    git merge master
    ```
3. If there are conflicts, follow GitHub's instructions for [Resolving a merge conflict using the command-line](https://help.github.com/articles/resolving-a-merge-conflict-using-the-command-line/). Be sure to test your changes before committing them. Return here when you are done.
4. Test the merged copy. If there are any problems, return to [Work on the issue](#work-on-the-issue) and continue from there.
5. Update your fork and the PR
    ```
    git push origin FEATURE_BRANCH
    ```

Congratulations, your PR is now up-to-date with the latest changes from upstream. Time to request a review.


### Request a review

__Assumptions__

* You are the contributor.
* You have an open PR.
* You are signed into GitHub.

__Instructions__

1. Navigate to your PR on the team's repository on GitHub.
2. Make a comment. In that comment at-mention one of your team-members who will play the role of _matainer_ (e.g., `@person`), and ask them to please review your work.


### Maintainer reviews the PR

__Assumptions__

* You are the maintainer.
* You are signed into GitHub.

__Instructions__

1. Navigate to the PR that needs reviewing on GitHub.
2. Review the changes and make sure they are up to the project's standards. Many projects have style guidelines and acceptance criteria such as "must pass all tests" and "contributions must include unit tests". The maintainer often must merge the contributor's feature branch into master in a local clone and confirm that it works as expected. As this activity is about training contributors, we will not go into the details about how to be a maintainer here.
3. After reviewing the PR, do one of the following (refer to the instructions in the [activity](README.md) for which you should pick)
    * Reject the PR by closing it and leaving a message of why you are closing it.
    * Accept the PR by merging it into master: choose "squash and merge" strategy for now and click __Merge pull request__.
    * Request modifications to the PR if it needs work by leaving a message in the PR indicating what needs to be done.


### Contributor decides what to do next

__Assumptions__

* You are the contributor.

__Instructions__

* If the _maintainer_ merged your PR into the master branch in the team repository, go to [Clean up](#clean-up).
* If the _maintainer_ closed the PR without merging (maybe because it's obsolete, or not a feature the maintainer wants, etc.), go to [Clean up](#clean-up).
* If the _maintainer_ asked for adjustments to your work, return to [Work on the issue](#work-on-the-issue) and make the requested changes.


### Clean up

__Assumptions__

* You are the contributor.
* You have a terminal opened in the root of your local clone.

__Instructions__

1. Checkout the master branch, update master with changes from upstream, and push those changes to your fork. This synchronizes master across your team's repository, your fork, and your clone.
    ```
    git checkout master
    git pull upstream master
    git push origin master
    ```
2. Delete the feature branch from your local repository.
    ```
    git branch -d FEATURE_BRANCH
    ```
    Note: if the last statement complains that the branch has not been merged, you may be trying to delete the wrong branch or the maintainer may have used a "merge" strategy that was not a merge at all. So first, check that you have the correct branch and that your pull-request for that branch has actually been merged. If so, and you are really, really, REALLY sure, then force the delete with a capital "D": `git branch -D FEATURE_BRANCH`.
3. Delete the feature branch from your fork.
    ```
    git push -d origin FEATURE_BRANCH
    ```

Congratulations, having cleaned up your repositories you have completed this workflow!