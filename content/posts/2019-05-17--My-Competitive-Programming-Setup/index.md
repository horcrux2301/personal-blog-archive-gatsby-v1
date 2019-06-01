---
title: My Competitive Programming Setup
subTitle: Using Atom with Bash and Python to get straight to the point
cover: setup.jpeg
category: competitive-programming
menuTitle: competitive-programming
---

## Main Setup

I use Atom as the main text editor. Atom has a ton of plugins that you can use to customise it depending on the your use. And if it doesn't exist you can create one on your own, like I [did](https://github.com/horcrux2301/AFCP) 😂.

To automate the boring stuff of creating folders or parsing contest pages I use shell scripts and python.

## Atom Packages

There are others that I use but the most important ones are - 

1. [Linter GCC](https://atom.io/packages/linter-gcc2) - Lint C/C++ files based on GCC. 
2. [File Header](https://atom.io/packages/file-header) - Auto insert file headers with date and time etc into your code.
3. [platformio-ide-terminal](https://atom.io/packages/platformio-ide-terminal) - Run terminal from inside of atom.



## Parse complete contests
---

The [package](https://github.com/horcrux2301/AFCP) I wrote can parse Codeforces contests easily. I used selenium to parse Codechef contests since I can't get access to their API and they didn't respond to my [request](https://discuss.codechef.com/t/codechef-api-access/21988) to gain access. I have added no support for other websites ( I am lazy ). However, I found a wonderful [Chrome Extension](https://github.com/jmerle/competitive-companion) to parse contests which supports almost all websites. But Atom is not a supported text editor for this extension so I put together a Python script that lets me do the same. You can parse contests as well as individual problems using this extension.


#### Step 1

Update the port in the extension settings. I have set it as 8085. If you change this update it in the python script as well.

![Settings](https://i.imgur.com/9LWMJyG.png)

#### Step 2

Create a file in python by using the code below. Run it in the directory in which you want to parse problems in. Then click on the extension button. Directories which their problems will be automatically created. You need tornado and colorama installed to use this script.

```python
#!/usr/bin/env python3
# parser.py
import tornado.ioloop
import tornado.web
import json
import os
from colorama import *
import sys

class MainHandler(tornado.web.RequestHandler):
    def post(self):
        data = json.loads(self.request.body)
        createDirectory(data)

def make_app():
    return tornado.web.Application([
        (r"/", MainHandler),
    ])

def createDirectory(data):
    current_dir = os.getcwd()
    problem_dir = current_dir + '/' + data['name']
    try:
        os.mkdir(problem_dir)
    except FileExistsError:
        print(Fore.RED + "Folder Exists " + data['name'])
        print(Style.RESET_ALL)
    except:
        print(Fore.RED + "An error occured while creating the directory" + data['name'])
        print(Style.RESET_ALL)

    problem_file = problem_dir + '/' + data['name'] + '.cpp'
    with open(problem_file, 'w') as f:
        f.close()

    file_input_base = problem_dir + '/input'
    file_output_base = problem_dir + '/output'
    file_now = 1
    tests = data['tests']
    total_files = len(tests)
    for test in tests:
        print(Fore.GREEN + "Creating test file " + str(file_now))
        print(Style.RESET_ALL)
        with open(file_input_base+str(file_now)+'.txt', 'w') as f:
            f.write(test['input'])
            f.close()
        with open(file_output_base+str(file_now)+'.txt', 'w') as f:
            f.write(test['output'])
            f.close()
        file_now+=1

    total_files+=1
    with open(file_input_base+str(total_files)+'.txt', 'w') as f:
            f.close()

    print(Fore.GREEN + "All Done")
    print("===============================\n")
    print(Style.RESET_ALL)

def done_all():
    tornado.ioloop.IOLoop.instance().stop()

if __name__ == "__main__":
    app = make_app()
    app.listen(8085)
    tornado.ioloop.IOLoop.current().start()
```

## Running test cases against multiple input files
---

For this I have put together a shell script. However there are 2 conditions that need to be fulfilled to use this script.

1. Make sure that the directory and file name of the code are same. (Otherwise with directories containing multiple C++ files the shell script won't know which one to run against the input files). For example - `../myProblem/myProblem.cpp`. The name of directory is `myProblem` and the name of the file is also `myProblem`. If you use the python script above to generate directories for problems this is already taken off.
2. The name of all the input file names should be of the format `input*.txt`. For example `input1.txt`. Corresponding output will be generated in `output1.txt`.

```bash
#!/bin/bash
# cppscript.sh
echo "Executing"
main_dir=$PWD
cpp_file=${main_dir##*/}
file_path="$main_dir/$cpp_file.cpp"
g++-9 -O2 -std=c++14 -Wall -Wextra -Wshadow -Wfatal-errors -Wl,-stack_size -Wl,256000000 -DLOCAL_DEFINE "$file_path"
obj_path="$main_dir/a.out"
for input in input*.txt
do
    if ! [ -s ${input} ]
    then
        echo -e "\033[31m\xE2\x9D\x97\xE2\x9D\x97 Empty file for ${input} \033[0m"
    else
        echo -e "\033[32mRunning for ${input} \033[0m"
        b=${input:5:1}
        temp_in="$main_dir/$input"
        temp_out="$main_dir/myOutput$b.txt"
        "$obj_path" <"$temp_in" >"$temp_out"

        cat "$temp_in"
        echo -e "=================================\n"
        echo -e "\033[32mOutput for ${input} \033[0m"
        cat "$temp_out"
        echo -e "=================================\n\n\n"
    fi
done

rm ./a.out
```

Notice that I am using the following as the compile command. Please edit it out to suit your needs. For example, you might have to run `g++` instead of `g++-9` like I am.

```bash
g++-9 -O2 -std=c++14 -Wall -Wextra -Wshadow -Wfatal-errors -Wl,-stack_size -Wl,256000000 -DLOCAL_DEFINE "$file_path"
```

## Stress testing your solutions
---

For this I have written a different blog. You can check it out [here](https://www.horcrux2301.dev/stress-testing-solutions-for-comeptitive-programming/).

## Script to create files for a problem
---

Now sometimes I wanted to create a directory with a certain name and input files. So I put together another script for the same.

```bash
#!/bin/bash
# makefiles.sh

echo Creating File              : makefiles.sh

current_dir=$PWD
cpp_dir="$current_dir/"

len="$#"
files=0
count=0

for var in "$@"
do
    (( count++  ))
    if [[ $count = $# ]]; then
        files=$var
    elif [[ $count = $(($# - 1))  ]]; then
        cpp_dir+="$var"
    else
        cpp_dir+="$var "
    fi
done

mkdir "$cpp_dir"
echo "$cpp_dir"

cpp_file+="$cpp_dir/"
count=0
for var in "$@"
do
    (( count++  ))
    if [[ $count = $# ]]; then
        files=$var
    elif [[ $count = $(($# - 1))  ]]; then
        cpp_file+="$var"
    else
        cpp_file+="$var "
    fi
done

cpp_file+=".cpp"
touch "$cpp_file"

for i in $(seq 1 $files)
do
    touch "$cpp_dir/input$i.txt"
done
```

You can use this script as `makefiles.sh "My Problem Name" 2`  to create a directory with the name `My Problem Name`. A `.cpp` file with 2 input test case files will also be generated.

## Run these scripts from anywhere
---

If you are on a UNIX based system (like MacOS or Linux) you can follow these steps to make these scripts an executable and then run it from any directory in the system. This will save you the hassle of creating a new shell script or python file in every directory where you want to parse problems or test your code.

1. Make the shell script executable using `chmod +x cppscript.sh`
2. Copy the script to `/usr/local/bin` using `cp cppscript.sh /usr/local/bin/cppscript.sh`

## Using this setup
---

Once you have parsed the files, you can use the [platformio-ide-terminal](https://atom.io/packages/platformio-ide-terminal) package in Atom to open up the terminal. Update the settings of this package under `Active Directory` and choose `Active File` option. Simply run `cppscript.sh` to run the code again all input files in the directory.

This is my entire setup. I hope this post was useful. In case of any doubts, hit me up on Twitter at this [thread](https://twitter.com/harshk2301/status/1129376470361501696?s=20).

