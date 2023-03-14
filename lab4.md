In this lab report, I will recreate how I got my 1:18 time in the CSE Labs Done Quick Tournament.

As in the [Github and Login Command-Line Setup](https://ucsd-cse15l-w23.github.io/week/week7/#github-and-login-command-line-setup), I set up ssh keys to log into my ieng6 account and push code to github quickly.
In preparation, I did the whole lab once before in preparation, so the commands would be stored in the terminal and easily accessed by pressing the <up> keys. Then I removed the directory by running `rm -rf lab7` and then typed `exit` to log out of ieng6. I also deleted the existing fork of the repository, and then created a new fork.

# 4. Log into ieng6
  
The `ssh cs15lwi23adv@ieng6.ucsd.edu` command was the last command I ran before entering into ieng6, so I pressed `<up><enter>` to run it.
 
# 5. Clone your fork of the repository from your Github account
  
The `git clone git@github.com:srubaiyat/lab7.git` command was the first command I ran after entering into ieng6, so I pressed `<up><up><up><up><up><up><up><up><up><up><up><up><enter>`(<up> 12 times and then enter) to run it. This created a directory called lab7 in the home directory of 'cs15lwi23adv@ieng6.ucsd.edu', so I typed `cd lab7` . 
 
# 6. Run the tests, demonstrating that they fail
  
The `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` and `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` commands were 7 commands up, so I pressed `<up><up><up><up><up><up><up><enter><up><up><up><up><up><up><up><enter>`(<up> 7 times and then enter, and again) to run them.
The output displayed was as below.
<img width="1041" alt="image" src="https://user-images.githubusercontent.com/122497388/221401292-d150b4a8-8f45-4285-80f4-afa26adccd7d.png">

# 7. Edit the code file to fix the failing test

I typed `nano L<tab>.java` to open ListExamples.java in nano. I pressed the `<down>` and `<right>` keys until I got to line 43 and changed line 43 from "index1 += 1;" to "index2 += 1;". I then pressed `<^O><enter><^X>` to save and exit the file. 
  
# 8. Run the tests, demonstrating that they now succeed
 
The `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` and `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` commands were 3 commands up, so I pressed `<up><up><up><enter><up><up><up><enter>`(<up> 3 times and then enter, and again) to run them.
The output displayed was as below.
<img width="1126" alt="image" src="https://user-images.githubusercontent.com/122497388/221401332-36ced86f-cdbb-40b3-a128-5a00c563fb08.png">
  
# 9. Commit and push the resulting change to your Github account
 
I typed `git add L<tab>.java` to indicate ListExamples.java should be part of the next commit. I typed `git commit -m "c"` to commit ListExamples.java. I then typed `git push origin main` to push the changed file to github. 

  
