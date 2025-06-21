---
date: 2025-06-21
title: "LARK Project"
description: "This is an explanation of a project I did in college that was developed to teach new users Unix/Linux commands"
tags: ["Unix", "Linux"]
type: "post"
---

## Github Link

[LARK Project Link](https://github.com/GabeALopez/lark-project)

## Explanation

This project, as the description shows, was to teach new user to Unix/Linux systems the commands that they would be using in their day to day life. Many of these commands included 'ls', 'cd', 'cat', etc. However the interesting spin me and my team members had was that we designed as a puzzle game with a story added with it.

The puzzles would get progressively get harder and harder, trying to get the player to build upon what they had learned in the past. For instance, I would teach players how to echo text into a file and the player would have to use 'cat' command they used in an earlier puzzle to stich together the "passcode" with using the '>>' symbol to progress into the next level. Furthermore, each level would come with a training to allow the player to first learn the tool and then play with it in a sandbox directory. 

For our 4th, below was an example script we used to check whether the player had the correct files in order:

```bash
#!/bin/bash

#Files that script accepts
FILE1=./iAmThePassword.txt
FILE2=./noIAmThePassword.txt
FILE3=./andIAmATxtFile.txt

echo "Give me file or be in denial"

#series of checks to see if the given files are in the current working directory
if test -f "$FILE1"
then
	echo "$FILE1 exists so I will persist."
	if test -f "$FILE2"
	then
		echo "$FILE2 is here so time to cheer."
		if test -f "$FILE3"
		then
			echo "My file is unblurred so here is your password:"
			echo "lincorpIsReallyCool"
			echo ""
			echo "Good agent you got the password. 
				Wow, that is one lame password.
				Whoever made that is either a 
				dork or stupid. Or both. No 
				wonder we got broken into."

			echo ""
			echo -e "\e[1mcd into theBeginningOfTheEnd\e[0m"
			echo ""
			cd ../../
			mv .theBeginningOfTheEnd/ theBeginningOfTheEnd/
			ls
			exec bash


			mv ../../.theBeginningOfTheEnd/ ../../theBeginningOfTheEnd/
		else
			echo "So close, no time to boast"
		fi
	else
		echo "The file is not on the stack so you must backtrack."
	fi
else
	echo "I don't see the file so I won't compile."
fi
```