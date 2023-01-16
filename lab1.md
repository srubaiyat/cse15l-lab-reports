In this week's lab, we installed Visual Studio Code, remotely connected to the lab computers in the CSE Basement, and tried some commands.

I already had VSCode, but the way to install it is to go to https://code.visualstudio.com/. 

<img width="1021" alt="image" src="https://user-images.githubusercontent.com/122497388/212572113-dbb30c83-3b09-47d3-b026-d254fc134df3.png">

Clicking the blue button which preselects the version downloadable for your device should automatically install it in a few minutes. After installing, you should be able to open a window that looks like this: 

<img width="1020" alt="image" src="https://user-images.githubusercontent.com/122497388/212595060-887151d3-966f-4a75-872d-dd929fee2b55.png">

I started off lab by setting up remote connection. First, I opened up the terminal, and typed in "ssh cs15lwi23adv@ieng6.ucsd.edu". It prompted me for my password, so I typed it in. 

<img width="707" alt="image" src="https://user-images.githubusercontent.com/122497388/212595518-8b56ae0d-6211-409c-96da-810ded6faf32.png">

Now that I was logged into the remote server, I tried out some commands.

<img width="655" alt="image" src="https://user-images.githubusercontent.com/122497388/212595997-1c20da2c-ce53-4337-9357-8e2832320d70.png">

I first typed in "pwd", to print out the working directory, which was "/home/linux/ieng6/cs15lwi23/cs15lwi23adv". 
I wanted to see if I could access another student's directory, so I typed in "cd .." to access the parent directory of all student directories "/home/linux/ieng6/cs15lwi23", and then typed in "ls cs15lwi23atj" to list the contents of the student directory "cs15lwi23atj". This was not possible, as I am not that student, and didn't have permissions to look at their directory. 
Then I typed in "cd public" and "ls" to see what was in the one non-student directory. I saw there was no file named "hello.txt", so I wondered what would occur if I typed in  "cd hello.txt". In response, the terminal said "No such file or directory".

