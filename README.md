# BotHunter

### Description

**BotHunter** is a machine-learning based GitHub bot identification tool written as a _Python_ script.
The tool accepts either a GitHub user account name to determine its contribution type (Human or Bot),
or the name of a repository (format: repo_owner/repo_name) to determine the contribution type of all contributors that are listed under 'insights --> contributors' in the corresponding GitHub repositoriy.
(Note that this list is often incomplete, there may be many other repository contributors that are not explicitly listed there.)

### Features

To determine the contirbution type of a GitHub account, **BotHunter** depends on the following 19 features that can be obtained through the GitHub API:

  Profile information: (obtained per accounrt through the GitHub Users API)
   1. Account login (username)
   2. Account name
   3. Account bio
   4. Number of followings
   5. Number of followers
   6. Account tag

  Account activity: (obtained per account using a maximum of 3 queries to the GitHub Events API)
  
   7. Total number of repository activities
   8. Total number of issue activities
   9. Total number of pull request activities
  10. Total number of commit activities
  11. Unique repository activities
  12. Unique issue activities
  13. Unique pull request activities
  14. Unique commit activities
  15. Median activity per day
  16. Median response time

  Text similarity: (obtained through the GitHub repository API)
  
  17. Issue/Pull request comments
  18. Preceding comments
  19. Commit messages


## Installation

Given that **BotHunter** has many dependencies, and in order not to conflict with already installed packages, it is recommended to use a virtual environment before its installation.
You can install and create a _Python virtual environment_ and then execute BotHunter in this environment.
You can use any virtual environment of your choice.
Below are the steps to install and create a virtual environment with **virtualenv**.

 - Ensure that you have the **pip** package manager for _Python_ installed on your machine.

 - Use the following command to install the virtual environment:
```
pip install virtualenv
```

 - Create a virtual environment in the folder where you want to place your files:
```
virtualenv <name>
```

 - Start using the virtual environment:
```
source <name>/bin/activate
```

 - After running this command your command line prompt will change to `(<name>) ...`

 - Create a fork from the current BotHunter GitHub repository and clone this fork to your local filesystem.

 - Navigate to the location in which BotHunter is cloned using the terminal command
```
cd <BotHunter location>
```

 - Install BotHunter dependencies from the provided requirements.txt with the pip command
```
pip install -r requirements.txt
```

- When you are finished running the script, quit the virtual environment:
```
deactivate
```

### Usage

To execute **BotHunter**, you need to provide a *GitHub personal access token* (API key).
Follow the instructions [here](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) to obtain such a token.

**Parameters List**:

 - `--key <APIKEY>` GitHub personal access token (key) required to extract data from the GitHub API

 - `--repo <REPO_OWNER/REPO_NAME>` Name of the GitHub repository to determine the type of all the contributors that are present in `https://github.com/repo_owner/repo_name/graphs/contributors'. Example:
   ```
   $ python BotHunter.py --key <YOURTOKEN> --repo <REPO_OWNER/REPO_NAME>
   ```

 - `--u <USERNAME>` The username for which the type needs to be determined. Example:
   ```
   $ python BotHunter.py --key <YOURTOKEN> --u <SOMEUSERNAME>
   ```

**Note**: Only either of `--repo` or `--u` can be given as input along with the `--key`.

### Examples
```
$ python BotHunter.py --key <YOURTOKEN> --u natarajan-chidambaram
natarajan-chidambaram: Human
```

```
$ python BotHunter.py --key <YOURTOKEN> --u bors
bors: Bot
```

```
$ python BotHunter.py --key <YOURTOKEN> --repo natarajan-chidambaram/BotHunter
natarajan-chidambaram: Human
```

### License

This project is distributed under parent repository's license - LGPL-2.1 license
