# git  

git story 

1. clone the git repo with readme file   
2. create "index.html" file. and 
```bash 
$ git status 
```  
and see Untracked files: index.html
3. add index.html file stage   
```bash 
$ git add index.html     
```    
4. modify the index.html file and 
```bash 
$ git status 
```  
and see, 
Changes to be committed: index.html    
Changes not staged for commit: index.html    
5. create "style.css" file. and
```bash 
$ git status 
```  
and see, 
Changes to be committed: index.html       
Changes not staged for commit: index.html    
Untracked files: style.css    
6. stash changes
```bash 
$ git stash 
```  
and see, 
Untracked files: style.css  not went to stash    
7. undo the stash.
```bash 
$ git stash pop
```  
and see, 
Changes to be committed: index.html   
Untracked files: style.css
*** Changes not staged for commit: index.html    ??? 

here modified unstage changes change to stage changes automatically but not untrack file.   
8. make some changes on index.html and 
```bash 
$ git status   
```  
and see,    
Changes to be committed: index.html       
Changes not staged for commit: index.html    
Untracked files: style.css   
```bash 
$ git status   
$ git restore --staged index.html    
```  
and see, 
Untracked files: style.css , index.html   (index.html file stage file not stop at "Changes not staged for commit")    
9. add stage to index.html after make some changes to index.html file and  
```bash 
$ git status   
$ git restore index.html    
```  
Changes to be committed: index.html  
(remove changes from "Changes not staged for commit" of index.html file not stay to untrack)       
Untracked files: style.css    
10. 

to see git all commit list with details  
```bash
$ git log  
# commit id 40 charater long sha id 
# Author name 
# commit data and time   
# commit message

#commit 53c000d6967dc436af015c8e5863858d6b73acf0 (HEAD -> main)
#Author: Samadhi Laksahan <samadhip@alliontechnologies.com>
#Date:   Fri Jan 13 22:03:54 2023 +0530
#    commit three

```

to see git all commit list without details  
```bash
$ git log  --oneline
# first 7 characters shortform of ssh id
# commit message   

# 53c000d (HEAD -> main) commit three
# 8bf33a2 index.html
# 93d4716 commit space
# 51394d6 commit 1
# 94d941d (origin/main, origin/HEAD) Initial commit
```
 
to see git all commit list with details changed files  
```bash
$ git log  --stat
# can see count of file-change and details of change inside file   
# commit message, data, author, sha id   

# commit 53c000d6967dc436af015c8e5863858d6b73acf0 (HEAD -> main)
# Author: Samadhi Laksahan <samadhip@alliontechnologies.com>
# Date:   Fri Jan 13 22:03:54 2023 +0530

#    commit three

# index.html | 1 +
# 1 file changed, 1 insertion(+)
```

to see git all commit list with details changed lines   
```bash
$ git log  --patch
# commit 53c000d6967dc436af015c8e5863858d6b73acf0 (HEAD -> main)
# Author: Samadhi Laksahan <samadhip@alliontechnologies.com>
# Date:   Fri Jan 13 22:03:54 2023 +0530

#     commit three

# diff --git a/index.html b/index.html
# index b9c3522..2d8d42f 100644
# --- a/index.html
# +++ b/index.html
# @@ -9,5 +9,6 @@
#  <body>
#      <p>commit one </p>
#      <p>commit two</p>
# +    <p>commit three</p>
#  </body>
#  </html>
# \ No newline at end of file
```

to see git all commit list with details and graph   
```bash
$ git log  --graph
# * commit 53c000d6967dc436af015c8e5863858d6b73acf0 (HEAD -> main)
# | Author: Samadhi Laksahan <samadhip@alliontechnologies.com>
# | Date:   Fri Jan 13 22:03:54 2023 +0530
# | 
# |     commit three
# | 
# * commit 8bf33a2c18ecf6ff22362936100c32597aebf80f

$ git log  --graph --online # short form
```

to see git all commit list with less details and graph   
```bash
# filter last 2 commit (add number after any git log cmd)
$ git log -2

# filter by date
$ git log --after "23-01-01"  # yy-mm-dd
$ git log --after "23-01-01" --before "23-01-01"  # yy-mm-dd

# filter by author 
$ git log --author "allioncore" # show only initial commit 
$ git log --author "samadhip@alliontechnoligies.com" # not show initial commit in list

# filter by commit message   
$ git log --grep="add *" # filter start from "add" word commit messages will list here
```

Reset and the Revert command
```bash
# see the current changes   
$ git log --oneline 

# remove last commit using reset  
$ git reset --hard Head~1
$ git reset --hard 8bf33a2 # 7 charactor id of after removing one (what should be Head commit id)

# remove multiple commit using reset(this will remove until sha1 id) 
$ git reset --hard 51394d6 # 7 charactor id of after removing one (which id should be the Head commit)   

# reset removed commit using reset (this will reset up to sha1 id) 
$ git reset --hard 53c000d # 7 charactor id of after removing one (which id should be the Head commit)

# remove by revert cmd
$ git revert 8bf33a2 # this not remove last one but make new commit without "8bf33a2" changes.   

# reset > for local changes that not pushed to remote
# revert > for remote changes and this can remove witout order.  

hare using revet we can remove '93d4716' by keeping '53c000d' and '8bf33a2'

# 53c000d (HEAD -> main) commit three
# 8bf33a2 index.html
# 93d4716 commit space
# 51394d6 commit 1
# 94d941d (origin/main, origin/HEAD) Initial commit

$ git revert 93d4716 # revert '93d4716' and fix conflicts 
$ git revert --continue # this will automatically make new commit to revert operation.  

# to show changes of sha1 id 
$ git show 93d4716

```

git diff

```bash
# working area - stage area
$ git diff 
# stage area - repository area
$ git diff --staged
# working area - repository area  
$  git diff HEAD


https://stackoverflow.com/questions/9834689/how-do-i-see-the-differences-between-two-branches
```
git remote url   
```bash
$ git remote -v
```

git check diff of remote changes  
```bash
$ git fetch
$ git diff --name-only HEAD..origin/<remote-branch-name> # HEAD..origin/main  mean current-local..remote-branch
# To see changes of a specific file
$ git diff HEAD..origin/<remote-branch-name> -- src/components/Header.tsx
# To see changes for all files  
$ git diff --stat HEAD..origin/<remote-branch-name>
# Compare commit with branch
$ git diff --name-only <ref1>..<ref2>
# To see commit logs
$ git log HEAD..origin/<remote-branch-name> --oneline
```

git check what is the latest updated branch(local/remote)  
```bash
# local
$ git branch --sort=-committerdate # latest branch on top
$ git branch --sort=committerdate # latest branch at end
# remote
$ git fetch
$ git branch -r --sort=-committerdate # latest branch on top
```

git resolve merge conflicts 
```bash
# first check conflict files
$ git diff --name-only --diff-filter=U

# you can manually edit files.
<<<<<<< HEAD
...your version...
=======
...incoming version...
>>>>>>> origin/main

# or you can take one side quickly
git checkout --ours -- path/to/file # keep *your* version of the file
git checkout --theirs -- path/to/file # keep *incoming/remote* version of the file

$ git diff --check # Quick check for leftover conflict markers by showing line numbers of files
$ git commit
$ git push
```

git clean 

* clean cmd don't tracked files and ignored files.   

untracked file.  

clean unstage changes and untracked files.   
```bash
$ git restore .  # clean all unstage file
$ git restore package.json # clean specific file
$ git clean -fd 
```

clean stage change/files  
```bash
$ git restore --staged <filename>  # restore specific file
$ git restore --staged .  
```
