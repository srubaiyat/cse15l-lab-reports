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
This was the most extensive part of the code. First, we redirect the output from the command to run the JUnit tests. Then we extract how many tests passed and failed from the JUnit output. 
```
grep "Tests run:" tests_output.txt > grep_results.txt
for value in `cat grep_results.txt`
do
    if [[ ${value:1:2}=="," ]]
        then
            TOTAL=${value:0:1}
        fi
        WRONG=${value}
done
RIGHT=$((TOTAL-WRONG))
RESULT=$RIGHT"/"$TOTAL

if [[ `grep -c "OK" tests_output.txt` -eq 1 ]]
    then
        echo "All tests passed"

    else
        echo $RESULT
fi
```

Although the first 11 commands appear to fail if all JUnit tests pass, no extra text is printed in the form of an error message and the script doesn't stop either because we didn't put `set -e`. No harm is done by some of these commands not running since the case where all JUnit tests pass doesn't depend on those commands. 

In the case some tests fail, the first 11 commands:
- look for the line with "Tests run:", where the number of failed tests and tests run are listed
- sets TOTAL to the number of tests run and sets WRONG to the number of failed tests
- sets RIGHT to TOTAL-WRONG, which is the number of tests passed
- sets RESULT to the fraction of JUnit tests passed

The last 8 commands check if all tests passed, and if not, prints RESULT, and if so, prints "All tests passed".
