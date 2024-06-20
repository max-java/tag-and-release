# tag-and-release
testing repo to play with tags and releases

#### See list of latest commits with short message
```
git log --oneline
```
#### See list of latest commits with short message and tag
```
git log --oneline --decorate
```
#### See list of latest commits with tags only
```
git for-each-ref --sort=-taggerdate --format '%(refname:short) %(objectname:short) %(subject)' refs/tags | while read tag hash subject; do printf "%-20s %-10s %s\n" "$tag" "$hash" "$subject"; done
```
#### Create tag on specific commit with message as bullet list (note that if you don't end line with ", message continues on a next line 
```
git tag -a v.0.3-rc c396fed -m "Summary:
* option 1
* option 2
- option 3
- option 4"
```
#### Verify tag
```
git show v.0.3-rc
git tag -n9 v.0.3-rc
```
#### Push tag to remote
```
git push origin v.0.3-rc
```
#### Push all tags to remote
```
git push --tags
```
#### Delete tag
```
git tag -d v.0.3-rc
```
#### Delete tag on remote
```
git push origin :refs/tags/v.0.3-rc
```
#### Rename tag on remote
```
git tag new old
git tag -d old
git push origin :refs/tags/old
git push --tags
```
#### Change tag message on remote. If you don't specify commit hash, it will be the latest commit ([run this to take commit hash](#See-list-of-latest-commits-with-tags-only))
```
git tag -f -a v.0.3-rc c396fed -m "Summary:
* option 1
* option 2
* option 3"
git push -f --tags
```

## Making release
After ongoing development is finished and changes ready to be released:
#### Code freeze - no new commits!
* create a new branch from main for bumping version 
```
git checkout -b release-1.0.3
```
*  on version property remove the -SNAPSHOT suffix and make it simply versioned, e.g. 1.0.3. 
* create a commit with corresponding message
```
git commit -m "Set version to 1.0.3"
```
* create a tag with a version to describe changes made since previos version in business terms (with or without point to specific commit, as it last commit need to be tagged), i.e.
```
git tag -a v.1.0.3 -m "Summary:
* option 1
* option 2
```
* push changes (both for commits and tags)
```
git push
git push --tags
```
* Create merge-request on the main branch and merge changes
* open tag on a github and verify it’s content
* click on “Create release from tag” button 
* click on “Generate release notes” button. It creates list of all merge requests betwen releases and link to comare source code between two versions. Send release name as corresponding version and add to the message Summary from the tag. 

```
## Summary:
* option 1
* option 2

## What's Changed
* {merge request name 1} in {megre request link 1}
* {merge request name 2} in {megre request link 2}
** Full Changelog**: {url}/compare/v.1.0.2...v1.0.3
```
* Mark as latest release and save
* Create merge request on release branch from main and once it reviewed - merge it.
#### Release code freeze: continue development as usual


