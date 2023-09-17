# learn-git

## Merge 2 repo khác nhau

```
# Assume the current directory is where we want the new repository to be created
# Create the new repository
git init

# Before we do a merge, we have to have an initial commit, so we'll make a dummy commit
git commit --allow-empty -m "Initial dummy commit"

# Add a remote for and fetch the old repo
# (the '--fetch' (or '-f') option will make git immediately fetch commits to the local repo after adding the remote)
git remote add --fetch old_a <OldA repo URL>

# Merge the files from old_a/master into new/master
git merge old_a/master --allow-unrelated-histories

# Move the old_a repo files and folders into a subdirectory so they don't collide with the other repo coming later
mkdir old_a
dir -exclude old_a | %{git mv $_.Name old_a}

# Commit the move
git commit -m "Move old_a files into subdir"

# Do the same thing for old_b
git remote add -f old_b <OldB repo URL>
git merge old_b/master --allow-unrelated-histories
mkdir old_b
dir –exclude old_a,old_b | %{git mv $_.Name old_b}
git commit -m "Move old_b files into subdir"
```