# An Introduction to the Linux Command Line

*Last updated: September 17, 2020*

## Getting Around in Linux

* File paths (directories or folders): `/`, `/home/<gatorlink>/`, `/blue/<group>/<gatorlink>/`
* `pwd`, `cd`, `ls`  (Where am I, change directory, list directory)
* `cp`, `mv`, `rm`  (copy, move, delete)
* `more`, `less`, `head`, `tail`, `cat`  (examine files)
* `nano`, `vim` (text editors in Linux)

## Making Things Easier

* **Tab completion**- type part of a path and hit tab-key, the shell will auto-complete for you
* **`history`**: redo something that you did before without retyping (use :arrow_up: arrow key )
* **`man`**: getting help, also `–h` or `--help` flag (e.g.: `man ls`)

## Learning by Doing

(Note: some of the data and examples are taken from [software- carpentry.org](https://swcarpentry.github.io/shell-novice/)):

1. Connect to HiPerGator:
   1. *Mac*:  `ssh <gatorlink>@hpg.rc.ufl.edu`
   1. *Windows*: hostname: `hpg.rc.ufl.edu`
   1. Type your password and hit return (no characters display while you type).
1. Where are you when you login? `pwd`
1. What files are there? `ls`
1. At Research Computing, we ask that users keep most of their data in the `/blue` folder. Let’s cd there: `cd /blue/<group>/<username>` (replace group with your PI’s group and username with your GatorLink)
1. Let’s make a directory to put some data in: `mkdir cli_demo`
1. Now what’s there? `ls –l`
   1. Linux commands usually have flags to change how they work
   1. `man`, `–h` or `--help` often give you help
1. Change into cli_demo directory: `cd cli_demo` or `cd cl<tab>`
1. Copy some demo data here (`.`):

    `cp -r /data/training/LinuxCLI/molecules .`

   1. Note the `-r` to recursively copy, since `cp` won’t copy directories by default
   1. Also note the “`.`” at the end to copy the molecules directory to your current location.
1. Check that the copy worked: `ls`
1. cd into the molecules directory: cd molecules
1. Look at these files with `more`, `cat`, `head`, `tail`:
   1. `more propane.pdb` and  `cat propane.pdb`
   1. `head propane.pdb`    or    `head –n2 propane.pdb`
   1. `tail propane.pdb`    or    `tail –n2 propane.pdb`
1. **Redirects**: You can redirect the output of a command to a file with the `>` character. **Caution: This erases the file first.** You can append to a file with `>>`
   1. `wc -l *.pdb > lengths.txt`
   1. Let’s see what this file looks like: `cat lengths.txt`
1. **Sorting**: We might want the lengths sorted: `sort -n lengths.txt`
   1. What happens without the `–n`?
1. `Pipes`: We can connect commands together by piping the output from one command into the input for the next command:
   1. `wc -l *.pdb | sort -n > lengths.txt`
   1. Or if we only want to know the shortest file: `wc -l *.pdb | sort -n | head -n1`
1. **`grep`**: We can search for text using grep:
   1. `grep ATOM propane.pdb`
1. *`awk:`* `awk` can do a lot, but one thing it’s good it is pulling out columns from files:
   1. `grep ATOM propane.pdb | awk '{print $3}'`
1. *`uniq`*: `uniq` is a command to find unique entries in a sorted list:
   `grep ATOM propane.pdb | awk '{print $3}' | sort | uniq`
1. **Loops**: One of the great things about the command line is the ability to automate repetitive tasks. Let’s say we want to verify that all our molecules are hydrocarbons (made up of only C and H atoms):  

    ```bash
    for molecule in *.pdb
    do
    echo $molecule
    grep ATOM $molecule | awk '{print $3}' | sort | uniq
    done
    ```

1. **Deleting files**: Let’s get rid of the lengths.txt file: `rm lengths.txt`
   1. That file is now gone!! There is no undo, no recycle bin or trash can. As soon as you type the command and hit return, the file is gone!
   1. Be careful, but don’t keep everything either!

## Additional exercises

* Which molecule has the most H atoms?
* Make a directory in your cli_demo folder and copy the methane.pdb file there (preferably without moving from the molecules directory)
* From the molecules directory, get the head of the methan.pdb file in the directory you created above.
* Change directories to the directory you made above, rename the methane.pdb file to my_methane.pdb.
* Edit the my_methane.pdb file and put your name as the AUTHOR.
* How many ATOMS does methane have?
* Use an SFTP program to download the molecules folder to your computer
