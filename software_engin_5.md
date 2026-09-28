User Manual Procedure: Setting Up a GitHub Repository and Making a First Commit
Prerequisites

Before starting, I need:

A computer with an internet connection.
A GitHub account.
Git installed on the computer.
A code editor such as Visual Studio Code.
Basic knowledge of using a computer and opening a terminal.
Procedure
Step 1: Open GitHub

Open GitHub in a web browser and sign in to my account.

Expected result: My GitHub account homepage appears.

Step 2: Create a new repository

Select New repository from the GitHub interface.

Expected result: The page for creating a new repository appears.

Step 3: Enter the repository name

Enter my-first-project as the repository name.

Expected result: The repository name appears in the repository name field.

Step 4: Set the repository visibility

Select Public as the repository visibility.

Expected result: The repository is set to public.

Step 5: Create the repository

Select Create repository.

Expected result: GitHub creates the new my-first-project repository.

Step 6: Open the terminal

Open Git Bash or another terminal on the computer.

Expected result: A terminal window opens and displays a command prompt.

Step 7: Create a project folder

Create a folder named my-first-project on the computer.

Expected result: The my-first-project folder appears on the computer.

Step 8: Move into the project folder

Navigate to the my-first-project folder in the terminal.

Expected result: The terminal is now working inside the project folder.

Step 9: Initialize Git

Run the following command:

git init

Expected result: Git creates a local repository in the project folder.

Step 10: Create a project file

Create a file named README.md inside the project folder.

Expected result: The README.md file appears in the project folder.

Step 11: Add the file to Git

Run:

git add README.md

Expected result: Git stages the README.md file for the next commit.

Step 12: Create the first commit

Run:

git commit -m "Initial commit"

Expected result: Git creates the first commit and displays a message confirming the commit.

Screenshot Description

I would include a screenshot of the terminal after running git commit -m "Initial commit". The screenshot should show the successful commit message and confirm that the README.md file was committed.

Troubleshooting

Common error: git is not recognized

This error usually means Git is not installed or the terminal cannot find Git. I would first check whether Git is installed by running:

git --version

If the command does not work, I would install Git and reopen the terminal before trying the command again.
