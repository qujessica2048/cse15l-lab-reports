# week 7 & 8 lab report!

## Part 1: the Code and Documentation
### ```grade.sh```:
```
set -e

rm -rf student-submission
git clone $1 student-submission

cd student-submission
if test -f ListExamples.java
then 
    echo "ListExamples.jav exists"
else 
    echo "ListExamples.java does not existtttttttt Score: 0/4"
    exit 1
fi

cp ListExamples.java ../

set +e 

cd ..
javac -cp ".:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar" TestListExamples.java ListExamples.java
if test $? -eq 0;
then
    echo "compile sucess!!!"
else 
    echo "compile unsuccessful! Score: 0/4"
    exit 1
fi


java -cp ".:lib/junit-4.13.2.jar:lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore TestListExamples > score.txt

score= grep -F "Failures: " score.txt
numFail= echo Score: $((4 - ${score:-1}))/4

```
&nbsp;

### Documentation
Using https://github.com/ucsd-cse15l-f22/list-methods-filename

![Image](res\lab7\methods-filename.png)

Using https://github.com/ucsd-cse15l-f22/list-methods-corrected

![Image](res\lab7\methods-corrected.png)

Using https://github.com/ucsd-cse15l-f22/list-methods-compile-error

![Image](res\lab7\compile-error.png)

&nbsp;

## Part 2: Tracing ```grade.sh```
Command: ```set -e```

&nbsp;
Standard Output: none

&nbsp;
Standard Error: none

&nbsp;
Return Code: 0

Command: ```git clone $1 student-submission```

&nbsp;
Standard Output: none

&nbsp;
Standard Error: none

&nbsp;
Return Code: 0

Command: ```cd student-submission```

&nbsp;
Standard Output: none

&nbsp;
Standard Error: none

&nbsp;
Return Code: 0

If Statement: ```if test -f ListExamples.java```

&nbsp;
Returns: ```true``` since file was found

Command: ```echo "ListExamples.jav exists"```

&nbsp;
Standard Output: ListExamples.jav exists

&nbsp;
Standard Error: none

&nbsp;
Return Code: 0

Command That Doesn't Run: ```echo "ListExamples.java does not existtttttttt Score: 0/4"```

&nbsp;
"Else" part of previous if statement that checked if the file was found

Command: ```cp ListExamples.java ../```

&nbsp;
Standard Output: none

&nbsp;
Standard Error: none

&nbsp;
Return Code: 0

Command: ```set +e```

&nbsp;
Standard Output: none

&nbsp;
Standard Error: none

&nbsp;
Return Code: 0

Command: ```cd ..```

&nbsp;
Standard Output: none

&nbsp;
Standard Error: none

&nbsp;
Return Code: 0

Command: ```javac -cp ".:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar" TestListExamples.java ListExamples.java```

&nbsp;
Standard Output: ```ListExamples.java:15: error: ';' expected
        result.add(0, s)
                        ^
1 error```

&nbsp;
Standard Error: none

&nbsp;
Return Code: nonzero

If Statement: ```if test $? -eq 0```

&nbsp;
Returns: ```false``` since exit code of previous command was nonzero

Command That Doesn't Run: ```echo "compile sucess!!!"```

&nbsp;
Condition of previous if statement was not satisfied

Command: ```echo "compile unsuccessful! Score: 0/4" exit 1```

&nbsp;
Standard Output: compile unsuccessful! Score: 0/4

&nbsp;
Standard Error: none

&nbsp;
Return Code: 0

All other commands do not run because this last command exits.