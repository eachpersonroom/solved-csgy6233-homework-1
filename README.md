Download Link: https://assignmentchef.com/product/solved-csgy6233-homework-1
<br>
In this assignment, you’ll start getting familiar with xv6 by writing a couple simple programs that run in the xv6 OS.




As a prerequisite, make sure that you have done the hello demo in Anubis to familiarize yourself with Anubis and xv6




A common theme of the homework assignments is that we’ll start o↵with xv6, and then add something or modify it in some way. This assignment is no exception.




Make sure you can build and run xv6. To build the OS, run make to compile xv6:<sub>            </sub>







$ make




Then, to run it inside of QEMU, you can do:<sub>      </sub>




$ make qemu




QEMU should appear and show the xv6 command prompt, where you can run programs inside xv6. It will look something like:





























































Figure 1: Starting xv6 in QEMU







You can play around with running commands such as ls, cat, etc. by typing them into the QEMU window; for example, this is what it looks like when you run    ls in xv6:







Figure 2: Running ls in xv6













Part 2: Implementing the uniq command <sub> </sub>




For this assignment you will be creating commonly used command line program in Linux called “uniq” but will be implementing this yourself in xv6 to get an idea of how command line programs are written.

uniq is a Unix utility which, when fed a text file, outputs the file with adjacent identical lines collapsed to one. If a filename is provided on the command line (i.e., uniq FILE) then uniq should open it, read, filter out, print without repeated lines in this file, and then close it. If no filename is provided, uniq should read from standard input.




For this assignment you will be running the uniq command on the README.md file included in xv6. Before you begin coding please delete all the text in README file and paste the following lines of text in the README.md file in its place. This is the file and subsequent text you will be running the uniq program on.




<u>Text to copy and paste into xv6 README.md file:</u>




No.  1

No.  2

No.  2

No.  2

<h1><a name="_Toc8418"></a>No.  3</h1>

No.  4

No.  5

No.  6

No.  6 No.  2 no. 2




Now that you have set up your test file you may begin coding by creating a uniq.c file and coding your program there.




Here’s an example of the basic usage of           uniq:




$ cat README.md

<h1><a name="_Toc8419"></a>No.  1</h1>

No.  2

No.  2

No.  2

No.  3

No.  4

No.  5

No.  6

No.  6 No.  2 no. 2




$ uniq README.md

<h1><a name="_Toc8420"></a>No.  1</h1>

No.  2

No.  3

No.  4

No.  5

No.  6

No.  2 no.  2




You should also be able to invoke it without a file, and have it read from standard input. For example, you can use a pipe to direct the output of another xv6 command into       uniq:




$ cat README.md | uniq

<h1><a name="_Toc8421"></a>No.  1</h1>

<h1><a name="_Toc8422"></a>No.  2</h1>

No.  3

No.  4

No.  5

No.  6 No.  2 no.  2










Hints




<ol>

 <li>Many aspects of this are similar to the wc.c program: both can read from standard input if no arguments are passed or read from a file if one is given on the command line. Reading its code will help you if you get stuck.</li>

</ol>




<ol start="2">

 <li>Still confused with uniq’s behavior? Use man uniq for help.</li>

</ol>




<ol start="3">

 <li>The following link should help give you an idea on how to parse command line arguments and fetch them from the main function : <u>https://dev-notes.eu/2018/03/parse-command-line-arguments-in-c/</u></li>

</ol>



























































































Part 3: Extending uniq <sub> </sub>




The traditional UNIX uniq utility can do lots of things, such as:




<ul>

 <li>-c: count and group prefix lines by the number of occurrences</li>

</ul>




<ul>

 <li>-d: only print duplicate lines</li>

</ul>




<ul>

 <li>-i: ignore di↵erences in case when comparing</li>

</ul>




Here, we are going to implement these three behaviors in your version of uniq. The expected output of these commands should be:<sub>              </sub>




$ uniq -c README.md

<a href="#_Toc8417"> 1 No………………. 1 </a>

<a href="#_Toc8418"> 3 No………………. 2 </a>

<a href="#_Toc8419"> 1 No………………. 3 </a>

<a href="#_Toc8420"> 1 No………………. 4 </a>

<a href="#_Toc8421"> 1 No………………. 5 </a>

<a href="#_Toc8422"> 2 No………………. 6 </a>




1 No. 2

1 no. 2




$ uniq -d README.md

No.  2

No. 6




$ uniq -i README.md

No.  1

No.  2

No.  3

No.  4

No.  5

No.  6

No. 2




$ uniq -c -i README.md

1 No. 1

3 No. 2

1 No. 3

1 No. 4

<ul>

 <li>5</li>

 <li>6</li>

</ul>

2 No. 2




Notice that ”No. 2” should be the same as ”no. 2” if uniq is not case-sensitive. Also, -c and -d won’t appear at the same time.





