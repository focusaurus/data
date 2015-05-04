## Part One: Bow to Your Sensei

![Bow to your Sensei](http://static1.1.sqspcdn.com/static/f/1209144/20265241/1347563118103/RexKwonDo2.jpg?token=mU%2Beslcb3UKPj3JU%2FUTKrbccAxI%3D)

These tips are the set of OMG we cannot pair for a single minute until you learn these basic dojo rules. If you haven't got these down, everything is going to take much longer than it needs to.

### tab completion

The shell can help you out with typing long filesystem paths and avoiding typos in command names. It does this with a feature called "tab completion". Tab completion allows you to start entering just the first few characters of something then type the <TAB> key and the shell will complete it for you. So for example, instead of typing `cd ./external/plugins`, you could type `cd ./ex<TAB>` and the shell would expand the rest of the directory name "external", allowing you to keep typing `pl<TAB>` to expand plugins. This saves a lot of typing and prevents typos from ruining your day. Pretty much every experienced command line user I've paired with uses tab completion on nearly every command they run.

### don't cd for one-off commands

Another common pattern I see with beginners at the command line is a tendency to `cd` to a new directory for every command. Think of `cd` like taking off your coat and staying a while. If you are just running a single command dealing with a different directory, there's no need to `cd` to that directory first. `cd` when you are going to stay in a single directory and run a bunch of commands for a while. This will keep your paths short since you can use relative paths and tab completion. But if you just want to list the files in `/tmp`, just run `ls /tmp` without `cd`.

In particular, avoid the tendancy to `cd` every time you use the `ls` command. It usually ends up causing you extra work to `cd` back to your project directory. `ls` can take the names of directories/files to list as command line arguments so instead of

    cd /var/log
    ls

just run

    ls /var/log


### understand space-delimited args

"Do I need to quote it?" is something beginners often ask. You may have heard that all the complex edge cases of bash quoting rules are complex and tricky, and that is indeed true. Here be dragons. However, for the basic cases, it's really simple. By default the command you enter is separated into distinct values on spaces. So if you enter `ls /tmp /home/me /var/log` the shell is going to parse that as 4 distinct tokens with `ls` being the program to run and each of the 3 directory paths as the arguments. So what that means is **when a value you want to pass to a program contains a space, you need to quote it so the shell knows it is one value not several**. So if I have a file path with a space in it like `/tmp/uprade notes.txt` and I want to pass that to the `wc` program, I need to type `wc "/tmp/upgrade notes.txt"` so the `wc` program gets just 1 argument that is a valid filesystem path instead of 2 arguments: `/tmp/upgrade` and `notes.txt`, neither of which are valid. This rule applies to the shell entirely, and it doesn't matter which program is at the start of your command line command, the shell does the parsing before passing the values as arguments to the program being executed.

### navigating command history

Another glaring sign that it's your first day at the command line is re-typing a command you recently ran. The shell keeps a history of commands you ran and makes it easy to re-run a previous command because this is something that happens all the time in typical interactive shell usage. Here are some shell history basics that will keep you moving fast.

- Use the up and down arrow keys to scroll back/forward through your history
  - CTRL-p (previous) and CTRL-n (next) do the same thing and fervent touch typists may prefer these as your hands don't need to leave the home row

And for something you remember running but it was far enough back that you'd need to hit the up arrow many times to find it, there is `CTRL-r` for reverse interactive searching your history. Type `CTRL-r` then any portion of the command you remember and the shell will search backward through your history for a match. Keep typing to find the exact match and hit `ENTER` when you see it to re-run that command. If you need to edit it before running again to modify it slightly, use the arrow keys to move your cursor and the line will be loaded as your current command but not yet executed.

For example:

    cd /tmp
    sudo restart nginx
    ls /var/log
    vi /tmp/some/file.txt
    <CTRL-r>restart<ENTER> #<- quickly re-run the sudo restart nginx command


### line editing keyboard shortcuts

Second only to re-typing previous commands in terms of obvious beginner indicators would be backspacing over most of a command to make an edit to the beginning of the command, then re-typing everything you deleted.

Instead, use the shell's interactive line editing features. These are keyboard shortcuts taken from the 2 most popular command-line text editors: vi and emacs. Most shells support both of these. By default the bash shell loads the emacs keybindings. You can switch to vi bindings with `set -o vi` and back to emacs with `set -o emacs`.

The most important ones for emacs are `CTRL-a` to move the cursor to the beginning of the line and `CTRL-e` to go to the end.

If you use `vi` for text editing, you'll love having all your favorite move/edit commands available.


## Part Two: Breaking Boards

![Breaking Boards](http://www.allstaractivities.com/images/karateKatieJumpSpinningBackKick1.jpg)

Now that you've got the basics, let's add some intermediate skills and understanding that will make you more effective.

Let's start with 2 issues that are a constant nuisance to beginners but once properly understood, immediately solvable every time for the intermediate developer.

### No such file or directory

One of the core subsystem of every computer is a hierarchical data structure called the filesystem. Overall, it's pretty great. It's extremely general purpose and versatile while being pretty straightforward
Another
No such file or directory
✓ ctrl-r history reverse incremental search
✓ arrow keys and ctrl-p ctrl-n to navigate command history
learn WTF sudo does
learn how command lines are verbalized
tar xvzf foo.tar.gz
mkdir -p temp
GNU conventions
one-off aliases
configure bash or zsh with dotfiles on github
link to oh-my-zsh
pbpaste pbcopy
link to my dotfiles
link to shell strict mode
link to Jessica Dillon's tutorials
link to shellcheck
link to shunit2 bat testing
use long options in scripts for readability

## References and Further Reading

- [Bash Emacs Editing Mode Cheat Sheet](http://www.catonmat.net/download/readline-emacs-editing-mode-cheat-sheet.pdf) by Peteris Krumins who writes [an outstanding blog with incredible unix expertise](http://www.catonmat.net/)
