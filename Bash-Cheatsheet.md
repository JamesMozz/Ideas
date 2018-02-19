### Setting up the Environment (One Time Setup)

- `developer@github`: fork repo: git://github/team-org/repoX -> git://github/developer/repoX
- `developer@workstation`: git clone git@github:developer/repoX.git
- `developer@workstation`: git remote add upstream git@github:team-org/repoX.git

### Synchronize Fork with Upstream

- `developer@workstation/master`: git pull upstream master
- `developer@workstation/master`: git push origin master

### Working on User Story/Defect

- `developer@workstation/master`: git checkout -b us-1234-branch
- `developer@workstation/us-1234-branch`: hack, hack, hack, build, test
- `developer@workstation/us-1234-branch`: git add ...
- `developer@workstation/us-1234-branch`: git commit -m "US#1234 ..." / "Defect#1234 ..."
- `developer@workstation/us-1234-branch`: git push -u origin us-1234-branch

### Rework commit before pull request (Stash) - optional

- `developer@github`: Check how many commits the fork is ahead with: `This branch is 13 commits ahead of devops-dojo:master.`
- `developer@workstation/us-1234-branch`: git rebase -i HEAD~13
- `developer@workstation/us-1234-branch`: in editor, use `pick` for the first commit and `squash` for the others 
- `developer@workstation/us-1234-branch`: save and close editor, then keep only one commit comment
- `developer@workstation/us-1234-branch`: git push -u origin us-1234-branch --force


### Pull Request

- `developer@github/developer/repoX`: open Pull Request against upstream/master
- `pull_request_build@jenkins`: build/test Pull Request branch and post result to GitHub
- `committer@github`: review Pull Request, comment, request rework

### Rework Pull Request

- `developer@workstation/us-1234-branch`: git pull upstream master
- `developer@workstation/us-1234-branch`: rework, rework, rework, build, test
- `developer@workstation/us-1234-branch`: git add ...
- `developer@workstation/us-1234-branch`: git commit
- `developer@workstation/us-1234-branch`: git push

### Pull Request Cont'd

- `pull_request_build@jenkins`: build/test Pull Request branch and post result to GitHub
- `committer@github`: review new changes, comment
- `committer@github`: merge Pull Request
- `master_build@jenkins`: build/test master branch

### Clean Branch

- `developer@workstation/us-1234-branch`: git checkout master
- `developer@workstation/master`: git pull upstream master
- `developer@workstation/master`: git push
- `developer@workstation/master`: git branch -d us-1234-branch
- `developer@workstation/master`: git push origin --delete us-1234-branch
 
### Reset origin with upstream

:warning: to avoid if someone forked your origin remote, as this rewrites history. But handy to reset forked repo with what is in upstream.

- `developer@workstation/master`: git remote update
- `developer@workstation/master`: git reset --hard upstream/master --
- `developer@workstation/master`: git push origin +master
