# Kali Linux Cheatsheet

## Others
### Customise Gnome favorite shortcut
`gksu -u <user> <command>` allows us to run a graphical application as a specified user.

Example : Chrome can't be run as root. So, add Chrome to the favorite bar then edit the file `nano /usr/share/applications/google-chrome.desktop`.

In the *[Desktop Entry]* section, change :
```
Exec=/usr/bin/google-chrome-stable %U
```
to
```
Exec=gksu -u maarti /usr/bin/google-chrome-stable %U
```
*(replace maarti by the name of a non-root user)*
