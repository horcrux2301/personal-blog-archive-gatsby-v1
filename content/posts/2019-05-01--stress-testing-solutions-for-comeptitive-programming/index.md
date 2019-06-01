---
title: Stress Testing Solutions for Competitive  Programming
subTitle: Chase those corner cases
category: competitive-programming
cover: stress.jpg
menuTitle: competitive-programming
---

Not being able to catch corner cases is a problem that I faced while solving problems in contests or while doing practice. Sometimes the code that I wrote was correct for all the test cases that I had but the judge still gave me WA, which made me frustated and un-motivated to solve more problems.

To stress test my solutions I use shell scripts that automate pretty much all of the stuff for me.  

To stress test you need 3 files and make sure these all are in the same directory - 

1. Your code (The code that you want to stress test).
2. The correct code (This is the file against which your code will be stress tested). Now you may be wondering if I already have the holy grail of correct code why won't I just submit that and be done with the problem. But either you 
    - Have written an optimised code with a better complexity. But you can't figure out where it's wrong. So writing a brute force and testing for smaller inputs might be helpful here.
    - Are doing practice and you already have a couple of solutions by other peole which has been judged correctly. So you can use their code to generate inputs where your code fails.
3. A program to generate random test cases.

## Your code
Create this file with any name you want. In this directory use `g++ -o a.out filename.cpp` to create the `a.out` executable.

## Correct code
Create this file with any name but preferably stress.cpp. Use `g++ -o stress.out stress.cpp` to create the `stress.out` executable.

## Program to generate test cases
I am using python since it's easier to quickly generate test cases of any kind. Keep the name of this python file as `stress.py`. 

## Shell script

Save the snippet below as file  `stress.sh`. 

```bash
# stress.sh
#!/bin/bash
start=0
curr_dir=$PWD

while [ $start -lt 1000 ]
do
    (( start++ ))
    if [ -e stress.py ]
    then
        python3 "$PWD/stress.py" > "$PWD/stressInput.txt"
        ./a.out < "$PWD/stressInput.txt" > "$PWD/myStressOutput.txt"
        ./stress.out < "$PWD/stressInput.txt" > "$PWD/stressOutput.txt"
        diff "$PWD/stressOutput.txt" "$PWD/myStressOutput.txt" || exit 1
        echo -e "\033[0;32mDone for $start \xE2\x9C\x93 \033[0m"
    else
        echo -e "\033[0;31m Python file not found \xE2\x9D\x8C \033[0m"
        break
    fi
done
```

The shell script first looks for a file with the name `stress.py`. If it exists, we create test cases using this file and generate `stressOutput` corresponding to the correct code and `myStressOutput.txt` for the code we want to test. `diff` is used to detect differences between the two files and if any, the process is stopped. You can then look at `stressInput.txt` to see a corner test case and `myStressOutput.txt` for your output and `stressOutput.txt` for the correct output. And using this information you might be able to finally get a hang of where your code went wrong.

Now I have limited the number of test cases in each loop to 1000. You can increase that in the shell script or run it again if you want to continue the testing. 

Finally run `stress.sh` in the directory where these 3 files are saved to run the testing.

----

If you are on a UNIX based system (like MacOS or Linux) you can follow these steps to make `stress.sh` an executable and then run it from any directory in the system. This will save you the hassle of creating a new shell script file in every directory where you want to stress test your solutions.

1. Make the shell scipt executable using `chmod +x stress.sh`
2. Copy the script to `/usr/local/bin` using `cp stress.sh /usr/local/bin/stress.sh`

I hope this post was useful. In case of any doubts, hit me up on Twitter at this [thread](https://twitter.com/harshk2301/status/1129376457224888325?s=20).
