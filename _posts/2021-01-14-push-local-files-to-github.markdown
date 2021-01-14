---
layout: post
title:  "Push Local Files to GitHub"
date:   2021-01-14 10:07:45 -0500
categories: jekyll update
---
After creating and updating my blog files locally on my computer, I was ready to
push them to the GitHub page.  The standard process is to go to the folder being
uploaded from the terminal, then to execute the following:

```shell
git status
git add .
git commit -m "Initial commit"
git push origin main
```

After this last step, I keep getting this error message:

```shell
! [rejected]        main -> main (non-fast-forward)
```

To get around this, instead of <code> git push origin main </code>, I had to
execute the following:

```shell
git fetch origin main:tmp
git rebase tmp
git push origin HEAD:main
git branch -D tmp
``` 
