# Let's Git Together - A Tale of Commitment

## ABOUT US - Underlying Concepts

### Git
- A version control tool
- Alternatives include SVN and CVS

### GitHub
- A company that acts a host in the cloud
- Alternatives include Bitbucket (Stash) and GitLab

### Commits
- Git is all about commit hashes
- Branch names are just pointers/references to commit hashes
- One commit hash could have multiple branch alias, but every commit must have a unique hash

## TERMS & CONDITIONS - Terminology

- Local: your local drive (computer)
- Remote: on the server, aka GitHub
- Branch: an alias which points to series of commits in one line of development
- Upstream: the remote counterpart of your local branch
- Top of tree: the most recent commit of your master
- Tracked file: a file that Git versions
- .gitignore: a list of files/folders/patterns that should never be tracked, such as tokens, auth keys, binaries (images, executables, etc.)
- HEAD - the commit/position on which you are locally
- HEAD^ or HEAD~1 - one commit before, aka the parent of, your current position
- HEAD^^ or HEAD~2 - two commits before, aka the grandparent of, your current position*
- Detached HEAD - your current position that is not the most recent commit

\* HEAD^^ and HEAD~2 might not always point to the same commit. If you need to refer to a commit more than 2 generations before, it’s better to look up the unique commit hash.

## SIGNING UP - Getting Started

### Forking and Cloning
- Log into your Github account.
- Go to `https://github.com/antoniawang/workshop` and click the `Fork` button in the upper right. Follow the directions to Fork the workshop to you repo.
- Migrate to the folder where you want to house this workshop’s repo files (this folder will be the parent directory). Follow the instuctions to clone: `git clone <YOUR-GITHUB-REPOS-URL>`.
- `cd` into `git_workshop`.
- Do a `git status` to make sure everything is where you want it.
- If you messed up, you can do `rm -rf .git` to “un-git”

### Starting from Scratch (unlikely)
- If you wanted, you can also start by creating some files in a local folder: `git init`


## THE DATING GAME - Adding and Committing

### Basics
- Create a file called `helloWorld.txt` and open it in your preferred text editor. Hint: useful commands are `touch` and `open`.
- Write the line “Hello World!” and save the file.
- Do `git status` and you should see a message about `helloWorld.txt` being an untracked file.
- Let's track it: `git add helloWorld.txt`. Do another `git status` and you should see `helloWorld.txt` is staged for commit.
- Now commit your changes and use the `-m` option to add a message: `git commit -m “created helloWorld”`. PRO TIP: ALWAYS have a USEFUL commit message, so your future self or another person working with you won't hate current you. Commit messages should describe the changes you made and, when applicable, include the JIRA ticket number.
- Push your changes to the remote (Github): `git push`.

### Ignoring the Signs
- Generally, you don’t want to track/version certain types of files: binary files (images, audio, videos, etc), databases, and passwords or keys. So put these in the `.gitignore.` file.
- Go to `https://confluence.creditkarma.com/display/QE/Quality+Engineering` and download the House QE bug sigel into your repo folder.
- Do a `git status`. It says no changes! Why? Let's look at our `.gitignore` file.
- Open `.gitignore` and you can see that we're ignoring (not going to track) all `.png` and `.jpg` files. Now comment out the line first line: `# *.png`. Save and exit.
- Now do `git status` again. See what’s changed? Git is asking if we want to track the House QE sigel image.
- Since we don't actually want to track an image file, do `git checkout .gitignore` to revert that comment change (we’ll go over how to revert file changes and commits in a bit). 
- Notice that your `.gitignore` file is back to it was in the beginning.
- Add the line `new_lyrics/` to your `.gitignore` file. Add and commit. Note: This prevents Git from tracking any new changes to files in that folder. We are not going to make any changes to the lyrics in that folder; they are there so you can easily copy and paste over new lyrics.
- On your own, you can download and track an image, make a change to the image (crop or annotate it), and see if you can understand the `git diff` report.

### Moving Fast
- In `helloWorld.txt`, add a line “I am going to change up some lyrics.”
- Open `bells.txt` and `new_lyrics/smells.txt`. Replace the first line of `bells.txt` with the first line of `smells.txt`.
- Add ahd commit your changes: `git add helloWorld.txt bells.txt`; `git commit -m "replaced first line of bells.txt"`.
- Replace second line in `bells.txt` with the second line from `smells.txt`.
- Open `history.txt` and `new_lyrics/tree.txt`. Replace the first line of `history.txt` with the first line of `tree.txt`.
- Add all files at once with `git add .`. Use `git status` to see you've added both files. Commit.
- In `helloWorld.txt`, add a line “I love The Simpsons.”
- Replace all the remaining lines in `bells.txt` with the remaining lines from `smells.txt`.
- Replace all the remaining lines in `history.txt` with the remaining lines from `tree.txt`.
- Do a `git status` and `git diff` just to check what's happening. PRO TIP: Use `git diff <fileNAME>` will show you the differences for an individual file.
- Add all files and commit in one step: `git commit -am “I am reckless and added all tracked files and committed in one line.”` Don’t do this unless you’re very sure about what you’re doing. Also, that is a very bad commit message.

### Playing the field 
- In `helloWorld.txt`, add a line “I don’t like The Simpsons.”
- Actually, that’s a lie! Do NOT commit that: do `git stash`.
- In `helloWorld.txt`, add a line “Let’s employ a nanny!”
- Can’t afford it: stash again.
- The stash is just a stack. You can take a peek at what’s at the top of the stack (the latest files you stashed away): `git stash show`.
- Actually, we are going get a nanny: `git stash pop` to place the last change back. 
- Now observe `helloWorld.txt`. That last line is now back, and it’s out of the stash stack.
- Add and commit.
- Now lets send all our changes to the remote: `git push origin master`.

## MULTIPLE PERSONAS - Branching
- Create a new branch: `git branch nanny` (since you’re on master, this will branch off `master` HEAD).
- Go to the new branch: `git checkout nanny`.
- In helloWorld, add a line “My nanny was named Mary Poppins.” Add and commit.
- Do a `git status` ; `git diff`.
- Open `helloWorld.txt' again and change that last line to "My nanny was named Shary Bobbins". Do NOT commit!
- Switch to branch `master`. Oh no! You got an error asking you to stash or commit changes before switching branches. We will do neither! We can use `git checkout to throw away our changes: `git checkout -- helloWorld.txt`. This option throws uncommitted changes you've made to a given file/path.
- Now switch to branch `master` again. Success!
- Create and switch to a new branch in one command: `git checkout -b bobbins.`
- In `helloWorld.txt`, add a line “My nanny was named Shary Bobbins.” Add and commit.
- Create and checkout a new branch, `temporary` (off of `bobbins`).
- Try to delete `temporary` branch: `git branch -D temporary`. OOPS, you got an error! You can’t delete a branch you’re currently on, duh.
- Checkout branch `nanny`, and delete branch `temporary`.
- Let’s also modify the first line of `sugar.txt` by capitalizing every word. Add and commit.
- Push your branch to the remote: `git push -u origin nanny`. PRO TIP: name the remote the same thing as your local. It makes thing easier.
- Checkout `bobbins`, open `sugar.txt` and `new_lyrics/corner.txt`. (Notice that `sugar.txt` does not have the changes you made on branch `nanny`.) Replace the first stanza of `sugar.txt` with the first stanza of `corner.txt`.
- Push your branch to the remote: `git push -u origin bobbins` (name it the same thing).
- Let’s create two more branches that we’ll use later: Checkout `master` and create and checkout a branch named `american`. Add and commit.
- Modify the first stanza of `sugar.txt` with whatever you like.
- Now checkout `nanny` and create and checkout a new branch,  `half`. 
- Modify the fourth stanza of `sugar.txt` by reversing the order of the last two lines. Add and commit.


## GETTING SERIOUS - Merging
- Go back to branch `master`.
- Before we do anything, we should ensure we have the latest `master`: `git pull origin master`. This pulls the latest version of the branch master from the remote and updates your local copy.
- Merge in `nanny`: `git merge nanny`. If you get a merge conflict, do `git diff` and see if you have extra whitespace at the end of your `helloWorld.txt`. If you need to fix this, do `git merge --abort`, then fix the whitespace and try again. Complete the merge by following the instructions on the screen. It will be a file in vim, which you will need to save by typing in `:wq`.
- Make a descriptive commit message indicating this was a merge. Your future self will thank you.
- Now push your updated copy of master to the remote: `git push origin master`.
- PRO TIP: It’s good practice to not keep around stale branches:`git branch -D nanny`.
- Now let’s do it again, merging in `bobbins`. What do you think will happen? Conflict! Let’s talk resolution!

## WE NEED COUNSELING - Conflict Resolution
### Merge Tool
- Do a `git status` to show the files which are conflicted.
- Show the diff of all files under conflict: `git diff`. 
- Use `git mergetool` to resolve conflicts. We are assuming we're all using the default `OpenDiff` tool.
- For files, select "choose right" in the dropdown. Save and quit the `OpenDiff` program.
- Then complete the merge (follow instructions on screen): `git commit`; save the commit message that appears in vim; `git push origin master`.


### Rebasing
- Remember we had those other two branches? Well now they’re super out of date. We should make sure they’re not as stale: `git checkout half`; 
`git rebase master`,
- Rebasing replays all the commits on the branch onto another branch, e.g. in this case you replay all the commits from half onto the new master. You can rebase any branch onto any other branch, as you like.
- Did you conflict? No, lucky ducky. If yes, follow these steps for manual conflict resolution.
- `git diff sugar.txt` to see the difference. Notice the lines which indicate where you have a conflict. Now open the file in an editor. Keep the line you want and delete all the git messages surrounding it. Save and quit.
- `git add sugar.txt` to indicate the conflict was resolved.
- git rebase --continue` to continue.
- We've successfully rebased. But what if this is just not working?

## THE BLAME GAME - Finding a scapegoat
- To get the history of your current branch: `git log`.
- To see the logs in an text format showing relations of branches, commits and merge points: `git log --graph`.
- Show the history for a particular file: `git log <someFILE>`.
- To show who made the last commit for each line of code: `git blame <someFILE>.`

## BREAKING UP IS (NOT) HARD TO DO - When It's Over.
### It's not you; it's me.
- In `helloWorld.txt`, add a line "Shary Bobbins will return." Add the file.
- Wait, she actually died at the end of the episode. We need to "un-add" that file: `git reset`.
- What if you want to reverse some commit from long ago? First, find the commit you want to reverse: `git log`. Find the commit where you wrote "My nanny was named Shary Bobbins." Copy that commit hash to clip board. Do `git revert <commitHASH>`. PRO TIP: This is why you need good commit messages. Also, the further back you go to revert, the riskier this becomes.
- Actually, we want that line back in. Rather than typing it again, we can revert that the previous revert: `git revert HEAD`.
- Sometimes, your local becomes out of date that you want to blow away all local changes (This happens a lot with CKVM). Do `git log` and you'll notice the last two commits were the "reverts." This is not useful, so let's get rid of them. `git reset --hard HEAD~2` or `git reset --hard <thatCOMMIT>`.

### Actually, it's you.
- Now we have this branch which was rebased onto the new `master`. Let's push it to the remote for posterity: `git push origin half`.
- Oh no! You've been rejected. Why? Because you have 1 commit each on your local and remote branches, and they're not the same.
- What to do? Option 1: `git pull origin half` to pull down the remote change and try to push again. This may work or it may conflict. It's the safe option.
- But we live on the edge, so we'll do option 2, blow away your remote changes with your local changes: `git push -uf origin half.` PRO TIP: BE VERY SURE YOU KNOW WHAT YOU'RE DOING HERE. THERE'S NO GOING BACK.











- Now push to the remote: `git push origin half`. Oh no, another conflict!

- But you need to be careful when rebasing: `git checkout american`.
- What will happen when we try to rebase on master? Conflict!
- Resolve it and then push the new branch


## FAMILY TREE -  Reviewing How We Got Here
- Once we’ve done all the merges, let’s look at how the tree looks. Use the following commands
- `git log` to show all previous commits
- `git log --graph` to show an ASCII graph of your git history
- 1git log --first-parent1 to show only the merges
- `git log <SOME_BRANCH>` to show git log as if you were on somebranch

**********************************************************

## COUNSELING AND CONFLICTS - Fixing the Kinks

### Rebasing

#### Before you rebase:
- Good practice: always rebase your branch on master before merge
- Go to your local branch: git checkout <new_branch_name>
- Download and update your new remote references (commits): git remote update --prune

#### So what does rebase do? 
- It picks a new starting point for your branch, e.g. master (or any commit), then replays/applies all your branch’s commits, in commit order (oldest first), on that new starting point
- Rebasing my local branch on the remote master: git rebase origin/master
- That line is the equivalent of executing these 4 lines:
1. git checkout master
2. git pull origin master
3. git checkout new_branch_name
4. git rebase master
-Ideally, you’ll see a bunch of “applying” messages and all ends well.

### Still having conflicts?

#### Oops! You still conflicts
- Use the git mergetool to help resolve changes
#### What if you need changes from someone/where else?
- On your current branch: git cherry-pick <some_commit_hash>
- Be careful as cherry-picking could may create conflicts

### The Blame Game

#### Finding a scapegoat
- To get the logs from the HEAD to the branch point off of master and down to beginning of history chronologically: git log 
- To see the logs in an text format showing relations of branches, commits and merge points: git log --graph
- Show the history for a particular file: git log <some_file>
- To show who made the last commit for each line of code: git blame <some_file>

## BREAKING UP IS (NOT) HARD TO DO

### It’s not you. It’s me.

#### Undoing you local changes
- Un-”add” files staged for commit: git reset 
- Blow away local changes on your local current branch to a commit hash: git reset --hard <commit_hash> 
-- Be careful using this, but can be applicable to CKVM
-- Examples: 
--- git reset --hard HEAD~2
--- git reset --hard origin/master

#### Let’s just undo one little thing
- To undo one particular commit: git revert <commit_hash>
- This command creates another commit which is the inverse of (cancels out) that particular commit hash 
- The older the commit you revert, the more dangerous it is
- This command won't work on a commit that is a merge commit (e.g. generated by git merge --no-ff). 

### No, I lied. It's actually you.

#### Erasing your online profile completely
- WARNING: VERY DANGEROUS
- Be wary if someone tells you to do this
- Blow away your remote reference and sets them to your new local: git push -f origin <new_branch_name>
