muq
===

Simple text file version control. To keep track of versions of plain textfiles such as configuration files and the likes.

## Purpose
I believe everybody has been there. That moment where you change the configuration of this or that, and you look into the folder of said configuration, and it looks like this:

```
dbconfig dbconfig_DONOTDELETE dbconfig_old dbconfig_older dbconfig_oldwww dbconfig.bak
```

*Now, which one was it again that I wanted to restore?*

Sure, it would be neater to track all the versions in a nice [Git](https://git-scm.com/) repository. But more often than not, you would find yourself in a situation where Git would be overkill, or simply not present on said machine. For this reason, I wrote a simple bash-script so you can do some rudimentary version control that is way better than simply littering the folder with all sorts of backups you have problems remembering the important When and Why, later on.

## Usage
`muq` is essentially a sort of stack, where you push your changes to. And if needed, you can pop previous changes out of that.

### init
Before anything else, you need to tell muq you wish to track the file.

```
muq init yourfile.txt
```

It will create an `.muq` folder, where it stores changes, messages and whatnot.

### status
To show the status of the file, the last push message and if it has recently been changed, simply punch:

```
muq status yourfile.txt
```

### log
To show the last 10 push messages of this file, use:

```
muq log yourfile.txt
```

If you want a certain amount of messages, just add it to the commandline:

```
muq log yourfile.txt 5
```

### push
If you have changed your file, you can push the changes by typing:

```
muq push yourfile.txt
```

It would be nice if you could tell why you changed the file, so it is recommended you add a message to the pushing-process:

```
muq push yourfile.txt "Changed blabla to true, because I can."
```

### pop
If the changes didn't do what you wanted it to do. You could return to the previous state using pop.

```
muq pop yourfile.txt
```

Or the state before that, or before that. Etc.

**Warning:** `pop` not only applies the previous `push`. It also removes it. Meaning you can go back, but can't go forward, unless you hit `reset`. If you wish to go back without removing the previous pushes, use `pick`.

### pick
If you really want to roll back all the way to a far certain past, you can use `pick` to roll back to a certain push.

```
muq pick yourfile.txt cfe249228e3eb18fa152e3e349ec55fa
```

**Note:** Unlike `pop`, this doesn't delete your previous pushes.

### reset
If everything has failed, you can easily return to the last push, using `reset`.

```
muq reset yourfile.txt
```

If everything has failed badly, you can also return to the very first version, by adding `top`.

```
muq reset yourfile.txt pop
```

**Note:** If you make changes after reset, and hit push. Make sure you mention the reset in the push message.

### Eventhooks
In case a change in a file requires to do stuff afterwards. Lessay, restarting a daemon or service. There are eventhooks present.
See the scripts in the `.muq/evts` folder for that.

**Note:** `pick` runs the `.pop`-script.

## Contributing
Yes, I would love me some pull requests. If you do, please update the AUTHORS file as well.

#### Features I would love to add

 * A minimized version. So one would be able to copypasta it over an SSH-shell.
 * Coloring.
 * Log output formatting.
 * Maybe some error handling?
 * Documentation would be nice.
 * Any other great ideas.

#### Features I would rather not add

 * Branching. If you want branches, use Git.
 * Remote-tracking. Use git. Or try to convince me.
 * Tracking of entire directories. We have git for that.

### Compatibility notes
Please note that it has to work on bare minimum installations (say, busybox-compatible). It is also much easier to copypasta a bash script over SSH, than trying to paste three odd Perl-modules.

## License
Copyright (c) 2015 Royi Eltink
License: MIT
