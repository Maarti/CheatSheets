# Perforce cheatsheet

## Getting started
Start server: `p4d -r path/to/server/folder -p localhost:1666` *(if that doesn't work, kill the "Helix..." service running that already use port 1666)*
Connect to server: `p4`
Check connexion: `p4 info`
Create a stream depot: `p4 depot -t stream JamCode`
Create a stream: `p4 stream -t mainline //JamCode/main`
Lists the streams: `p4 streams`

Set P4CLIENT env. variable: `set P4CLIENT=my_workspace_name`
Bind workspace to the stream: `p4 client -S //JamCode/main`
Verify workspace has been created: `p4 clients -S //JamCode/main`

## Definitions
 A Perforce **depot** is a repository of files that lives in a Perforce server. A Perforce server can have any number of depots and each depot can contain any number of files.
 
 A Perforce **workspace** or client is an object in the system that maps a set of files in the Perforce server to a location on a user's file system.
 
## [Git:Perforce Command Mappings](https://www.perforce.com/manuals/v15.1/dvcs/_git_perforce_command_mappings.html)
|              Git Command             |           Perforce Command          |
|:------------------------------------:|:-----------------------------------:|
| git add                              | p4 reconcile                        |
| git branch                           | p4 switch -l                        |
| git checkout --orphan new_branch     | p4 switch -cm new_stream            |
| git checkout branch                  | p4 switch stream                    |
| git clone repository                 | p4 clone -p host:port -r remote     |
| git commit                           | p4 submit                           |
| git init                             | p4 init                             |
| git merge branch                     | p4 merge --from stream              |
| git pull                             | p4 fetch -u -r remote -S stream     |
| git pull --all                       | p4 fetch -u                         |
| git push                             | p4 push -r remote -S stream         |
| git push --all                       | p4 push                             |
| git rebase                           | p4 unsubmit followed by p4 resubmit |
| git remote                           | p4 remotes                          |
| git remote add new_remote repository | p4 remote new_remote                |
| git status                           | p4 status                           |