## The UNIX environment

In Bioinformatics, UNIX is the preferred environment: nearly all available software is written for UNIX. Before we get into true analysis, it's critical to become familiar with this working environment.

----
### First things first: setting up 

#### Mac and Linux systems, conventiently, are already UNIX-based - Windows, however, is not. This doesn't matter; for those of you running Windows, we'll need to configure your machines to run a virtual UNIX envrionment. 

If you have Windows 10, [this is easy.](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/)

Once you've done this, you can open a terminal one of two ways:
1. Click on the Ubuntu icon
2. Open your command line and type 'bash'

Users with earlier versions of windows need to configure a [virtual machine.](https://blog.storagecraft.com/the-dead-simple-guide-to-installing-a-linux-virtual-machine-on-windows/)

#### Throughout all of this, you'll want a dedicated desktop program with which to write scripts, view files, and so on. Normal word processors (like Word) aren't ideal due to limits in accepted file format, and due to an excess of graphical options. 

- For Windows, [Notepad++](https://notepad-plus-plus.org) or [Atom](https://atom.io)
- For Mac, [TextWrangler](http://www.barebones.com/products/bbedit/) or [Atom](https://atom.io)
- For Linux, [Atom](https://atom.io)

In addition to these, you'll want to get familiar with terminal-based text editing software. All of these are already built-in with Unix, so you don't need to download anything. They each have a steep learning curve, but can be incredibly powerful when you're comfortable using them. Best to pick one and learn it well!

- [nano](https://www.nano-editor.org) - probably the easiest to start with!
- [vim](https://www.vim.org) - I'm personally familiar with this one.
- [emacs](https://www.gnu.org/software/emacs/) - You're on your own with emacs. I'm not familiar. 

Now I'll have each of you open a terminal and test these out!

#### While in this class, one of our primary goals is to teach you to be comfortable working exclusively via the terminal. That said, it can sometimes be useful to have a graphical user interface available for file exploration, especially when working on a remote server. 

- For Windows, use [winSCP](https://winscp.net/eng/download.php)
- For Mac & Linux, use [CyberDuck](https://cyberduck.io)
----

### [A crash-course in bash](https://github.com/chazgoo/Shantou-2018/tree/master/UNIX/bash)

For nearly all file manipulations we'll do, and for any "bioinformatic" analysis programs we'll run, we'll be using bash in the terminal.

Bash is one of several available **shell** languages that allow a user to communcate with the computer's **kernel**. The kernel refers to the active machine-language processes interacting with the computer hardware - this is not generally readable by humans, and so we rely on the shell to allow us to communicate with the computer. 

The kernel is essentially the "linux" or "mac or "windows" itself. The shell is how we communicate with it.

Bash is a very common shell language, and is my favorite, so that's what we'll be working with! 

----

### [A crash-course in R](https://github.com/chazgoo/Shantou-2018/tree/master/UNIX/R)

An underlying goal in bioinformatic analysis is to produce data that we can visually interperet. An endlessly-useful tool for this is R.

R is a statistical programming language capable of handling massive data-sets (like those we're working on), and is something that all bioinformaticians should be aware of, if not fluent in. A huge number of academic publications use R data analysis, and we'll make use of it later in this course for a variety of things.

To be fair, there are many such languages available (the major one being [Anaconda](https://www.anaconda.com/download/), a distribution of [Python](https://www.python.org)) - that said, we'll be able to utilize R effectively in the least amount of time. If you're interested in more sophisticated programming, Python is a highly versatile and powerful language to learn. 

----

### Some other resources

1. [The Bash Guide](https://guide.bash.academy): this is an extremely well-written and thorough guide to the intricacies of Bash. Well-worth your time if you want a deeper understanding of the UNIX environment.  

2. [Bioinformatic one-liners](https://github.com/stephenturner/oneliners#etc) compiled by Stephen Turner. These are somewhat advanced compared to what we did today, but resemble the kinds of commands we'll use later in the course.

3. [UNIX commands for NGS data processing](http://userweb.eng.gla.ac.uk/umer.ijaz/bioinformatics/linux.html) written by U. Ijaz. A great cheat-sheet for UNIX commands, and specific commands for dealing with next-gen sequencing data. The exercises herein are very similar to the kind of work we're hoping to achieve in this course.

4. [Python For Biologists](https://pythonforbiologists.com) is a fantastic resource for getting started with Python. This is an extremly powerful programming language, and is something you should check out if you're serious about Bioinformatics. Look at the Python Tutorial section. Sadly, I don't have time (on top of everything else) to get everyone up to speed with Python in two weeks.  







