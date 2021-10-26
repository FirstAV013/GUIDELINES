# Working with GitHub
The guidelines below describe how we work with GitHub

## Table of content
- [Naming repositories](#naming-repositories)
- [Branching strategy](#branching-strategy)
- [Committing & pushing](#committing--pushing)
- [Pull requests](#pull-requests)

## Naming repositories (1)
Please follow the naming convention below when creating a repository:
1. Repository names are written in English
2. Repository names consist of three parts:
   1. Location
   2. Solution
   3. Name

3. Every part is seperated by an underscore (`_`)
4. Every part is train cased (`TRAIN-CASE`)

Examples:
> BASIC-FIT_SCALA-TOETERS-EN-BELLEN  
> RITUALS_CONTENT-PREVIEW-TOOL  
> BRIGHTSIGN_NOC-POST-SCRIPT

___

## Naming repositories (2)
Please follow the naming convention below when creating a repository:
1. Repository names are written in English
2. Repository names are kebab cased (`kebab-case`)
3. Repository names start with client name or `fi` for internal repositories
4. Repository names end with a short description (max. 3 words)

Examples:
> fi-brightsign-web  
> fi-scala-api-nu-nl  
> fi-scala-api-wheather  
> rituals-player-app  
> rituals-brightsign-collection  
> basicfit-lambda-functions  

___

## Branching strategy
We use Gitflow as a branching strategy, the tutorial below describes this workflow:  
https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow

___

## Committing & pushing
Please follow the guidelines below when committing code to a repository:
1. All code should be part of a repository
2. Code is commited and pushed at the of the day
3. Keep commits as small as possible
4. Write short descriptive commit messages (max. 50 characters)

___

## Pull requests
Please follow the guidelines below when working with pull requests:
1. All code should be reviewed and approved by another developer before merging to `main` branch
2. Write a short description explaining what code has changed and what the reviewer should pay extra attention to
3. Be gentle when reviewing code, developers are sensitive