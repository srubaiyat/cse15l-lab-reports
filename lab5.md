For my 5th lab report, I will revisit lab 6, and explain my grade.sh for that assignment. The lab writeup stated a general workflow for our code, so I will first go through explaining what I did for each step, and conclude the lab report with the entire code for my grade.sh.

# 1. Clone the repository of the student submission to a well-known directory name
This was included in the starter code. This deletes any prior student repositories, clones the new one, and puts it into a directory called `student-submission`.
```
rm -rf student-submission
git clone $1 student-submission
echo 'Finished cloning'
```

# 2. Check the correct file has been submitted
I used -f to check if there was a file called `ListExamples.java` in `student-submission`.
```
if [[ -f student-submission/ListExamples.java ]]
    then
        echo "Found ListExamples.java"
    else
        echo "Missing file ListExamples.java"
        exit
fi
```

# 3. Get the student code and your test .java file into the same directory
This was in the starter code.
```
cp student-submission/ListExamples.java ./
```
# 4. Compile your tests and the student’s code
The compile command was in the starter code.
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

javac -cp $CPATH *.java
```

# 5. Run the tests and report the grade based on the JUnit output
This was the most extensive part of the code. First, we redirect the output from the command to run the JUnit tests. Then we extract how many tests passed and failed from the JUnit output, which shouldn't give an error message 
