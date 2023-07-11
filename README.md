This repository contains specifications, solutions, and test drivers for the [Foundations of Applied Mathematics labs](https://foundations-of-applied-mathematics.github.io), as well as tools for automating the grading process.
Skip down to [Setup](#setup) for setup instructions.

The labs in this curriculum aim to introduce computational and mathematical concepts, walk through implementations of those concepts in Python, and use industrial-grade code to solve interesting, relevant problems.
Lab assignments are usually about 5-10 pages long (occasionally longer) and include code examples (yellow boxes), important notes (green boxes), warnings about common errors (red boxes), and about 3-7 exercises (blue boxes).
The lab manuals can be downloaded from [foundations-of-applied-mathematics.github.io](http://foundations-of-applied-mathematics.github.io/).

As the instructor, you have access to specifications, solutions, and test drivers, as well as some tools for automating the grading process.
If you have not received these materials, contact us at [acme@mathematics.byu.edu](mailto:acme@mathematics.byu.edu).
To teach this class successfully, you should be very familiar with [Python](https://www.python.org/about/gettingstarted/) and have at least some introductory experience with [Jupyter Notebook](http://jupyter.org/).

**Contents**

- [Repository Organization](#repository-organization)
    - [Labs](#labs)
    - [Homework](#homework)
    - [Records](#records)
    - [Student Folders](#student-folders)
    - [Other Files](#other-files)
- [Setup](#setup) (with Git)
- [Grading](#grading)
    - [Custom Test Drivers](#custom-test-drivers)
    - [Correcting Grading Mistakes](#correcting-grading-mistakes)
- [Using Git](#using-git)
    - [Common Git Commands](#common-git-commands)
    - [Submodules](#submodules)
    - [Example Work Session](#example-work-session)
- [Contributing](#contributing)

# Repository Organization

To get started, unzip the `.zip` file for your course and move it somewhere where it won't get lost.
Before detailing the setup procedure, we describe the contents of the resulting folder.

### Labs

The `_Labs/` directory contains one folder for each lab, such as `PythonIntro/`.
Each subfolder contains the following files.

- _Specifications_: What the students are given to start with, such as `python_intro.py`. These are included here just for your reference.
- _Solutions_: Usually `solutions.py` or `solutions.ipynb`. **These files should be kept private**, but they are an important reference for the instructor.
- _Test driver_: `test_driver.py`. These files help automate the grading process. Not every lab has a test driver, but the grading script still automates the grading process somewhat regardless (see [Grading](#grading)). Note that some test drivers depend on the solutions file, so if there is a test driver, do **not** move, rename, or drastically edit the solutions. **Please keep these files private!**
- _Data files_: After running `download_data.sh`, data files for each lab are also placed in the lab folders. Not every lab has accompanying data files.

See [Student-Materials/wiki/Lab-Index](https://github.com/Foundations-of-Applied-Mathematics/Student-Materials/wiki/Lab-Index) for the complete list of labs, their specifications and data files, and the manual that each lab belongs to.

**_WARNING:_** Do **not** move or rename the individual lab folders (otherwise the grader will not be able to find the test drivers).
Your folder and file names must match [Student-Materials/wiki/Lab-Index](https://github.com/Foundations-of-Applied-Mathematics/Student-Materials/wiki/Lab-Index).
Students should also be aware that they should not change folder or file names, or the grader will not find their files.

**_WARNING:_** If you decide to change the name of the `_Labs/` folder, you must also change the `LAB_DIR` variable in `class_info.py` to match the new name (otherwise the automated grader will fail).

### Homework

The `_Homework/` directory is an optional way to collect non-lab coding assignments.
The grader can quickly distribute feedback for these assignments, but it does no automated testing.
See [Custom Test Drivers](#custom-test-drivers).

**_WARNING:_** If you decide to change the name of the `_Homework/` folder, you must also change the `HW_DIR` variable in `class_info.py` **and** instruct each of your students to change the names of their `_Homework/` folders to match the new name.

### Records

The `_Records/` directory, which is automatically created during the first grading session, contains the scores file (`scores.csv`) and custom test driver configuration files (`DataVisualization.p`, etc.).
The grader automatically updates `scores.csv` during each grading session, but you can also edit `scores.csv` directly in a text editor or with a spreadsheet program like Microsoft Excel.
**We strongly recommend making copies of `scores.csv` often since there is no automatic safeguard to keep `scores.csv` from being deleted**.

**_WARNING:_** If you decide to change the name of the `_Records/` folder, you must also change the `RECORDS_DIR` variable in `class_info.py` to match the new name (otherwise the grader will just create a new `_Records/` folder and scores file).

It should be abundantly clear by now that changing folder and file names is not a good idea if you want to use the automated test drivers.

### Student Folders

After the initial [setup process](#setup), the main directory should contain one folder for each student.
Students should have access to their individual folders, but not to your main directory or any other student folders.
For example, if Jane Doe and John Smith are in your class and your curriculum includes Introduction to Python and Data Visualization, your file structure should look something like this.

```bash
JaneDoe/                      # Only you and Jane Doe can access this folder.
    DataVisualization/
        data_visualization.ipynb  # Jupyter Notebook specifications file.
    PythonIntro/
        python_intro.py           # Python specifications file.
        PythonIntro_feedback.txt  # Feedback file for this lab.
    _Homework/
        hw1.ipynb                 # Non-lab homework assignment.
JohnSmith/                    # Only you and John Smith can access this folder.
    DataVisualization/
        data_visualization.ipynb
    PythonIntro/
        python_intro.py
        PythonIntro_feedback.txt  # Feedback file for this lab.
    _Homework/
        hw1.ipynb
_Homework/                    # Only you can access the rest of these folders.
    hw1.ipynb
_Labs/
    DataVisualization/
        MLB.npy                   # Data file for this lab.
        anscombe.npy
        countries.npy
        data_visualization.ipynb  # Jupyter Notebook specifications file.
        earthquakes.npy
        solutions.ipynb           # Solutions file.
    PythonIntro/
        python_intro.py           # Python specifications file.
        solutions.py              # Solutions file.
        test_driver.py            # Test driver.
_Records/
    scores.csv                    # Scores file.
    DataVisualization.p           # Custom test driver configuration file.
base_test_driver.py           # Other files for setup and grading.
class_info.py
# ...
```

### Other Files

The rest of the files in the main directory are for setup, automated grading, and record keeping.

- `class_info.py`: Contains information about the students and the labs. The other Python files in the main directory depend on this file, and it must be filled out by the instructor at the beginning of the semester.
- `grader.py`: The main script for grading student submissions, recording results, and submitting feedback.
- `display.py`: Convenience script for viewing the scores file.
- `download_data.sh`: Downloads data files and places them in the appropriate lab folders. You should only have to run this once as part of the setup.
- `install_dependencies.sh`: Installs the third-party Python packages used by the labs. You should only have to run this once as part of the setup.
- `base_test_driver.py`, `custom_test_driver.py`: auxiliary files for the automated test drivers. You don't need to do anything with these, but be careful not to delete or modify them.

These files are also helpful for file and feedback management.

- `git_setup.py`: Installs or removes student repositories as git submodules.
- `distribute_hw.sh`: Copies a file from your `_Homework/` folder to each student's `_Homework/` folder and pushes them via git.
- `submit_feedback.sh`: Submits existing feedback files to students via git.
- `update_repositories.sh`: Updates all student repositories via git.
- `prepare_notebooks.py`: Compiles students' Jupyter notebook files into HTML to allow the test driver to automatically display them in your browser.

Most of these files have a `--help` option to show more detailed instructions on their usage.
For example, run `python grader.py --help` or `bash distribute_hw.sh --help` for more information on these files.

# Setup

**_DISCLAIMER_**: We strongly recommend using a Unix-based operating system (Mac or Linux) for the labs and for grading.
Unix has a true bash terminal, works well with git and python, and is the preferred platform for computational and data scientists.
It is possible to do this curriculum with Windows, but expect some road bumps along the way.

This website is a _git repository_, an online storage place for code and other small files.
[_Git_](http://git-scm.com/) is the underlying software that manages updates between this online repository and the copies of the repository, called _clones_, stored locally on computers.
If git is not already installed on your computer, download it at [http://git-scm.com/downloads](http://git-scm.com/downloads).
If you have never used git, you might want to read a few of the following resources.

- [Official git tutorial](https://git-scm.com/docs/gittutorial)
- [Bitbucket git tutorials](https://www.atlassian.com/git/tutorials)
- [GitHub git cheat sheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)
- [GitLab git tutorial](https://docs.gitlab.com/ce/gitlab-basics/start-using-git.html)
- [Codecademy git lesson](https://www.codecademy.com/learn/learn-git)
- [Git training video series by GitHub](https://www.youtube.com/playlist?list=PLg7s6cbtAD15G8lNyoaYDuKZSKyJrgwB-)

As the instructor, **it is very important for you to be comfortable with git** because students will have many git-related questions in the beginning.

There are many websites for hosting online git repositories.
We recommend using [Bitbucket](https://bitbucket.org/) because new users are immediately allowed a few private repositories, and it is easy to upgrade to unlimited private repositories with an academic email address.
You could use a service other than Bitbucket, such as [GitHub](https://github.com/) or [GitLab](https://about.gitlab.com/), but we only include instructions here for setup with Bitbucket.
The setup process for this instructor repository is similar to the setup process for the student repositories.

1. _Sign up_. Create a Bitbucket account at [https://bitbucket.org](https://bitbucket.org).
If you use an academic email address (ending in `.edu`, etc.), you will get free unlimited public and private repositories.

2. _Make a new repository_.
On the Bitbucket page, click the **+** button from the menu on the left and, under **CREATE**, select **Repository**.
Provide a name for the repository, mark the repository as **private** (**this is very important!**), and make sure the repository type is **Git**.
For **Include a README?**, select **No** (if you accidentally include a README, delete the repository and start over).
For **Include a .gitignore?**, select **No** (if you accidentally include a .gitignore, delete the repository and start over).
Under **Advanced settings**, enter a short description for your repository, select **No forks** under forking, and select **Python** as the language.
Finally, click the blue **Create repository** button.
Take note of the URL of the webpage that is created; it should be something like `https://bitbucket.org/<name>/<repo>`.

3. _Connect your folder to the new repository_.
In a shell application (Terminal on Linux or Mac, or [Git Bash](https://gitforwindows.org/) on Windows), enter the following commands.
```bash
# Navigate to your folder.
$ cd /path/to/folder  # cd means 'change directory'.

# Make sure you are in the right place.
$ pwd                 # pwd means 'print working directory'.
/path/to/folder
$ ls *.md             # ls means 'list files'.
README.md             # This means README.md is in the working directory.

# Connect this folder to the online repository.
$ git init
$ git remote add origin https://<name>@bitbucket.org/<name>/<repo>.git

# Record your credentials.
$ git config --local user.name "your name"
$ git config --local user.email "your email"

# (Optional) Instruct git to cache your password for 1 hour at a time.
$ git config --local credential.helper "cache --timeout 3600"

# Add the contents of this folder to git and update the repository.
$ git add --all
$ git commit -m "initial commit"
$ git push origin master
```
For example, if your Bitbucket username is `greek314`, the repository is called `acmev1`, and the folder is called `Instructor-Materials/` and is on the desktop, enter the following commands.
```bash
# Navigate to the folder.
$ cd ~/Desktop/Instructor-Materials

# Make sure this is the right place.
$ pwd
/Users/Archimedes/Desktop/Instructor-Materials
$ ls *.md
README.md

# Connect this folder to the online repository.
$ git init
$ git remote add origin https://greek314@bitbucket.org/greek314/acmev1.git

# Record credentials.
$ git config --local user.name "archimedes"
$ git config --local user.email "greek314@example.com"
$ git config --local credential.helper "cache --timeout 3600"

# Add the contents of this folder to git and update the repository.
$ git add --all
$ git commit -m "initial commit"
$ git push origin master
```
If you enter the repository URL incorrectly in the git remote add origin step, you can reset it with the following line.
```bash
$ git remote set-url origin https://<name>@bitbucket.org/<name>/<repo>.git
```

4. _Get **write** access to student repositories_.
Each student needs to give you **write** access to their repository so that you can grade their files and provide feedback.
Gather the URLs of the student repositories (of the form `https://bitbucket.org/<name>/<repo>`), perhaps through a quiz on the first day of class.
You should be able to go directly to each repository in a web browser without a **404** or **Access denied** message.
For example, if Jane Doe has `jdoe47` as her Bitbucket username and her repository is called `herrepo`, you should be able to view the repository at `https://bitbucket.org/jdoe47/herrepo`.

5. _Add student submodules to your repository_.
Fill in the `STUDENTS` dictionary in `class_info.py` with each student's name mapping to the URL of their repository.
For instance, add the line `"JaneDoe": "https://bitbucket.org/jdoe47/herrepo",` to `STUDENTS`.
The name that you use as the key (`"JaneDoe"`) will become the name of the folder where that student's materials reside.
We recommend using camel case **without spaces** (`"JaneDoe"`, `"JohnSmith"`, etc.).
After filling in `class_info.STUDENTS`, run `python git_setup.py` to install the students' repositories as submodules.
More details on what this file does are given [below](#using-git).

6. _Download data files_.
Many labs have accompanying data files.
To download these files, navigate to your clone and run the `download_data.sh` bash script, which downloads the files and places them in the correct lab folder for you.
You can also find individual data files through [Student-Materials/wiki/Lab-Index](https://github.com/Foundations-of-Applied-Mathematics/Student-Materials/wiki/Lab-Index).
```bash
# Navigate to your folder and run the script.
$ cd /path/to/folder
$ bash download_data.sh
```

7. _Install Python package dependencies_.
The labs require several third-party Python packages that don't come bundled with Anaconda.
Run the following command to install the necessary packages.
```bash
# Navigate to your folder and run the script.
$ cd /path/to/folder
$ bash install_dependencies.sh
```

8. (Optional) _Clone your repository_.
If you want your repository on a different computer, clone your repository with the following commands.
```bash
# Navigate to where you want to put the folder.
$ cd ~/Desktop/or/something/

# Clone the folder from the online repository.
$ git clone https://<name>@bitbucket.org/<name>/<repo>.git <foldername>

# Add your credentials to the new folder.
$ cd <foldername>
$ git config --local user.name "your name"
$ git config --local user.email "your email"
$ git confit --local credential.helper "cache --timeout 3600"

# Fill in the student modules and get data files.
$ python git_setup.py
$ bash download_data.sh
```

# Grading

The file `grader.py` applies the test drivers to student submissions and drops feedback files in the students' folders.
Start the grader by specifying the lab or homework assignment to grade.
For example, to grade Introduction to Python, since the corresponding folder is called `PythonIntro/`, run `python grader.py PythonIntro`.
To grade a homework assignment called `_Homework/hw1.ipynb`, run `python grader.py hw1.ipynb`.
The grader will prompt you for confirmation on the assignment and students to grade, then test each student's code.
Run `python grader.py --help` to see more options for using the grader.

The grader generates feedback files, such as `JaneDoe/PythonIntro/PythonIntro_feedback.txt`, for each student.
If the file already exists, the feedback from the current grading session is appended to the old file, so no previous feedback is ever lost.
These feedback files can be sent to the students with `bash submit_feedback.sh`.

Lab and homework scores are recorded in `_Records/scores.csv`.
Only the highest score is recorded: if Jane Doe scores 42 points on an assignment and later (for whatever reason) only scores 40 points, `scores.csv` will record 42 instead of 40.
Use `display.py` to quickly display parts of the scores file; run `python display.py --help` for options.

### Custom Test Drivers

Assignments are usually submitted as Python files (`.py`) or Jupyter Notebooks (`.ipynb`).
Individual `test_driver.py` files load and directly test code from `.py` files, but Jupyter Notebooks must be inspected and graded manually.
However, using `grader.py` for a lab with a Jupyter Notebook specifications file, or for a homework assignment in the `_Homework/` folder, activates a "custom test driver" that records scores and distributes feedback files like usual.
Custom driver configurations are stored as pickle files (`.p`) in the `_Records/` directory.
If there is no existing configuration for a lab or assignment, the grader will ask you to configure a custom driver by entering a number of problems, then labels and point values for each problem.
Use the `prepare_notebooks.py` script before starting the grader to allow the grader to display Jupyter Notebook files automatically.

### Continuing Grading When Interrupted

When grading, it is likely that you will end up in a situation where you need to stop grading and resume later.
For example, suppose that you had to leave and do something else before finishing, or that your computer crashed or lost power.
The grader updates the `scores.csv` file and all feedback files immediately after each student has finished being graded, so you do not ever need to worry about already-entered scores being lost.
The first time you are grading a lab, the `--less` argument of `grader.py` is extremely helpful for continuing where you left off.
This argument lets you specify a number; the grader will then grade every student with a score less than that number.
By using `--less 1`, you will grade all students who have not yet been graded.
For example, to do this with the `PythonIntro` lab:

`python grader.py PythonIntro --less 1`.

### Correcting Grading Mistakes

It's easy to make a mistake when grading the labs.
Depending on the type of error that occurs, there are several options.
Suppose, for example, that a test driver prompts you to grade a problem out of 5 points, and you enter 3 on accident even though the student deserved full credit.
In this case, on the prompt for comments, enter a keyboard interrupt (`ctrl+C` or `cmd+C`); the grader will then prompt asking if you want to regrade the question.

On the other hand, if you accidentally enter full points even if the student should not have received full credit, you can also input a keyboard interrupt.
It will in this case ask if you wish to abort grading.
Enter `y` once for it to stop grading the student, and `n` on the second question to continue grading the other students.
Then, once grading is finished, the grader will display for which students you aborted grading, making it easy to see which ones need regraded.

As a final (albeit more complicated) option, when the test driver asks you for comments, make the comment `"REGRADE"` (or some other distinctive word or phrase).
Then, after grading everyone, do a `grep` for feedback files with `"REGRADE"` in them:

`grep -l "REGRADE" */*/*_feedback.txt`.

Then delete those files, noting which students to run the test driver on again:

`grep -l "REGRADE" */*/*_feedback.txt | xargs rm -v`.

Alternatively, revert those feedback files to their previous state:

`git submodule foreach "grep -l 'REGRADE' */*_feedback.txt | xargs git checkout --"`

See [Submodules](#submodules) for more on the `git submodule` command.

# Using Git

Git manages the history of a file system through _commits_, or checkpoints.
Use `git status` to see the files that have been changed since the last commit.
These changes are then moved to the _staging area_, a list of files to save during the next commit, with `git add <filename(s)>`.
Save the changes in the staging area with `git commit -m "<A brief message describing the changes>"`.

All of these commands are done within a clone of the repository, stored somewhere on a computer.
This repository must be manually synchronized with the online repository via two other git commands: `git pull origin master`, to pull updates from the web to the computer; and `git push origin master`, to push updates from the computer to the web.

### Common Git Commands

| Command | Explanation |
|:--------|:------------|
| `git status` | Display the staging area and untracked changes. |
| `git pull origin master` | Pull changes from the online repository. |
| `git push origin master` | Push changes to the online repository. |
| `git add <filename(s)>` | Add a file or files to the staging area. |
| `git add -u` | Add all modified, tracked files to the staging area. |
| `git commit -m "<message>"` | Save the changes in the staging area with a given message. |
| `git checkout -- <filename>` | Revert changes to an unstaged file since the last commit. |
| `git reset HEAD -- <filename>` | Remove a file from the staging area. |
| `git diff <filename>` | See the changes to an unstaged file since the last commit. |
| `git diff --cached <filename>` | See the changes to a staged file since the last commit. |
| `git config --local <option>` | Record your credentials (`user.name`, `user.email`, etc.). |

**_NOTE_**: When pulling updates with `git pull origin master`, your terminal may sometimes display the following message.
```bash
Merge branch 'master' of https://bitbucket.org/<name>/<repo> into master

# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.
~
~
```
This means that someone else (a student) has pushed a commit that you do not yet have, while you have also made one or more commits locally that they do not have.
This screen, displayed in [_vim_](https://en.wikipedia.org/wiki/Vim_(text_editor)), is asking you to enter a message (or use the default message) to create a _merge commit_ that will reconcile both changes.
To close this screen and create the merge commit, type `:wq` and press `enter`.

### Submodules

A git repository can be placed within another git repository as a _submodule_, meaning the inner repository acts independent of the outer repository.
The command `git submodule` manages communications between the outer and inner repositories.
After filling in `class_info.STUDENTS`, run `python git_setup.py` to install the students' repositories as submodules to this repository.
If it doesn't work for every student the first time (for instance, if a student did not give you access to his or her repository), run `python git_setup.py` again to make another attempt.

Interacting with these submodules, especially if there many of them, can be messy.
If you `cd` into a submodule, it is treated exactly like its own git repository.
If you stay one level above the submodules (in the main directory for this repository), however, you can instruct git to execute the same command in every installed submodule with

`git submodule foreach "<command> ||:"` (**memorize this!**).

The `||:` (with vertical OR/pipe characters, not the number 1 or the letter l) ensures that if the command fails for one of the submodules, it continues on with the other submodules.
The following are examples of what you might want to do with `git submodule foreach`.

| Command                                         | Explanation               |
|:------------------------------------------------|:--------------------------|
| `git submodule foreach "git status"` | Get info about each repository's state. |
| `git submodule foreach "git pull origin master"` | Update every student repository. |
| `git submodule foreach "git add -u"` | Add every already-tracked file to the staging area. |
| `git submodule foreach "git add */*feedback.txt"` | Add all feedback files to the staging area. |
| `git submodule foreach "git commit -m '<message>'"` | Commit changes in each repository with a message. |
| `git submodule foreach "git push origin master"` | Push changes to their corresponding online repository. |

To avoid problems, include `||:` with the inner command (for example, `git submodule foreach "git pull origin master ||:"`).
If you make a mistake with a student's files, you can always go back in the git history.
To discard changes and revert to the last commit in each repository (**USE WITH CAUTION**), run `git submodule foreach "git reset --hard HEAD"`.

If you ever have a permissions problem with git submodules, try this solution (this requires that you know your `root` password).

- In the directory where there is a problem, run `ls -al` from the command line. This will print, among other things, the owner and group names for the file. You should notice most files are set to your username and group, but the problem files may have a different username.
- In the main directory of the repository, run `sudo chown -R <username>:<groupname>`, replacing `<username>` and `<groupname>` with your user and group names. This changes the owner of all files in the folder and its subfolders (recursively) back to you.

### Example Work Session

```bash
# Update student repositories.
$ bash update_repositories.sh

# ...

# Grade Jane Doe and John Smith on Introduction to Python.
$ python grader.py PythonIntro JaneDoe JohnSmith
The following students will be graded:
    JaneDoe
    JohnSmith
on PythonIntro/python_intro.py
Proceed? (yes/[no]): yes                          # Confirm grading session.
# ...                                             # Grade each student.
Results:                                          # Report grading results.
    JaneDoe                  35
    JohnSmith                 0

# Check that the feedback files exist.
$ ls */PythonIntro/*feedback.txt
JaneDoe/PythonIntro/PythonIntro_feedback.txt
JohnSmith/PythonIntro/PythonIntro_feedback.txt

# Submit feedback to the students.
$ ./submit_feedback.sh python_intro
```

# Contributing

To report bugs in the provided materials, typos or inaccuracies in the labs, or any other problems, [submit an issue on Github](https://github.com/Foundations-of-Applied-Mathematics/Labs/issues/new).
Please contact us at [acme@mathematics.byu.edu](mailto:acme@mathematics.byu.edu) if you have specific questions or feedback.
