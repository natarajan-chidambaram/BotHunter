# BotHunter

### Description
BotHunter is a machine-learning based GitHub bot identification script that can be executed through command-line.

BotHunter accepts either a username to determine the type of contirbutor or the name of a repository (format: repo_owner/repo_name) to determine the type of contributors that are present in 'repository --> insights --> contributors'.

### Features
To determine the contirbutor type, bothunter depends on the following 19 features that are obtained through GitHub API:

  Profile information:
  1. Account login
  2. Account name
  3. Account bio
  4. Number of followings
  5. Number of followers
  6. Account tag

  Account activity:
  
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

  Text similarity:
  
  17. Issue/Pull request comments
  18. Preceding comments
  19. Commit messages

Data for computing the features in profile information is obtained through GitHub Users API, account activity is obtained by making a maximum of 3 queries to the GitHub Events API and text similarity is obtained through repository API.

## Installation
Given that BotHunter has many dependencies, and in order not to conflict with already installed packages, it is recommended to use a virtual environment before its installation. You can install and create a _Python virtual environment_ and then execute BotHunter in this environment. You can use any virtual environment of your choice. Below are the steps to install and create a virtual environment with **virtualenv**.

Use the following command to install the virtual environment:
```
pip install virtualenv
```
Create a virtual environment in the folder where you want to place your files:
```
virtualenv <name>
```
Start using the environment by:
```
source <name>/bin/activate
```
After running this command your command line prompt will change to `(<name>) ...`

Now you can fork the BotHunter repository from 'https://github.com/natarajan-chidambaram/BotHunter' and clone it to your local system.

Navigate to the location in which BotHunter is cloned using the terminal command
```
cd <BotHunter location>
```
and you can install BotHunter dependencies from the provided requirements.txt with the pip command
```
pip install -r requirements.txt
```
When you are finished running the script, you can quit the environment by:
```
deactivate
```

### Usage
To execute BotHunter, you need to provide a *GitHub personal access token* (API key). You can follow the instructions [here](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) to obtain such a token.

**Parameters List**:

`--key <APIKEY>` GitHub personal access token (key) required to extract data from the GitHub API

`--repo <REPO_OWNER/REPO_NAME>` Name of the GitHub repository to determine the type of all the contributors that are present in `https://github.com/repo_owner/repo_name/graphs/contributors'

> Example: $ python BotHunter.py --key token --repo repo_ownwer/repo_name

`--u <USERNAME>` The username for which the type needs to be determined
> Example: $ python BotHunter.py --key token --u username

**Note**: Only either of `--repo` or `--u` can be given as input along with the `--key`.

### Examples
```
$ python BotHunter.py --key token --u natarajan-chidambaram
natarajan-chidambaram: Human
```

```
$ python BotHunter.py --key token --u bors
bors: Bot
```

```
$ python BotHunter.py --key token --repo natarajan-chidambaram/BotHunter
natarajan-chidambaram: Human
```

### License

This project is distributed under parent repository's license - LGPL-2.1 license
