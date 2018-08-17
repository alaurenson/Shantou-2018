## Day 2: Guided bash exercise

Today, we're going to do things a little differently

NO DOWNLOADS!

----

I'm basically going to simplify the instructions from the Unix and Perl Primer, and we're going to work through them all together. In the future - know that textbook is a great reference if you have the time to go through it. 


### 1. Open a new terminal

Mac, use your spotlight to open a UNIX terminal.

Windows, follow me on the screen. 
- Open a Command Prompt, then type `bash` and press enter. 
	

### 2. `pwd` (present working directory)

```
# To display the file structure leading to where you're currently working

$ pwd 
```

Mac, yours will look more simple than mine!
	
Windows, because we're actually running linux within windows will look like this: `/mnt/c/Users/Your_name/`

Remember this! It's not set as your home directory - you'll have to come here to find your desktop. 
	
### 2. `cd` (change directory)

```
# to go down to your Desktop

$ cd Desktop 
```

### 3. Go back with `cd ..`

```
# cd .. will always take you back one directory

$ cd ..
```

### 4. Navigate to bash_practice/

```
cd Desktop/bash_practice/
```
- Use TAB to autocomplete terms!!!
- Also, Notice that you can move more than one directory at a time. 
	
### 5. `ls` (list)

```
# list all the files in your current directory
$ ls 

# You can also list the files in other directories. 
ls Unix_and_Perl_course/
```

What you're seeing is the contents of a directory within your current pwd!
	
### 6. Use `pwd` to check your current working directory again

```
$ pwd
/mnt/c/Users/Charles/Desktop/bash_practice

$ cd Unix_and_Perl_course/

$ pwd
/mnt/c/Users/Charles/Desktop/bash_practice
```
- Do you notice that every time you use cd, the next directory stacks onto the pwd in your prompt?
	
### 7. The home directory

There's an important difference between mac and windows here:

```
$ cd 
# Your pwd is now empty
```

### 8. Get back to where you want to be!

**Mac**, your home directory is easy 
```
# I think this should do it!
$ cd Desktop/	
```

**Windows**
```
$ cd /mnt/c/Users/Your_name/Desktop/	
```
- Running unix on windows has some funny issues - and this is one of them.
	
### 8b. Return to bash_practice
```
$ cd bash_practice
```

### 9.  `..` will always take you back ONE directory. 
```
# You can also chain them together!
$ cd ../../
```

Where are you now? 
	
- Return to bash_practice
- How do you get there?
	
### 11. options

UNIX commands often have options to modify their function. Explore ls
	
```
$ ls -l  
$ ls -lh   
$ ls -R
```
How do these differ?
-l  = (long), gives more informartion about the file
-lh = (long, human readable), not evident here, but it shortens numbers

### 12. `clear` (Self explanatory)

```
$ clear
```
	
### 13. `man` (manuals!)

```
$ man ls
```
man will show the full documentation for any command. There's a lot here, but it can be very helpful!

Use your up/down keys to scroll
	
Quit with `q`
	
### 14. `mkdir` (make directory)

Get into the Unix_and_Perl_course/ directory (with cd)

```
$ mkdir temp
$ mkdir temp1 				# (check with ls)
$ mkdir -p temp2/temp3 			# (check with ls - where is temp3?)
```

Go into temp2 and check with ls, cd .. out of it

### 15. `rmdir` (remove directory)
```
$ rmdir temp1
$ rmdir temp2 				# (why didn't temp2 work?)
$ cd temp2; rmdir temp3
$ cd ..
$ rmdir temp2
```

### 16. practice tab autocomplete
```
$ pwd
$ cd 
```
Now, navigate back to Unix_and_Perl_course/. 

Use the last pwd output to help you! 
Try to use TAB to autocomplete your entries!
	
### 17. `touch` (make an empty file)
```
$ touch this.txt
$ touch that.txt
$ ls
```

### 18. `mv` (move a file)
```	
$ mv this.txt temp/
$ ls
$ mv that.txt temp/
$ ls 
```

### 18. Practice moving

```
$ touch something.txt; touch nothing.txt
$ ls	
```

And now for your first regular expression! `*`

To save time, we can use * to substitute for anything!

```	
$ mv *thing.txt temp/
```

### 19. Practice `*`, and the dangers of `rm` (remove)
```
$ cd temp/
$ ls
```

It is possible to delete everything on your computer, including the operating system, with a single command. I'm serious. I will not tell you how to do this, but it's built with rm. 

`rm`, unless you use `-i`, does not ask, it just deletes. Immediately. Unrecoverably. ALWAYS use `-i`

```
$ rm -i th*.txt (why didn't something.txt or nothing.txt dissapear?)
$ rm -i *thing.txt
```

### 20. `alias` (custom commands)

You can use 'alias' to build your own temporary commands!
Because rm is dangerous without -i, let's do this:
```	
$ alias rm='rm -i'
$ touch test
$ rm test (see how it now asks you?)
```

alias can use turn any phrase you want into a command, as long as what's `='here'` is actually bash.
	
### 20. `cp` (copy)
```
$ touch algae.txt
$ cp algae.txt more_algae.text
$ rm -i *ae.txt
```

----

*Now we have a little knowledge on how to get around. Let's start interacting with actual files!*


### 21. `less` (open a file without editing)

```
$ less Data/Arabidopsis/At_proteins.fasta
```

Once in the 'less' call screen - 
- h (for help commands)
- scroll with up/down
- q (quit)
		
### 22. "Hidden" files
	
Bash hides files that begin with a '.'
You can see them by using ls -a (list all)

```
$ ls
$ ls -a (in Unix_and_Perl_course/)
```
What's that??

### 23. profiles and source

Remember aliases? 

Look at .profile with `less`, what can you tell about the aliases there?
	
`source` will allow you to set a profile for your current terminal

```
$ source .profile
```

Do you see an error?
We need to modify the .profile file in order to fix it!
		
### 24. `nano`, a text editor

Navigate to Unix_and_Perl_course/ 

Use `pwd` to find the full directory!

```
$ nano .profile
```

Use your arrow keys to find the line that begins with HOME
	
Edit that line to say "HOME="/mnt/c/Users/Charles/Desktop/bash_practice/Unix_and_Perl_course" (whatever your pwd was)
	
- use ctrl + O to 'write out', or save the edit. 
- You're prompted for a filename. Press enter to keep the same file name
- use ctrl + X to exit nano
	
Now try again. 

```
source .profile
```

What differences can we see?
	
**Note - this only lasts as long as the terminal is open. If you close the terminal, you'll need to re-do any aliases or sourced profiles.** 
	
### 25. Now, there are some changes in your terminal!

```
$ cd			# (will now send you directly to Unix_and_Perl_course/, which is your new home directory)	
```

Check with `pwd`!
	
If we got here today, I'd be totally thrilled. 

### 26. scripts!
```
$ less .profile 
```
Look at the PATH line - every computer has one. It tells UNIX where to look for programs.
	
When we sourced .profile, we set the PATH to look in the Code/ directory. 
```	
$ cd code
$ ls -a
```

Notice that there's nothing? We haven't written any code yet.
	
$ touch hello.sh
$ sh is for 'shell script'
	
$ nano hello.sh
$ type this exactly:
	
> # my first Unix shell script  
> echo "Hi there world!"
	
- ctrl+O, Enter, ctrl X
	
Now do this:
```
$ hello.sh 
```
Do you see your message? 
	
If there's a 'permission' error, you'll need to type:
```
$ chmod u+x hello.sh
```

### 27. One more script

Navigate to Data/Unix_test_files, use ls to check it out. It's a mess!
	
Navigate back to Code/ (remember, back is `cd ..`)
```	
$ nano cleanup.sh	
```

type the following exactly
	
	#!/bin/bash  
	mv *.txt Text  
	mv *.jpg Pictures  
	mv *.mp3 Music  
	mv *.fa Sequences
	
Then do this: ctrl + O, enter, ctrl + X
	
Navigate back to Data/Unix_test_files, and use `ls` to check it out before the next step.
```
$ cleanup.sh
$ ls
```
Now it's clean!
	
### 28. Finally, let's look at some biology!

### 29. `grep` (match pattern - I have no idea why it's called 'grep')

navigate to Data/Arabidopsis
```
$cd Data/Arabidopsis
```

let's look at a fasta file
```
$ less intron_IME_data.fasta
```

Appreciable, but it's a lot!
What if we only wanted the header lines? 

```
grep ">" At_proteins.fasta
```

Woah! You can kill any active process with `ctrl+C`
	
Let's make that grep call more useful:

Time-saver - use the up key to look at your previously-called command!
```
# To print to the screen
$ grep ">" At_proteins.fasta | less

# TO print to a new file
$ grep ">" At_proteins.fasta > headers.txt
```	
	


	

	
	
	
