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
- Now commit your changes and use the `-m` option to add a message: `git commit -m “created helloWorld”`. PRO TIP: ALWAYS have a commit message or your future self or another person working with you will hate current you. Commit messages should describe the changes you made and, when applicable, include the JIRA ticket number.
- Push your changes to the remote (Github): `git push`.

### Ignoring the Signs
- Generally, you don’t want to track/version certain types of files: binary files (images, audio, videos, etc), databases, and passwords or keys. So put these in the `.gitignore.` file.
- Go to `https://confluence.creditkarma.com/display/QE/Quality+Engineering` and download the House QE bug sigel into your repo folder.
- Do a `git status`. It says no changes! Why? Let's look at our `.gitignore` file.
- Open `.gitignore` and you can see that we're ignoring (not going to track) all `.png` and `.jpeg` files. Now comment out the line first line: `# *.png`. Save and exit.
- Now do `git status` again. See what’s changed? We are now tracking House QE sigel image. Do a `git diff` and try to understand the gibberish.
- Since we don't actually want to track an image file, do `git checkout .gitignore` to revert that comment change (we’ll go over how to revert file changes and commits in a bit). 
- Notice that your `.gitignore` file is back to it was in the beginning.
- Add the line `new_lyrics/` to your `.gitignore` file. I'll explain in the next section. Add and commit.
- On your own, you can try to track an image, make a change to the image (crop or annotate it), and see if you can understand the `git diff` report.

### Moving Fast
- In `helloWorld.txt`, add a line “I am going to change up some lyrics.”
- Open `bells.txt` and `new_lyrics/smells.txt`. Replace the first line of `bells.txt` with the first line of `smells.txt`. Note that we will not actually changing any of the files in the `new_lyrics` folder (hence why we put that line earlier in `.gitignore`). They are just there so you can have the new lyric handy.
- Git add and commit.
- Replace second line in `bells.txt` with the second line from `smells.txt`.
- Open `history.txt` and `new_lyrics/tree.txt`. Replace the first line of `history.txt` with the first line of `tree.txt`.
- Add all files at once with `git add .` and commit. See how it added both files.
- In `helloWorld.txt`, add a line “I love The Simpsons.”
- Replace all the remaining lines in `bells.txt` with the remaining lines from `smells.txt`.
- Replace all the remaining lines in `history.txt` with the remaining lines from `tree.txt`.
- Do a `git status` and `git diff` just to check what's happening.
- Add all files and commit in one step: `git commit -am “I am reckless and added all tracked files and committed in one line.”` Don’t do this unless you’re very sure about what you’re doing. Also, that is a very bad commit message.

### Playing the field 
- In `helloWorld.txt`, add a line “I don’t like The Simpsons.”
- Actually, that’s a lie! Do NOT commit that: do `git stash`.
- In `helloWorld.txt`, add a line “Let’s employ a nanny!”
- Can’t afford it: stash again.
- The stash is just a stack. You can take a look at what’s at the top of the stack (the latest change you stashed away_: `git stash peek`.
- Actually, we are going get a nanny: `git stash pop` to place the last change back. 
- Now observed `helloWorld.txt`. That last line is now back, and it’s out of the stash stack (do a `git stash peek`).
- Add and commit.

## MULTIPLE PERSONAS - Branching
- Create a new branch: `git branch nanny` (since you’re on master, this will branch off `master` HEAD).
- Go to the new branch: `git checkout nanny`.
- In helloWorld, add a line “My nanny was named Mary Poppins.” DO NOT COMMIT!!
- Do a `git status` ; `git diff`.
- Create and switch to a new branch in one command: `git checkout -b bobbins.` This actually branches off of master because you did not commit your changes on branch `nanny`.
- Do a `git status` ; `git diff`. Note that the diff is the same! This is because we haven’t committed yet.
- In `helloWorld.txt`, add a line “My nanny was named Shary Bobbins.” Add and commit.
- Create and checkout a new branch, `temporary` (off of `bobbins`).
- Try to delete `temporary` branch: `git branch -D temporary`. OOPS, you got an error! You can’t delete a branch you’re currently on, duh.
- Checkout branch `nanny`, and delete branch `temporary`. 
- Now add and commit `nanny`.
- Let’s also modify the first line of `sugar.txt` by capitalizing every word. Add and commit.
- Push your branch to the remote: `git push -u origin nanny`. PRO TIP: name the remote the same thing as your local. It makes thing easier.
- Checkout `bobbins`, open `sugar.txt` and `new_lyrics/corner.txt`. (Notice that `sugar.txt` does not have the changes you made on branch `nanny`.) Replace the first stanza of `sugar.txt` with the first line of `corner.txt`.
- Push your branch to the remote: `git push -u origin bobbins` (name it the same thing).
- Let’s create two more branches that we’ll use later: Checkout `master` and create and checkout a branch named `american`. Add and commit.
- Modify the first stanza of `sugar.txt` with whatever you like.
- Now checkout `nanny` and create and checkout a new branch,  `half`. 
- Modify the fourth stanza of `sugar.txt`. Add and commit.



**********************************************************




## MULTIPLE PERSONAS - Branching
- Show all you branches: git branch 
- Create a new branch: git branch <new_branch_name>
- Switch to a branch: git checkout <branch_name>
- Creates new branch and switch to that branch: 
- git checkout -b <new_branch_name> 
- List all the remote branches: git branch -r 
- Delete the local copy of your branch: 
- git branch -D <name_of_branch>



## PLAYING THE FIELD - Stashing
You want to mess around without any commitments? Stash it!
1. Make a change
2. Test it out
3. It sucks, but I want keep it on the side? git stash
Each of your stashed changes gets added to a stack
- To retrieve your most recent stashed change: git stash pop (repeat until your stack is empty)
- To see what is at the top of your stack: git stash show

## GETTING SERIOUS AND SETTLING DOWN - Making It Permenant

### Sending Your Branch to the Remote
- Push your branch to the remote: git push -u origin <new_remote_name> 
- This creates remote upstream of your local branch
- Usually, your new remote name should be the same as your local branch name

### Merging
1. Always test changes before you merge - a Continuous Integration (CI) system
2. Go back to your master branch: git checkout master
3. Update your local master to the remote Top of the Tree:git pull origin master 
4. Has master changed? - if yes, you’ll need to rebase
5. Otherwise, merge and see on which commit the merge occurred: git merge --no-ff <new_branch_name>
6. Complete merge by following instructions on the screen

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
