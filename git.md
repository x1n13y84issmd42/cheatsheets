## Merge using theirs

    git checkout branchA
    git merge -X theirs branchB

In case the merge deletes files from branchA, there may be a conflict. `git rm` the conflicting files, then merge should go smoothly.