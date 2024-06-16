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

