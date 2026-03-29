---
tags: ['CheatSheet', 'Tools']
date: 2026-03-29
status: complete
---


# Programmer Tools

---
## 0x00 ~ Code Editors

### Vim, Code Editor used in 42

VIM is the text editor used in 42. You access a file by using ```vim filename```. To exit VIM  with elegance vim type ```:q```, if you fail to exit VIM you might consider becoming a freelance web developer.

> To generate a truly random string, put a web developer in front of Vim and tell them to exit

You can access VIM configuration by typing
```
vim ~/.vimrc
```

Below is my configuration
```
set number							" Show line number
syntax on							" Highlight syntax
set mouse=r							" Enable mouse click, + enable to copy paste without taking line number
set cursorline						" Enables cursor line position tracking
hi Normal guibg=NONE ctermbg=NONE	" keep vim transparency
highlight CursorLine ctermfg=darkgreen ctermbg=darkgrey cterm=bold	" highlight row with foreground background and style as defined
"highlight CursorColumn ctermbg=darkgrey								" hilight column
highlight CursorLineNR ctermfg=red ctermbg=darkblue cterm=bold	" Sets the line numbering to red background

set cursorcolumn 					" Highlight current column
set tabstop=4						" set tab to 4 spaces
set autoindent						" auto indent file on save

set modeline				" make vim change in a specific file
set modelines=5
```

Some shortcuts that are very handy:
```
CTRL+HOME	send you at the beginning of the file
CTRL+END	send you at the end of the file
YY			copy
PP			paste
DD			delete row
D5D			delete 5 rows
w			save file
q			quit file
:vs {file location}		open another file on the side
:ws			save and quit
ZZ			save and quit
:x			save and quit
:q!			quit without change
ZQ			quit without change
```

### Visual Studio Code

I love VIM and it will always be useful to know how to use it, especially now with the "Cloud" being something you might have to access servers who lack code editors with real GUI.

That said If you want to give a try to another editor I would recommend Visual Studio Code.

My settings.json:
```
{
    "workbench.colorTheme": "Monokai",
    "glassit-linux.opacity": 93
}
```

### Atom

Good editor also, quite hackable, I have been using it for years but recently switch to VIM & VS Code


---
## 0x01 ~ Terminal Bash

[Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) is the terminal you will be using

You can create alias by accessing
```
vim ~/.bashrc
```

```
alias ls="ls -la"
```

PS: Don't create this alias on another's student computer, even thought you might think it is funny, it will wipe out everything:
```
alias ls="rm -rf ./~"
```


---
## 0x02 ~ Git

### Setting up a new Git Repository using [CLI](https://en.wikipedia.org/wiki/Command-line_interface)

It can be done easily using the following command line:  
```
reponame='docker'
mkdir $reponame
touch README.md
git init
git add README.md
git commit -m "[INIT] First commit"
git remote add origin git@github.com:agavrel/$reponame.git
git push -u origin master
```

### Change last commit without changing commit message

> **I choose a lazy person to do a hard job. Because a lazy person will find an easy way to do it** ― *Bill Gates*

It can be done easily using the following command line
```
git add README.md \
&& git commit --amend --no-edit \
&& git push --force
```
**NB: Beware because it will destroy the previous commit with all what it implies**


### Check file committed and unpushed yet

```
git diff --stat --cached origin/master
```

### Undo git add

```
git reset <file>
```


---
## 0x03 ~ Productivity Gains 

> **One of my most productive days was throwing away 1000 lines of code** ― *[Ken Thompson](https://en.wikipedia.org/wiki/Ken_Thompson)*

### [Compile and Execute file on changes](https://superuser.com/questions/181517/how-to-execute-a-command-whenever-a-file-changes?page=2&tab=votes#tab-top)

Create ou run the following script (necessite to download ```sudo apt-get install inotifywait```)
```
while inotifywait -e close_write agavrel.s; do \
nasm -f elf64 agavrel.s \
&& gcc agavrel.c agavrel.o -o a.out \
&& ./a.out arg1 arg2 \
; done
```
Now each time you compile your file you will set the output, very efficient with a transparent editor.

**Use the following script and give the .c file as argument:**
```
while inotifywait -e close_write $1; do \
gcc $1 \
&& ./a.out \
; done
```

---
### [Run Commands in Background](https://linuxize.com/post/how-to-run-linux-commands-in-background/)

You can have multiple processes running in the background at the same time with ```&``` after the command.  
However the background process will continue to write messages to the terminal from which you invoked the command.  

To suppress the stdout and stderr messages use the following syntax:  
```
command > /dev/null 2>&1 &
```

```>/dev/null 2>&1``` means redirect ```stdout``` to ```/dev/null``` and ```stderr``` to ```stdout```

Use the jobs utility to display the status of all stopped and background jobs in the current shell session:
```
jobs -l
```
_NB: a Job is the process running thanks to the command execution_

To bring the job to the foreground use :
```
fg %ID
```
NB: you can use ```bg``` to do the reverse, from foreground to background.

To kill the process use:
```
kill -9 ID
```
Obviously replace ```ID``` in the above examples with the job ID you got from ```jobs -l```.


---

### Read first 8 bytes of a file

```
hexdump -C -n 8 filename
```


---
## 0x04 ~ [Add a a new binary in the PATH environment variable](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix)

Example with terraform:
```
sudo mkdir /opt/terraform
unzip ~/Downloads/terraform_0.12.13_linux_amd64.zip /opt/terraform
```

add to PATH environment variable:
```
export PATH="$PATH:/opt/terraform"
```

then create simlink in /user/bin
```
cd /usr/bin
sudo ln -s /opt/terraform terraform
```

Update path for current session
```
source ~/.profile
```
or
```
source ~/.bashrc
```


---
## 0x05 ~ Computer Graphics Libraries (Ubuntu)

#### Minilibx Installation

Link
```
https://github.com/42Paris/minilibx-linux
```

### SDL2 Installation

Link
```
http://www.libsdl.org/download-2.0.php#source
```

Then
```
./configure
&& make
&& sudo make install
&& sudo apt-get install ibsdl2-dev libsdl2-ttf-dev
&& sudo apt-get libsdl2-image-2.0-0 libsdl2-image-dev
```


---
# :gem: Curated list of Programming Learning Materials

*Only petty thieves would google the following material, adding "torrent" or "pdf" keywords, real Gentlemen would purchase a digital copy*  

**NB: If you want to complain about a copyright enfringment, kindly raise an issue or send me an email and I will remove the offending link**  

---
## 0x00 ~ C Knowledge

```c
 <stdio.h>

int f(int n) {*&n*=2;}

int main(void) {
    printf("%d\n", f(0b10101));
}
```

> **C is [quirky](https://en.wiktionary.org/wiki/quirky), flawed, and an enormous success** ― *[Dennis Ritchie, Creator of the C language](https://en.wikipedia.org/wiki/Dennis_Ritchie)*

Title | How Interesting | Author
---|---|---
**[The C Programming Language 2nd Ed Subsequent Edition](https://www.goodreads.com/book/show/515601.The_C_Programming_Language)** | :two_hearts: | *by Brian Kernighan and Dennis Ritchie*
**[Obscure C Features](https://multun.net/obscure-c-features.html)** | :star::star::star::star::star: | *[by Multun](https://github.com/multun)*
**[Characters, Symbols and the UTF-8 Miracle - Computerphile](https://www.youtube.com/watch?v=MijmeoH9LT4)** | :star::star::star::star: | *by Tom Scott*
**[Automatic Vectorization](https://www.codingame.com/playgrounds/283/sse-avx-vectorization/autovectorization)** | :star::star::star::star: | *[by Marchete](https://github.com/marchete)*
**[Writing Solid Code](http://cs.brown.edu/courses/cs190/2008/documents/restricted/Writing%20Solid%20Code.pdf)** | :star::star::star::star: | *by Steve Maguire*
**[Fast wc Multithread SIMD](https://github.com/expr-fi/fastlwc)** | :star::star::star::star: | *by [expr-fi](https://github.com/expr-fi)*
**[OpenMP Multithreading Programming](https://bisqwit.iki.fi/story/howto/openmp/)** | :star::star::star::star: | *by Joel Yliluoma*
**[Understanding lvalues and rvalues](https://eli.thegreenplace.net/2011/12/15/understanding-lvalues-and-rvalues-in-c-and-c/)** | :star::star::star::star: | *by Eli Bendersky*
**[The Practice of Programing](http://index-of.co.uk/Etc/The.Practice.of.Programming.-.B.W..Kernighan..pdf)** | :star::star::star: | *by Brian W. Kernighan and Rob Pike*
**[Modern C](https://gforge.inria.fr/frs/download.php/file/38170/ModernC.pdf)** | :star::star::star: | *by Jens Gustedt*
**[Duff's Device](http://www.lysator.liu.se/c/duffs-device.html)** | :star::star::star: | *by Tom Duff*
**[Structure Packing](http://www.catb.org/esr/structure-packing/)** | :star::star::star: | *by Eric S. Raymond*
**[Cello, High Level Programming to C](https://github.com/orangeduck/Cello)** | :star::star::star: | *by Daniel Holden*
**[Asynchronous Routines for C](https://hackaday.com/2019/09/24/asynchronous-routines-for-c/)** | :star::star::star | *by AI William*
**[Are Global Variables Bad](https://stackoverflow.com/questions/484635/are-global-variables-bad)** | :star: | *StackOverFlow*


---
## 0x01 ~ Algorithm

> **When you see a good move, look for a better one** ― *[Emanuel Lasker](https://en.wikipedia.org/wiki/Emanuel_Lasker)*

Title | How Interesting | Author
---|---|---
**[Nailing the Coding Interview](https://github.com/agavrel/Nailing-the-Coding-Interview)** | :kr: | *by Antonin Gavrel*
**[A curated list of Awesome Competitive Programming](https://codeforces.com/blog/entry/23054)** | :star::star::star::star: | *by Inishan (Jasmine Chen)*
**[The Algorithm Design Manual](https://www.goodreads.com/book/show/425208.The_Algorithm_Design_Manual)** | :star::star::star::star: | *by Steven S. Skiena*
**[Games of Magnus Carlsen and Tactics, 2013](https://www.youtube.com/watch?v=Na9g-RzSLuY&t=8m35s)** | :star::star::star::star: | *by [GM Varuzhan Akobian](https://en.wikipedia.org/wiki/Varuzhan_Akobian)*
**[A tour of the top 5 sorting algorithms with Python code](https://medium.com/@george.seif94/a-tour-of-the-top-5-sorting-algorithms-with-python-code-43ea9aa02889)** | :star::star: | *by George Seif*

> **Strategy requires thought, tactics require observation** ― *[Max Euwe](https://en.wikipedia.org/wiki/Max_Euwe)*


---
## 0x02 ~ Bitwise Manipulations

> **The word bit is a contraction of binary digit that was coined by the statistician John Tukey in the mid 1940s** ― *Brian W. Kernighan, D Is for Digital*

Title | How Interesting | Author
---|---|---
**[Hacker's Delight](https://doc.lagout.org/security/Hackers%20Delight.pdf)** | :two_hearts: | *by Henry S. Warren Jr.*
**[Bit Twiddling Hacks](https://graphics.stanford.edu/~seander/bithacks.html)** | :two_hearts: | *by Sean Eron Anderson*
**[De Bruijn Sequence](https://www.chessprogramming.org/De_Bruijn_Sequence)** | :star::star:


---
## 0x03 ~ Network

> **I would tell you a joke about UDP but I’m afraid you wouldn’t get it**

Title | How Interesting | Author
---|---|---
**[Next Generation Kernel Network Tunnel - WireGuard](https://www.wireguard.com/papers/wireguard.pdf)** | :two_hearts: | by JA Donenfeld |
**[Onion Routing](https://www.youtube.com/watch?v=QRYzre4bf7I)** | :star::star::star::star: | *by Computerphile*
**[TCP Meltdown](https://www.youtube.com/watch?v=AAssk2N_oPk)** | :star::star: | *by Computerphile*


---
## 0x04 ~ Hacking & Security

> **Never underestimate the determination of a kid who is time-rich and cash-poor** ― *Cory Doctorow, Little Brother*

Title | How Interesting | Author
---|---|---
**[Smashing The Stack For Fun And Profit](http://www-inst.eecs.berkeley.edu/~cs161/fa08/papers/stack_smashing.pdf)** | :two_hearts: | *by Aleph One*
**[Violent Python - A Cookbook for Hackers, FA, PT and SE](https://repo.zenk-security.com/Programmation/Violent%20Python%20-%20A%20Cookbook%20for%20Hackers,%20Forensic%20Analysts,%20Penetration%20Testers%20and%20Security%20Enginners.pdf)** | :two_heats: | *by TJ O'Connor*
**[Breaking the x86 Instruction Set](https://www.youtube.com/watch?v=KrksBdWcZgQ)** | :star::star::star::star::star: | *[by Domas](https://github.com/xoreaxeaxeax)*
**[Buffer Overflow, Race Condition, Input Validation, Format String](http://www.cis.syr.edu/~wedu/Teaching/cis643/schedule.html)** | :star::star::star::star: | *by Wenliang (Kevin) Du*
**[Meltdown](https://meltdownattack.com/meltdown.pdf)** | :star::star::star::star: | *by Lipp, Schwarz, Gruss, Prescher, Haas, Mangard, Kocher, Genkin, Yarom, and Hamburg*
**[Basic Linux Privilege Esclation](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/)** | :star::star::star: | *by g0tmi1k* 
**[Network Protocol Fuzzing and Buffer Overflow](https://blog.own.sh/introduction-to-network-protocol-fuzzing-buffer-overflow-exploitation/) | :star::star::star::star: | *by Joey Lane*
**[Secure Programming HOWTO](https://dwheeler.com/secure-programs/Secure-Programs-HOWTO.pdf)** | :star::star::star: | *by David A. Wheeler*
**[Padding the struct](https://www.nccgroup.trust/us/about-us/newsroom-and-events/blog/2019/october/padding-the-struct-how-a-compiler-optimization-can-disclose-stack-memory/)** | :star::star::star: | by *NCC Group*
**[Efficiently Generating Python Hash Collisions](https://www.leeholmes.com/blog/2019/07/23/efficiently-generating-python-hash-collisions/)** | :star::star:
**[Stochastic Process Wikipedia](https://en.wikipedia.org/wiki/Stochastic_process)** | :star::star:
**[Gimli: a cross-platform permutation](https://eprint.iacr.org/2017/630.pdf)** | :star::star:
**[LiveOverflow](https://www.youtube.com/channel/UClcE-kVhqyiHCcjYwcpfj9w)** | :star::star:

<details>

<summary>*p/q2-q4*</summary>

**[Forum cracks the vintage passwords of Ken Thompson and other Unix pioneers](https://arstechnica.com/information-technology/2019/10/forum-cracks-the-vintage-passwords-of-ken-thompson-and-other-unix-pioneers/)**  
**[Most Common Chess Openings](https://www.thesprucecrafts.com/most-common-chess-openings-611517)**  
**[Kasparov Miniature and Tactics/Endgames | Kids' Class - GM Varuzhan Akobian](https://www.youtube.com/watch?v=_B39II74Pkc)**  

</details>

> **When in doubt, use bruteforce** ― *[Ken Thompson](https://en.wikipedia.org/wiki/Ken_Thompson)*


---
## 0x05 ~ Computer Graphics

> **Programming is not a zero-sum game. Teaching something to a fellow programmer doesn't take it away from you. I'm happy to share what I can, because I'm in it for the love of programming** ― *[John Carmack](https://en.wikipedia.org/wiki/John_Carmack)*

Title | How Interesting | Author
---|---|---
**[SDL2 Tutorial](https://lazyfoo.net/tutorials/SDL/01_hello_SDL/linux/index.php)** | :two_hearts: | *by mysterious Lazyfoo*
**[The Book of Shaders](https://thebookofshaders.com/01/)** | :two_hearts: | *by Patricio Gonzalez Vivo & Jen Lowe*
**[Fast Inverse Square Root](https://en.wikipedia.org/wiki/Fast_inverse_square_root)** | :two_hearts: | attributed to John Carmack (Quake III)
**[Game Engine Architecture](http://ce.eng.usc.ac.ir/files/1511334027376.pdf)** | :star::star::star::star::star: | *by Jason Gregory*
**[Introduction to Computer Graphics](https://www.youtube.com/watch?v=t7g2oaNs-c8&list=PLQ3UicqQtfNuKZjdA3fY1_X9gXn13JLlW&index=1)** | :star::star::star::star::star: | *by Justin Solomon*
**[RayCasting Tutorial + Source Code](https://lodev.org/cgtutor/raycasting.html)** | :star::star::star::star::star: | *by Lodev*
**[Shaders Programming](https://www.hiteshsahu.com/blogs)** | :star::star::star::star: | *by [Hitesh Sahu](https://github.com/hiteshsahu)*
**[Coding Minecraft in two days](https://youtu.be/4O0_-1NaWnY)** *(source code)[https://github.com/jdah/minecraft-weekend]* | :star::star::star::star::star: | *by [Jdah](https://github.com/jdah)*
**|[Moving Frostbite to Physically Based Rendering 3.0](https://seblagarde.files.wordpress.com/2015/07/course_notes_moving_frostbite_to_pbr_v32.pdf)** | :star::star::star::star: | *by Sebastien Lagarde and Charles de Rousiers*
**[3d Fractal Flame Wisps](https://tigerprints.clemson.edu/cgi/viewcontent.cgi?article=2704&context=all_theses)** | :star::star::star: | *by [Yujie Shu](https://www.semanticscholar.org/author/Yujie-Shu/11523322)*
**[Geometry Caching Optimizations in Halo 5](https://www.youtube.com/watch?v=uYAjUOlEgwI)** | :star::star::star: | *by Zabir Hoque and Ben Laidlaw*
**[Physically-Based Shading at Disney](https://disney-animation.s3.amazonaws.com/library/s2012_pbs_disney_brdf_notes_v2.pdf)** | :star::star::star: | *by Brent Burley, Walt Disney Animation Studios*
**[Light and Shadows in Graphics](https://www.youtube.com/watch?v=LUjXAoP5GG0)** | :star::star: | *by Tom Scott*
**[Screen Space Ambient Occlusion Tutorial](http://john-chapman-graphics.blogspot.com/2013/01/ssao-tutorial.html)** | :star::star: | *by Tom Scott*
**[Exponentiation by Squaring](https://en.wikipedia.org/wiki/Exponentiation_by_squaring)**  | :star: | *Wikipedia*


---
## 0x06 ~ Computer Vision & AI

> **It is through science that we prove, but through intuition that we discover** ― *[Henri Poincaré](https://en.wikipedia.org/wiki/Henri_Poincar%C3%A9)*

Title | How Interesting | Author
---|---|---
**[OpenCV Tutorial](https://docs.opencv.org/2.4/opencv_tutorials.pdf)** | :star::star::star:


---
## 0x07 ~ C++ Optimization

> **C++ is a horrible language. It's made more horrible by the fact that a lot of substandard programmers use it, to the point where it's much much easier to generate total and utter crap with it** ― *Linus Torvalds 2007*

Title | How Interesting | Author
---|---|---
**[Optimizing software in C++](https://www.agner.org/optimize/optimizing_cpp.pdf)** | :two_hearts: | *by Agner Fog*
**[Intel Intrinsics Guide](https://software.intel.com/sites/landingpage/IntrinsicsGuide/)** *[What is it](https://en.wikipedia.org/wiki/Intrinsic_function)* | :two_hearts: | *Intel*
**[Software Performance and Indexing](https://lemire.me/en/#publications)** | :two_hearts: | *by [Daniel Lemire](https://github.com/lemire)*
**["Low Latency C++ for Fun and Profit"](https://www.youtube.com/watch?v=BxfT9fiUsZ4)** | :star::star::star::star: | *by Carl Cook*
**[Why I Created C++](https://www.youtube.com/watch?v=JBjjnqG0BP8)** | :star::star::star: | *Bjarne Stroustrup*
**[CppCon 2018 “High-Radix Concurrent C++”](https://www.youtube.com/watch?v=75LcDvlEIYw)** | :star::star::star: | *Olivier Giroux*
**[C++ Features](https://github.com/AnthonyCalandra/modern-cpp-features)**| :star::star::star: | *by Anthony Calandra*


---
## 0x08 ~ Assembly Optimization

> **People say that you should not micro-optimize. But if what you love is micro-optimization... that's what you should do** ― *Linus Torvalds*

Title | How Interesting | Author
---|---|---
**[Intel® 64 and IA-32 architectures software developer’s manual](https://software.intel.com/en-us/download/intel-64-and-ia-32-architectures-sdm-combined-volumes-1-2a-2b-2c-2d-3a-3b-3c-3d-and-4)** | :two_hearts: | *Intel*
**[Optimizing subroutines in assembly x86 language](https://www.agner.org/optimize/optimizing_assembly.pdf)** | :two_hearts: | *by Agner Fog*
**[Online Compiler Explorer](https://godbolt.org/)** | :star::star::star::star::star: | *by Godbolt*
**[Online Assembler and Disassembler](https://defuse.ca/online-x86-assembler.htm#disassembly)** | :star::star::star::star: | *by [Taylor Hornby](https://github.com/defuse)*
**[A Guide to inline assembly for C and C++](https://www.ibm.com/developerworks/rational/library/inline-assembly-c-cpp-guide/)** | :star::star::star::star: | *by Salma Elshatanoufy and William O'Farrell*
**[Tips for Golfing in x86/x64 Bytecode](https://codegolf.stackexchange.com/questions/132981/tips-for-golfing-in-x86-x64-machine-code)** | :star::star::star: | *by StackExchange*
**[The Art of Assembly Language](http://www.staroceans.org/kernel-and-driver/The.Art.of.Assembly.Language.2nd.Edition.pdf)** | :star::star: | *by Randal Hyde*
**[GDB Tutorial](https://www.cs.cmu.edu/~gilpin/tutorial/)** | :star::star: | *by Andrew Gilpin*
**[Examining Arm VS x86 Memory Models with Rust](https://www.nickwilcox.com/blog/arm_vs_x86_memory_model/)** | :two_hearts: | *by [Nick Wilcox](https://www.nickwilcox.com/blog/)*

---
## 0x09 ~ Functional Programing *[by Leonard Marquez](https://github.com/keuhdall)*

> **A monad is just a monoid in the category of endofunctors, what's the problem?** ― *James Iry*

Title | How Interesting | Author
---|---|---
**[Learn You a Haskell for Great Good!](http://learnyouahaskell.com/chapters)** | :two_hearts: | *by Miran Lipovača*
**[Functors, Applicatives, And Monads In Pictures](http://adit.io/posts/2013-04-17-functors,_applicatives,_and_monads_in_pictures.html)** | :two_hearts: | *by Aditya Bhargava*
**[Category Theory course by Bartosz Milewski](https://www.youtube.com/watch?v=I8LbkfSSR58&list=PLbgaMIhjbmEnaH_LTkxLI7FMa2HsnawM_)** | :star::star::star::star::star: | *by Bartosz Milewski*
**[Wise Man's Haskell](https://andre.tips/wmh/)** | :star::star::star::star: | *by Andre Popovitch*
**[Real World Haskell](http://book.realworldhaskell.org/read/)** | :star::star::star: | *by Bryan O'Sullivan*
**[Martin Odersky's Scala course](https://www.coursera.org/learn/progfun1)** | :star::star: | *by Martin Odersky*


---
## 0x0A ~ Computer Architecture

> **And luckily right at that moment my wife went on a 3 weeks vacation to take my one year old (roughly) to visit my in-laws who were in California, this period long, 1 week, 1 week, 1 week... and we had Unix** ― *[Ken Thompson](https://en.wikipedia.org/wiki/Ken_Thompson), [VCF East 2019](https://www.youtube.com/watch?v=EY6q5dv_B-o&t=23m11s)*

Title | How Interesting | Author
---|---|---
**[Digital Design and Computer Architecture](http://www.csit-sun.pub.ro/courses/cn2/Digital_design_book/Digital%20Design%20and%20Computer%20Architecture.pdf)** | :star::star::star::star: | **  
**[X86 vs ARM](https://fossbytes.com/cpu-comparison-x86-arm-cpu-benchmark/amp/)** | :star::star::star: | *Fossbytes*  
**[MIPS Processors](https://stackoverflow.com/questions/2635086/mips-processors-are-they-still-in-use-which-other-architecture-should-i-learn)** | :star::star: | *Stack Overflow*  


---
## 0x0B ~ Misc

> **...and Unix is an example of a proper name, and, is not likely to be in the dictionary ever** ― *[Brian W. Kernighan](https://en.wikipedia.org/wiki/Brian_Kernighan) (1982)*

Title | How Interesting | Author
---|---|---
**[AVIF for Next Generation Image Coding](https://netflixtechblog.com/avif-for-next-generation-image-coding-b1d75675fe4)** | :star::star::star::star::star: | *By Aditya Mavlankar, Jan De Cock, Cyril Concolato, Kyle Swanson, Anush Moorthy and Anne Aaron*
**[UNIX AT&T Archives film from 1982](https://www.youtube.com/watch?v=XvDZLjaCJuw)** | :two_hearts: | *by Bell Laboratories*
**[A Super Mario 64 decompilation](https://github.com/agavrel/sm64)** | :star::star::star::star::star: | *by a bunch of clever folks*
**[The Go Programming Language](https://www.gopl.io/ch1.pdf)** | :star::star::star::star::star: |  *by Alan A. A. Donovan and Brian W. Kernighan*
**[Vim 101 Quick Movement](https://medium.com/usevim/vim-101-quick-movement-c12889e759e0)** | :star::star::star::star: | *Alex R. Young*
**[Software Version Control Visualization](https://github.com/acaudwell/Gource)** : :star::star::star::star: | *by [Andrew Caudwell](https://github.com/acaudwell)*
**[Math for Game Programmers: Dark Secrets of the RNG](https://www.youtube.com/watch?v=J5qnnxFoBss)** | :star::star::star: | *by Shay Pierce*
**[Clean Code](https://www.investigatii.md/uploads/resurse/Clean_Code.pdf)** | :star::star::star: | *by Robert C. Martin*
**[Why Java Suck](https://tech.jonathangardner.net/wiki/Why_Java_Sucks)** | :star: | *by Jonathan Gardner*
**[XOR Linked List – A Memory Efficient Doubly Linked List](http://en.wikipedia.org/wiki/XOR_linked_list)** | :star: | *Wikipedia* 
**[XOR Linked List – C Implementation](https://stackoverflow.com/questions/3531972/c-code-for-xor-linked-list)** | :star: | *StackOverFlow*


---
## 0x0C ~ Mobile App Development

Title | How Interesting | Author
---|---|---
**[Framework: Flutter Hello World](https://flutter.dev/docs/get-started/codelab)** | :two_hearts: | *by Flutter Team (Google)*
**[Images: About Webp](https://www.smashingmagazine.com/2019/10/speed-up-your-website-webp)** | :star::star: | *Suzanne Scacca*

---
## 0x0D ~ Science-Fiction Masterpieces

> **To succeed, planning alone is insufficient. One must improvise as well** ― *Isaac Asimov, Foundation*

Format | Title | How Interesting | Author
---|---|---|---
Book | **[The Foundation](https://en.wikipedia.org/wiki/Foundation_series)** | :two_hearts: | *by [Isaac Asimov](https://en.m.wikipedia.org/wiki/Isaac_Asimov)*
Book | **[The Hitchhiker's Guide to the Galaxy](https://www.goodreads.com/book/show/841628.The_Hitchhiker_s_Guide_to_the_Galaxy)** | :two_hearts: | *by [Douglas Adams](https://en.m.wikipedia.org/wiki/Douglas_Adams)*
AudioBook | **[The Hitchhiker's Guide to the Galaxy](https://www.youtube.com/watch?v=dPbr0v_V-cI&list=PLYT7LhCzuTTdtIGcDOP-PPMxAWYo3qF5r&index=3&t=3167s)** | :two_hearts: | *by Douglas Adams and read by Stephen Moore*
Movie | **[Ready Player One](https://en.wikipedia.org/wiki/Ready_Player_One_(film))** | :two_hearts: | by *[Steven Spielberg](https://en.wikipedia.org/wiki/Steven_Spielberg)*
Movie | **[Matrix](https://en.wikipedia.org/wiki/The_Matrix)** | :two_hearts: | *by the Wachowskis*
Book | **[Hyperion](https://en.m.wikipedia.org/wiki/Hyperion_(Simmons_novel))** | :star::star::star::star: | *by [Dan Simmons](https://en.m.wikipedia.org/wiki/Dan_Simmons)*
Movie | **[War Games](https://en.wikipedia.org/wiki/WarGames)** | :star::star::star: | *directed by John Badham*
Book | **[Elon Musk Biography](https://www.goodreads.com/book/show/25541028-elon-musk)** | :star::star::star::star::star: | *by Ashlee Vance*


---
# Tutorials

<a href="https://www.youtube.com/watch?v=Jen46qkZVNI&t=30s" target="_blank"><img src="http://img.youtube.com/vi/Jen46qkZVNI/0.jpg"
alt="Boxer's Perfect Rush SCV" width="240" height="180" border="10" /></a>

---
## 0x00 ~ Optimization - Aiming for the lowest latency

When you want to aim for lowest latency - *i.e maximum speed* - there are many things that will improve your program to create a better binary: Optimization flag, parallelization, vectorization and carefully crafting your algorithm.


### Optimization flags

Especially for Computer Graphics projects, you will want to turn on these optimization flags, [listed on gcc website](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html).

> Without any optimization option, the compiler’s goal is to reduce the cost of compilation and to make debugging produce the expected results. Statements are independent: if you stop the program with a breakpoint between statements, you can then assign a new value to any variable or change the program counter to any other statement in the function and get exactly the results you expect from the source code.
Turning on optimization flags makes the compiler attempt to improve the performance and/or code size at the expense of compilation time and possibly the ability to debug the program.

**To use it simply compile the program with:**
```
gcc -O2 a.c
```
NB: It is the letter 'o' and not a zero. You may also use O3.


### Multithreading and Parallelization

The historical (and current) approach is to add more power via [multithreading](https://en.wikipedia.org/wiki/Multithreading_(computer_architecture)), [multiprocessing](https://en.wikipedia.org/wiki/Multiprocessing), [Grid Computing](https://en.wikipedia.org/wiki/Grid_computing) or even [Cloud Computing](https://en.wikipedia.org/wiki/Cloud_computing). Two libraries exist for this use: [OpenMP](https://www.openmp.org/wp-content/uploads/openmp-examples-4.5.0.pdf) and [pthread](http://man7.org/linux/man-pages/man7/pthreads.7.html), you will have to compile respectively with:
```
gcc -fopenmp -O3 a.c
```
and:
```
gcc -pthread -O3 a.c
```


### [Vectorization](https://en.wikipedia.org/wiki/Streaming_SIMD_Extensions)

> Modern graphics processing units (GPUs) are often wide SIMD implementations, capable of branches, loads, and stores on 128 or 256 bits at a time.
Intel's latest AVX-512 SIMD instructions now process 512 bits of data at once.

As a double is 64 bits - *i.e 8 bytes or octets* - **instead of iterating overs value 1 by 1, you will be able to compute up to 8 double at the time** - *i.e 512 / 64* - if your computer support it (but most likely, as of 2020, your computer will only handle 256 bits register).

**Vectorization the most efficient way to quickly gain performance gains without the overhead of threads' initialization**.

**Demonstration: Getting Min and Max value from a float array**
```c
/* Vectorization example by agavrel */
 <stdio.h>  // printf
 <stdlib.h> // rand()
 <time.h>   // time
 <xmmintrin.h>  // 128 bits register _m128

float m128_max_float(__m128 src) {
    __m128 n[4];

	// a) n[0] = src >> 64                                  So lets say src is composed of floats a b c d, it becomes 0 0 a b
    n[0] = _mm_shuffle_ps(src, src, _MM_SHUFFLE(0,0,3,2));
	// b) n[1] = {max(a,0), max(b,0) max(a,c) max(b,d)}     NB: actually we don't care about the two highest float at this point, I will call them 'x': {x, x max(a,c) max(b,d)}
    n[1] = _mm_max_ps(src, n[0]);                             
	// c) n[2] = n[1] >> 32                                 So n2 become {0 x x max(a,c)}
    n[2] = _mm_shuffle_ps(n[1], n[1], _MM_SHUFFLE(0,0,0,1));
	// d) n[3] = {x x x max(max(a,c), max(b,d))}
    n[3] = _mm_max_ps(n[1], n[2]);                            

    return _mm_cvtss_f32(n[3]);   // d) Hence max(a,b,c,d), stored in the lowest 32 bits of n[3], is loaded into a float that we return. We don't care about the other bits
}

float m128_min_float(__m128 src) {
    __m128 n[4];

    n[0] = _mm_shuffle_ps(src, src, _MM_SHUFFLE(0,0,3,2));
    n[1] = _mm_min_ps(src, n[0]);
    n[2] = _mm_shuffle_ps(n[1], n[1], _MM_SHUFFLE(0,0,0,1));
    n[3] = _mm_min_ps(n[1], n[2]);

    return _mm_cvtss_f32(n[3]);
}

 SIZE  1000000000L // 1 billion. Yes.

void  get_min_max(long i, float array[i]) {
  __m128 max;
  __m128 min;
  
  max = _mm_loadu_ps(array); // will load first 4 float into max
  min = _mm_loadu_ps(array); // will load first 4 float into min
  while ((i -= 4L))
  {
    __m128 tmp = _mm_loadu_ps(array + i);
    max = _mm_max_ps(max, tmp);
    min = _mm_min_ps(min, tmp);
  }

  printf("Max value: %f\t Min value: %f\n", m128_max_float(max), m128_min_float(min));
}

void  get_min_max_like_bocalian(long size, float array[size]) {
  float max;
  float min;
  int i;

  max = array[0];
  min = array[0];
  i = 1L;
  while (i < size)
  {
    float tmp = array[i++];
    max = tmp < max ? max : tmp;
    min = tmp > min ? min : tmp;
  }

  printf("Max value: %f\t Min value: %f\n", max, min);
}

int main()
{
  long i;
  float *data;
  clock_t time;

  srand(time(NULL));  // seed
  data = (float *)malloc(SIZE * sizeof(float));
  i = -1L;
  while (++i < SIZE) {
    data[i] = (float)rand() / (float)(RAND_MAX) * 1000.0f;
   /* printf("%.02f\t\t", data[i]);     // I commented these lines because it slows considerably the program.
    if (!(i & 15))
      printf("\n");*/
  }

  time = clock();
  get_min_max(SIZE, data);
  time = clock() - time;
  double elapsed_time = ((double)time) / CLOCKS_PER_SEC;
  printf("Executed in %f seconds\n", elapsed_time);

  time = clock();
  get_min_max_like_bocalian(SIZE, data);
  time = clock() - time;
  elapsed_time = ((double)time) / CLOCKS_PER_SEC;
  printf("Executed in %f seconds\n", elapsed_time); 

  return 0;
}
```

And compile with:
```
gcc vectorization.c -O3  && ./a.out 
```

You will notice that the vectorized approach will be about 3 times faster (NB: For this specific example). If I was using mm256 or mm512 registers, the vectorized program would be even faster by a factor of 2 and 4 respectively.

*Now that you realize the performance boost, how about using what you just learn for your RayTracing project?*


### Combining Optimization Flags, Parallelization and Vectorization

*a) **You can take a look at [this very interesting project](https://github.com/expr-fi/fastlwc/blob/master/fastlwc-mt.c)** which aim to show how fast wc can get using the various tools C has to offer to optimize speed. After downloading the file, you will also need to download the header: [simd.h](https://github.com/expr-fi/fastlwc/blob/master/simd.h), which make use of [Intel intrinsic](https://software.intel.com/sites/landingpage/IntrinsicsGuide/).*  

*b) Compile it with the flags:*
```
gcc fastlwc-mt.c -fopenmp -O3
```

*c) Create a random file:*
```
dd if=/dev/urandom of=sample.txt bs=64M count=16 iflag=fullblock
```

*d) Compare wc with the new binary with:*
```
time ./a.out sample.txt \
&& time wc sample.txt
```

### The Right Algorithm

**The right algorithm is usually the corner stone of an efficient program.**

*How about solving this [algorithm problem](https://github.com/agavrel/Nailing-the-Coding-Interview/tree/master/math/the_dancer):*

```c
int32_t dancer_position(uint32_t time_elapsed) { ;}
```


### Exploring Compiler's Assembly Output

Let's take and example with the brilliant [UTF-8](https://en.wikipedia.org/wiki/UTF-8) implementation, especially at how continuation bytes are designed: 

> continuation bytes start with 10 while single bytes start with 0 and longer lead bytes start with 11

Let's say that you have to write a function that determines if the byte is a continuation one, you can think of many ways that would end with the same result. But they will have a different output in their assembly.


You can retain the two first bits wwith ```& 0b11000000``` and then make sure that the first one is set and the second one is not with ```== 0b10000000``` :
```c
 <stdbool.h>

bool is_utf8_continuation_byte(char c) {
	return ((c & 0b11000000) == 0b10000000);  
}
```

Which corresponds to the following compiler output with ```gcc x86-64 9.3 with -O3 optimization flag``` :
```asm
and     edi, 192
cmp     edi, 128
sete    al
```


Another way would be to shift the bits to the right:
```c
bool is_utf8_continuation_byte(char c) {
	return (!((((unsigned char)c >> 6) ^ 0b10)));
}
```
Here I cast c into unsigned in order to be able to shift the MSB to the right with ```(unsigned char)c```  
Then I shift it 6 times to the right with ``` >> 6``` because we do not care about the content of the 6 lowest bits.  
Finally I xor the result by 0b10 with ```^ 0b10```, which corresponds to specification of a continuation byte as quoted before.
As a number xored by itself gives 0, I use the exclamation mark ! to reverse the result from 0 to 1. (Else we would have to rename the function ```is_not_utf8_continuation_byte```)


It is not producing the following output that you could imagine:
```asm
sar     edi, 6
xor     edi, 2
not		edi,
```

But the optimized version:
```asm
movzx   edi, dil
sar     edi, 6
cmp     edi, 2
sete    al
```
It's even less efficient.


Finally since the valid range 0b10111111 to 0b10000000 (corresponding to -128 to -65, both included), you can add 0b01000000 and check if the byte is negative:
```c
bool is_utf8_continuation_byte(char c) {
	return (c + 0b01000000 < 0);
}
```

In other word you compare to -64 and check if it is lower:
```asm
cmp     dil, -64
setl    al
```

**To see the assembly output you can use the following command which will generate an assembly file with intel syntax (more readable than AT&T):**
```
gcc -O3 -S -masm=intel a.c && cat a.s
```

*or use the excellent [compiler explorer from godbolt](https://godbolt.org/)*

**I hope that you liked this demonstration that shows that functions with same behaviors can produce different assembly output, hence being more or less efficient. If you want to build your program to be the most efficient you should explore the assembly code of functions in critical loops**


---
## 0x01 ~ Computer Graphics - Using [SDL2](https://www.libsdl.org/index.php) to create Fractal

### Using SDL2 to create Computer Graphics
You can follow tutorials to create a simple program with SDL on [Lazyfoo's website](https://lazyfoo.net/tutorials/SDL/01_hello_SDL/linux/index.php) or on SDL2 official website.

You will also have to install SDL2:
```
brew install sdl2
```

With SDL2 you have to first ```init_sdl``` - *see function below*. Then you will keep the user entertained with a loop ```while (42)``` that can only be escaped by clicking on the the close button or pressing escape. While the loop is active, user's actions will be recorded thanks to ```SDL_PollEvent```. You then draw pixel by using ```SDL_RenderDrawPoint``` and you refresh image with ```SDL_RenderPresent```.

### Example with a Barnsley Fern Fractal

[Michael Barnsley](https://en.wikipedia.org/wiki/Michael_Barnsley) was a British mathematician who coined a fractal algorithm to represent a fern.  

![Barnsley Fern](https://raw.githubusercontent.com/agavrel/42_CheatSheet/master/img/BarnsleyFern.png)

The algorithm is explained in detail on [wikipedia](https://en.wikipedia.org/wiki/Barnsley_fern)  

Find below the code for the whole program, compile it with :
```
gcc barnsley.c -lSDL2 -O3
```

You will need about 10 000 iterations of n to draw the shape. On each keypress you will increase the number of iterations by 400.
```c
 message "\033[1;31mRequire SDL2\033[0m, \033[1;92mbrew install sdl2\033[0m and compile with \033[1;5;36mgcc barnsley.c -lSDL2\033[0m  && ./a.out  " __FILE__ "..."
// gcc main.c -lSDL2 -O3 -Wall -Werror -Wextra --pedantic&& ./a.out
 <stdio.h>
 <SDL2/SDL.h>
 <stdbool.h>

 WINDOW_WIDTH	600
	WINDOW_HEIGHT	800

typedef struct		s_cnb
{
	double			real;
	double			imag;
}					t_cnb;

typedef struct		s_pixel
{
	int				x;
	int				y;
}					t_pixel;

void	barnsley(SDL_Renderer *renderer, t_cnb *c) {
	float	rng;
	t_pixel	i;
	static const float probability[3] = {0.01f, 0.08f, 0.15f};
	long n = 400;

	while (n--) {
		rng = ((float)rand() / (float)RAND_MAX);
		if (rng <= probability[0]) {
			c->real = 0;
			c->imag *= 0.16f;
		}
		else if (rng <= probability[1]){
			c->real = -0.15f * c->real + 0.28f * c->imag;
			c->imag = 0.26f * c->real + 0.24f * c->imag + 0.44f;
		}
		else if (rng <= probability[2]) {
			c->real = 0.2f * c->real + -0.26f * c->imag;
			c->imag = 0.23f * c->real + 0.22f * c->imag + 1.6f;
		}
		else {
			c->real = 0.85f * c->real + 0.04f * c->imag;
			c->imag = -0.04f * c->real + 0.85f * c->imag + 1.6f;
		}
		i.x = (c->real + 3) * 70;
		i.y = WINDOW_HEIGHT - c->imag * 70;
    	SDL_RenderDrawPoint(renderer, i.x, i.y);
	}
}

bool	error_sdl(char *error_msg) {
	printf( "%s! SDL_Error: %s\n", error_msg, SDL_GetError() );
	return false;
}

bool	init_sdl(SDL_Window **window, SDL_Renderer **renderer) {
	if (SDL_Init(SDL_INIT_VIDEO) < 0)
		return (error_sdl("SDL could not initialize!"));
	SDL_CreateWindowAndRenderer(WINDOW_WIDTH, WINDOW_HEIGHT, 0, window, renderer);
	if (*window == NULL)
		return (error_sdl("Window could not be created!"));
	SDL_SetRenderDrawColor(*renderer, 0, 0, 0, 0);
	SDL_RenderClear(*renderer);
    SDL_SetRenderDrawColor(*renderer, 0xbf, 0xff, 0, 0);

	return true;
}

int		main(void) {
    SDL_Event event;
    SDL_Window *window;
	SDL_Renderer *renderer;
	t_cnb c;
	
	if (!(init_sdl(&window, &renderer)))
		return 1;

	c = (t_cnb) {.real = 0, .imag = 0}; // PS: legal for Norminette
    while (42) {
		if (SDL_PollEvent(&event)) {
			if (event.type == SDL_QUIT)
				break ;
			else if (event.type == SDL_KEYDOWN) {
				if (event.key.keysym.sym == SDLK_ESCAPE)
					break ;
				barnsley(renderer, &c);
				SDL_RenderPresent(renderer);
			}
		}
    }
    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(window);
    SDL_Quit();
    return EXIT_SUCCESS;
}
```

---
## 0x02 ~ Hacking - Buffer Overflow

### Introduction

Let's take a look at the function strcpy, shall we? Type ```man strcpy``` in your terminal:

> *The  strcpy() function copies the string pointed to by src, including the terminating null byte ('\0'), to the buffer pointed to by dest.  The strings may not overlap, and the destination string dest must be large enough to receive the copy.  Beware of buffer overruns!  **(See BUGS.)***

**NB: Usage of brackets for what is considered as one of the most critical security flaw in the world**

> ***BUGS:**  
If  the  destination  string of a strcpy() is not large enough, then anything might happen ― **NB: Undefined Behavior**.  Overflowing fixed-length string buffers is a favorite cracker technique for taking complete control of the machine.  Any time a program reads or copies data into a buffer, the program first needs to  check  that  there's  enough  space. This may be unnecessary if you can show that overflow is impossible, but be careful: programs can get changed over time, in ways that may make the impossible possible.*

```c
 <string.h>
 <stdio.h>

int main(void) {
	char s[11];

	strcpy(s, "hello world");
	puts(s);	

	return 0;
}
```

While this look okay if you count each letter, if you happen to read again the definition of strcpy (just above) you will notice: 
> ***including the terminating null byte ('\0')***

So you are trying to copy 12 characters in fact, into a 11 characters buffer. You will get the nice message:

```bash
In function ‘main’:
warning: ‘__builtin_memcpy’ writing 12 bytes into a region of size 11 overflows the destination [-Wstringop-overflow=]
strcpy(s, "hello world");
```

In fact all functions that you will find in [```#include <banned.h>```](https://github.com/git/git/blob/master/banned.h) represent potential security risks and should be avoided as much as possible.

### Buffer overflow to hijack a password

```c
 <stdio.h>
 <string.h> // for strcmp, compare two strings and return 0 if they are equal

char    *strcpy_until(char *dst, char *src, char until)
{
	int i = -1;

	while (src[++i] != until)
		dst[i] = src[i];
    
	return (dst);
}

int     main(int ac, char **av) {
    int n = 5;
    char password[] = "sarang hae"; // we don't know
    char buffer[4] = "kkk";

    if (ac != 2)
        return 1;
    printf("n equals %d\n", n);
    printf("you would have never guessed, password was '%s'\n\n", password);
    char *s = &buffer[3];
    char shellcode[] = "\x42\x61\x67\x61\x76\x72\x65\x6c\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x2a\x00\x00\x01";
    strcpy_until(s, shellcode, '\x01');
    printf("n equals '%d'\n", n);
    printf("password now equals: '%s'\n", password);

    if (!strcmp(password, av[1])) {
        printf("\nSuccessfully hacked user with password \e[1;5;92m%s\e[0m\n", password);        
    }
    return 0;
}
```
*Would you have guessed the password?*  

Some explanations:
* ```strcpy_until``` will copy until a specific character, hence allowing to bypass the NULL that terminates the string
* ```char shellcode[]``` can be used to, instead of just replacing value at memory addresses, execute the value that have been replaced. See next below...


### Shellcode Execution to get root access

> **When something is important enough, you do it even if the odds are not in your favor** ― *Elon Musk*

You will now have to compile with:
```
gcc -fno-stack-protector -z execstack a.c
```

* ```-fno-stack-protector a.c``` is to disable the [Stack-Guard mechanism](https://en.wikipedia.org/wiki/Buffer_overflow_protection)
* Compiler make prevent stack from being executable and ```-z execstack``` reverse that protection.


Last you will also **temporarily** disable randomize va space with:
```
sudo sysctl -w kernel.randomize_va_space=0
```
NB: You can use safer method ```setarch `uname -m` -R /bin/bash``` which is [more safe](https://askubuntu.com/questions/318315/how-can-i-temporarily-disable-aslr-address-space-layout-randomization)

Once done with experiments do not forget to set back randomize back to normal:
```
sysctl -a --pattern "randomize" && \
sudo sysctl -w kernel.randomize_va_space=2
```

{WIP}


---
## 0x03 ~ Chess Bitboard

Often you will have programs where you want to represent data the following way:

```c
int	map[8][8];
```

While it looks like it is convenient, you can make it convenient using the right functions. But if you are using an integer to tell if the board is filled with pieces, you are wasting a lot of memory.

```c++
 <iostream>
 <map>

using namespace std;

void    print_binary(uint64_t n)
{
    uint64_t mask = 0;
    for (mask = ~mask ^ (~mask >> 1); mask != 0; mask >>= 1)
        putchar('0' + !!(n & mask));
    putchar('\n');
}

void    fill_board(uint64_t board[12], uint64_t *used_cells)
{
    const uint64_t initial_pos[6] = {   0b0000000011111111000000000000000000000000000000001111111100000000, // most right is a1, most left is h8
                                        0b1000000100000000000000000000000000000000000000000000000010000001,
                                        0b0100001000000000000000000000000000000000000000000000000001000010,
                                        0b0010010000000000000000000000000000000000000000000000000000100100,
                                        0b0001000000000000000000000000000000000000000000000000000000001000,
                                        0b0000100000000000000000000000000000000000000000000000000000010000
    };
    const uint64_t  color_mask[2] = {   0b0000000000000000000000000000000011111111111111111111111111111111,
                                        0b1111111111111111111111111111111100000000000000000000000000000000
    };

	*used_cells = 0;
    for (int i = 0; i < 12; i++) {
        board[i] = (initial_pos[i >> 1]) & (color_mask[i & 1]);
		*used_cells |= board[i];
	}
}

void    display_board(uint64_t board[12])
{
    for (int i = 0; i < 12; i++)
        print_binary(board[i]);
}

std::map<string, uint64_t>  fill_move() {
    std::map<string, uint64_t>  move;

    for (char r = '1'; r <= '8'; r++) {
        for (char c = 'a'; c <= 'h'; c++) {
            char cell[3] = {c, r, '\0'};
            move[cell] = (1UL << (8 * (c - 'a'))) << (r - '1');
        }
    }
    return move;
}

enum PIECE {
    __PAWN_W = 0,
    __PAWN_B,
    __ROOK_W,
    __ROOK_B,
    KNIGHT_W,
    KNIGHT_B,
    BISHOP_W,
    BISHOP_B,
    _QUEEN_W,
    _QUEEN_B,
    __KING_W,
    __KING_B = 11
};


int main()
{    
    uint64_t    board[12];
	uint64_t	used_cells;
    std::map<string, uint64_t> move = fill_move();

    fill_board(board, &used_cells);
    display_board(board);
    
    putchar('\n');
    print_binary(board[__PAWN_W]);

    if (board[__PAWN_W] & move["b4"]) // check if exist
        board[__PAWN_W] ^=  ((move["b4"] | move["e4"]));
    
    print_binary(board[__PAWN_W]);
    putchar('\n');

    return 0;
}
```


--- 
# Epilogue

--- 
## 0x00 ~ Wanted Pull Requests

> **If you know how to make software, then you can create big things** ― *Xavier Niel*

*One function related to each 42 project to help students get started*  
*In-depth examples with pointers*  
*Books on system design*  
*Exemple of a Makefile "qui fait le cafe"*


---
## 0x01 ~ Question ? Broken Link ? Wanna contribute ?

> **I think it's very important to have a feedback loop, where you're constantly thinking about what you've done and how you could be doing it better** ― *Elon Musk*

*Raise an issue or even better: submit a pull request*

First fork the repository and clone it locally (you will be forgiven for this kind of git clone)

Make the desired changed to the README.md file

Then open the terminal containing your fork and enter:
```
git checkout -b agavrel
git commit -am "[ADD] Interesting link about C Hash"
git push --set-upstream origin agavrel
```

Go back to internet and you will see that you can submit a pull request.

*I will personally review contributions*


---
## 0x02 ~ Liked it ?
*Show your appreciation by starring the repo, sharing on slack, RT and 'lache un com magueule' skyblog™*

![Kimg Jeong Un applauding](https://raw.githubusercontent.com/agavrel/42_CheatSheet/master/img/kimjeongun_meme.gif)

> 잘했어 동무 계속 [배우자](https://www.youtube.com/watch?v=ukBcC-sK3wQ) ― *Good Job Comrade, let's keep studying*


---
## :musical_score: 0x2A ~ About the Author

**Antonin GAVREL**

*Feel free to reach me on [LinkedIn](https://www.linkedin.com/in/antonin-gavrel-086b2618/)*
