# week 4 & 5 lab report!

## Part 1: the ```less``` command
### Example 1: ```less -g``` ###
This command will print out just the first line of the results of the ```less``` command. This could be useful if files were structured to always have a summary on the first line, and whoever's searching could easily get an idea of what's in the file.

The command run here was ```less -g technical/plos/pmed.0020273.txt```

![Image](res\lab5\less-g.png)


&nbsp;
### Example 2: ```less -N``` ###
This option shows line numbers when showing the result of the ```less``` command. This could be useful if someone wanted to peek at the file and find a certain line to do more commands on.

The command run here was ```less -N technical/plos/pmed.0020273.txt```

![Image](res\lab5\less-N.png)


&nbsp;
### Example 3: ```less -X``` ###
This option allows the output of the ```less``` command to remain in the terminal when usually by default it disappears when ```q``` is pressed. This could be useful if someone wanted to see the commands used to print out this result at the same time.

The command run here was ```less -X technical/plos/pmed.0020273.txt```

![Image](res\lab5\less-X.png)


&nbsp;

## Part 2: the ```find``` command
### Example 1: ```find -name``` ###
This command will print out the files that include the specified string in its name. This would be useful to find all the files of a certain type.

The command run here was ```find 911report -name "*.txt"```

![Image](res\lab5\find-name.png)


&nbsp;
### Example 2: ```find -newer``` ###
This option prints out all the files that are newer than the specified file. This would be useful for version control or just to check modifications.

The command run here was ```find -newer "./plos/pmed.0020242.txt"```

![Image](res\lab5\find-newer.png)


&nbsp;
### Example 3: ```find -empty``` ###
This option finds all the files and directories that are empty. This would be useful for finding if any files or directories are mistakenly empty, as in they shouldn't be.

The command run here was ```find -empty```

![Image](res\lab5\find-empty.png)


&nbsp;

## Part 3: the ```grep``` command
### Example 1: ```grep -i``` ###
This command searches for a specified string without case-sensitivity. This would be useful for checking certain files contained words without looking at capitalization.

The command run here was ```grep -i "TecHnoloGy" technical\911report\chapter-1.txt```

![Image](res\lab5\grep-i.png)


&nbsp;
### Example 2: ```grep -c``` ###
This option prints out the number of occurences of the string specified. This is useful for data analysis since one doesn't need to read the entire file to find how many occurences there are.

The command run here was ```grep -c "war" 911report/chapter-1.txt```

![Image](res\lab5\grep-c.png)


&nbsp;
### Example 3: ```grep -n``` ###
This command prints out the line number and the line that contains the specified word. This is useful since it would allow a user to know which line to change that contains the specified word.

The command run here was ```grep -n "war" 911report/chapter-1.txt```

![Image](res\lab5\grep-n.png)


&nbsp;