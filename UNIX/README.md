## The UNIX environment

In Bioinformatics, UNIX is the preferred environment: nearly all available software is written for UNIX. Before we get into true analysis, it's critical to become familiar with this working environment.

----
### First things first: setting up 

#### Mac and Linux systems, conventiently, are already UNIX-based - Windows, however, is not. This doesn't matter; for those of you running Windows, we'll need to configure your machines to run a virtual UNIX envrionment. 

If you have Windows 10, [this is easy.](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/)

Users with earlier versions of windows need to configure a [virtual machine.](https://blog.storagecraft.com/the-dead-simple-guide-to-installing-a-linux-virtual-machine-on-windows/)

#### Throughout all of this, you'll want a dedicated desktop program with which to write scripts, view files, and so on. Normal word processors (like Word) aren't ideal due to limits in accepted file format, and due to an excess of graphical options. 

- For Windows, [Notepad++](https://notepad-plus-plus.org) or [Atom](https://atom.io)
- For Mac, [TextWrangler](http://www.barebones.com/products/bbedit/) or [Atom](https://atom.io)
- For Linux, [Atom](https://atom.io)

In addition to these, you'll want to get familiar with terminal-based text editing software. All of these are already built-in with Unix, so you don't need to download anything. They each have a steep learning curve, but can be incredibly powerful when you're comfortable using them. Best to pick one and learn it well!

- [vim](https://www.vim.org)
- [nano](https://www.nano-editor.org) - probably the easiest to start with!
- [emacs](https://www.gnu.org/software/emacs/)

#### While in this class, one of our primary goals is to teach you to be comfortable working exclusively via the terminal. That said, it can sometimes be useful to have a graphical user interface available for file exploration, especially when working on a remote server. 

- For Windows, use [winSCP](https://winscp.net/eng/download.php)
- For Mac & Linux, use [CyberDuck](https://cyberduck.io)
----

### [A crash-course in bash]()

For nearly all file manipulations we'll do, and for any "bioinformatic" analysis programs we'll run, we'll be using bash in the terminal.

Bash is one of several available **shell** languages that allow a user to communcate with the computer's **kernel**. The kernel refers to the active machine-language processes interacting with the computer hardware - this is not generally readable by humans, and so we rely on the shell to allow us to communicate with the computer. 

The kernel is essentially the "linux" or "mac or "windows" itself. The shell is how we communicate with it.

Bash is very common shell language, and is my favorite, so that's what we'll be working with! 

----

### [A crash-course in R]()

An underlying goal in bioinformatic analysis is to produce data that we can visually interperet. An endlessly-useful tool for this is R.

R is a statistical programming language capable of handling massive data-sets (like those we're working on), and is something that all bioinformaticians should be aware of, if not fluent in. A huge number of academic publications use R data analysis, and we'll make use of it later in this course for a variety of things.

To be fair, there are many such languages available (the major one being Anaconda, a distribution of Python) - that said, we'll be able to utilize R effectively in the least amount of time. If you're interested in more sophisticated programming, Python is a fantastic language to learn. 

----

### Other resources and further reading









