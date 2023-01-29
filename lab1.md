In this week's lab, we installed Visual Studio Code, remotely connected to the lab computers in the CSE Basement, and tried some commands.

Installing Visual Studio Code
------------------------------

I already had VSCode, but the way to install it is to go to [https://code.visualstudio.com/](https://code.visualstudio.com/). 

<img height="500" alt="image" src="https://user-images.githubusercontent.com/122497388/212572113-dbb30c83-3b09-47d3-b026-d254fc134df3.png">

Clicking the blue button which preselects the version downloadable for your device should automatically install it in a few minutes. After installing, you should be able to open a window that looks like this: 

<img height="500" alt="image" src="https://user-images.githubusercontent.com/122497388/212595060-887151d3-966f-4a75-872d-dd929fee2b55.png">

Remotely Connecting
-------------------

I started off lab by setting up remote connection. First, I opened up the terminal, and typed in `ssh cs15lwi23adv@ieng6.ucsd.edu`. It prompted me for my password, so I typed it in. 

```
genie@Sumadhus-MacBook-Air ~ % ssh cs15lwi23adv@ieng6.ucsd.edu
(cs15lwi23adv@ieng6.ucsd.edu) Password: 
Last login: Sat Jan 28 15:42:57 2023 from 166.198.37.129
Hello cs15lwi23adv, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   12:25:01   16  0.09,  0.08,  0.12
ieng6-202   12:25:01   10  1.01,  1.13,  1.16
ieng6-203   12:25:01   9   4.04,  4.11,  4.13


       *** Network Delay Issue ***
	   2022-01-24 - ???
We're aware of an issue with network delay 
that is causing slowness on the systems. 

ITS is currently troubleshooting the cause
of this issue. Please be patient with the
slowness until the root cause is determined.


 
Sun Jan 29, 2023 12:28pm - Prepping cs15lwi23
[cs15lwi23adv@ieng6-203]:~:35$ pwd
/home/linux/ieng6/cs15lwi23/cs15lwi23adv
```

Trying Some Commands
--------------------

Now that I was logged into the remote server, I tried out some commands.

```
[cs15lwi23adv@ieng6-203]:~:42$ pwd
/home/linux/ieng6/cs15lwi23/cs15lwi23adv
[cs15lwi23adv@ieng6-203]:~:43$ cd ..
[cs15lwi23adv@ieng6-203]:cs15lwi23:44$ pwd
/home/linux/ieng6/cs15lwi23
[cs15lwi23adv@ieng6-203]:cs15lwi23:45$ ls cs15lwi23atj
ls: cannot open directory cs15lwi23atj: Permission denied
[cs15lwi23adv@ieng6-203]:cs15lwi23:46$ cd public
[cs15lwi23adv@ieng6-203]:public:47$ pwd
/home/linux/ieng6/cs15lwi23/public
[cs15lwi23adv@ieng6-202]:public:48$ ls
README.class       bin        broadcast.sh  modulefiles
README.instructor  broadcast  hello.txt
[cs15lwi23adv@ieng6-202]:public:49$ cd hello.txt
-bash: cd: hello.txt: Not a directory
[cs15lwi23adv@ieng6-202]:public:50$ 
```

I first typed in `pwd`, to print out the working directory, which was `/home/linux/ieng6/cs15lwi23/cs15lwi23adv`. 
I wanted to see if I could access another student's directory, so I typed in `cd ..` to access the parent directory of all student directories `/home/linux/ieng6/cs15lwi23`, and then typed in `ls cs15lwi23atj` to list the contents of the student directory `cs15lwi23atj`. This was not possible, as I am not that student, and didn't have permissions to look at their directory. 
Then I typed in `cd public` and `ls` to see what was in the one non-student directory. I saw there was no file named "hello.txt", so I wondered what would occur if I typed in  `cd hello.txt`. In response, the terminal said `Not a directory`.
