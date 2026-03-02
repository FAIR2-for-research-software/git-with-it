---
title: Setup
---

## Git

There are many [Git][git] clients (porcelains) out there and many Integrated Development Environments (IDEs) support Git
actions and facilitate using the bewildering array of options, but this course teaches the Command Line Interface (CLI)
to Git as it means we have a consistent interface to teach the _principles_ that you can take away to your own choice of
Git client. Below there are instructions for installing Git on each of the three most common operating systems.

Please complete these setup tasks **before** attending the course. If you have any issues getting setup please either
contact an instructor in advance or arrive early and seek assistance from an instructor.

## Miniforge/Conda

We use the [Miniforge][miniforge]  virtual environment management system to install virtual
environments and Git as it provides a consistent experience across operating systems.

::::::::::::::::::::::::::::::::::::::: discussion

Follow the [install instructions][miniforge_install] for your operating system to install Miniforge.

:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: solution

### Windows

> Download and execute the Windows installer. Follow the prompts, taking note of the option to "Create start menu
> shortcuts". The most convenient and tested way to use the installed software (such as commands `conda` and `mamba`) is
> via the "Miniforge Prompt" installed to the start menu.

Once installed you should find the _Miniforge Prompt_ in your Start menu.

:::::::::::::::::::::::::

:::::::::::::::: solution

### Unix-like (Linux, MacOS, WSL)

``` bash
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
```

``` bash
wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
```

Then...

``` bash
bash Miniforge3-$(uname)-$(uname -m).sh
```

Answer the prompts for selecting an installation location. At the end of the installation you will see the following
output and question...

``` bash
installation finished.
Do you wish to update your shell profile to automatically initialize conda?
This will activate conda on startup and change the command prompt when activated.
If you'd prefer that conda's base environment not be activated on startup,
   run the following command when conda is activated:

conda config --set auto_activate_base false

Note: You can undo this later by running `conda init --reverse $SHELL`

Proceed with initialization? [yes|no]
[no] >>> yes
```

Answer `yes` as it ensures that the `conda` base environment is activated each time you create

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

### Unable to activate environment

If you are prompted to run `conda init` before `conda activate` and find this doesn't work then its possible a key step
was missed out, most likely answering `yes` to have your shell profile updated mentioned above. To rectify this the
following might help...

``` bash
source activate base
```

::::::::::::::::::::::::::::::::::::::::::::::::

## Create a Virtual Environment

We now need to create a virtual environment and install Python, Git and OpenSSH within it.

::::::::::::::::::::::::::::::::::::::: discussion

You should now create a virtual environment for the course and install Git and OpenSSH from the Conda-Forge channel.

:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: solution

``` bash
conda create --name git-with-it --channel conda-forge python git openssh
```

As the prompt suggests activate the environment...

``` bash
conda activate git-with-it
```

Check these are installed using the following commands

``` bash
which {git,ssh,ssh-keygen}
```

This will print out the path to each of the programmes `git`, `ssh` and `ssh-keygen`, the first part of the path will
depend on _your_ computer, but  the last part of the output of each should  `miniforge/bin/git`, `miniforge/bin/ssh` and
`miniforge/bin/ssh-keygen` respectively. An example is shown below.

``` bash
 which {git,python,ssh,ssh-keygen}
/home/neil/miniforge3/bin/git
/home/neil/miniforge3/bin/python
/home/neil/miniforge3/bin/ssh
/home/neil/miniforge3/bin/ssh-keygen
```

:::::::::::::::::::::::::

## GitHub

You will also need an account on [GitHub][gh]. If you do not already have one please
[register](https://github.com/signup), if you have an academic email address such as `@<institute>.ac.uk` or
`@<institute.edu>` then registering with this address will give you access to a few more features.

### SSH Keys

::::::::::::::::::::::::::::::::::::::: discussion

## ESSENTIAL

You **MUST** generate an SSH key _using a secure password_, then add the public component to your [GitHub
account][github_ssh].

:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: solution

### Generate SSH Keys

There is a detailed [article][ssh-keygen] on creating SSH keys under Linux and OSX that works with Git installed under
the Conda/Miniforge install you should have made following the above instructions.
It is recommended to use the newer [ed25519][ssh-ed25519] algorithm. In a terminal or Git Bash shell, you can do this
using the following commands. You will be prompted to enter your password twice, **make sure to enter a secure
(i.e. long) password, password-less keys are insecure!** and make sure you remember what the password is (**Hint** use a
password manager!).

```bash
ssh-keygen -a 100 -t ed25519
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/neil/.ssh/id_ed25519):
Enter passphrase for "id_ed25519" (empty for no passphrase):
Enter same passphrase again:
```

As shown above, you will need to confirm the location that the SSH keys will be saved to (hit enter to select the
default which will be `~/.ssh/id_ed25519`) and _then_ enter a secure passphrase (you will be asked to enter it twice to
confirm you know what it is, do not forget it!).

This creates two files in the `~/.ssh/` directory by default, the private key (`~/.ssh/id_ed25519'`) and the public key
(`~/.ssh/id_ed25519.pub`). These are text files and it is the contents of the later with the `.pub` extension that you
need to add to GitHub (see next solution). You can view the contents of the `~/.ssh/id_ed25519.pub` file that you need
to copy to your GitHub account with.

```bash
cat ~/.ssh/id_ed25519.pub
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIARcKip5cMGhQvOooF0sAFTvLAj8R7wz+7cPV9BndPtL neil@haldane
```

:::::::::::::::::::::::::

:::::::::::::::: solution

### Adding Keys to GitHub (All OSs)

Once you have created your SSH key you need to copy it to your account, got to _Settings > SSH and GPG Keys_ and click
on the _New SSH key_ button. Enter a name for your key, set the **Key type** to _Authenticaion Key_ and paste your
public key (the contents of the file ending in `.pub`) into the **Key** box then click the _Add SSH key_ button.

:::::::::::::::::::::::::

:::::::::::::::: solution

### Checking your key works

You can test if you have setup your SSH key by running the following command which should produce similar output.

```bash
ssh -T git@github.com
Hi ns-rse! You've successfully authenticated, but GitHub does not provide shell access.
```

If you do **not** see the above successful authentication message please get in touch **before** the course starts.
:::::::::::::::::::::::::

## Clone a repository

To undertake the work in this course you need to have a Git repository to work on. We will use the
[python-maths][python-maths] repository for this.

::::::::::::::::::::::::::::::::::::::: discussion

### Cloning `python-maths`

You should clone the [python-maths][python-maths] repository _before_ joining the first training session to the computer
you will be using to undertake the work. As you have now setup SSH keys under your GitHub account you can

- Navigate to [python-maths][python-maths] (use `Ctrl+click` to open in a new tab).
- Click on the green Code button.
- On the Local tab select SSH
- Use the Copy button to the right of `git@github.com:FAIR2-for-research-software/python-maths.git` to copy  the SSH
  URL.

:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: solution

You can clone the repository with the following...

``` bash
git clone git@github.com:FAIR2-for-research-software/python-maths
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

Prior to attending the course you should have...

- Installed Miniforge on your computer.
- Created a virtual environment called `git-with-it` and included both `git` and `openssh` in this environment.
- Created an SSH key and uploaded the public component to your GitHub Account (_Settings > SSH and GPG
  Keys_).
- Cloned the [python-maths][python-maths] repository.

::::::::::::::::::::::::::::::::::::::::::::::::

[gh]: https://github.com
[git]: https://git-scm.com/
[github_ssh]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account
[miniforge]: https://github.com/conda-forge/miniforge
[miniforge_install]: https://github.com/conda-forge/miniforge?tab=readme-ov-file#install
[python-maths]: https://github.com/FAIR2-for-research-software/python-maths
[ssh-ed25519]: https://blog.g3rt.nl/upgrade-your-ssh-keys.html
[ssh-keygen]: https://www.digitalocean.com/community/tutorials/how-to-create-ssh-keys-with-openssh-on-macos-or-linux
