### Guided bash exercise

Today, we're going to do things a little differently!

NO DOWNLOADS!

----

I'm basically going to simplify the instructions from the Unix and Perl Primer, and we're going to work through them all together. In the future - know that textbook is a great reference if you have the time to go through it. 


1. Open a new terminal

  - Mac, use your spotlight to open a UNIX terminal. 

	- Windows, follow me on the screen. 
	- Open a Command Prompt, then type `bash` and press enter. 
	

2. pwd (present working directory)

	- type 'pwd' to display the file structure leading to where you're currently working
	
	- Mac, yours will look more simple
	
	- Windows, because we're actually running linux within windows will look like this:

Remember this!
```	
/mnt/c/Users/Your_name/
```
	
2. cd (change directory)

	- type 'cd Desktop' to go down to your Desktop

3. Go back with cd ..

4. type cd Desktop/bash_practice

	- Use TAB to autocomplete terms that exist in
	
	Notice that you can move more than one directory at a time!
	
5. ls (list)

	- type ls, it will list all the files
	
	- type ls Unix_andPerl_course/
	
	What you're seeing is the contents of a directory within your current pwd
	
6. Use pwd to check your current working directory again

```
/mnt/c/Users/Charles/Desktop/bash_practice
```

	Do you notice that every time you use cd, the next directory stacks onto the pwd in your prompt?
	
7. The home directory

	There's an important difference between mac and windows here:
	
	- type cd (blank) 
	
	Your pwd is now empty. 
	
8. Get back to where you want to be!

	Mac, your home directory is easy 
	- type cd Desktop/ to get back
	
	Windows, you have to all of this:
	- cd /mnt/c/Users/Charles/Desktop/
	
	Running unix on windows has some funny issues - and this is one of them.
	
8. Return to bash_practice

	- cd bash_practice
	
9.  `..` will always take you up ONE directory. 

	- cd ../../..
	Where are you now? 
	
	Return to bash_practice

	How do you do this?
	
11. options

	UNIX commands often have options to modify their function. Explore ls
	
	ls -l  
	ls -lh   
	ls -R
	
13. clear (clear screen)

	Self explanatory
	
12. man (manuals!)

	- man ls 
	man will show the full documentation for any command. There's a lot here, but it can be very helpful!
	
	Use your up/down keys to scroll
	
	quit with `q`
	
13. mkdir (make directory)

	Go into the Unix_and_Perl_course/ directory (with cd)
	
	- mkdir temp
	- mkdir temp1 (check with ls)
	- mkdir -p temp2/temp3 (check with ls - where is temp3?)
		go into temp2 and check with ls, cd .. out of it
	
14. rmdir (remove directory)

	- rmdir temp1
	- rmdir temp2 (why didn't temp2 work?)
	- cd temp2; rmdir temp3
	- cd ..
	- rmdir temp2
	
15. practice tab autocomplete

	- cd 
	Then navigate back to Unix_and_Perl_course/. Try to use TAB to autocomplete your entries
	
16. touch (make an empty file)

	- touch this.txt
	- touch that.txt
	- ls
	
17. mv (move a file)
	
	- mv this.txt temp/
	- ls
	- mv that.txt temp/
	- ls 
	
18. Practice moving

	- touch something.txt; touch nothing.txt
	- ls
	
	And now for your first regular expression! `*`
	To save time, we can use * to substitute for anything!
	
	- mv *thing.txt temp/
	
19. Practice *, and the dangers of rm (remove)

	- cd temp/
	- ls
	
	
	- rm -i th*.txt (why didn't something.txt or nothing.txt dissapear?)
	- rm -i *thing.txt
	
20. alias (custom commands)

	You can use 'alias' to build your own temporary commands!
	Because rm is dangerous without -i, let's do this:
	
	- alias rm='rm -i'
	- touch test
	- rm test (see how it now asks you?)
	
	alias can use turn any phrase you want into a command, as long as what's 'here' is bash
	
20. cp (copy)

	- touch algae.txt
	- cp algae.txt morealgae.text
	- rm -i *ae.txt

Now we have a little knowledge on how to get around. Let's start interacting with actual files!


21. less (open a file without editing)
	- less Data/Arabidopsis/At_proteins.fasta
		- h (for help commands)
		- scroll with up/down
		- q (quit)
		
22. "Hidden" files
	
	Bash hides files that begin with a '.'
	You can see them by using ls -a (list all)
	
	- ls -a (in Unix_and_Perl_course/)
	
23. profiles and source

	remember aliases? 
	look at .profile with `less`, what can you tell about the aliases there?
	
	`source` will allow you to set a profile for your current terminal
	- source .profile
	
		Do you see an error?
		We need to modify the .profile file in order to fix it!
		
24. nano, a text editor

	navigate to Unix_and_Perl_course/, use pwd to find the full directory

	- nano .profile
	use your arrow keys to find the line that begins with HOME
	
	edit that line to say "HOME="/mnt/c/Users/Charles/Desktop/bash_practice/Unix_and_Perl_course" (whatever your pwd was)
	
	- use ctrl + O to 'write out', or save the edit. Press enter to keep the same file name
	- use ctrl + X to exit nano
	
	now try 
	- source .profile
	What differences can we see?
	
	Note - this only lasts as long as the terminal is open. If you close the terminal, you'll need to re-do any aliases or sourced profiles. 
	
25. Note that now, if you type

	- cd
	
	It will send you directly to Unix_and_Perl_course/
	
	check with pwd!
	
If we got here, I'll be thrilled. 

26. scripts!

	- less .profile 
	look at the PATH line - every computer has one. It tells UNIX where to look for programs.
	When we sourced .profile, we set the PATH to look in the Code/ directory. 
	
	- cd code
	- ls -a
	Notice that there's nothing? We haven't written any code yet.
	
	- touch hello.sh
	sh is for 'shell script'
	
	- nano hello.sh
	- type this exactly:
	
	# my first Unix shell script  
	echo "Hello World"
	
	- ctrl O, enter, ctrl X
	
	- hello.sh 
	Do you see your message? 
	
	If there's a 'permission' error, you'll need to type 
	- chmod u+x hello.sh
	
27. One more script

	Navigate to Data/Unix_test_files, use ls to check it out. It's a mess!
	
	Navigate back to Code/
	
	- nano cleanup.sh
	
	type the following exactly
	
	#!/bin/bash  
	mv *.txt Text  
	mv *.jpg Pictures  
	mv *.mp3 Music  
	mv *.fa Sequences
	
	- ctrl + O, enter, ctrl + X
	
	Navigate back to Data/Unix_test_files, ls to check it out
	
	- cleanup.sh
	- ls
	Now it's clean!
	
28. Finally, let's look at some biology!

29. grep (match pattern - I have no idea why it's called 'grep')

	navigate to Data/Arabidopsis
	- cd Data/Arabidopsis
	
	let's look at a fasta file
	- less intron_IME_data.fasta
	
	Appreciable, but it's a lot!
	What if we only wanted the header lines? 
	
	- grep ">" At_proteins.fasta
	
	Woah! You can kill any active process with ctrl+C
	
	Let's make that more useful
	
	- grep ">" At_proteins.fasta | less (use up key to avoid rewriting!)
	
	Or
	
	- grep ">" At_proteins.fasta > headers.txt
	
	


	

	
	
	
