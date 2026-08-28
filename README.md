# Instructions
These instructions use `<gh-username>` as a placeholder for your own github username. You should replace it with your username in any command.

## Fork this git repository
**Fork** this repository to your personal GitHub space. Specifically:
1. Make sure you are logged in to github.com
2. Go to <https://github.com/ubsuny/compphys-git-exercise>
3. Click the "fork" button
4. On the forking page, accept the default option and click "Create fork"

## Clone the forked repository to your laptop:
```
git clone git@github.com:<gh-username>/compphys-git-exercise
```

You can use the following commands to inspect the branches and remote configuration:

```
git branch -a # -a lists both local and remote branches
git remote -v # -v is verbose mode
```

## Exercise 1: a simple git add/commit/push
1. Copy the file `template.md` to `<gh-username>.md` (just work in your local `main` branch, don't worry about creating a new branch):
```bash
cp template.md <gh-username>.md
```
2. Open the new file in a text editor and answer the questions.
```bash
nano <gh-username>.md
# (Answer the questions)
```
3. Commit the new file to your local git repo. Specifically:
    1. Stage the file (i.e., tell git you want this file in your next commit) with `git add <gh-username>.md`
    2. Do `git status` to see what happened.
    3. Commit the file (wrap up the staged files into a commit) with `git commit -m "type a log message"`)
    4. Do `git status` again to see what happened.
    5. Do `git log` to see your commit, now permanently recorded in the history of this branch.
```
git add <gh-username>.md
git status
git commit -m "Add <gh-username>.md"
git status
git log
```
4. Push the files to the remote repo on github.
```
git push 
# Or maybe 'git push origin main'
```
5. Check that you can see the updates on github.com (i.e. open a web browser and find the updated files). 

If you can see the updates on github, then the instructor can see them, too. When we get to homework assignments, this counts as "turning in" the assignment. You can continue pushing more changes until the due date (or beyond, depending on the instructor). 

6. Create a **pull request** to merge your fork back to the original ubsuny repo. Navigate to your forked repo on github: there should be a big green button to create a pull request. Note: pull requests are a GitHub-specific feature (not part of git), but are nonetheless a key part of managing software projects.


## Exercise 2: working with a branch
1. Inside your local `compphys-git-exercise` folder, create a new branch with the following command:

```
git switch -c feature-test
```

`git switch` is the overall command for switching between branches. The `-c` flag **c**reates a new branch, so this command basically creates a new branch, and then switches to it. 

2. Make a modification to `<gh-username>.md`. For example, add your favorite color at the bottom.
3. Repeate the git add and commit:
```
git add <gh-username>.md
git commit -m "Add favorite color"
```
You now have a new commit on the feature branch, corresponding to the new `<gh-username>.md` file. 
4. Finally, let's merge the new commit back into your `main` branch. First, switch back to the `main` branch:
```
git switch main
```
If you look at your markdown file now (`less <gh-username>.md`), the update will not be there, because it only exists in the `feature-test` branch. Don't worry! Nothing has been deleted. Similarly, if you do `git log`, you will not see the new commit. 

Next, we merge the `feature-test` branch into the `main` branch:
```
git merge feature-test
```
You should now see the color update in `less <gh-username>.md`, as well as the new commit in `git log`. 


## Exercise 3: pulling and merging updates 
Once the instructor has merged everyone's pull requests, your local repo will now be out of sync with the ubsuny repo. Let's use git to synchronize your local repo, basically downloading everyone's `<gh-username>.md` files. 

First, your local repo is only connected to your fork on github, not the ubsuny repo. We can use `git remote add` to add the ubsuny repo as another remote:
```
git remote add ubsuny git@github.com:ubsuny/compphys-git-exercise
```

If you do `git remote -v`, you should see the new remote named `ubsuny` connected to your local repo. 

Next, use `git fetch` and `git merge` (`git pull` is another way, basically combining the two commands):
```
git fetch ubsuny
git merge ubsuny/main
```

Hopefully, the merge operation goes smoothly. If not, resolving merge conflicts is worth learning, but is a bit beyond the scope of this exercise (see, for example, [github merge conflict tutorial](https://docs.github.com/en/pull-requests/how-tos/merge-and-close-pull-requests/resolving-a-merge-conflict-using-the-command-line)). 

