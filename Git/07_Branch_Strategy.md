# Branch Strategy

<br/>

## Branch Types

1. main
2. develop
3. feature/xxx
4. release/xxx
5. hotfix/xxx

<br/>

## Overall Branch Strategy Flow

1. When a product requirement (Theme) occurs, a repository is created and a main branch is created simultaneously
2. When main branch is created, immediately create a develop branch for development and set it as the default branch
3. Feature branches are created from the develop branch and occur each time a feature (Story) is written
4. When one feature branch development is complete, merge it into the develop branch (Epic)
5. When Stories come together to form an Epic, a release branch is created
6. When the release branch is complete, merge it into both main branch and develop branch
7. If a problem is detected in the main branch, hotfix branch is created from the main branch
8. When the hotfix branch is complete, merge it into both main branch and develop branch

<br/>

## Rules by Branch

### main

- The main branch stores official release records
- PR acceptance from release branches is performed by the project manager
- Means that the problems in the requested release branch have been confirmed to be resolved

### develop

- Develop serves as an integration point for branch feature development
- Merging into develop means that the review and testing of the integrating branch has been completed

### feature/xxx

- xxx means the feature being written e.g. when developing authentication feature: feature/auth
- Each feature should be developed by creating a new branch, and its naming should clearly indicate what function that branch performs
- The MR for that branch is requested by the person in charge to the master before sprint completion, and the master approves it as a sign of agreement and acceptance that there are no problems with that feature
- When modifying and adding to that branch, the minor version is upgraded
- In very rare cases (depending on importance), the middle version is upgraded

### release/xxx

- xxx means a sequence of numbers according to the release version rules e.g. 1.2.3
- Created when the develop branch has completed sufficient feature development for release or when the release schedule is approaching
- When release preparation is complete in the created release branch, create a PR to main
- Numbers are version names, listed separated by '.' according to the following rules:
  - Major version: Theme update
  - Middle version: Epic-level update or large-scale Story update that could be handled as an Epic
  - Minor version: Story-level update and patches

### hotfix/xxx

- xxx means the meaning of the generated issue
- Creating a hotfix branch means that a critical bug has occurred in the released product
- Used to quickly patch releases

<br/>

## Commands by Branch

### Develop Branch

```shell
git branch develop
git push -u origin develop
```

- When initially creating, create a develop branch from the main branch and push it to the server
- Merge to main by Epic units

### Feature Branches

```shell
git checkout develop
git checkout -b feature/branch
```

- Each new feature (Story) should be developed by creating a new branch
- In other words, when implementing a feature of any unit, create that branch from the develop branch and develop it
- When creating a branch, the naming should clearly indicate what function that branch performs

```shell
git checkout develop
git merge feature/branch
git branch -d feature/branch
```

- Generally, feature branches are created from the latest develop branch
- Proceed with commits by Task units
- When Story is complete, push to server (remote) for backup / collaboration / code review
- When requesting code review, the reviewer fetches that branch, checks it, and reviews
- When development of one feature is complete, merge it back into the develop branch and delete the feature branch
- **Feature branches never interact directly with the main branch**

### Release Branches

```shell
git checkout develop
git checkout -b release/0.1.0
```

- Creating a release branch is created from the develop branch according to the release timing
- If the develop branch has completed sufficient feature development for release
- Or if the release schedule is approaching, start release preparation in the created release branch
- New feature development cannot be added to the release branch
- Only perform bug fixes, documentation creation, and other release preparation work

```shell
git checkout main
git merge release/0.1.0
git checkout develop
git merge release/0.1.0
git branch -d release/0/1/0
```

- While using release-only branches for release preparation, other teams can proceed with next release feature development
- When release preparation is complete, merge the release branch into both main branch and develop branch and delete the release branch
- Merge the release branch into the main branch and tag the version information

### Hotfix Branches

```shell
git checkout main
git checkout -b hotfix/branch
```

- Hotfix branches are used to quickly patch releases
- Hotfix branches are created from the main branch

```shell
git checkout main
git merge hotfix/branch
git checkout develop
git merge hotfix/branch
git branch -D hotfix/branch
```

- When the fix is complete, merge it into the main branch and develop branch (or current release branch) and tag the updated version in the main branch
- When the fix is complete, like the release branch, the hotfix branch is merged into both the main branch and develop branch and the hotfix branch is deleted
