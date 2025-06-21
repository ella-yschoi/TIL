# Install Git

<br/>

## Installing brew on Mac

1. Visit the [Git homepage](https://git-scm.com/), click [Download for Mac] to download
2. Open terminal on Mac
3. Visit the [Homebrew homepage](https://brew.sh/), then enter the command below in terminal

   ```shell
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

4. Enter the password you use to log into Mac in terminal
5. After installation is complete, enter the help command to verify installation was successful

   ```shell
   brew help
   ```

6. If you get an error like `zsh: command not found: brew`, it's because you're using an M1 Mac, so enter the command below

   ```shell
   eval $(/opt/homebrew/bin/brew shellenv)
   ```

<br/>

## Installing Git on Mac

1. Enter the git installation command in terminal

   ```shell
   brew install git
   ```

2. After installation, if version information appears when you enter the version check command, installation is complete!

   ```shell
   git --version
   ```

3. Additionally, if you want to change the default branch name from `master` to `main`, enter the command below

   ```shell
   git config --global init.defaultBranch main
   ```

4. If you're using git for the first time on this device, enter the commands below in order

   ```shell
   git config --global user.email "ella@gmail.com"
   git config --global user.name "Ella"
   ```
