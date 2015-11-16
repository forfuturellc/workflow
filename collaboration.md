
# collaboration


## toc:

* [scm](#scm)
    * [configuration](#configuration)
    * [branching model](#branching-model)
    * [naming](#naming)
    * [hygiene](#hygiene)
    * [tips](#tips)
* [repository hosting](#repository-hosting)
    * [milestones](#milestones)
    * [issues](#issues)
    * [issue referencing](#issue-referencing)
* [peer review](#peer-review)
* [references](#references)


### scm:

We will be using [git][git] as our SCM.


#### configuration:

Ensure you have `git` configured correctly with your username and email address.
This ensures your commits are tracked easily.

```bash
$ git config user.name "your-username"          # your github username
$ git config user.email "john@example.com"      # your email-address, on Github
```


#### branching model:

The branching model used is similar to [this one][nvie-model].

At all times, 2 branches are maintained, namely **master** and **develop**.

The **master** branch, at all times, should remain stable and production-ready.
All tests on code in this branch should **always** pass.

The **develop** branch is the main branch used for developing. Assessment of
progress of the project will be done using this branch. Frequent commits are
expected on this branch.

Ultimately, there are three kinds of branches (except the ones stated above):

1. **feature branches**
1. **release branches**
1. **hotfix branches**

**Feature branches** should be branched from the **develop** branch, for the main purpose
of adding new features.

```bash
$ git checkout develop                      # checkout the develop branch
$ git checkout -b feature/twitter-login     # creating a new feature branch
```

Once the feature is completed, the branch should be merged back to **develop** branch.

```bash
$ git checkout develop                      # checkout the develop branch
$ git merge --no-ff feature/twitter-login   # merge the feature branch into develop branch
```

**Release branches** should be branched from the **develop** branch, for the purpose of making
a new release.

```bash
$ git checkout develop                      # checkout the develop branch
$ git checkout -b release/0.0.0             # creating a new release branch
```

Once a release has been prepared for the world, it should be merged to both **master** and
**develop** branch.

```bash
$ git checkout master                       # checkout the master branch
$ git merge --no-ff release/0.0.0           # merge release branch into master

$ git checkout develop                      # checkout the develop branch
$ git merget --no-ff release/0.0.0          # merge also into develop branch
```

**Hotfix branches** should be branched from the **master** branch, for the main purpose
of making quick fixes to bugs reported for code in production (in **master** branch).

```bash
$ git checkout master                       # checkout the master branch
$ git checkout -b hotfix/failed-login       # creating a new hotfix branch
```

Once the fix has been made and verified (with tests), the branch should be merged back
to **master** branch. It should also be merged to **develop** branch to ensure future versions
get the fix.

```bash
$ git checkout master                       # checkout the master branch
$ git merge --no-ff hotfix/failed-login     # merging the hotfix branch into master

$ git checkout develop                      # do the same for the develop branch
$ git merget --no-ff hotfix/failed-login    # merging into develop
```


#### naming:

When naming your feature, hotfix and release branches, follow these naming guidelines:

1. Prefix the branch name with the name of the type of branch i.e. if it's a feature branch,
the prefix would be `feature/`, `hotfix/` for hotfix branches and `release/` for release branches.
1. Add a short and descriptive label e.g. `feature/twitter-login`
1. Use dashes (-) in place of spaces
1. If several persons are working on same feature/release/hotfix, suffix the name with the
developer's username e.g. `hotfix/failed-login/gochomugo`


#### hygiene:

If a feature, release or hotfix branch is merged fully into the respective branches, it should
be deleted from the remote repository.

```bash
$ git push origin :feature/twitter-login    # deleting the 'feature/twitter-login' from remote
```


#### tips:

1. [git style guide][git-style-guide]
1. [git extra][git-extras]

    <iframe src="https://player.vimeo.com/video/45506445" width="500" height="313" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe> <p><a href="https://vimeo.com/45506445">Git Extras - Introduction</a> from <a href="https://vimeo.com/user8021748">tjholowaychuk</a> on <a href="https://vimeo.com">Vimeo</a>.</p></p>


### repository hosting:

We will be using [Github][github] for hosting our git repositories.


#### milestones:

Milestones are created for notable achievements/markers in the progress of
your project. For example, a new version deserves its own milestone,
appropriately named, which in this case would be `v1` (for version 1).

Use of milestones is helpful in grouping commits and issues. Also makes assessing
progress easier.


#### issues:

For each feature and bug, an issue should be created for it. Discussion around the
feature or bug will be done in the issue thread. Once a feature is completed, or
a bug is fixed, the corresponding issue should be closed.


#### issue referencing:

In **all** commits working towards a feature or bug fix, the relevant issue should be
referenced in the commit message.

```bash
Fix twitter login

Some description would go here......

issue: #11
```

Note that we have added `issue: #11` to mean that this commit is working towards
a feature/bug fix, in issue 11.

Learn more on [referencing issues on Github][github-writing].


### peer review:

To ensure high quality of code, peer review will be done every week. The assigned peer will, at the
end of the week i.e. before the start of the next sprint, should review your code. Should defects in
the code be noted, such as duplicated code, the peer should create an issue for each defect. Further
discussions will be done in the issue thread.


### references:

* [A successful branching model][nvie-model]
* [Git][git]
* [Github][github]
* [Git extras][git-extras]
* [Writing on Github][github-writing]


<!-- All external links come here, for easier updating and referencing multiple times -->
[git]:http://git-scm.com/ "Git"
[git-extras]:https://github.com/tj/git-extras "Git Extras"
[git-style-guide]:https://github.com/agis-/git-style-guide "Git Style Guide"
[github]:https://github.com "Github"
[github-writing]:https://help.github.com/articles/writing-on-github/ "Writing on Github"
[nvie-model]:http://nvie.com/posts/a-successful-git-branching-model/ "A successful git branching model"
[nvie-diagram]:res/git-model.png

