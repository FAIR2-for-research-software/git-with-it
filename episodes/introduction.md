---
title: "Introduction"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions

- Who else is doing this course?
- What can you expect from this course?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Find out something interesting about other participants.
- Understand the way in which you are expected to behave and interact with other participants.
- Have an overview of the content and material that will be covered.
- Pair up with another participant to collaborate with during this workshop.

::::::::::::::::::::::::::::::::::::::::::::::::

[Git][git] is, in 2025, the most widely used version control system by far. It was developed by Linus Torvalds to manage
[Linux kernel][linux] development and since then has exploded. Websites such as [GitHub][gh] and [GitLab][gl], both
types of Forge^[1], facilitate asynchronous collaboration on common code bases and underpin many, many software projects
from enterprise grade tools such as the aforementioned [Linux kernel][linuxGithub], the increasingly popular
[Rust][rustGitHub] through to niche products such as [Snapcast][snapcast] or Android apps for tracking your exercise
such as [OpenTracks][openTracks].

Git and Forges are wonderful tools for
collaboration. However, because of the complexities of version controlling software in distributed, collaborative
environments the tool itself, Git, has become quite complex. There are many different tasks that one may wish to
undertake and often several different ways of achieving these.

It's relatively easy to get the _basics_ of working with [Git][git] on your own or with small groups to work
collaboratively on code development. If you aren't already familiar with these basics then this course isn't for you
(yet!) and you would benefit from an introductory course such as [Git, GitHub through GitKraken : From Zero to
Hero!][zeroHero] or the [Software Carpentry : Version Control with Git][swCarpentryGit]. This course aims to show you
some of the more involved ways to use Git in a collaborative environment.

Most of the ways in which collaboration can be eased is through a better understanding of how Git works and by
maintaining clean and focused commits which make the task of reviewing work easier for those you are collaborating with.

## Code of Conduct

To make clear what is expected, everyone participating in The Carpentries activities is required to abide by our
[Code of Conduct][coc]. Any form of behaviour to exclude, intimidate, or cause discomfort is a violation of the Code of
Conduct. In order to foster a positive and professional learning environment we encourage you to:

- Use welcoming and inclusive language
- Be respectful of different viewpoints and experiences
- Gracefully accept constructive criticism
- Focus on what is best for the community
- Show courtesy and respect towards other community members

If you believe someone is violating the Code of Conduct, we ask that you report it to The Carpentries Code of Conduct
Committee by completing [this form](https://goo.gl/forms/KoUfO53Za3apOuOK2).

## Icebreaker

::: challenge

## Collaboration

Since this course is all about collaboration we would like you now to pair up with another participant in order to
undertake the exercises contained in this course. This could be the person sitting next to you if this is an in-person
course or if the course is online one of the instructors will pair you up at random.

Once paired up please add details to the [Collaborative Notepad][collab_notepad] along with your GitHub usernames.

::::::::::::::::::::::::::::::::::::: callout

The aim of pairing up is _not_ to divide the tasks between people. There are a few exceptions but for most tasks you
should work with your partner to solve each of the challenges, but with one person at the "driving seat" making the
changes to the code as required.

You should discuss what you think the solution should be as you work through the challenge.

This is a software development technique known as [Pair Programming][pairprogramming] and by discussing the solutions
you will hopefully come away with a better understanding of the material.

::::::::::::::::::::::::::::::::::::::::::::::::

## Getting to Know Each Other

In order to break the ice and find out something about the other participants on this course, please think about a
situation BVC (**B**efore **V**ersion **C**ontrol) where you might have had a problem that Version Control would have
prevented. This might be deleting files by mistake or making changes to code that broke your programme and not being
unable to undo them. Alternatively you could describe a mistake you've made AVC (**A**fter  **V**ersion **C**ontrol)
where you perhaps committed to the wrong branch or deleted something.

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::: solution

## In-Person

If the course is being run in person please describe the situation to the person or people sat next to you. Write your
answer in the collaborative pad under a heading with your name.

:::::::::::::::::::::::::::::::::

:::::::::::::::::::::::: solution

## Online

If you are participating online please write down your names of pairs and provide an answer in the collaborative notepad.

:::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

Before the start of the course you should setup a new [collaborative pad][collab_notepad] where participants can answer
questions and collaborate.

If running the course online you should have a list of participants and have paired them off at random.

When explaining the challenge remember to let participants know that they can use these pages to work through the steps,
this is particularly important for those who are not overly familiar with Python.

Once people have completed the task ask for volunteers to describe their experiences BVC.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

If anyone has multiple GitHub accounts it is possible that permission may be denied which force pushing if the wrong SSH
key is used. It is simple to work around this by adding the following to the `.git/config` of the user and ensuring it
points to the correct private SSH key that is associated with the account they wish to use.

``` bash
[core]
    ...
    sshCommand = ssh -i ~/.ssh/id_ed25519 -F /dev/null
```

The important part is that it points to the correct SSH key, in the above this is `~/.ssh/id_ed25519` which will
need modifying to reflect the users key for the account they wish to use.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

## Cloning Repositories

::::::::::::::::::::::::::::::::::::: challenge

## Choose Roles, Clone Repository and

In your pairs you now need to decide who is to take on each of the two roles. There isn't much between them in terms of
what you will be doing but one person needs to be the **repository owner** and one person needs to be a
**collaborator**.

Follow the instructions below under each section. If you have any questions please do not hesitate to ask.

:::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::: solution

## Clone the repository

Click on the _Code_ button at [Python Maths][pythonmaths] and then the _SSH_ tab. Copy the URL. If you want to clone the
work to `~/work/git/` then in a terminal run the following commands (be wary of copy and pasting them `<owners_id>`
needs replacing)

``` bash
cd ~/work/git
git clone git@github.com:<owners_id>/python-maths
cd python-maths
git fetch origin {divide,multiply,ns-rse/merge-conflict}
```

### Edit `.git/config`

Both users should now edit the `.git/config` file and modify line 7 where the `url` of the `origin` is defined and
replace `ns-rse` with the GitHub username of the person who will be the Repository Owner. For example if the repository
owner uses the `alice_and_bob` username on GitHub it should read.

``` bash
 [remote "origin"]
     url = git@github.com:alice_and_bob/python-maths.git
     fetch = +refs/heads/*:refs/remotes/origin/*
```

This edit changes the `origin` to be the empty repository you created under the _Repository Owner's_ account called
`python-maths` and pushes the cloned repository there.

### Force Push

**NB** This step is _just_ for the **Repository Owner**, the **Collaborator** should **not** perform this step.

The repository owner should now create an empty repository called `python-maths` using the [new repo][gh_newrepo], do
_not_ add a license or `.gitignore` to the repository, it should be **completely empty**.

The Repository Owner can push the cloned repository to their account with the following command, the `--force` is
optional and shouldn't be required unless you have inadvertently initialised the repository with additional files.

``` bash
git push --force
```

:::::::::::::::::::::::::::::::::

:::::::::::::::::::::::: solution

## Protect the Main Branch

**NB** This step is _just_ for the **Repository Owner**, the **Collaborator** should **not** perform this step.

On the `python-maths` repository you both now have access to, protect the `main` branch to require approvals.

1. _Settings > Branches > Add classic branch protection rule_
2. Enter `main` under _Branch name pattern_
3. Check the boxes _Require a pull request before merging_ and _Require approvals_
4. Prevent the repository owner from bypassing the rules by checking _Do not allow bypassing the above settings_.
5. Save the changes using the button at the bottom of the page.

:::::::::::::::::::::::::::::::::

:::::::::::::::::::::::: solution

## Invite your Collaborator

**NB** This step is _just_ for the **Repository Owner**, the **Collaborator** should **not** perform this step.

The Repository owner should now invite their collaborator to work on the repository.

1. Navigate to _Settings > Collaborators_
2. Click on _Add People_ and enter the GitHub username of your collaborator.

The **Collaborator** should receive an email invitation to collaborate and should accept it.

:::::::::::::::::::::::::::::::::

:::::::::::::::::::::::: solution

## Install the Package

**NB** Both the **Repository Owner**, the **Collaborator** should perform this step.

If you have not already done so activate the `git-collaboration` environment you created as described in the setup
instructions.

``` bash
conda activate git-collaboration
```

You can now install the package and its test dependencies in an editable format so that as you work on the package the
changes you make will instantly be available. Make sure you are in the `python-maths` directory (use `pwd` to show where
you are and `cd` to change directory).

``` bash
pwd
cd ~/work/git/python-maths
pip install -e .[tests,dev]
```

You can optionally check everything is installed and runs by running the tests via [pytest][pytest].

``` bash
pytest
========================================== test session starts ==========================================
platform linux -- Python 3.13.1, pytest-8.3.4, pluggy-1.5.0
Matplotlib: 3.10.0
Freetype: 2.6.1
rootdir: /home/neil/tmp/gitcollab-20250210/python-maths
configfile: pyproject.toml
testpaths: tests
plugins: cov-6.0.0, github-actions-annotate-failures-0.3.0, mpl-0.17.0
collected 25 items

tests/test_arithmetic.py .....................                                                                                                           [ 84%]
tests/test_trig.py ....                                                                                                                                  [100%]

---------- coverage: platform linux, python 3.13.1-final-0 -----------
Name                        Stmts   Miss  Cover
-----------------------------------------------
pythonmaths/arithmetic.py       8      0   100%
pythonmaths/trig.py             4      0   100%
-----------------------------------------------
TOTAL                          12      0   100%


========================================== 25 passed in 0.28s ===========================================
```

:::::::::::::::::::::::::::::::::

After completing these steps you should both have a copy of the `python-maths` repository on your local computer.

<!-- ::::::::::::::::::::::::::::::::::::: challenge -->

<!-- ## Working with your Collaborator -->

<!-- As a quick recap there are two issue templates `01 Zero Division` and `02 Square Root`. Assign one of -->
<!-- these issues each and work through the tasks to add the relevant functionality (instructions, commands -->
<!-- and codes to copy and paste are provided in each of the issues). Once you have committed the changes -->
<!-- push them to GitHub and make a Pull Request asking your collaborator to review your code (note the -->
<!-- instructions in the Square Root task). Review your collaborators code and approve the Pull Request. -->

<!-- ::::::::::::::::::::::::::::::::::::: -->

<!-- :::::::::::::::::::::::: solution -->

<!-- ## Zero Division -->

<!-- The instructions should have taken you through the various steps of adding an Exception to the divide -->
<!--  function which raises an error when the supplied value of `y` is zero. A test should have been added -->
<!-- which checked this is raised when zero is passed. -->

<!-- ``` python -->
<!-- def divide(x: int | float, y: int | float) -> float: -->
<!--     """ -->
<!--     Divide x by y. -->

<!--     Parameters -->
<!--     ---------- -->
<!--     x : int | float -->
<!--         Numerator for division. -->
<!--     y : int | float -->
<!--         Denominator for division. -->

<!--     Returns -->
<!--     ------- -->
<!--     float -->
<!--         The result of dividing `x` by `y`. -->

<!--     Examples -->
<!--     -------- -->
<!--     >>> from python_math import arithmetic -->
<!--     >>> arithmetic.divide(10, 2) -->
<!--         5.0 -->
<!--     >>> arithmetic.divide(5, 2) -->
<!--         2.5 -->
<!--     """ -->
<!--     try: -->
<!--         return x / y -->
<!--     except ZeroDivisionError as e: -->
<!--         raise ZeroDivisionError( -->
<!--             "You can not divide by 0, please choose another value for 'y'." -->
<!--         ) from e -->
<!-- ``` -->

<!-- ``` python -->
<!-- def test_divide_zero_division_exception() -> None: -->
<!--     """Test that a ZeroDivisionError is raised by the divide() function.""" -->
<!--     with pytest.raises(ZeroDivisionError): -->
<!--         arithmetic.divide(2, 0) -->
<!-- ``` -->

<!-- The test should have passed on the Continuous Integration of GitHub Actions. -->

<!-- ::::::::::::::::::::::::::::::::: -->

<!-- :::::::::::::::::::::::: solution -->

<!-- ## Square Root -->

<!-- The instructions should have taken you through the the various steps of adding a Square root function. -->
<!-- A test shold have been added which checks the square root of the numbers `4`, `9`, `25` and `2`. -->

<!-- ``` python -->
<!-- def square_root(x): -->
<!--     """Return the square root of a number. -->

<!--     Parameters -->
<!--     ========== -->
<!--     x : int | float -->
<!--         The number for which you wish to find the square root. -->

<!--     Returns -->
<!--     ======= -->
<!--     float -->
<!--         The square root of x. -->

<!--     Examples -->
<!--     ======== -->
<!--     >>> from python_math import arithmetic -->
<!--     >>> arithmetic.square_root(4) -->
<!--         2.0 -->
<!--     >>> arithmetic.square_root(169) -->
<!--         13.0 -->
<!--     """ -->
<!--     return x ** (1 / 2) -->
<!-- ``` -->

<!-- ``` python -->

<!-- @pytest.mark.parametrize( -->
<!--     ("x", "target"), -->
<!--     [ -->
<!--         pytest.param(4, 2, id="square root of 4"), -->
<!--         pytest.param(9, 3.0, id="square root of 9"), -->
<!--         pytest.param(25, 5.0, id="square root of 25"), -->
<!--         pytest.param(2, 1.4142135623730951, id="square root of 2"), -->
<!--     ], -->
<!-- ) -->
<!-- def test_square_root(x: int | float, target: int | float) -> None: -->
<!--     """Test the square_root() function.""" -->
<!--     pytest.approx(arithmetic.square_root(x), target) -->
<!-- ``` -->

<!-- ::::::::::::::::::::::::::::::::: -->

::::::::::::::::::::::::::::::::::::: callout

If desired you can between you update the Metadata in `pyproject.toml`. It is important to have accurate Metadata in this
file because if you ever publish your package to [Python Package Index (PyPI)][pypi] it will be used.

To update the metadata create a branch and update lines 12 and 13 with your names and email addresses. Push the changes,
create a pull request and merge the changes.

::::::::::::::::::::::::::::::::::::::::::::::::

^[1]: The term "forge" refers to a web-based collaborative software platform.  [GitHub][gh] and [GitLab][gl] are perhaps
the most well known but there are many others including [BitBucket][bitbucket],  [Codeberg][codeberg], and
[ForgeJo][forgejo] and [SourceHut][sourcehut].

[bitbucket]: https://bitbucket.org/
[coc]: https://docs.carpentries.org/policies/coc/
[codeberg]: https://codeberg.org/
[collab_notepad]: https://docs.google.com/document/d/1deRatN-J7RDLaEW2_rE1a01pH2INL2KermibFY9vqYk/edit?tab=t.0
[forgejo]: https://forgejo.org/
[git]: https://git-scm.com
[gh]: https://github.com
[gh_newrepo]: https://github.com/new
[gl]: https://gitlab.com
[linux]: https://www.kernel.org
[linuxGithub]: https://github.com/torvalds/linux
[openTracks]: https://github.com/OpenTracksApp/OpenTracks
[pairprogramming]: https://en.wikipedia.org/wiki/Pair_programming
[pypi]: https://pypi.org/
[pythonMaths]: https://github.com/ns-rse/python-maths
[pytest]: https://docs.pytest.org/
[rustGithub]: https://github.com/rust-lang/rust
[snapcast]: https://mjaggard.github.io/snapcast/
[sourcehut]: https://sourcehut.org/
[swCarpentryGit]: https://swcarpentry.github.io/git-novice/
[zeroHero]: https://srse-git-github-zero2hero.netlify.app
