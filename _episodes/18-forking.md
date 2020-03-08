---
layout: episode
title: Forking workflow exercise
teaching: 10
exercises: 20
questions:
  - How can we collaborate with people who we might not know yet?
  - What is a fork?
  - What is a pull request or merge request?
  - What is code review?
  - How do teams collaborate on GitHub or GitLab or Bitbucket?
objectives:
  - Get a mental representation of what is happening on GitHub.
  - Get comfortable with the forking workflow.
keypoints:
  - Working with multiple remotes is not as scary as it looks.
  - "`origin` is just an alias."
  - We can add and remove remotes.
  - We can call these aliases as we like.
  - We synchronize remotes via the local clone.
  - "To see all remotes use `git remote -v`."
  - If you are more than one person contributing to a project, implement code review.
---


In this exercise, we make a fork, push to that fork, and make a pull
request to the "central" repository. Later we will exercise updating the individual forks
after changes from all participants have been merged.

As an example we will collaboratively develop a cookbook for taco recipes,
inspired by [tacofancy](https://github.com/sinker/tacofancy).

We recommend that you discuss with your neighbor throughout the exercise.

Objectives:

- Learn how to fork, modify the fork, and file a pull request towards the forked repo.
- Learn how to update your fork with upstream changes.

We will do this exercise on [GitHub](https://github.com) but also
[GitLab](https://gitlab.com) and [Bitbucket](https://bitbucket.org) allow
similar workflows and basically everything that we will discuss is transferable.

<div class="alert alert-dismissible alert-warning">
  <button type="button" class="close" data-dismiss="alert">&times;</button>
  <h4 class="alert-heading">We will work with a new repository for this exercise!</h4>
  <p>
    For this exercise we will fork a different repository compared to earlier today.
    Please step out of the repository and check that you fork the <b>forking</b>-workflow-exercise.
  </p>
</div>


### Part A: Fork and clone

First fork [this repository]({{ site.forking_workflow_exercise_url }})
into your namespace and then clone the fork to your computer.

Here is a pictorial representation of this part:

![]({{ site.baseurl }}/img/git-collaborative/forking/forking-1.svg)

This is how it looks after we fork:

*central*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-01.svg)

- A fork is basically a (bare) clone.
- The upstream repo and the fork are in principle independent repositories.
- When forking we copy all commits, all branches.

After we clone the fork we have three in principle independent repositories:

*central*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-01.svg)

*local*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-local-01.svg)


### Part B: Open an "issue" as a change proposal

Before we start any coding, open a new "Issue" on the central repository as a
"proposal" where you describe your idea for a recipe with the possibility to
collect feedback from others. After creating this issue note the issue number.
We will later refer to this issue number.

Discuss with your neighbor why it can be useful to open an issue before
starting the actual coding.


### Part C: Modify and commit

Before we do any modification, we create a new branch and switch to it: this is
a good reflex and a good practice. Choose a branch name which is descriptive of
its content.

On the new branch create a new file which will hold your recipe,
for instance `traditional_coderefinery_tacos.md` (but change the name). You can get inspired
[here](https://github.com/sinker/tacofancy/tree/master/full_tacos). Hopefully we all use different
file names, otherwise we will experience conflicts later (which is also interesting!).

There is also a file called `test.py` which will automatically verify whether your recipe contains the string
"taco" (case insensitive). This is there to slowly introduce us to automated testing.

Once you are happy with your recipe, commit the change and in your commit
message reference the issue which you have opened earlier with "this is my
commit message; closes #N" (use a more descriptive message and replace N by the
actual issue number).

And here is a picture of what just happened:

*central*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-01.svg)

*local*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-local-02.svg)


### Part D: Push your changes to the fork

Now push your new branch to your fork. Your branch is probably called something else than "feature". Also verify where
"origin" points to.

```shell
$ git push origin feature
```

*central*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-01.svg)

*fork*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-local-03.svg)


### Part E: File a pull request

Then file a pull request from the branch on your fork towards the master branch on the repository where you forked from.

Here is a pictorial representation for parts D and E:

![]({{ site.baseurl }}/img/git-collaborative/forking/forking-2.svg)

A pull-request means: "please review my changes and if you agree, merge them with a mouse-click".

Once the pull-request is accepted, the change is merged:

*central*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-local-03.svg)

Wait here until we integrate all pull requests into the central repo
together on the big screen.

Observe how the issues automatically close after the pull requests are merged
(provided the commit messages contain [the right keywords](https://help.github.com/en/articles/closing-issues-using-keywords)).


> ## (Optional) Exercise: try to send a conflicting pull request
>
> If you complete parts A-E much earlier than others, try to send another pull request
> where you anticipate a conflict with your first pull request.
{: .challenge}

> ## (Optional) Exercise: practice making changes to your pull request
>
> You can do that by pushing new commits to the branch where you sent the pull
> request from. Observe how they end up added to your pull request.
{: .challenge}


### Part F: Update your fork

We do this part **after the contributions from all participants have been integrated**.

Once this is done, practice to update your forked repo with the upstream
changes and verify that you got the files created by other participants.

Make sure that the contributions from other participants are not only on your local repository
but really also end up in your fork.

Here is a pictorial representation of this part:

![]({{ site.baseurl }}/img/git-collaborative/forking/forking-3.svg)

We will discuss two solutions:


#### Longer route

- Upstream repo receives other changes (other merged pull-requests)
- How do we get these changes to the forked repo?

```shell
$ git remote add upstream {{ site.forking_workflow_exercise_url }}.git
$ git fetch upstream
```

*central*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-local-04.svg)

```shell
$ git checkout master
$ git merge upstream/master
```

*central*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-02.svg)

*local*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-local-05.svg)

```shell
$ git push origin master
```

*central*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-03.svg)

*fork*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-remote-04.svg)

*local*: ![]({{ site.baseurl }}/img/git-collaborative/forking/github-local-06.svg)


#### Shorter route

Remotes are aliases. We can use remote URLs directly.

Here we pull from the central repo and push to our fork:

```shell
$ git checkout master
$ git pull {{ site.forking_workflow_exercise_url }}.git master
$ git push https://github.com/user/forking-workflow-exercise.git master
```

---

## Discussion point: naming

In GitHub or BitBucket asking someone to bring code from a forked repo or
branch to the main repo is called a **pull request**. In GitLab it is called a
**merge request**. Which one do you feel is more appropriate and in which
context?

---

## Always create a feature branch

- Never commit to the branch you wish to submit the pull request towards.
- For each pull request create a new branch.

Motivation:

- Limits the risk that commits get accidentally appended to an open pull request.
- History-rewrite (rebased and/or squashed commits) on the central repository does not lead to a diverging local default branch.

See also [this blogpost](https://blog.jasonmeridth.com/posts/do-not-issue-pull-requests-from-your-master-branch/) for an explanation.

---

## Code review

- You see what others are working on
- Collaborative learning
- OK if students and junior researchers review senior researchers
- Improves quality of the code
