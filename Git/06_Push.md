# git push

<br/>

## 1. Push to Github Repository from VScode

### (1) Create a new Repository on Github

- Click Repositories in the top left of your Github profile screen → Click [New] button in the top right
- Set Owner, Repository name, Description, README, etc., then click [Create Repository]

### (2) Open VScode and create a new file

- Create a folder (Repository to upload to Github)
- Create a new file inside that folder

### (3) Initialize git

```shell
git init
```

- Or click [Initialize Repository] button in the Source Control window (branch-shaped icon on the left side of VScode) to initialize
- This creates and initializes a Repository locally
- This means you'll now manage files in this folder using git commands

### (4) Add to push list

```shell
git add
git commit
```

### (5) Push to Repository created on Github

```shell
git push -u Repository address branch_name

# Example
git push -u https://github.com/ella-yschoi/TIL.git main
```

- This means pushing the main branch to the Repository
- If it asks you to log into github, just log in
- The `-u` option means remember the address you just entered, so from now on you don't need to enter the long address, just enter git push

<br/>

## 2. If entering the Repository address is tedious

### (1) Store Repository address as a variable

```shell
# Store Repository address as a variable
git remote add origin Repository address branch_name

# Example
git remote add origin https://github.com/ella-yschoi/TIL.git main
```

```shell
# Push after storing Repository address as a variable
git push origin branch_name

# Example
git push origin main
```

### (2) If you want to see the variable list

```shell
git remote -v
```
